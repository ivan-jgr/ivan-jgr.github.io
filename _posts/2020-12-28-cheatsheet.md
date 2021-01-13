---
layout: post
title:  "Cheatsheet"
date:   2020-12-03 15:00:00 -0600
categories: math
published: true
---

### **Superficies Parametrizadas**
#### Vectores Tangentes a una Superficie Parametrizada
Si $$\Phi$$ es la parametrización de una superficie $$S$$, entonces:

$$\mathbf{T}_u = \dfrac{\partial \Phi}{\partial u} = \left\langle \dfrac{\partial x}{\partial u}, \dfrac{\partial y}{\partial u},\dfrac{\partial z}{\partial u}  \right\rangle \quad \mathbf{T}_v = \dfrac{\partial \Phi}{\partial v} = \left\langle \dfrac{\partial x}{\partial v}, \dfrac{\partial y}{\partial v},\dfrac{\partial z}{\partial v}  \right\rangle$$

#### Diferencial de Área Superficial

$$dS = \Vert \mathbf{T}_u \times \mathbf{T}_v \Vert dudv = \Vert \mathbf{N} \Vert dudv$$

#### Plano Tangente a una Superficie en el Punto $$(x_0, y_0, z_0)$$

$$(x-x_0, y-y_0, z-z_0) \cdot \mathbf{N} = 0$$

#### Integral de Área Superficial

$$A(S) = \displaystyle\iint_S \, dS = \iint_D \Vert \mathbf{T}_u \times \mathbf{T}_v \Vert dudv$$

### **Integral de Superficie**
#### Sobre Campos Escalares

$$\displaystyle\iint_S f(x, y, z) \, dS = \iint_D f(\Phi(u, v)) \Vert \mathbf{T}_u \times \mathbf{T}_v \Vert dudv$$

#### Sobre Campos Vectoriales (Flujo)

$$\displaystyle\iint_S \mathbf{F} \cdot \mathbf{\hat{n}} \, dS = \iint_D \mathbf{F}(\Phi(u, v)) \cdot \dfrac{\mathbf{N}}{\Vert \mathbf{N} \Vert} \Vert \mathbf{T}_u \times \mathbf{T}_v \Vert dudv = \iint_D \mathbf{F}(\Phi(u, v)) \cdot \mathbf{N} \,\, dudv$$

#### Divergencia

$${\rm div} \, \mathbf{F}  = \lim_{\Delta V\to 0} \frac{1}{\Delta V} \displaystyle\bigcirc \!\!\!\!\!\!\!\!\iint_S \mathbf{F} \cdot \mathbf{\hat{n}} \, dS$$

- Divergencia en Coordenadas Cartesianas:
Si $$\mathbf{F} = M \mathbf{\hat{i}} + N \mathbf{\hat{j}} +  P\mathbf{\hat{k}}$$

$$\nabla \cdot \mathbf{F} = \displaystyle\frac{\partial M}{\partial x} + \frac{\partial N}{\partial y} + \frac{\partial P}{\partial z}$$

- Divergencia en Coordenadas Cilíndricas:
Si $$\mathbf{F} = F_r \mathbf{\hat{r}} + F_\theta \mathbf{\hat{\theta}} +  F_z\mathbf{\hat{k}}$$

$$\nabla\cdot \mathbf{F} = \frac{1}{r}\frac{\partial}{\partial r} (r F_r) + \frac{1}{r}\frac{\partial F_\varphi}{\partial \varphi} + \frac{\partial F_z}{\partial z}$$

- Divergencia en Coordenadas Esféricas:
Si $$\mathbf{F} = F_r \mathbf{\hat{\rho}} + F_\theta \mathbf{\hat{\theta}} +  F_\phi\mathbf{\hat{\phi}}$$

$$\nabla\cdot \mathbf{F} = \frac{1}{\rho^2}\frac{\partial}{\partial \rho} (r^2 F_\rho)
+ \frac{1}{\rho{\sin}\theta}\frac{\partial}{\partial \theta} ({ \sin}\theta F_\theta) + \frac{1}{\rho{\sin}\theta}\frac{\partial F_\varphi}{\partial \varphi}$$

