---
title: "Теория вероятностей и математическая статистика"
subtitle: "Непрерывные распределения."
institute: "Программы БИ, УЦП, ТАДвБ ВШБ ВШЭ."
author: "Глеб Карпов"
format: 
    beamer:
        pdf-engine: xelatex
        aspectratio: 169
        fontsize: 9pt
        theme: Singapore
        fonmttheme: serif
        section-titles: true
        incremental: false
        include-in-header: ../files/xeheader.tex  # Custom LaTeX commands and preamble
---

## Равномерное распределение

В первом физическом примере линейная плотность была **постоянной** на отрезке $[0,\, 10]$ и нулевой вне него.

\begin{tikzpicture}
    \begin{scope}[yshift=2.6cm]
        \begin{axis}[
            width=9.5cm, height=1.6cm,
            xmin=-1, xmax=12, ymin=-0.4, ymax=1.4,
            axis lines=center,
            xlabel={$x$}, ylabel={Объект},
            xtick={0,2,4,6,8,10}, ytick=\empty,
            xlabel style={below}, ylabel style={left},
            grid=major, grid style={dashed,gray!30}, clip=false
        ]
        \addplot[thick, blue, fill=blue!20, fill opacity=0.7] coordinates {
            (0,0) (0,1) (10,1) (10,0) (0,0)
        } \closedcycle;
        \node[above] at (5,1) {Рельс :)};
        \end{axis}
    \end{scope}

    \begin{scope}
        \begin{axis}[
            width=9.5cm, height=3.4cm,
            xmin=-1, xmax=12, ymin=-0.05, ymax=0.18,
            axis lines=center,
            xlabel={$x$}, ylabel={$f_X(x)$},
            xtick={0,2,4,6,8,10},
            ytick={0,0.1}, yticklabels={0,$1/10$},
            xlabel style={below}, ylabel style={left},
            grid=major, grid style={dashed,gray!30}, clip=false
        ]
        \addplot[thick, red, fill=red!20, fill opacity=0.6, domain=0:10, samples=50] {0.1} \closedcycle;
        \addplot[thick, red, domain=-1:0, samples=5] {0};
        \addplot[thick, red, domain=10:12, samples=5] {0};
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        \end{axis}
    \end{scope}

    \begin{scope}[xshift=10.2cm, yshift=0.4cm]
        \node[draw, fill=gray!10, rounded corners, align=center, font=\small] at (0,0.8) {
            $X \sim U(0,10)$\\[0.3em]
            $f_X(x)=\dfrac{1}{10}$ на $[0,10]$
        };
        \node[align=left, font=\small] at (0,-0.7) {
            Постоянная плотность\\
            $=$ равномерность
        };
    \end{scope}
\end{tikzpicture}

## Равномерное распределение
### Определение

:::{.callout-definition}
Случайная величина $X$ имеет **равномерное распределение** на отрезке $[a,b]$ ($a < b$), пишем $X \sim U(a,b)$, если
$$
f_X(x) =
\begin{cases}
\dfrac{1}{b-a}, & a \leq x \leq b,\\[0.4em]
0, & \text{иначе.}
\end{cases}
$$
:::

- Высота прямоугольника подобрана так, чтобы площадь равнялась $1$: $\displaystyle (b-a)\cdot\frac{1}{b-a} = 1$.
- Интерпретация: вероятность «равномерно размазана» по $[a,b]$; ни одна точка внутри отрезка не предпочтительнее другой.

## Равномерное распределение
### Функция распределения

Для $X \sim U(a,b)$ накопленная вероятность — это кумулятивная масса из физической аналогии:
$$
F_X(x) =
\begin{cases}
0, & x < a,\\[0.3em]
\dfrac{x-a}{b-a}, & a \leq x \leq b,\\[0.3em]
1, & x > b.
\end{cases}
$$

