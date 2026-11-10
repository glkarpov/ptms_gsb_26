---
title: "Теория вероятностей и математическая статистика"
subtitle: "Многомерное нормальное распределение. Центральная предельная теорема."
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
## Напоминание: Линейная комбинация случайных величин

Предположим, что у нас есть $X$ и $Y$ — две случайные величины. Следующие свойства работают для *любой* возможной природы этих переменных.

\begin{enumerate}
    \item Линейное свойство математического ожидания: $E[aX \pm bY] = a E[X] \pm b E[Y]$.
    \item Дисперсия линейной комбинации: $Var[aX \pm bY] = a^2 Var[X] + b^2 Var[Y] \pm 2ab\biggl(E[XY] - E[X]E[Y]\biggr)$.
    \item Если $X$ и $Y$ независимы: $Var[aX \pm bY] = a^2 Var[X] + b^2 Var[Y]$.
\end{enumerate}

## Многомерное нормальное распределение (МНР)

:::{.callout-definition}
Пара случайных величин $(X, Y)$ имеет **двумерное нормальное распределение**, если для всех $a, b \in \mathbb{R}$ линейная комбинация $aX + bY$ имеет одномерное нормальное распределение.
:::

:::{.callout-definition}
Вектор случайных величин $\mathbf{X} = (X_1, X_2, \ldots, X_n)$ имеет **многомерное нормальное распределение** (МНР), если для всех векторов $\mathbf{a} \in \mathbb{R}^n$ линейная комбинация $\mathbf{a}^{\top} \mathbf{X}$ имеет одномерное нормальное распределение.

$\mathbf{a}^{\top} \mathbf{X} = a_1 X_1 + a_2 X_2 + \ldots + a_n X_n$
:::


## Устойчивость нормального распределения

\begin{itemize}
    \item \textbf{Ключевое свойство}: Нормальное распределение \textbf{устойчиво} относительно линейных преобразований.
    
    \item Если $X \sim \mathcal{N}(\mu, \sigma^2)$, то для любых констант $a \neq 0$ и $b$:
    $$
    Y = aX + b \sim \mathcal{N}(a\mu + b, a^2\sigma^2)
    $$
    
    \item \textbf{Интерпретация}: Линейное преобразование нормальной случайной величины даёт нормальную случайную величину.
\end{itemize}

## Устойчивость нормального распределения
### Линейная комбинация двух независимых нормальных величин

Пусть $X_1 \sim \mathcal{N}(\mu_1, \sigma_1^2)$, $X_2 \sim \mathcal{N}(\mu_2, \sigma_2^2)$ независимы, и $Y = a X_1 + b X_2$.

\begin{enumerate}
    \item \textbf{Характеристики} (работают для любых случайных величин):
    $$
    E[Y] = a\mu_1 + b\mu_2, \qquad
    \operatorname{Var}(Y) = a^2\sigma_1^2 + b^2\sigma_2^2.
    $$
    \item \textbf{Тип распределения}: независимые нормальные $(X_1, X_2)$ задают двумерное нормальное распределение, поэтому $Y = aX_1 + bX_2$ тоже нормальна.
    \item \textbf{Параметры}: у нормального закона параметры совпадают с матожиданием и дисперсией, значит
    $$
    Y \sim \mathcal{N}\bigl(a\mu_1 + b\mu_2,\; a^2\sigma_1^2 + b^2\sigma_2^2\bigr).
    $$
\end{enumerate}

Частный случай $a = b = 1$: $X_1 + X_2 \sim \mathcal{N}(\mu_1 + \mu_2, \sigma_1^2 + \sigma_2^2)$.

## Устойчивость нормального распределения
### Обобщение на $n$ переменных

Пусть $X_1, \ldots, X_n$ независимы и $X_i \sim \mathcal{N}(\mu_i, \sigma_i^2)$, а $Y = \sum_{i=1}^{n} a_i X_i$.

\begin{enumerate}
    \item \textbf{Характеристики} (по свойствам $E$ и $\operatorname{Var}$):
    $$
    E[Y] = \sum_{i=1}^{n} a_i \mu_i, \qquad
    \operatorname{Var}(Y) = \sum_{i=1}^{n} a_i^2 \sigma_i^2.
    $$
    \item \textbf{Тип распределения}: набор независимых нормальных величин имеет многомерное нормальное распределение, поэтому любая линейная комбинация $Y$ нормальна.
    \item \textbf{Параметры}: раз параметры нормального закона — это как раз $E[Y]$ и $\operatorname{Var}(Y)$, получаем
    $$
    Y \sim \mathcal{N}\left(\sum_{i=1}^{n} a_i \mu_i,\; \sum_{i=1}^{n} a_i^2 \sigma_i^2\right).
    $$
