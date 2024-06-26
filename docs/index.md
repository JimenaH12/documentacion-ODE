## Método de Euler 

El método de Euler es muy sencillo, se basa en la expansión de Taylor de la función x(t). Tenemos $$ \text{Expansión Taylor} \Rightarrow x(t+h) = x(t) + h\frac{dx}{dt} + \overbrace{ \frac{h^2}{2} \frac{d^2x}{dt^2} } ^{\epsilon} + O(h^3). $$ Esto implica que para avanzar en el tiempo la función por un paso h, el cual suponemos que es lo suficientemente pequeño, basta con utilizar la ecuación $$ \boxed{x(t + h) = x(t) + hf(x,t).} $$ El error asociado con la aproximación está ligado a la cantidad de veces que hagamos la aproximación, es decir, al número de pasos en el tiempo que utilicemos en nuestra solución. Lo podemos estimar de la siguiente forma $$ \sum\epsilon = \sum_{k=0}^{N-1}\frac{h^2}{2}\left. \frac{d^2x}{dt^2} \right|{x_k, t_k} = \frac{h}{2}\sum{k=0}^{N-1}h\left.\frac{df}{dt}\right|_{x_k, t_k}\ \approx \frac{h}2\int_a^b\frac{df}{dt}d t = \frac{h}{2}\left[f_b - f_a\right]. $$ En la ecuación anterior asumimos que tomamos N=(b-a)/h pasos temporales para llegar al punto final.

Entonces, naturalmente, el error total de aproximación depende h linealmente multiplicado por el intervalo en el cual realizamos la integración.

    Para algunas aplicaciones, esto es suficiente. Para otras, necesitamos una mejor aproximación.
    El algoritmo toma la siguiente forma:
    Empezar con t=t_{0}, x=x_{0}
    Discretizar el tiempo en pasos temporales de forma equidistante con espaciamiento , donde cada punto en el tiempo está denotado con t_{i}
    Para cada punto en el tiempo encontrar x utilizando el resultado de la iteración previa: x_{i} = x_{i-1} +hf(x_{i-1})

## Método de Rung-Kutta de 2$^{\rm do}$ Orden (RK2)

Este método se implementa para utilizar el punto medio (t+h/2) para evaluar el método de Euler. Esto con el objetivo de alcanzar una mejor aproximación para el valor de h 

Tenemos $$ x(t + h) = x\left(t + \frac{h}{2}\right) + \frac{h}{2}\left(\frac{{\rm d}x}{{\rm d}t}\right){t+h/2} + \frac{h^2}{8}\left(\frac{{\rm d}^2x}{{\rm d}t^2}\right){t+h/2} + O(h^3). $$ Similarmente, podemos hacer lo mismo para , tal que $$ x(t) = x\left(t + \frac{h}{2}\right) - \frac{h}{2}\left(\frac{{\rm d}x}{{\rm d}t}\right){t+h/2} + \frac{h^2}{8}\left(\frac{{\rm d}^2x}{{\rm d}t^2}\right){t+h/2} + O(h^3). $$ Al sustraer ambas ecuaciones obtenemos $$ x(t + h) = x(t) + h\left(\frac{{\rm d}x}{{\rm d}t}\right)_{t+h/2} + O(h^3) $$ Finalmente, $$ \boxed{x(t + h) = x(t) + hf[x(t + h/2), t + h/2] + O(h^3)}. $$

Con esto se llega a un nuevo orden h^{3}, el cual nos genera una mejor aproximación. No obstante, se requiere conocer el valor de la función de punto medio x(t+h/2), pero para esto se puede utilizar el método de Euler con el paso h/2, (x+h/2) = x(t) + h/2 f(x,t). Así se encuentran las ecuaciones del método RK2:

* $k_1 = hf(x, t)$,
* $k_2 = hf\left(x + \frac{k_1}{2}, t+\frac{h}2\right)$,
* $x(t+h) = x(t) + k_2


## Método de Runge-Kutta de 4$^{\rm to}$ Orden

Para este método, se puede utilizar lo anterior, pero con más puntos ubicados entre x(t)$ y $x(t + h)$ realizando expansiones de Taylor. Así se logra agrupar términos de orden $h^3$, $h^4$, los cuales permiten incrementar el orden de aproximación. Este método es el más utilizado para resolver ODEs, es fácil de programar y devuelve resultados precisos.

Haciendo el álgebra se obtiene:

* $k_1 = hf(x, t)$,
* $k_2 = hf\left(x + \frac{k_1}{2}, t+\frac{h}2\right)$,
* $k_3 = hf\left(x + \frac{k_2}{2}, t+\frac{h}2\right)$,
* $k_4 = hf\left(x + k_3, t + h \right)$,
* $x(t+h) = x(t) + \frac{1}{6}(k_1 + 2 k_2 + 2k_3 + k_4)$.

 
Nota: El error de aproximación es $O(h^5)$, mientras que el error global es aproximadamente del orden $O(h^4)$.