\begin{tikzpicture}
    \begin{scope}
        \begin{axis}[
            width=7.5cm, height=3.8cm,
            xmin=-1, xmax=12, ymin=-0.05, ymax=0.18,
            axis lines=center,
            xlabel={$x$}, ylabel={$f_X(x)$},
            xtick={0,10}, xticklabels={$a{=}0$,$b{=}10$},
            ytick={0,0.1}, yticklabels={0,$1/(b-a)$},
            xlabel style={below}, ylabel style={left},
            grid=major, grid style={dashed,gray!30}, clip=false,
            title={Плотность}
        ]
        \addplot[thick, red, fill=red!20, fill opacity=0.55, domain=0:10, samples=40] {0.1} \closedcycle;
        \addplot[thick, red, domain=-1:0, samples=5] {0};
        \addplot[thick, red, domain=10:12, samples=5] {0};
        \draw[thick, red] (0,0) -- (0,0.1);
        \draw[thick, red] (10,0) -- (10,0.1);
        \end{axis}
    \end{scope}

    \begin{scope}[xshift=8.2cm]
        \begin{axis}[
            width=7.5cm, height=3.8cm,
            xmin=-1, xmax=12, ymin=-0.1, ymax=1.25,
            axis lines=center,
            xlabel={$x$}, ylabel={$F_X(x)$},
            xtick={0,10}, xticklabels={$a$,$b$},
            ytick={0,0.5,1},
            xlabel style={below}, ylabel style={left},
            grid=major, grid style={dashed,gray!30}, clip=false,
            title={Функция распределения}
        ]
        \addplot[thick, violet, domain=-1:0, samples=5] {0};
        \addplot[thick, violet, domain=0:10, samples=60] {0.1*x};
        \addplot[thick, violet, domain=10:12, samples=5] {1};
        \end{axis}
    \end{scope}
\end{tikzpicture}

## Равномерное распределение
### Математическое ожидание

Пусть $X \sim U(a,b)$. Плотность кусочно задана на трёх областях — разбиваем интеграл по этим же областям:
$$
f_X(x) =
\begin{cases}
\textcolor{red}{0}, & x < a \\
\textcolor{violet}{1/(b-a)}, & a \leq x \leq b \\
\textcolor{blue}{0}, & x > b
\end{cases}
$$

\begin{gather*}
E[X] = \int\limits_{-\infty}^{+\infty} x f_X(x)\, dx
= \int\limits_{-\infty}^{a} x\,\textcolor{red}{f_X(x)}\, dx
+ \int\limits_{a}^{b} x\,\textcolor{violet}{f_X(x)}\, dx
+ \int\limits_{b}^{+\infty} x\,\textcolor{blue}{f_X(x)}\, dx \\[0.4em]
= \int\limits_{-\infty}^{a} x\,\textcolor{red}{0}\, dx
+ \int\limits_{a}^{b} x\,\textcolor{violet}{\frac{1}{b-a}}\, dx
+ \int\limits_{b}^{+\infty} x\,\textcolor{blue}{0}\, dx
= \frac{1}{b-a} \cdot \frac{x^2}{2}\Big|_{a}^{b}
= \frac{b^2 - a^2}{2(b-a)} = \frac{(b-a)(b+a)}{2(b-a)} = \frac{a+b}{2}.
\end{gather*}

Среднее — середина отрезка $[a,b]$.

## Равномерное распределение
### Второй момент и дисперсия

Снова три области плотности:
\begin{gather*}
E[X^2] = \int\limits_{-\infty}^{+\infty} x^2 f_X(x)\, dx
= \int\limits_{-\infty}^{a} x^2\,\textcolor{red}{f_X(x)}\, dx
+ \int\limits_{a}^{b} x^2\,\textcolor{violet}{f_X(x)}\, dx
+ \int\limits_{b}^{+\infty} x^2\,\textcolor{blue}{f_X(x)}\, dx \\[0.4em]
= \int\limits_{-\infty}^{a} x^2\,\textcolor{red}{0}\, dx
+ \int\limits_{a}^{b} x^2\,\textcolor{violet}{\frac{1}{b-a}}\, dx
+ \int\limits_{b}^{+\infty} x^2\,\textcolor{blue}{0}\, dx
= \frac{1}{b-a} \cdot \frac{x^3}{3}\Big|_{a}^{b}
= \frac{b^3 - a^3}{3(b-a)}.
\end{gather*}

Разложение $b^3-a^3=(b-a)(a^2+ab+b^2)$ даёт $E[X^2]=\dfrac{a^2+ab+b^2}{3}$. Тогда
\begin{gather*}
\operatorname{Var}[X] = E[X^2] - \bigl(E[X]\bigr)^2
= \frac{a^2+ab+b^2}{3} - \left(\frac{a+b}{2}\right)^2
= \frac{4(a^2+ab+b^2) - 3(a+b)^2}{12}
= \frac{(b-a)^2}{12}.
\end{gather*}

## Экспоненциальное распределение
### Определение и примеры

Типичные ситуации: время до отказа прибора, время ожидания следующего звонка, время между событиями простого потока с интенсивностью $\lambda$.

:::{.callout-definition}
Случайная величина $X$ имеет **экспоненциальное распределение** с параметром $\lambda > 0$, пишем $X \sim \operatorname{Exp}(\lambda)$, если
$$
f_X(x) =
\begin{cases}
\textcolor{red}{0}, & x < 0,\\[0.3em]
\textcolor{violet}{\lambda e^{-\lambda x}}, & x \geq 0.
\end{cases}
$$
:::