\end{enumerate}

## Логика высказываний: независимость и многомерное нормальное

\begin{center}
\begin{tikzpicture}
    \filldraw[thick, fill=blue!12] (0,0) circle (3.0);
    \filldraw[thick, fill=orange!30] (0.2,-0.55) circle (1.45);
    \node[font=\small] at (0,2.35) {многомерное нормальное};
    \node[font=\small, align=center] at (0.2,-0.55) {независимые\\нормальные};

    % B: MVN, но зависимые
    \fill (-1.15,0.55) circle (0.1);
    \node[left, font=\small, align=right] at (-1.3,0.55) {$B$: MVN,\\но зависимы};

\end{tikzpicture}
\end{center}

Независимые нормальные величины всегда дают многомерное нормальное распределение (внутренний круг).
Обратное неверно: бывает многомерное нормальное с зависимыми компонентами.

## МНР с зависимыми компонентами
### Как считать параметры линейной комбинации

Пусть $(X,Y)$ — двумерное нормальное, $E[X]=\mu_X$, $E[Y]=\mu_Y$,
$\operatorname{Var}(X)=\sigma_X^2$, $\operatorname{Var}(Y)=\sigma_Y^2$, и $\operatorname{Cov}(X,Y)=\sigma_{XY} \neq 0$
(компоненты зависимы). Рассмотрим $T = aX \pm bY$.

\begin{enumerate}
    \item \textbf{Характеристики} (общие формулы; независимость не нужна):
    $$
    E[T] = a\mu_X \pm b\mu_Y,
    \qquad
    \operatorname{Var}(T) = a^2\sigma_X^2 + b^2\sigma_Y^2 \pm 2ab\,\sigma_{XY}.
    $$
    Появился «перекрёстный» элемент $\pm 2ab\,\sigma_{XY}$: если бы $X$ и $Y$ были независимы, он бы исчез.
    \item \textbf{Тип}: если $(X,Y)$ многомерно нормально, то линейная комбинация $T=aX\pm bY$ имеет нормальное распределение.
    \item \textbf{Параметры}: у нормального закона они совпадают с характеристиками, поэтому
    $$
    T \sim \mathcal{N}\bigl(a\mu_X \pm b\mu_Y,\; a^2\sigma_X^2 + b^2\sigma_Y^2 \pm 2ab\,\sigma_{XY}\bigr).
    $$
\end{enumerate}

## Ковариационная матрица

Дисперсию и ковариацию пары $(X,Y)$ записывают в виде \textbf{ковариационной матрицы}
$$
\Sigma =
\begin{pmatrix}
\operatorname{Var}(X) & \operatorname{Cov}(X,Y) \\
\operatorname{Cov}(Y,X) & \operatorname{Var}(Y)
\end{pmatrix}
=
\begin{pmatrix}
\sigma_X^2 & \sigma_{XY} \\
\sigma_{XY} & \sigma_Y^2
\end{pmatrix}.
$$

\begin{itemize}
    \item На диагонали стоят дисперсии, вне диагонали — ковариации.
    \item Матрица симметрична: $\operatorname{Cov}(X,Y)=\operatorname{Cov}(Y,X)$.
    \item При независимости $X$ и $Y$ имеем $\sigma_{XY}=0$, и $\Sigma$ диагональна.
    \item При $\sigma_{XY}\neq 0$ - это как раз случай многомерного нормального распределения с зависимыми компонентами.
\end{itemize}

## Пример
### Двумерное нормальное с ненулевой ковариацией

Пусть известно, что $(X,Y)$ имеет двумерное нормальное распределение,
$$
E[X]=2,\quad E[Y]=6,\quad \operatorname{Var}(X)=4,\quad \operatorname{Var}(Y)=4,\quad \operatorname{Cov}(X,Y)=\tfrac12.
$$

\begin{enumerate}
    \item Запишите ковариационную матрицу $\Sigma$.
    \item Найдите распределение суммы $T=X+Y$.
    \item Вычислите $P(X+Y > 11)$.
\end{enumerate}

## Пример
### Решение: двумерное нормальное с ненулевой ковариацией

