

## 极限

1.   求$f(x) = \frac{|ln|x||}{x^2-1}$的间断点

     **间断点：**$0, \pm1$

     $\lim\limits_{x \to 0}f(x) = \frac{+\infty}{-1} = -\infty$

     $\lim\limits_{x \to 1^+}f(x) = \lim\limits_{x \to 1^+}\frac{\ln x}{(x+1)(x-1)} =\lim\limits_{x\to 1^+}\frac{1}{x+1} \cdot \frac{\ln\left[1+(x-1)\right]}{(x-1)} = \frac{1}{2}$

     $\lim\limits_{x \to 1^-}f(x) = -\lim\limits_{x \to 1^-}\frac{\ln x}{(x+1)(x-1)} =-\lim\limits_{x\to 1^-}\frac{1}{x+1} \cdot \frac{\ln\left[1+(x-1)\right]}{(x-1)} = -\frac{1}{2}$

     $\lim\limits_{x \to 1^+}f(x) = \lim\limits_{x \to 0}\frac{\ln x}{(x+1)(x-1)} =\lim\limits_{x\to 1^+}\frac{1}{x+1} \cdot \frac{\ln\left[1+(x-1)\right]}{(x-1)} = \frac{1}{2}$

     $\lim\limits_{x \to -1^-}f(x) = \lim\limits_{x \to -1^+}\frac{-\ln (-x)}{(x+1)(x-1)} =-\lim\limits_{x\to -1^+}\frac{1}{x-1} \cdot \frac{\ln\left[1-(x+1)\right]}{(x+1)} = -\frac{1}{2}$

     $\lim\limits_{x \to -1^-}f(x) = \lim\limits_{x \to -1^-}\frac{\ln (-x)}{(x+1)(x-1)} =\lim\limits_{x\to -1^-}\frac{1}{x-1} \cdot \frac{\ln\left[1-(x+1)\right]}{(x+1)} = \frac{1}{2}$

     $\therefore \pm1是跳跃间断点，0是无穷间断点$
