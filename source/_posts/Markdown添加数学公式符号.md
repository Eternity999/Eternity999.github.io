---
title: Markdown添加数学公式符号
tags:
  - 'Markdown'
  - ''
date: 2021-03-14 01:33:04
updated:
categories: 
keywords:
description: Markdown使用笔记（适用于mathjax）
top _img:
comments:
cover: http://www.codingsoho.com/media/filer_public_thumbnails/filer_public/e0/11/e011e343-d76c-4803-8d4e-c2bde8911fce/markdown.jpg__800x450_q85_crop_subsampling-2.jpg
toc:
toc_number:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax: true
katex: false
aplayer:
highlight_shrink:
aside:
---
1. 指数和下标可以用^和_后加相应字符来实现。
2. 平方根（square root）的输入命令为：\sqrt，n 次方根相应地为: \sqrt[n]。方根符号的大小由LATEX自动加以调整。也可用\surd 仅给出符号。
3. 命令\overline 和\underline 在表达式的上、下方画出水平线。
4. 命令\overbrace 和\underbrace 在表达式的上、下方给出一水平的大括号。
5. 向量（Vectors）通常用上方有小箭头（arrow symbols）的变量表示。这可由\vec 得到。另两个命令\overrightarrow 和\overleftarrow在定义从A 到B 的向量时非常有用。
6. 分数（fraction）使用\frac{…}{…} 排版。一般来说，1/2 这种形式更受欢迎，因为对于少量的分式，它看起来更好些。
7. 积分运算符（integral operator）用\int 来生成。求和运算符（sum operator）由\sum 生成。乘积运算符（product operator）由\prod 生成。上限和下限用^ 和_来生成，类似于上标和下标。
8. 特殊字形：符号：\mathcal，如$ \mathcal{ABC} $； \mathbb，如$ \mathbb{ABC} $ ；\mathscr，如$ \mathscr{ABC} $。


## 符号类
### 希腊字母
|符号	| 写法 |
| :-: | :-: |
| α	| \alpha |
| β	| \beta  |
| γ	| \gamma |
| δ	| \delta |
| Δ	| \Delta |
| ϵ	| \epsil |
| ε	| \varep |
| ζ	| \zeta  |
| η	| \eta   |
| θ	| \theta |
| Θ	| \Theta |
| ϑ	| \varth |
| ι	| \iota  |
| κ	| \kappa |
| λ	| \lambd |
| Λ	| \Lambd |
| μ	| \mu |
| ν	| \nu |
| ξ	| \xi |
| Ξ	| \Xi |
| π	| \pi |
| Π	| \Pi |
| ϖ	| \varpi |
| ρ	| \rho   |
| ϱ	| \varrh |
| σ	| \sigma |
| Σ	| \Sigma |
| ς	| \varsi |
| τ	| \tau   |
| υ	| \upsil |
| Υ	| \Upsil |
| ϕ	| \phi   |
| Φ	| \Phi   |
| φ	| \varph |
| χ	| \chi   |
| ψ	| \psi   |
| Ψ	| \Psi   |
| ω	| \omega |
| Ω	| \Omega |
* 若需要大写希腊字母，将命令首字母大写即可。
* 若需要斜体希腊字母，将命令前加上var前缀即可。
### 运算符号
| 符号 | 写法 |
| :-: | :-: |
| $ x^2 $ | x^2 |
| $ \theta_i $ | \theta_i |
| $ \frac{ x }{ y } $ | \frac{ x }{ y } |
| $ \sqrt{ x } ; \sqrt[n]{ x } $ | \sqrt{ x } ; \sqrt[n]{ x } | 
| $ \partial J $ | \partial J |
|	$ \sum_{k=1}^{m} $ | \sum_{k=1}^{m} |
|	$ \int_{-\pi}^{\pi} x^2 {\rm d}x $ | \int_{-\pi}^{\pi} x^2 {\rm d}x |
|	$ \iiiint $ | \iiiint |
| $ \oint $ | \oint |
| $ \mathrm{d} $ | \mathrm{d} |
| $ \prime $ | \prime |
| $ \imath $ | \imath |
| $ \jmath $ | \jmath |
| $ \infty $ | \infty |
| $ \nabla $ | \nabla |
| $ \lim\limits_{n \rightarrow +\infty} \frac{1}{n(n+1)} $ | \lim\limits_{n \rightarrow +\infty} \frac{1}{n(n+1)} |
|	$ \prod_{i=0}^n \frac{1}{i^2} $ | \prod_{i=0}^n \frac{1}{i^2} |
| $ \frac{d}{dx}e{ax}=ae{ax}\quad \sum_{i=1}^{n}{(X_i-\overline{X})^2} $ | \frac{d}{dx}e{ax}=ae{ax}\quad \sum_{i=1}^{n}{(X_i-\overline{X})^2} |
| $ \vec{a} \cdot \vec{b}=0 $ | \vec{a} \cdot \vec{b}=0 |
| $ limn→+∞nlimn→+∞n \lim_{n\rightarrow+\infty} n $ | limn→+∞nlimn→+∞n \lim_{n\rightarrow+\infty} n |
| $ \frac{\partial f(x,y)}{\partial x} $ | \frac{\partial f(x,y)}{\partial x} |