$$
\Sigma =
\begin{pmatrix}
\operatorname{Var}(X) & \operatorname{Cov}(X,Y) \\
\operatorname{Cov}(Y,X) & \operatorname{Var}(Y)
\end{pmatrix}
=
\begin{pmatrix}
4 & 1/2 \\
1/2 & 4
\end{pmatrix}.
$$
Характеристики суммы:
\begin{align*}
E[T] &= E[X]+E[Y] = 2+6 = 8,\\
\operatorname{Var}(T) &= \operatorname{Var}(X)+\operatorname{Var}(Y)+2\operatorname{Cov}(X,Y)
= 4+4+2\cdot\tfrac12 = 9.
\end{align*}
Так как $(X,Y)$ двумерно нормально, то линейная комбинация $T$ имеет нормальное распределение. Для него параметры совпадают с характеристиками:
$$
\mu_T = E[T] = 8, \qquad \sigma_T^2 = \operatorname{Var}(T) = 9,
$$
поэтому $T\sim\mathcal{N}(\mu_T,\sigma_T^2)=\mathcal{N}(8,9)$. Тогда
$$
P(T>11)=P\!\left(Z>\frac{11-\mu_T}{\sigma_T}\right)
=P\!\left(Z>\frac{11-8}{3}\right)=P(Z>1)=1-\Phi(1).
$$

## Как ведет себя сумма случайных величин?
### Пример: функция от двух дискретных случайных величин

Предположим, что мы бросаем два $6$-гранных кубика, независимых друг от друга. В итоге мы наблюдаем дискретный случайный вектор $(X,Y)$, где $X$ и $Y$ — случайные величины, соответствующие выпавшим числам на каждом из кубиков.
Поскольку существует $36$ различных пар, совместная функция вероятности задается как: $P(X=x_i, \, Y=y_j) = \frac{1}{36}$.

Введем новую случайную величину $T$ как функцию от $X$ и $Y$: $T = f(X,Y) = X + Y$. Построим функцию вероятности для случайной величины $T$.

## Как ведет себя сумма случайных величин?
### Построение функции вероятности для $T = X + Y$

Для каждого значения $t$ случайной величины $T$ найдем все пары $(x,y)$, которые дают в сумме $t$:

\begin{itemize}
    \item $T = 2$: только $(1,1)$
    \item $T = 3$: $(1,2), (2,1)$  
    \item $T = 4$: $(1,3), (2,2), (3,1)$
    \item $T = 5$: $(1,4), (2,3), (3,2), (4,1)$
    \item $T = 6$: $(1,5), (2,4), (3,3), (4,2), (5,1)$
    \item $T = 7$: $(1,6), (2,5), (3,4), (4,3), (5,2), (6,1)$
    \item $T = 8$: $(2,6), (3,5), (4,4), (5,3), (6,2)$
    \item $T = 9$: $(3,6), (4,5), (5,4), (6,3)$
    \item $T = 10$: $(4,6), (5,5), (6,4)$
    \item $T = 11$: $(5,6), (6,5)$
    \item $T = 12$: только $(6,6)$
\end{itemize}

## Как ведет себя сумма случайных величин?
### Таблица функции вероятности

\begin{center}
\begin{tabular}{|c|c|c|c|c|c|c|c|c|c|c|c|}
\hline
$t$ & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 & 11 & 12 \\
\hline
$P(T = t)$ & $\frac{1}{36}$ & $\frac{1}{18}$ & $\frac{1}{12}$ & $\frac{1}{9}$ & $\frac{5}{36}$ & $\frac{1}{6}$ & $\frac{5}{36}$ & $\frac{1}{9}$ & $\frac{1}{12}$ & $\frac{1}{18}$ & $\frac{1}{36}$ \\
\hline
\end{tabular}
\end{center}

### График функции вероятности

\begin{center}
\begin{tikzpicture}[scale=0.8]
% Оси
\draw[->] (0,0) -- (14,0) node[right] {$t$};
\draw[->] (0,0) -- (0,3.5) node[above] {$P(T = t)$};

% Сетка
\draw[gray, very thin] (0,0) grid (14,3.5);

% Подписи осей
\foreach \x in {2,3,4,5,6,7,8,9,10,11,12}
    \draw (\x,0) -- (\x,-0.1) node[below] {\x};