### **Teorema de Gauss-Ostrogradsky**

$$\boxed{\displaystyle \iiint_W \text{div} \, \mathbf{F} \, dV = \displaystyle\bigcirc \!\!\!\!\!\!\!\!\iint_{\partial W} \mathbf{F} \cdot \mathbf{\hat{n}} \, dS}$$

### **Integrales de Línea**

#### Sobre Campos Escalares

$$\displaystyle\int_{\mathbf{c}} f ds = \displaystyle\int_a^b f(\mathbf{c}(t)) \Vert \mathbf{c}'(t) \Vert \, dt$$

#### Sobre Campos Vectoriales (Trabajo)

$$\displaystyle\int_{\mathbf{c}} \mathbf{F} \cdot \mathbf{ds} = \displaystyle\int_a^b \mathbf{F}(\mathbf{c}(t)) \Vert \mathbf{c}'(t) \Vert \, dt$$

#### Área de una Región

$$A(D) = \dfrac{1}{2} \int_{\partial D} x dy - ydx$$

#### Rotacional (Curl)

$$\text{rot} \, \mathbf{F} \cdot \mathbf{\hat{n}} = \lim_{\rho \rightarrow 0} \dfrac{1}{A(S_\rho)} \oint_{\partial S_\rho} \mathbf{F} \cdot \mathbf{ds}$$

- Rotacional en Coordenadas Cartesianas: 
Si $$\mathbf{F} = M \mathbf{\hat{i}} + N \mathbf{\hat{j}} +  P\mathbf{\hat{k}}$$

$$\nabla \times \mathbf{F} =
\begin{vmatrix} \mathbf{\hat i} & \mathbf{\hat i} & \mathbf{\hat k} \\
{\dfrac{\partial}{\partial x}} & {\dfrac{\partial}{\partial y}} & {\dfrac{\partial}{\partial z}} \\
M & N & P \end{vmatrix}$$

- Rotacional en Coordenadas Cilíndricas:
Si $$\mathbf{F} = F_r \mathbf{\hat{r}} + F_\theta \mathbf{\hat{\theta}} +  F_z\mathbf{\hat{k}}$$

$$\nabla \times \mathbf{F} = \dfrac{1}{r}
\begin{vmatrix} \mathbf{\hat r} & \mathbf{\hat \theta} & \mathbf{\hat k} \\
{\dfrac{\partial}{\partial r}} & {\dfrac{\partial}{\partial \theta}} & {\dfrac{\partial}{\partial z}} \\
F_r & rF_\theta & F_z \end{vmatrix}$$

- Rotacional en Coordenadas Esféricas:
Si $$\mathbf{F} = F_r \mathbf{\hat{\rho}} + F_\theta \mathbf{\hat{\theta}} +  F_\phi\mathbf{\hat{\phi}}$$

$$\nabla \times \mathbf{F} = \dfrac{1}{\rho^2 \sin^2 \theta}
\begin{vmatrix} \mathbf{\hat \rho} & r\mathbf{\hat \theta} & r \sin \theta \mathbf{\hat \phi} \\
{\dfrac{\partial}{\partial r}} & {\dfrac{\partial}{\partial \theta}} & {\dfrac{\partial}{\partial \phi}} \\
F_r & rF_\theta & r \sin \theta F_\phi \end{vmatrix}$$

### **Teorema Fundamental de las Integrales de Línea**

$$\boxed{\displaystyle \int_{\mathbf{c}} \nabla f \cdot \mathbf{ds} = f(\mathbf{c}(b)) - f(\mathbf{c}(a))}$$

### **Teorema de Green**

$$\displaystyle \oint_{\partial D^+} P dx + Q dy = \displaystyle\iint_{D} \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} \right) dxdy$$

### **Teorema de Stokes**

$$\boxed{\displaystyle \iint_S (\nabla \times \mathbf{F}) \cdot \mathbf{\hat{n}} \, dS = \oint_{\partial S} \mathbf{F} \cdot dl}$$