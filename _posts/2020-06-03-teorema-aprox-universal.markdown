---
layout: post
title:  "El Teorema de Aproximación Universal"
date:   2020-06-03 23:30:34 -0600
categories: jekyll update
---
Una de los hechos que me parecen interesantes acerca de las redes neuronales es que pueden aproximar casi cualquier función, $$f(x)$$ y lo más sorprendente es que esto aplica incluso si consideramos una red neuronal con una sola hidden layer.

En el paper original que probó este resultado se usó el teorema de Hahn-Banach, el teorema de Representación de Riesz y análisis de Fourier. Los papers más reconocidos al respecto son [Aproximation by Superposition of a Sigmoidal Function](http://www.dartmouth.edu/~gvc/Cybenko_MCSS.pdf) por  George Cybenko (1989) y [Multilayer feedforward networks are universal approximators](https://www.sciencedirect.com/science/article/abs/pii/0893608089900208) por  Kurt Hornik, Maxwell Stinchcombe, and Halbert White (1989).

Aquí intentaremos explorar algunos aspectos de la publicación de Cybenko sin recurrir a detalles matemáticos avanzados. El objetivos será obtener un poco de intuición sobre por qué las redes neuronales son aproximadores universales y las limitaciones en complejidad computacional que nos pondrán los pies sobre la tierra nuevamente.  

Primero es necesario definir a lo que nos referimos como "casi cualquier función"

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
