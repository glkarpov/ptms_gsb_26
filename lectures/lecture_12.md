---
title: "Теория вероятностей и математическая статистика"
subtitle: "Методы точечной оценки. Метод моментов. MLE."
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
        incremental: true
        include-in-header: ../files/xeheader.tex  # Custom LaTeX commands and preamble
---

## Моменты случайной величины

\begin{itemize}
    \item \textbf{Момент $k$-го порядка} случайной величины $X$ — это математическое ожидание $k$-й степени $X$:
    $$
    \mu_k = E[X^k]
    $$
    
    \item \textbf{Первый момент} ($k=1$): $\mu_1 = E[X]$ — математическое ожидание.
    
    \item \textbf{Второй момент} ($k=2$): $\mu_2 = E[X^2]$.
    
    \item \textbf{Центральный момент $k$-го порядка}:
    $$
    \mu_k' = E[(X - E[X])^k]
    $$
    
    \item \textbf{Второй центральный момент}: $\mu_2' = E[(X - E[X])^2] = \text{Var}(X)$ — дисперсия.
\end{itemize}

## Выборочные моменты

\begin{itemize}
    \item Для случайной выборки $X_1, \ldots, X_n$ определяем \textbf{выборочные моменты}:
    
    \item \textbf{Выборочный момент $k$-го порядка}:
    $$
    m_k = \frac{1}{n}\sum_{i=1}^{n} X_i^k
    $$
    
    \item \textbf{Выборочный центральный момент $k$-го порядка}:
    $$
    m_k' = \frac{1}{n}\sum_{i=1}^{n}(X_i - \bar{X})^k
    $$
    
    \item Выборочные моменты являются оценками соответствующих теоретических моментов.
\end{itemize}

## Связь между параметрами и характеристиками случайной величины

\begin{itemize}
    \item Часто характеристики распределения зависят от неизвестного параметра $\theta$:
    $$
        E[X] = f(\theta), \qquad \operatorname{Var}[X] = g(\theta)
    $$
    
    \item Пример: если $X\sim\mathrm{Exp}(\lambda)$, то $E[X]=1/\lambda$.

    \item Пример: если $X\sim\mathrm{U}(a, \; b)$, то $E[X] = \frac{a+b}{2}$.

    \item Пример: если $X\sim\mathcal{N}(\mu, \; \sigma^2)$, то $E[X] = \mu$.

    \item Мы можем оценить характеристику через некую статистику (например: $E[X] \approx \bar{x}$),
    а затем, зная связь между характеристикой и параметром, выразить последний и получить оценку для него.
\end{itemize}

## Метод моментов

\begin{itemize}
    \item \textbf{Идея метода моментов}: приравнять выборочные моменты к теоретическим моментам распределения.
    
    \item Если распределение зависит от $k$ параметров, используем первые $k$ моментов.
\end{itemize}

:::{.callout-definition}
**Метод моментов** для оценки параметров:

\begin{enumerate}
    \item Выразить теоретические моменты через неизвестные параметры.
    
    \item Приравнять выборочные моменты к теоретическим:
    $$
    m_i = \mu_i(\theta_1, \ldots, \theta_k), \quad i = 1, \ldots, k
    $$
    
    \item Решить систему уравнений относительно параметров $\theta_1, \ldots, \theta_k$.
\end{enumerate}
:::

## Пример: Метод моментов для экспоненциального распределения

\begin{itemize}
    \item Пусть $X_1, \ldots, X_n \sim \text{Exp}(\lambda)$ — время до события (например, время до поломки устройства).
    
    \item Нужно оценить параметр $\lambda$ (интенсивность).
    
    \item \textbf{Шаг 1}: Теоретический момент первого порядка:
    $$
    \mu_1 = E[X] = \frac{1}{\lambda}
    $$
    
    \item \textbf{Шаг 2}: Выборочный момент первого порядка:
    $$
    m_1 = \bar{X}
    $$
    
    \item \textbf{Шаг 3}: Приравниваем и выражаем параметр как оценку:
    $$
    \bar{X} = \frac{1}{\lambda} \quad \Rightarrow \quad \hat{\lambda}_{MM} = \frac{1}{\bar{X}}
    $$
\end{itemize}

## Пример: Метод моментов для равномерного распределения