Функция распределения:
$$
F_X(x) =
\begin{cases}
0, & x < 0,\\[0.3em]
1 - e^{-\lambda x}, & x \geq 0.
\end{cases}
$$

Параметр $\lambda$ — интенсивность: чем больше $\lambda$, тем быстрее «убывает» плотность и тем меньше типичные значения $X$.

## Экспоненциальное распределение
### Математическое ожидание

Две области плотности:
\begin{gather*}
E[X] = \int\limits_{-\infty}^{+\infty} x f_X(x)\, dx
= \int\limits_{-\infty}^{0} x\,\textcolor{red}{f_X(x)}\, dx
+ \int\limits_{0}^{+\infty} x\,\textcolor{violet}{f_X(x)}\, dx \\[0.4em]
= \int\limits_{-\infty}^{0} x\,\textcolor{red}{0}\, dx
+ \int\limits_{0}^{+\infty} x\,\textcolor{violet}{\lambda e^{-\lambda x}}\, dx.
\end{gather*}

Интегрирование по частям ($u=x$, $dv=\lambda e^{-\lambda x}\,dx$):
\begin{gather*}
\int\limits_{0}^{+\infty} x\,\lambda e^{-\lambda x}\, dx
= \Bigl[-x e^{-\lambda x}\Bigr]_{0}^{+\infty}
+ \int\limits_{0}^{+\infty} e^{-\lambda x}\, dx
= 0 + \frac{1}{\lambda}\Bigl[-e^{-\lambda x}\Bigr]_{0}^{+\infty}
= \frac{1}{\lambda}.
\end{gather*}

Итак, $\displaystyle E[X] = \frac{1}{\lambda}$.

## Экспоненциальное распределение
### Дисперсия

$$
\operatorname{Var}[X] = E[X^2] - \bigl(E[X]\bigr)^2
= \frac{2}{\lambda^2} - \left(\frac{1}{\lambda}\right)^2
= \frac{1}{\lambda^2}.
$$

Итого для $X \sim \operatorname{Exp}(\lambda)$: $\displaystyle E[X]=\frac{1}{\lambda}$, $\displaystyle \operatorname{Var}[X]=\frac{1}{\lambda^2}$.

## Нормальное распределение

\begin{itemize}
    \item Функция плотности вероятности параметризована двумя константами $\mu$ и $\sigma^2$ и записывается как:
$$
    f_X(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2\sigma^2}}, \; \forall x \in \mathbb{R}
$$

    \item Параметры влияют на вид функции плотности и, как следствие, на "поведение" нормальной случайной величины. Чтобы подчеркнуть конкретную нормальную величину, с конкретно рассматриваемым набором параметров, мы пишем:
$$
    X \sim \mathcal{N} \, (\mu, \sigma^2)
$$

\end{itemize}

::: {.callout-note title="Характеристики нормальной величины"}
Имеет место интересное совпадение параметров и характеристик нормальной случайной величины:
$$
    E[X] = \mu, \; Var[X] = \sigma^2
$$
Будьте внимательны, в общем случае параметры и характеристики случайной величины совпадать не обязаны.
:::

## Влияние параметров на функцию плотности

