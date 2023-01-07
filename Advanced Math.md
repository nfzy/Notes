# Chapter 1 函数与极限

## 映射

### 单射

$f:R \rightarrow R, \forall x \in R,f(x) = x^2$

### 满射

$X = \{(x,y) | x^2 +y^2 = 1\}, Y = \{(x,0) | |x| \leq 1\}, f:X\rightarrow Y$

### 一一映射

$f:[-\frac{\pi}{2}, \frac{\pi}{2}] \rightarrow [-1,1], f(x) = \sin x$



## 定理推导

### 极限

#### 极限数列不等式性质

设$\lim\limits_{n\to\infin}x_n = a,\quad\lim\limits_{n \to \infin}y_n = b$

1.   若$a>b$，则$\exist N$，当$n>N$时有$x_n > y_n$
2.   若$n>N$时$x_n \geq y_n$，则$a \geq b$

$$\forall \varepsilon = \frac{a+b}{2},\quad\exists N_1,|x_n - a| < \varepsilon\quad\exist N_2 ,\ |y_n - b| < \varepsilon,\\M = max\{N_1, N_2\}||\\ \because|x_n - a|< \frac{(a-b)}{2}\ \therefore x_n>\frac{(a+b)}{2}\\ \because|y_n - b|< \frac{(a-b)}{2} \therefore y_n>\frac{(a+b)}{2}\\\therefore x_n > y_n$$

### 拉格朗日中值定理

$$F'(x) = f'(x) - \frac{f(b)-f(a)}{b-a}\\ F(x) = f(x) - \frac{f(b)-f(a)}{b-a}\cdot x\\F(a) = f(a) - \frac{f(b)-f(a)}{b-a}\cdot a = \frac{bf(a) - af(b)}{b-a}\\F(b) = f(b) - \frac{f(b)-f(a)}{b-a}\cdot b = \frac{bf(a) - af(b)}{b-a} \\ F(a) = F(b).\\由罗尔定理得有一点得\xi\in(a,b),使得F'(\xi) = 0.\\ 即f'(\xi) = \frac{f(b)-f(a)}{b-a} \Longrightarrow f(b)-f(a) = f'(\xi)(b-a).$$

### 柯西中值定理

$$G'(x) = f'(x)\cdot[F(b)-F(a)] - F'(x)\cdot [f(b)-f(a)]\\G(x) =  f(x)\cdot[F(b)-F(a)] - F(x)\cdot[f(b)-f(a)]\\G(a) = f(a)\cdot[F(b)-F(a)] - F(a)\cdot[f(b)-f(a)] = f(a)\cdot F(b) - F(a)\cdot f(b)\\G(b) = f(b)\cdot[F(b)-F(a)] - F(b)\cdot[f(b)-f(a)] = f(a)\cdot F(b) - F(a)\cdot f(b)\\G(a) =G(b)\\由罗尔定理得有一点得\xi\in(a,b),使得G'(\xi) = 0.\\ 即 \frac{f(b)-f(a)}{F(b)-F(a)} = \frac{f'(\xi)}{F'(\xi)}$$

### 定积分

1.   $[a_1, b_1] \subset[a,b]\ f(x)\equiv -1,则\int_{a_1}^{b1}f(x)dx>\int_a^bf(x)dx$


## 错题
### 一元函数的导数与微分概念及其计算

1. 设 $f(x_0) \not = 0 ,f(x)$ 在 $x=x_0$ 连续，则 $f(x)$ 在 $x_0$ 可导是 $|f(x)|$ 在 $x_0$ 处可导的***充分必要***条件
   解析：由 $f(x_0) \not= 0 \Rightarrow f(x_0) > 0$ 或 $f(x_0) < 0$ ，因 $f(x)$ 在点 $x_0$ 处连续，则 $f(x)$ 在 $x_0$ 某邻域是保号的，即 $\delta > 0$ ,当 $|x-x_0|< \delta$ 时，

2. 设 $f(x)$ 在点 $x_0$ 处可导，且 $f(x_0) = 0$ ,则 $f'(x_0) = 0$ 是 $|f(x)|$ 在 $x_0$ 可导的***充分必要***条件.

3. 设 $F(x) = g(x)\varphi(x),\varphi(x)$ 在 $x = a$ 连续但不可导，又 $g'(x)$ 存在，则 $g(a) = 0$ 是 $F(x)$ 在 $x = a$ 可导的***充分必要***条件.
    解析：由
    $
    \begin{aligned}
    F'(x)& =\lim\limits_{x\to a}\frac{F(x) - F(a)}{x - a} \\&=\lim\limits_{x\to a}\frac{g(x)\varphi(x) - g(a)\varphi(a)}{x - a} \\&=\lim\limits_{x\to a}\frac{g(x) - g(a)}{x-a}\cdot\varphi(x)\\& = \lim\limits_{x\to a} \varphi(x)\cdot g'(a)\\& = \varphi(a)\cdot g'(a)
    \end{aligned}
    $

4. 把 $y$ 看作自变量，$x$ 为因变量，变换方程 $\frac{dy}{dx}\cdot \frac{d^3y}{dx^3} - 3(\frac{d^2y}{dx^2})^2 = x$

    *   $\frac{dy}{dx} = \frac{1}{\frac{dx}{dy}} = (\frac{dx}{dy})^{-1}$

    *   $\frac{d^2y}{dx^2} = \frac{d[(\frac{dx}{dy})^{-1}]}{dx} = \frac{d[(\frac{dx}{dy})^{-1}]}{dy}\cdot \frac{dy}{dx} = (-1)\cdot (\frac{dx}{dy})^{-3}\cdot \frac{d^2x}{dy^2}$

    *   $\frac{d^3y}{dx^3} = \frac{d[-(\frac{dx}{dy})^{-3}\cdot \frac{d^2x}{dy^2}]}{dx}  = \cdots = 3(\frac{dx}{dy})^{-5}\cdot({\frac{d^2x}{dy^2}})^{2} - (\frac{dx}{dy})^{-4}\cdot \frac{d^3x}{dy^3}$
    
    *   $\therefore 即\frac{d^3x}{dy^3} + x(\frac{dx}{dy})^{5} = 0$ 
    

​	