\begin{itemize}
    \item Пусть $X_1, \ldots, X_n \sim \text{Uniform}(0, \theta)$ — равномерное распределение на интервале $[0, \theta]$.
    
    \item Нужно оценить параметр $\theta$ (верхнюю границу интервала).
    
    \item \textbf{Шаг 1}: Теоретический момент первого порядка:
    $$
    \mu_1 = E[X] = \frac{0 + \theta}{2} = \frac{\theta}{2}
    $$
    
    \item \textbf{Шаг 2}: Выборочный момент первого порядка:
    $$
    m_1 = \bar{X}
    $$
    
    \item \textbf{Шаг 3}: Приравниваем и выражаем параметр как оценку:
    $$
    \bar{X} = \frac{\theta}{2} \quad \Rightarrow \quad \hat{\theta}_{MM} = 2\bar{X}
    $$
    
    \item \textbf{Интуиция}: Если среднее значение равно $\frac{\theta}{2}$, то верхняя граница $\theta$ в два раза больше среднего.
\end{itemize}

## Пример: Метод моментов для биномиального распределения

\begin{itemize}
    \item Пусть $X_1, \ldots, X_n \sim \mathrm{Bin}(m, p)$,
    где число испытаний $m$ известно, а вероятность успеха $p$ неизвестна.
    
    \item \textbf{Шаг 1}: Теоретический момент первого порядка:
    $$
    \mu_1 = E[X] = mp
    $$
    
    \item \textbf{Шаг 2}: Выборочный момент первого порядка:
    $$
    m_1 = \bar{X}
    $$
    
    \item \textbf{Шаг 3}: Приравниваем и выражаем параметр как оценку:
    $$
    \bar{X} = mp \quad \Rightarrow \quad \hat{p}_{MM} = \frac{\bar{X}}{m}
    $$
    
    \item \textbf{Замечание}: при $m = 1$ это схема Бернулли,
    и $\hat{p}_{MM} = \bar{X}$ --- просто выборочная доля.
\end{itemize}

## Метод максимального правдоподобия (MLE)

\begin{center}
\textit{Какое значение параметра делает\\
наблюдаемые данные наиболее правдоподобными?}
\end{center}

\begin{itemize}
    \item Именно эту идею реализует метод максимального правдоподобия
    (Maximum Likelihood Estimation, \textbf{MLE}).
\end{itemize}

## Сначала вспомним: вероятность при известном параметре

\begin{itemize}
    \item Пусть модель известна полностью: параметр $\theta$ задан.
    
    \item Тогда мы умеем считать вероятности при этом $\theta$:
    \begin{itemize}
        \item дискретная модель: вероятность $P_X(x | \theta)$;
        \item непрерывная модель: с помощью плотности $f_X(x | \theta)$.
    \end{itemize}
    
    \item Пример (монета): $P(X=1) = p$, $P(X=0) = 1-p$.
\end{itemize}

## А теперь параметр неизвестен, данные уже есть

\begin{itemize}
    \item В статистике обычно наоборот:
    \begin{itemize}
        \item данные $x_1, \ldots, x_n$ уже получены
        (реализация случайной выборки);
        \item параметр $\theta$ неизвестен.
    \end{itemize}
    
    \item Вопрос меняется:
    
    \begin{center}
    не «какова вероятность данных при данном $\theta$?»,\\
    а «при каком $\theta$ наши данные выглядят наиболее естественно?»
    \end{center}
\end{itemize}

## Правдоподобие: разные «вселенные» параметра

\begin{itemize}
    \item Случайный генератор - монетка с неизвестным параметром $p$, вероятностью орла.
    
    \item Наблюдение: выпал \textbf{орёл}.
    
    \item Нельзя сразу сказать «вероятность орла равна $0.5$»: мы не знаем, какая это монета. Мы находимся в задаче статистики, нам надо разгадать параметр случайной величины.
    
    \item Возможная идея: представить разные «вселенные» ---
    в каждой своя монета со своим $p$ ---
    и спросить, насколько естественно увидеть то, что мы увидели.
\end{itemize}

## Вселенная 1: $p = 0.5$

\begin{itemize}
    \item Если монета честная, то $P(\text{орёл}) = 0.5$.
\end{itemize}