![Влияние параметра $\mu$](mu_influence_normal.pdf){#fig-mu}

## Влияние параметров на функцию плотности

![Влияние параметра $\sigma$](sigma_influence_normal.pdf){#fig-sigma}

## Влияние параметров на функцию плотности

![Влияние параметра $\sigma$](sigma_area_diff.pdf){#fig-sigma-diff}

## Стандартная нормальная величина
### Все нормальные равны, но одно равнее других

\begin{itemize}
    \item Поскольку существует бесконечное число пар $(\mu, \sigma^2)$, существует также бесконечное число различных нормальных распределений.
    \item Это потребовало бы вычисления десятков сложных вероятностных интегралов каждый раз.
    \item Что если вычисление вероятности \textbf{любой} нормальной СВ можно свести к знанию всего одной переменной?
\end{itemize}

## Стандартная нормальная величина
### Все нормальные равны, но одно равнее других

\begin{itemize}
    \item Встречайте \textit{стандартную} нормальную случайную величину:
$$
    Z \sim \mathcal{N} \, (0,1), \quad f_Z(x) = \frac{1}{\sqrt{2 \pi}} e^{-\frac{x^2}{2}}, \; \forall x \in \mathbb{R}
$$

    \item Давным-давно математики вычислили десятки вероятностных интегралов и создали таблицу стандартного нормального распределения, которая показывает значения функции распределения $F_Z(x)$ для многих возможных значений $x$.
    \item Мы можем найти любую вероятность любой нормальной случайной величины, преобразовав её в стандартную нормальную.
\end{itemize}

## Стандартная нормальная величина
### Формула преобразования

- Пусть $X$ — нормальная случайная величина и $X \sim \mathcal{N} \, (\mu, \sigma^2)$.
- Тогда следующая функция (преобразование) преобразует $X$ в стандартную нормальную величину:
$$
    Z = \frac{X - \mu}{\sigma}
$$
![Преобразование в стандартную нормальную](x2z_transform.pdf){#fig-x2z}

## Стандартная нормальная величина
### Преобразование сохраняет накопленные вероятности

![Равные накопленные площади до $a$ и $a'$](x2z_transform_areas.pdf){#fig-x2z-areas}

## Стандартная нормальная величина

Ключевое свойство: кумулятивная площадь под плотностью **до** точки не меняется при стандартизации. Если $a' = \dfrac{a - \mu}{\sigma}$ — образ точки $a$, то
$$
P(X \leq a) = P\!\left(Z \leq a'\right)
\quad\Longleftrightarrow\quad
F_X(a) = F_Z(a').
$$

- Пусть $X$ — нормальная случайная величина и $X \sim \mathcal{N} \, (\mu, \sigma^2)$.
- Нас интересует некоторая вероятность $P(a < X < b)$, $\forall a, \, b: a \leq b$.
- Применим преобразование к каждой части неравенства, чтобы не нарушить его:
\begin{equation*}
    P(a < X < b) = P \left( \underbrace{\frac{a - \mu}{\sigma}}_{\tilde{a}} < \underbrace{\frac{X - \mu}{\sigma}}_{Z} < \underbrace{\frac{b - \mu}{\sigma}}_{\tilde{b}}  \right) =  P \left( \tilde{a} < Z < \tilde{b} \right) = F_Z(\tilde{b}) - F_Z(\tilde{a}).
\end{equation*}

## Стандартная нормальная величина

![Вычисление вероятности с использованием ФР](normal_cdf_diff.pdf){#fig-normal_cdf_diff}

## Стандартная нормальная величина
![Таблица стандартного нормального распределения](normal_distr_table.pdf){#fig-normal_table}


## Пример

Если $X$ — нормально распределенная случайная величина со средним $6$ и дисперсией $25$, найти:
    \begin{enumerate}
        \item $P(6 \leq X \leq 12)$,
        \item $P(0 \leq X \leq 8)$,
        \item $P(-2 < X \leq 0)$.
    \end{enumerate}

## Пример
### Вопрос 1

$P(6 \leq X \leq 12)$

\begin{itemize}
    \item $X \sim \mathcal{N}(6, 25)$, значит $\mu = 6$, $\sigma = 5$
    \item Преобразование: $Z = \frac{X - 6}{5}$
    \item $P(6 \leq X \leq 12) = P\left(\frac{6-6}{5} \leq Z \leq \frac{12-6}{5}\right) = P(0 \leq Z \leq 1.2)$
    \item $= F_Z(1.2) - F_Z(0) = 0.8849 - 0.5 = 0.3849$
\end{itemize}

## Пример
### Визуализация вопроса 1

![](problem_1.png){#fig-problem-1 width=70%}

## Пример
### Вопрос 2

$P(0 \leq X \leq 8)$

\begin{itemize}
    \item Преобразование: $Z = \frac{X - 6}{5}$
    \item $P(0 \leq X \leq 8) = P\left(\frac{0-6}{5} \leq Z \leq \frac{8-6}{5}\right) = P(-1.2 \leq Z \leq 0.4)$
    \item Используем свойство симметрии: $F_Z(-1.2) = 1 - F_Z(1.2) = 1 - 0.8849 = 0.1151$
    \item $= F_Z(0.4) - F_Z(-1.2) = 0.6554 - 0.1151 = 0.5403$
\end{itemize}

## Пример
### Визуализация вопроса 2

![Визуализация вопроса 2](problem_2.png){#fig-problem-2 width=70%}

## Пример
### Вопрос 3

$P(-2 < X \leq 0)$

\begin{itemize}
    \item Преобразование: $Z = \frac{X - 6}{5}$
    \item $P(-2 < X \leq 0) = P\left(\frac{-2-6}{5} < Z \leq \frac{0-6}{5}\right) = P(-1.6 < Z \leq -1.2)$
    \item Используем свойство симметрии: $F_Z(-1.2) = 1 - F_Z(1.2) = 1 - 0.8849 = 0.1151$
    \item $F_Z(-1.6) = 1 - F_Z(1.6) = 1 - 0.9452 = 0.0548$
    \item $= F_Z(-1.2) - F_Z(-1.6) = 0.1151 - 0.0548 = 0.0603$
\end{itemize}

## Пример
### Визуализация вопроса 3

![Визуализация вопроса 3](problem_3.png){#fig-problem-3 width=70%}
