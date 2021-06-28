---
layout: post
title: VoxelMorph
date: 2021-02-04

tags: registration spatial-transformation
splash_img_source: /assets/img/voxelmorph/architecture.png
splash_img_caption: Arquitectura de VoxelMorph. Tomada del <a href="https://arxiv.org/pdf/1809.05231.pdf">paper original</a>. # Splash image caption

# Optional front matter
updated: 2021-02-05 # Updated date in YYYY-MM-DD format
author: 
  name: Iván Grijalva # Author name, if not provided defaults to site.author.name
  homepage: http://example.com # Author link, if not provided defaults to site.author.homepage
pin: false # true if this post must be pinned on top of the page, default is false.
listed: false # false if this post must NOT be included on the posts page, sitemap, and any of the tag pages, default is true
index: true # When false, <meta name="robots" content="noindex"> is added to the page, default is true
---

Una de las arquitecturas para registro de imágenes que me pareció mas parecida a [DIRNet](https://arxiv.org/pdf/1704.06065.pdf) es VoxelMorph, basicamente la diferencia entre ambas es que la segunda usa una UNet para generar *registration field* como se puede ver en la arquitecta.

La idea general de VoxelMorph es que aprende una función (*parameterized registration function*) de un conjunto de volúmenes.

Si $F$ y $M$ denotan las imágenes fijas y en movimiento (la que se quiere registrar) y $\phi$ el *registration field* que mapea las coordenadas de $F$ a las coordenadas de $M$, entonces buscamos minimizar

$$\hat{\phi} =  \text{argmin}_\phi \,\, [\mathcal{L}(F, M, \phi) + \lambda  \mathcal{L}_{smooth}(\phi)]$$

Notar que $\mathcal{L}(F, M, \phi)$ puede escribirse como $\mathcal{L}_{sim}(F, M \circ \phi)$, donde $$\mathcal{L}_{sim}$$ mide la "similitud" entre la imagen fija $F$ y la imagen deformada $M \circ \phi$ y $$\mathcal{L}_{smooth}$$ impone regularización.

Para $$\mathcal{L}_{simm}$$ usaremos **MSE** (Mean Square Loss) y **NCC** (Normalized Cross Correlation), pero existen otras métricas comunes asociadas. Además usaremos $\phi = Id + \mathbf{u}$, i.e. el desplazamiento de $F$ a $M$ para cada *voxel*.

La función que realiza el registro se modela tal que $g_\theta (F, M) = \mathbf{u}$, donde $\theta$ son los parámetros de una red convolucional, una UNet.


Implementaremos una versión 2D de VoxelMorph para obtener un poco de intuición sobre su funcionamiento, para esto abajo se muestra la implementación de una UNet con filtros de 64, 128, 256 y 512 (notar que no es la UNet original).

```python

class DoubleConv(nn.Module):
    """
    [Conv2d -> BarchNorm -> ReLU] x 2
    """
    def __init__(self, in_channels, out_channels):
        super(DoubleConv, self).__init__()
        self.conv = nn.Sequential(
            nn.Conv2d(in_channels, out_channels, 3, 1, 1, bias=False),
            nn.BatchNorm2d(out_channels),
            nn.ReLU(inplace=True),

            nn.Conv2d(out_channels, out_channels, 3, 1, 1, bias=False),
            nn.BatchNorm2d(out_channels),
            nn.ReLU(inplace=True),
        )
    
    def forward(self, x):
        return self.conv(x)

class Unet(nn.Module):
    """
    Módulo de UNet.
    canales de entrada: 1 canal para F + 1 canal para M
    salida: 2 "canales", un canal para el desplazamiento dx y otro para dy
    """
    def __init__(self, in_channels=2, out_channels=2, features = [64, 128, 256, 512]):
        super(Unet, self).__init__()
        self.ups  = nn.ModuleList()
        self.downs = nn.ModuleList()
        self.pool = nn.MaxPool2d(kernel_size=2, stride=2)

        # Downsample
        for feature in features:
            self.downs.append(DoubleConv(in_channels, feature))
            in_channels = feature
        
        # Upsample
        for feature in reversed(features):
            self.ups.append(nn.ConvTranspose2d(
                2*feature, feature, kernel_size=2, stride=2)
            )
            self.ups.append(DoubleConv(feature*2, feature))

        
        self.botleneck = DoubleConv(features[-1], features[-1] * 2)
        self.final_conv = nn.Conv2d(features[0], out_channels, kernel_size=1)
    
    def forward(self, x):
        skip_connections = []

        for down in self.downs:
            x = down(x)
            skip_connections.append(x)
            x = self.pool(x)
        
        x = self.botleneck(x)
        skip_connections = skip_connections[::-1] # reverse
        
        for idx in range(0, len(self.ups), 2):
            x = self.ups[idx](x)
            skip_connection = skip_connections[idx // 2]
            
            if skip_connection.shape != x.shape:
                x = F.resize(x, size=skip_connection.shape)

            concatenated_skip = torch.cat((skip_connection, x), dim=1)
            x = self.ups[idx + 1](concatenated_skip)
        
        return self.final_conv(x)
```

La implementación anterior recibe las imagenes fijas y en movimiento concatenadas, la entrada tiene shape `(batch, 2, ancho, alto)` y devuelve un tensor con shape `(batch, dx, dy)`.

Para el transformador espacial utilizaremos la implementación `torch.nn.functional.grid_sample` de pytorch.


```python

class SpatialTransform(nn.Module):
    def __init__(self, size):
        super(SpatialTransform, self).__init__()
        
        # [[0, 1, 2, ..., ancho], [0, 1, 2, ..., alto]]
        vectors = [ torch.arange(0, s) for s in size ]
        #[(0, 0), (0, 1), ...., (ancho, alto)] 
        grids = torch.meshgrid(vectors) 
        grid  = torch.stack(grids)
        # agregar la dimensión del batch
        grid  = torch.unsqueeze(grid, 0)
        grid = grid.type(torch.FloatTensor)
        self.register_buffer('grid', grid)

    def forward(self, src, flow):
        # phi = Id + u
        phi = self.grid + flow 

        shape = flow.shape[2:]

        for i in range(len(shape)):
            phi[:,i,...] = 2*(phi[:,i,...]/(shape[i]-1) - 0.5)

        if len(shape) == 2:
            phi = phi.permute(0, 2, 3, 1) 
            phi = phi[..., [1,0]]
        elif len(shape) == 3:
            phi = phi.permute(0, 2, 3, 4, 1) 
            phi = phi[..., [2,1,0]]

        # Aplicar la deformación: phi (M)
        return F.grid_sample(src, phi, mode='bilinear')

```

Finalmente el módulo para VoxelMorph:

```python

class VoxelMorph(nn.Module):
    def __init__(self, size):
        super(VoxelMorph, self).__init__()

        self.unet = Unet()
        self.spatial_transform = SpatialTransform(size)

    def forward(self, fixed, moving):
        x = torch.cat([fixed, moving], dim=1)
        flow = self.unet(x)
        warped = self.spatial_transform(moving, flow)

        return warped, flow

```

Usaremos algunos *toy datasets* para visualizar resultados preliminares.