% Столбцы гистограммы
\draw[fill=blue!30] (1.5,0) rectangle (2.5,0.5) node[above, xshift=-0.3cm] {$\frac{1}{36}$};
\draw[fill=blue!30] (2.5,0) rectangle (3.5,1) node[above, xshift=-0.3cm] {$\frac{1}{18}$};
\draw[fill=blue!30] (3.5,0) rectangle (4.5,1.5) node[above, xshift=-0.3cm] {$\frac{1}{12}$};
\draw[fill=blue!30] (4.5,0) rectangle (5.5,2) node[above, xshift=-0.3cm] {$\frac{1}{9}$};
\draw[fill=blue!30] (5.5,0) rectangle (6.5,2.5) node[above, xshift=-0.3cm] {$\frac{5}{36}$};
\draw[fill=red!30] (6.5,0) rectangle (7.5,3) node[above, xshift=-0.3cm] {$\frac{1}{6}$};
\draw[fill=blue!30] (7.5,0) rectangle (8.5,2.5) node[above, xshift=-0.3cm] {$\frac{5}{36}$};
\draw[fill=blue!30] (8.5,0) rectangle (9.5,2) node[above, xshift=-0.3cm] {$\frac{1}{9}$};
\draw[fill=blue!30] (9.5,0) rectangle (10.5,1.5) node[above, xshift=-0.3cm] {$\frac{1}{12}$};
\draw[fill=blue!30] (10.5,0) rectangle (11.5,1) node[above, xshift=-0.3cm] {$\frac{1}{18}$};
\draw[fill=blue!30] (11.5,0) rectangle (12.5,0.5) node[above, xshift=-0.3cm] {$\frac{1}{36}$};
\end{tikzpicture}
\end{center}

### Промежуточный вывод
Мы на очень простом примере можем пронаблюдать, как функция вероятности суммы одинаково распределенных дискретных величин получает "усиление" в центральных значениях, так как к этим элементарным исходам приводят больше комбинаций изначальных величин.

## Центральная предельная теорема
### Предпосылки

\begin{itemize}
    \item Пусть $X_1, X_2, \; \ldots$ — последовательность независимых случайных величин, взятых из одного и того же распределения, т.е. все $X_i$ имеют одинаковое математическое ожидание $E[X] = \mu$, одинаковую дисперсию $Var[X] = \sigma^2 < \infty$. 

    \item Мы конструируем \textbf{новую} случайную величину как частичную сумму первых $n$ случайных величин $X_i$:
    $$
    S_n = \sum \limits_{i=1}^{n} X_i.
    $$

    \item Согласно свойствам математического ожидания и дисперсии, характеристики новой случайной величины:
    \begin{gather*}
        E[S_n] = E \Bigl[ \sum \limits_{i=1}^{n} X_i \Bigr] = \sum \limits_{i=1}^{n} E[X_i] = n \mu \\
        Var[S_n] = Var \Bigl[ \sum \limits_{i=1}^{n} X_i \Bigr] = \sum \limits_{i=1}^{n} Var[X_i] = n \sigma^2
    \end{gather*}
\end{itemize}

## Центральная предельная теорема

\begin{itemize}
    \item \textbf{Центральная предельная теорема}: распределение такой случайной величины $S_n$ стремится к нормальному распределению при $n \rightarrow \infty$: 
    $$
    S_n  \rightarrow  Y \sim \mathcal{N}(n \mu, n \sigma^2)
    $$

    \item Душно:
    $$
      \forall x \in \mathbb{R} \quad  P(S_n < x) \underset{n \rightarrow \infty}{\longrightarrow} P(Y < x), \text{ где } Y \sim \mathcal{N}(n \mu, n \sigma^2),
    $$
    что означает, что в каждой точке $x$ функция распределения $F_{S_n}(x)$ стремится к функции распределения $F_Y(x)$, т.е. они буквально "накладываются" друг на друга и теперь характеризуют одну и ту же случайную величину.

    \item Проще говоря: $S_n \sim \mathcal{N}(n \mu, n \sigma^2)$, когда $n$ достаточно велико.
    \item Обычно "достаточно велико" это $n \geq 30$.
\end{itemize}

## Центральная предельная теорема
### Формулировка через стандартизацию