\begin{center}
\includegraphics[width=0.62\textwidth]{../files/mle_coin_universe_p05.pdf}
\end{center}

## Вселенная 2: $p = 0.1$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.1$, наш орёл --- странное событие.
\end{itemize}

\begin{center}
\includegraphics[width=0.62\textwidth]{../files/mle_coin_universe_p01.pdf}
\end{center}

## Вселенная 3: $p = 0.8$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.8$, орёл почти ожидаем.
\end{itemize}

\begin{center}
\includegraphics[width=0.62\textwidth]{../files/mle_coin_universe_p08.pdf}
\end{center}

## Что мы сравниваем?

\begin{itemize}
    \item В рассмотренных выше примерах реализация зафиксирована: орёл уже выпал.
    
    \item Меняется только параметр $p$ --- в какой вселенной мы находимся.
    
    \item Смотрим высоту столбика над \textbf{орлом}:
    насколько эта вселенная хорошо объясняет данные.
\end{itemize}

:::{.callout-definition}
\textbf{Функция правдоподобия} $L(\theta)$ ---
вероятность или плотность уже полученных данных,
рассмотренная как функция параметра $\theta$.
Данные фиксированы; меняется только $\theta$,
и по величине $L(\theta)$ можно оценивать,
насколько хорошо этот параметр объясняет наблюдение.
:::

При одном орле:
$$
L(p) = P(X=1 \mid p) = p.
$$

## График 
### Функция правдоподобия для одного эксперимента Бернулли, $x=1$

\begin{itemize}
    \item $L(p)=p$ --- прямая: чем больше $p$, тем правдоподобнее орёл.
    
    \item Максимум на краю: $\hat{p}_{\mathrm{MLE}}=1$.
    При одном орле «самая правдоподобная» вселенная --- в которой всегда выпадает орел
    (с малой выборкой MLE бывает экстремальным).
\end{itemize}

\begin{center}
\includegraphics[width=0.62\textwidth]{../files/mle_bern_n1.pdf}
\end{center}

## Эксперимент с двумя бросками монеты
### Реализация: орёл, решка

\begin{itemize}
    \item Два независимых броска, параметр $p$ (вероятность орла) неизвестен.
    
    \item Наблюдение: \textbf{орёл, решка}.
    Вероятность такого исхода
    $$
    P\left( (x_1 = 1, \; x_2 = 0) \mid p \right) = p \cdot (1-p).
    $$
    
    \item Если рассматриваем как функцию от параметра, получается функция правдоподобия:
    $$
    L(p) = p \cdot (1-p).
    $$
    
    \item Дальше перебираем вселенные:
    подставляем разные $p$ и смотрим высоту столбика.
\end{itemize}

## Вселенная 1: $p = 0.5$

\begin{itemize}
    \item Если монета честная, то
    $$
    P(\text{орёл, решка})
    = 0.5\cdot 0.5 = 0.25.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin2_mixed_universe_p05.pdf}
\end{center}

## Вселенная 2: $p = 0.9$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.9$, то
    $$
    P(\text{орёл, решка})
    = 0.9\cdot 0.1 = 0.09.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin2_mixed_universe_p09.pdf}
\end{center}

## Вселенная 3: $p = 0.1$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.1$, то
    $$
    P(\text{орёл, решка})
    = 0.1\cdot 0.9 = 0.09.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin2_mixed_universe_p01.pdf}
\end{center}


## График: Бернулли, $n=2$, данные $(1,0)$

\begin{center}
\includegraphics[width=0.72\textwidth]{../files/mle_bern_n2_mixed.pdf}
\end{center}

## Эксперимент с двумя бросками монеты
### Реализация с двумя орлами

\begin{itemize}
    \item Снова два независимых броска, параметр $p$ неизвестен.
    
    \item Наблюдение: \textbf{два орла}.
    Вероятность такого исхода
    $$
    P\left( (x_1 = 1, \; x_2 = 1) \mid p \right) = p \cdot p.
    $$
    
    \item Если рассматриваем как функцию от параметра, получается функция правдоподобия:
    $$
    L(p) = p \cdot p = p^2.
    $$
    
    \item Дальше прыгаем в несколько вселенных
    и посмотрим на значения правдоподобия.
\end{itemize}

## Вселенная 1: $p = 0.5$