### 关系运算符
| 符号 | 写法 |
|  :-: | :-: |
| $ \pm $| \pm |
| $ \mp $| \mp |
| $ \times $| \times |
| $ \div $| \div |
| $ \nmid $| \nmid |
| $ \cdot $| \cdot |
| $ \ast $| \ast |
| $ \bigodot $| \bigodot |
| $ \bigotimes $| \bigotimes |
| $ \bigoplus $| \bigoplus |
| $ \leq $| \leq |
| $ \geq $| \geq |
| $ \nleq $| \nleq |
| $ \ngeq $| \ngeq |
| $ \neq $| \neq |
| $ \approx $| \approx |
| $ \equiv $| \equiv |
| $ \coprod $| \coprod |

### 三角运算符
| 符号 | 写法 |
|  :-: | :-: |
| $ \bot $ | \bot |
| $ \angle $ | \angle |
| $ 30^\circ $ | 30^\circ |
| $ \sin $ | \sin |
| $ \cos $ | \cos |
| $ \tan $ | \tan |
| $ \cot $ | \cot |
| $ \sec $ | \sec |
| $ \csc $ | \csc |

### 对数函数
| 符号 | 写法 |
|  :-: | :-: |
| $\ln15 $ | \ln15 |
| $\log_2 10 $ | \log_2 10 |
| $\lg7 $ | \lg7 |

### 逻辑运算符
| 符号 | 写法 |
|  :-: | :-: |
| $ \because $ | \because |
| $ \therefore $ | \therefore |
| $ \forall $ | \forall |
| $ \exists $ | \exists |
| $ \not= $ | \not= |
| $ \not> $ | \not> |
| $ \not\subset $ | \not\subset |

### 戴帽符号
| 符号 | 写法 |
|  :-: | :-: |
| $ \hat{y} $ | \hat{y} |
| $ \check{y} $ | \check{y} |
| $ \breve{y} $ | \breve{y} |
| $ \tilde{y} $ | \tilde{y} |
| $ \bar{y} $ | \bar{y} |
| $ \acute{y} $ | \acute{y} |
| $ \grave{y} $ | \grave{y} |
| $ \mathring{y} $ | \mathring{y} |
| $ \dot{y} $ | \dot{y} |
| $ \ddot{y} $ | \ddot{y} |


### 连线符号
| 符号 | 写法 |
|  :-: | :-: |
| $ \overline{a+b+c+d} $ | \overline{a+b+c+d} |
| $ \underline{a+b+c+d} $ | \underline{a+b+c+d} |
| $ \overbrace{a+\underbrace{b+c}_{1.0}+d}^{2.0} $ | \overbrace{a+\underbrace{b+c}_{1.0}+d}^{2.0} |

### 箭头符号
| 符号 | 写法 |
|  :-: | :-: |
| $	\uparrow $ | \uparrow |
| $	\Uparrow $ | \Uparrow |
| $	\downarrow $ | \downarrow |
| $	\Downarrow $ | \Downarrow |
| $	\rightarrow $ | \rightarrow |
| $	\Rightarrow $ | \Rightarrow |
| $	\leftarrow $ | \leftarrow |
| $	\Leftarrow $ | \Leftarrow |
| $	\longleftarrow $ | \longleftarrow |
| $	\Longleftarrow $ | \Longleftarrow |
| $	\longrightarrow $ | \longrightarrow |
| $	\Longrightarrow $ | \Longrightarrow |