\begin{itemize}
    \item Проводим операцию стандартизации введенной ранее случайной величины $S_n$:
    $$
    Z_n = \frac{S_n - E[S_n]}{\sqrt{Var[S_n]}} = \frac{S_n - n \mu}{\sigma \sqrt{n}}
    $$

    \item Характеристики:
    \begin{gather*}
    E[Z_n] = E \Biggl[ \frac{S_n - n \mu}{\sigma \sqrt{n}} \Biggr] = E \Biggl[\frac{S_n}{\sigma \sqrt{n}} \Biggr] - E \Biggl[\frac{n \mu}{\sigma \sqrt{n}} \Biggr] = \frac{n \mu}{\sigma \sqrt{n}} - \frac{n \mu}{\sigma \sqrt{n}} = 0 \\
    Var[Z_n] = Var \Biggl[ \frac{S_n - n \mu}{\sigma \sqrt{n}} \Biggr] = Var \Biggl[\frac{S_n}{\sigma \sqrt{n}} \Biggr] + Var \Biggl[\frac{n \mu}{\sigma \sqrt{n}} \Biggr] = \frac{Var[S_n]}{n \sigma^2} + 0 = 1
    \end{gather*}

    \item Тогда говорим, что:
    $$
      \forall x \in \mathbb{R} \quad  P(Z_n < x) \underset{n \rightarrow \infty}{\longrightarrow} P(Z < x), \text{ где } Z \sim \mathcal{N}(0, 1)
    $$
    Или проще: стандартизованная частичная сумма $Z_n \sim \mathcal{N}(0,1)$, когда $n$ достаточно велико.
    
    Обычно требуем $n \geq 30$.
\end{itemize}

## Напоминание: Биномиальное распределение

\begin{itemize}
    \item Пусть $X \sim \text{Bin}(n, p)$ — биномиальная случайная величина.
    
    \item $X$ можно представить как сумму $n$ независимых бернуллиевских случайных величин:
    $$
    X = X_1 + X_2 + \ldots + X_n, \quad \text{где } X_i \sim \text{Bernoulli}(p)
    $$
    
    \item Характеристики:
    \begin{itemize}
        \item $E[X] = np$
        \item $\text{Var}(X) = np(1-p)$
    \end{itemize}
\end{itemize}

## Интегральная теорема Муавра-Лапласа (ИТМЛ)

:::{.callout-theorem}
Пусть $X \sim \text{Bin}(n, p)$. При больших $n$ биномиальное распределение приближается нормальным:
$$
X \sim \mathcal{N}(np, np(1-p))
$$

\textbf{Условия}: $n$ достаточно велико (обычно $n \geq 30$), и желательно $np > 5$ и $n(1-p) > 5$; или в эквивалентной форме $npq \geq 25$, где $q = 1-p$.

Это частный случай ЦПТ для суммы бернуллиевских случайных величин!
:::

## Нормализованная форма ИТМЛ

\begin{itemize}
    \item Нормализованная случайная величина:
    $$
    Z = \frac{X - np}{\sqrt{np(1-p)}}
    $$
    
    \item При больших $n$:
    $$
    Z \sim \mathcal{N}(0, 1)
    $$
    
    \item Это позволяет использовать стандартную нормальную таблицу для вычисления вероятностей биномиального распределения!
\end{itemize}

## Применение ИТМЛ: вычисление вероятностей

\begin{itemize}
    \item Для биномиального распределения $X \sim \text{Bin}(n, p)$:
    $$
    P(a \leq X \leq b) \approx P\left(\frac{a - np}{\sqrt{np(1-p)}} \leq Z \leq \frac{b - np}{\sqrt{np(1-p)}}\right), 
    $$
    где $Z \sim \mathcal{N}(0, 1)$.
\end{itemize}

## Пример: применение ИТМЛ

\begin{itemize}
    \item Пусть $X \sim \text{Bin}(150, 0.4)$. Найти $P(48 \leq X \leq 72)$.
    Условие применимости: $npq = 150 \cdot 0.4 \cdot 0.6 = 36 \geq 25$.

    \item \textbf{Точное вычисление} (через биномиальное распределение):
    $$
    P(48 \leq X \leq 72) = \sum_{k=48}^{72} \binom{150}{k} (0.4)^k (0.6)^{150-k} \approx 0.9632
    $$

    \item \textbf{Приближение через нормальное распределение}:
    \begin{itemize}
        \item Параметры: $\mu = np = 60$, $\sigma^2 = npq = 36$, $\sigma = 6$
        \begin{align*}
        P(48 \leq X \leq 72) &\approx P\left(\frac{48 - 60}{6} \leq Z \leq \frac{72 - 60}{6}\right) \\
        &= P(-2 \leq Z \leq 2) \\
        &\approx 0.9545
        \end{align*}
    \end{itemize}

    \item \textbf{Сравнение}: Нормальное приближение даёт результат $0.9545$, близко к точному значению $0.9632$.
\end{itemize}