\begin{itemize}
    \item Если монета честная, то
    $$
    P(\text{два орла}) = 0.5 \cdot 0.5 = 0.25.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin2_universe_p05.pdf}
\end{center}

## Вселенная 2: $p = 0.9$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.9$, то
    $$
    P(\text{два орла}) = 0.9 \cdot 0.9 = 0.81.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin2_universe_p09.pdf}
\end{center}

## Вселенная 3: $p = 0.1$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.1$, то
    $$
    P(\text{два орла}) = 0.1 \cdot 0.1 = 0.01.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin2_universe_p01.pdf}
\end{center}

## График: Бернулли, $n=2$, данные $(1,1)$

\begin{center}
\includegraphics[width=0.55\textwidth]{../files/mle_bern_n2_heads.pdf}
\end{center}

## Три броска: решка, орёл, решка

\begin{itemize}
    \item Три независимых броска, параметр $p$ неизвестен.
    
    \item Наблюдение: \textbf{решка, орёл, решка}.
    Вероятность такого исхода
    $$
    P\left( (x_1 = 0, \; x_2 = 1, \; x_3 = 0) \mid p \right)
    = (1-p) \cdot p \cdot (1-p).
    $$
    
    \item Если рассматриваем как функцию от параметра, получается функция правдоподобия:
    $$
    L(p) = (1-p) \cdot p \cdot (1-p) = p(1-p)^2.
    $$
    
    \item Дальше перебираем вселенные
    и подставляем разные $p$.
\end{itemize}

## Вселенная 1: $p = 0.1$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.1$, то
    $$
    P(\text{решка, орёл, решка})
    = 0.9\cdot 0.1\cdot 0.9 = 0.081.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_one_universe_p01.pdf}
\end{center}

## Вселенная 2: $p = 0.2$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.2$, то
    $$
    P(\text{решка, орёл, решка})
    = 0.8\cdot 0.2\cdot 0.8 = 0.128.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_one_universe_p02.pdf}
\end{center}

## Вселенная 3: $p = 1/3$

\begin{itemize}
    \item Если $P(\text{орёл}) = 1/3$, то
    $$
    P(\text{решка, орёл, решка})
    = \frac{2}{3}\cdot\frac{1}{3}\cdot\frac{2}{3}
    = \frac{4}{27}\approx 0.148.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_one_universe_p13.pdf}
\end{center}

## Вселенная 4: $p = 0.5$

\begin{itemize}
    \item Если монета честная, то
    $$
    P(\text{решка, орёл, решка})
    = 0.5\cdot 0.5\cdot 0.5 = 0.125.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_one_universe_p05.pdf}
\end{center}

## Вселенная 5: $p = 2/3$

\begin{itemize}
    \item Если $P(\text{орёл}) = 2/3$, то
    $$
    P(\text{решка, орёл, решка})
    = \frac{1}{3}\cdot\frac{2}{3}\cdot\frac{1}{3}
    = \frac{2}{27}\approx 0.074.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_one_universe_p23.pdf}
\end{center}

## Вселенная 6: $p = 0.8$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.8$, то
    $$
    P(\text{решка, орёл, решка})
    = 0.2\cdot 0.8\cdot 0.2 = 0.032.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_one_universe_p08.pdf}
\end{center}

## Вселенная 7: $p = 0.9$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.9$, то
    $$
    P(\text{решка, орёл, решка})
    = 0.1\cdot 0.9\cdot 0.1 = 0.009.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_one_universe_p09.pdf}
\end{center}


## График: Бернулли, $n=3$, данные $(0,1,0)$

\begin{center}
\includegraphics[width=0.72\textwidth]{../files/mle_bern_n3_010.pdf}
\end{center}

## Три броска: решка, орёл, орёл

\begin{itemize}
    \item Снова три независимых броска, параметр $p$ неизвестен.
    
    \item Наблюдение: \textbf{решка, орёл, орёл}.
    Вероятность такого исхода
    $$
    P\left( (x_1 = 0, \; x_2 = 1, \; x_3 = 1) \mid p \right)
    = (1-p) \cdot p \cdot p.
    $$
    
    \item Если рассматриваем как функцию от параметра, получается функция правдоподобия:
    $$
    L(p) = (1-p) \cdot p \cdot p = p^{2}(1-p).
    $$
    
    \item Дальше перебираем те же значения $p$.