### 省略号
| 符号 | 写法 | 名字 |
|  :-: | :-: | :-: |
| $	\ldots $ | \ldots | 底端对齐的省略号 |
| $	\cdots $ | \cdots | 中线对齐的省略号 |
| $	\vdots $ | \vdots | 竖直对齐的省略号 |
| $	\ddots $ | \ddots | 斜对齐的省略号 |

### 集合运算
| 符号 | 写法 | 名字 |
|  :-: | :-: | :-: |
| $	x\in y $ | x\in y | 属于运算 |
| $	x\notin y $ | x\notin y | 不属于运算 |
| $	x\not\in y $ | x\not\in y | 不属于运算 |
| $	x\subset y $ | x\subset y | 子集运算 |
| $	x、supset y $ | x、supset y | 子集运算 |
| $	x\subseteq y $ | x\subseteq y | 真子集运算 |
| $	x\subsetneq y $ | x\subsetneq y | 非真子集运算 |
| $	x\supseteq y $ | x\supseteq y | 真子集运算 |
| $	x\supsetneq y $ | x\supsetneq y | 非真子集运算 |
| $	x\not\subset y $ | x\not\subset y | 非子集运算 |
| $	x\not\supset y $ | x\\not\supset y | 非子集运算 |
| $	x\cup y $ | x\cup y | 并集运算 |
| $	x\cap y $ | x\cap y | 交集运算 |
| $	x\setminus y $ | x\setminus y | 差集运算 |
| $	x\bigodot y $ | x\bigodot y | 同或运算 |
| $	x\bigotimes y $ | x\bigotimes y | 同与运算 |
| $	\mathbb{R} | \mathbb{R} | 实数集合 |
| $	\mathbb{Z} | \mathbb{Z} | 自然数集合 |
| $	\emptyset $ | \emptyset | 空集 |
| $	\forall $ | \forall | 任意符号 |
| $	\exists y $ | \exists | 存在符号 |

### 括号
| 符号 | 写法 |
|  :-: | :-: |
| 大括号:$ \lbrace a+x \rbrace $ | \lbrace a+x \rbrace |
| 尖括号:$ \langle x \rangle $ | \langle x \rangle |
| 上取整:$ \lceil \frac{x}{2} \rceil $ | \lceil \frac{x}{2} \rceil |
| 下取整:$ \lfloor x \rfloor $ | \lfloor x \rfloor |
| 原始括号:$ \lbrace \sum_{i=0}^{n}i^{2}=\frac{2a}{x^2+1} \rbrace $	| \lbrace \sum_{i=0}^{n}i^{2}=\frac{2a}{x^2+1} \rbrace |
| 全包括号:$ \left\lbrace \sum_{i=0}^{n}i^{2}=\frac{2a}{x^2+1} \right\rbrace $	| \left\lbrace \sum_{i=0}^{n}i^{2}=\frac{2a}{x^2+1} \right\rbrace |
| 上大括号:$ \overbrace{1+2+3+4}^{2.0} $ | \overbrace{1+2+3+4}^{2.0} |
| 下大括号:$ \underbrace{1+2+3+4}_{2.0} $ | \underbrace{1+2+3+4}_{2.0} |
```markdown
$$ \big(\big) \Big(\Big) \bigg(\bigg) \Bigg(\Bigg) $$
```
$$ \big(\big) \Big(\Big) \bigg(\bigg) \Bigg(\Bigg) $$

### 占位符
两个quad空格，符号：\qquad，如：$ x\qquad y $
quad空格，符号：\quad，如：$ x\quad y $

### 矩阵类
| 符号 | 写法 |
|  :-: | :-: |
| $ \vec{ a } $ | \vec{ a } |

给公式编号,如（1）
```markdown
$$e^{i\theta}=cos\theta+\sin\theta i\tag{1}$$
```
$$e^{i\theta}=cos\theta+\sin\theta i\tag{1}$$

## 使用Google Chart的服务器
```html
<img src="http://chart.googleapis.com/chart?cht=tx&chl= 在此插入Latex公式" style="border:none;">
````
例如：
```html
<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" style="border:none;">
```
公式显示结果为：（需要科学上网才能 load 出来）
<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" style="border:none;">

### 参考资料
[Cmd Markdown 公式指导手册](https://www.zybuluo.com/codeep/note/163962)
[Markdown数学公式语法](https://www.cnblogs.com/xym4869/p/11282586.html)