\end{itemize}

## Вселенная 1: $p = 0.1$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.1$, то
    $$
    P(\text{решка, орёл, орёл})
    = 0.9\cdot 0.1\cdot 0.1 = 0.009.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_two_universe_p01.pdf}
\end{center}

## Вселенная 2: $p = 0.2$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.2$, то
    $$
    P(\text{решка, орёл, орёл})
    = 0.8\cdot 0.2\cdot 0.2 = 0.032.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_two_universe_p02.pdf}
\end{center}

## Вселенная 3: $p = 1/3$

\begin{itemize}
    \item Если $P(\text{орёл}) = 1/3$, то
    $$
    P(\text{решка, орёл, орёл})
    = \frac{2}{3}\cdot\frac{1}{3}\cdot\frac{1}{3}
    = \frac{2}{27}\approx 0.074.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_two_universe_p13.pdf}
\end{center}

## Вселенная 4: $p = 0.5$

\begin{itemize}
    \item Если монета честная, то
    $$
    P(\text{решка, орёл, орёл})
    = 0.5\cdot 0.5\cdot 0.5 = 0.125.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_two_universe_p05.pdf}
\end{center}

## Вселенная 5: $p = 2/3$

\begin{itemize}
    \item Если $P(\text{орёл}) = 2/3$, то
    $$
    P(\text{решка, орёл, орёл})
    = \frac{1}{3}\cdot\frac{2}{3}\cdot\frac{2}{3}
    = \frac{4}{27}\approx 0.148.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_two_universe_p23.pdf}
\end{center}

## Вселенная 6: $p = 0.8$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.8$, то
    $$
    P(\text{решка, орёл, орёл})
    = 0.2\cdot 0.8\cdot 0.8 = 0.128.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_two_universe_p08.pdf}
\end{center}

## Вселенная 7: $p = 0.9$

\begin{itemize}
    \item Если $P(\text{орёл}) = 0.9$, то
    $$
    P(\text{решка, орёл, орёл})
    = 0.1\cdot 0.9\cdot 0.9 = 0.081.
    $$
\end{itemize}

\begin{center}
\includegraphics[width=0.58\textwidth]{../files/mle_coin3_two_universe_p09.pdf}
\end{center}


## График: Бернулли, $n=3$, данные $(0,1,1)$

\begin{center}
\includegraphics[width=0.72\textwidth]{../files/mle_bern_n3_011.pdf}
\end{center}

## Общий рецепт: как строить $L(\theta)$

\begin{itemize}
    \item Для i.i.d. выборки независимость даёт произведение:
    $$
    L(\theta)
    =
    \prod_{i=1}^{n} P_\theta(X_i = x_i)
    \quad\text{или}\quad
    \prod_{i=1}^{n} f_\theta(x_i).
    $$
    
    \item Формула как у совместной вероятности/плотности,
    но аргумент --- параметр $\theta$ при фиксированных данных.
    
    \item Каждое новое наблюдение домножает свой вклад.
\end{itemize}

## Оценка максимального правдоподобия

:::{.callout-definition}
$$
\hat{\theta}_{\mathrm{MLE}}
=
\arg\max_{\theta} L(\theta).
$$
Выбираем $\theta$, при котором правдоподобие данных максимально.
:::

\begin{itemize}
    \item Интуиция: подкручиваем параметр, чтобы модель
    лучше всего объясняла выборку.
    
    \item Часто удобнее максимизировать $\ell(\theta)=\log L(\theta)$:
    логарифм монотонен, произведение $\to$ сумма.
\end{itemize}

## Бернулли при произвольном $n$

\begin{itemize}
    \item $n$ бросков, $y$ орлов:
    $L(p)=p^{y}(1-p)^{n-y}$.
    
    \item $\ell'(p)=0$ даёт
    $$
    \hat{p}_{\mathrm{MLE}} = \frac{y}{n}.
    $$
    
    \item То есть MLE --- просто доля орлов
    (и то же, что $\bar{X}$ для Бернулли).
    
    \item Пример: $n=10$, $y=7$ $\Rightarrow$ $\hat{p}=0.7$.
\end{itemize}

## Резюме: вероятность vs правдоподобие

В контексте \textbf{дискретных} распределений:

\begin{itemize}
    \item Вероятность и правдоподобие --- по сути одно и то же,
    только с разных точек зрения.
    
    \item \textbf{Вероятность}: мы знаем, в какой вселенной находимся,
    и вероятности всех событий в этой одной вселенной
    суммируются в $1$.
    
    \item \textbf{Правдоподобие}: мы знаем, что наблюдали,
    и смотрим вероятность \textbf{именно этого наблюдения}
    в любой возможной вселенной.
\end{itemize}

## Непрерывный случай: одно наблюдение Exp

\begin{itemize}
    \item Модель $\mathrm{Exp}(\lambda)$, есть одна реализация $x>0$:
    $$
    L(\lambda)=\lambda e^{-\lambda x}.
    $$
    
    \item При фиксированном $x$ это функция от $\lambda$:
    сначала растёт, потом падает.
\end{itemize}

## Одно наблюдение Exp: где максимум?

\begin{itemize}
    \item Логарифм сохраняет точку максимума,
    а производную упрощает:
    $$
    \ell(\lambda)
    =
    \log L(\lambda)
    =
    \log\lambda - \lambda x.
    $$
    
    \item Дифференцируем по $\lambda$:
    $$
    \ell'(\lambda) = \frac{1}{\lambda} - x.
    $$
    
    \item Оптимизация --- критическая точка $\ell'(\lambda)=0$:
    $$
    \frac{1}{\lambda} - x = 0
    \quad\Rightarrow\quad
    \frac{1}{\lambda} = x
    \quad\Rightarrow\quad
    \hat{\lambda} = \frac{1}{x}.
    $$
    
    \item Это максимум: $\ell''(\lambda)=-1/\lambda^{2}<0$
    при любом $\lambda>0$.
    Пример: $x=2$ $\Rightarrow$ $\hat{\lambda}=1/2$.
\end{itemize}

## График: Exp, $n=1$, $x=2$

\begin{center}
\includegraphics[width=0.72\textwidth]{../files/mle_exp_n1.pdf}
\end{center}

## Два наблюдения Exp: $(x_1,x_2)=(1,3)$

\begin{itemize}
    \item Независимость $\Rightarrow$ произведение плотностей:
    $$
    L(\lambda)
    =
    f(1\mid\lambda)\, f(3\mid\lambda)
    =
    \bigl(\lambda e^{-\lambda\cdot 1}\bigr)
    \bigl(\lambda e^{-\lambda\cdot 3}\bigr).
    $$
    
    \item Упрощаем:
    $$
    L(\lambda)
    =
    \lambda\cdot\lambda\cdot e^{-\lambda(1+3)}
    =
    \lambda^2 e^{-4\lambda}.
    $$
    
    \item И берем логарифм:
    $$
    \ell(\lambda)
    =
    \log L(\lambda)
    =
    2\log\lambda - 4\lambda.
    $$
\end{itemize}

## Два наблюдения Exp: где максимум?

\begin{itemize}
    \item Производная:
    $$
    \ell'(\lambda)
    =
    \frac{2}{\lambda} - 4.
    $$
    
    \item Критическая точка $\ell'(\lambda)=0$:
    $$
    \frac{2}{\lambda} = 4
    \quad\Rightarrow\quad
    \hat{\lambda} = \frac{2}{4} = \frac{1}{2}.
    $$
\end{itemize}

## График: Exp, $n=2$, данные $(1,3)$

\begin{center}
\includegraphics[width=0.72\textwidth]{../files/mle_exp_n2.pdf}
\end{center}

## Exp: произвольный $n$

\begin{itemize}
    \item Для выборки:
    $$
    L(\lambda)
    =
    \lambda^n \exp\Bigl(-\lambda\sum_{i=1}^{n} x_i\Bigr),
    \qquad
    \ell(\lambda)
    =
    n\log\lambda - \lambda\sum_{i=1}^{n} x_i.
    $$
    
    \item $\ell'(\lambda)=0$ даёт
    $$
    \hat{\lambda}_{\mathrm{MLE}}
    =
    \frac{n}{\sum x_i}
    =
    \frac{1}{\bar{X}}.
    $$
    
    \item Тот же ответ, что у метода моментов:
    большое среднее время $\Rightarrow$ маленькая интенсивность.
\end{itemize}
