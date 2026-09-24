\documentclass[12pt, one-sided]{amsart}
\usepackage{amsmath,amssymb,amsfonts,amstext,amsthm}
\usepackage{color}
\usepackage{fullpage}
\usepackage[all]{xy}
\usepackage{graphicx} % Required for inserting images
% Proclamation definitions in the most emphatic (plain) style:
\theoremstyle{plain}
\newtheorem{theorem}{Theorem}[section]
\newtheorem{corollary}[theorem]{Corollary}
\newtheorem{proposition}[theorem]{Proposition}
\newtheorem{lemma}[theorem]{Lemma}
% Proclamation definitions in the less emphatic (definition) style:
\theoremstyle{definition}
\newtheorem{definition}[theorem]{Definition}
\newtheorem{example}[theorem]{Example}
\newtheorem{examples}[theorem]{Examples}
\newtheorem{exercise}[theorem]{Exercise}
\newtheorem{exercises}[theorem]{Exercises}
\newtheorem{counterexample}[theorem]{Counterexample}
\newtheorem{remark}[theorem]{Remark}
\newtheorem{remarks}[theorem]{Remarks}
\newtheorem{application}[theorem]{Application}
\newtheorem{question}[theorem]{Question}
\newtheorem*{acknow}{Acknowledgements}
% Proclamation definitions in the least emphatic (remark) style:
\theoremstyle{remark}
%\newtheorem{remark}{Remark}
\newtheorem*{notation}{Notation}
\newcommand{\nor}[1]{\left\Vert #1\right\Vert} %\nor{x}=||x||
\newtheorem{week}{Week}[section]
\title{Lecture notes}
%\author{Christian B\"onicke}
%\date{September 2024}
\setcounter{section}{0}
\begin{document}

\maketitle

\section{Introduction to Metric Spaces}

Metric spaces were introduced by Fr\'echet in his PhD dissertation in 1906. The mathematicians of that time were studying various spaces (mainly spaces of functions) and they had various notions of \emph{convergence} in such spaces. For each space its own notion of convergence was introduced, and studied. Of course, similarities were noticed and Fr\'echet realised that these arguments can be unified by introducing an abstract concept of a \emph{metric} or \emph{distance function}. He could show that many of these spaces were instances of his new concept of a metric space. Then, by proving one result axiomatically from the metric axioms, it automatically holds for all instances.

In the modern view, the concept of a metric space is just an axiomatisation of the notion of distance. As we will see, different notions of distance are very important since they occur all the time in mathematics, statistics and physics. Many geometric objects rely on a notion of distance (e.g. the unit sphere in $\mathbb R^n$ is exactly the set of points at distance $1$ from the origin). So, it is natural to distill some common properties of distances in various contexts and set them as axioms. 

As already mentioned above, distance plays a fundamental role in the definition of convergence. Let us recall that definition from calculus:
\begin{definition}
    Let $(x_n)_n$ be a sequence of real numbers and $x\in \mathbb R$. Then $(x_n)_n$ \textbf{converges to $x$}, if for every $\varepsilon>0$ there exists an $N\in \mathbb{N}$ such that $\vert x-x_n\vert<\varepsilon$ for all $n\geq N$. 
\end{definition}
In other words: for every error tolerance (the $\varepsilon$) the \textit{distance} between $x_n$ and $x$ is eventually (i.e. past the the index $N$) less than the error tolerance.

Our first goal is to formalise the concept of \textit{distance}. This is the content of the following definition:

%%%%%%%%%%%%%%%%%%%%
\begin{definition} Let $X$ be a non-empty set.
A \textbf{metric} (or distance function) on $X$ is a function $$d \colon X \times X \to \mathbb R, \ (x,y)\mapsto d(x,y)$$
satisfying the following three properties:
\begin{enumerate}
\item[(M1)] $d(x,y) = 0$ if and only if $x=y$;
\item[(M2)] $d(x,y) = d(y,x)$ for all $x,y \in X$;
\item[(M3)] $d(x,y) \leq d(x,z) + d(z,y)$ for all $x,y,z \in X$.
\end{enumerate}
The pair $(X,d)$ is called a \textbf{metric space}. 
\end{definition}

%%%%%%%%%%%%%%%%%%%%
\noindent Let us record a few remarks on the axioms in the definition above:
\begin{itemize}
    \item (M1) says that each point has zero distance from itself, and that distinct points must have a non-zero distance.
    \item (M2) says that the distance from $x$ to $y$ is the same as the
distance from $y$ to $x$. We say that $d$ is \textbf{symmetric}.
    \item (M3) is called the \textbf{triangle inequality} and gets its name from the fact that the length of any side of a triangle is at most the sum of the lengths of the other two sides.
It says that a journey from $x$ to $y$ doesn't get any shorter if you take a detour via $z$, but may possibly get longer.
\item We can combine the axioms to prove that the distance between any two points must be non-negative: indeed, for all $x,y\in X$ we have
$$2d(x,y)=d(x,y)+d(x,y)\stackrel{(M2)}{=}d(x,y)+d(y,x)\stackrel{(M3)}{\geq} d(x,x)\stackrel{(M1)}{=}0, $$
so dividing by $2$ gives $d(x,y)\geq 0$. 
\end{itemize}

Let us now consider some examples:
\begin{example}[Euclidean space] The first example is the $n$-dimensional \textbf{Euclidean space} $(\mathbb R^n, d_2)$ where for two points $x=(x_1,\ldots, x_n)$ and $y=(y_1,\ldots, y_n)$ in $\mathbb R^n$ we define their \textbf{Euclidean distance} by
 $$d_2(x,y) := \sqrt{\sum_{i=1}^n (x_i-y_i) ^2}.$$

 It is easy to see that $(M1)$ and $(M2)$ are satisfied. To see that $(M3)$ holds let $z=(z_1,\ldots, z_n)$ be a third point in $\mathbb R^n$. 
 Then writing out the inequality $d_2(x,z)\leq d_2(x,y) + d_2(y,z)$ we have to prove
 $$\sqrt{\sum_{i=1}^n (x_i-z_i) ^2}\leq \sqrt{\sum_{i=1}^n (x_i-y_i) ^2}+\sqrt{\sum_{i=1}^n (y_i-z_i) ^2}$$
 To simplify things introduce auxiliary variables $r_i:=x_i-y_i$ and $s_i:=y_i-z_i$. Plugging these in, the above inequality becomes
    $$\sqrt{\sum_{i=1}^n (r_i+s_i) ^2}\leq \sqrt{\sum_{i=1}^n r_i^2}+\sqrt{\sum_{i=1}^n s_i^2}$$
    Since both sides arc non-negative, it is equivalent (squaring both sides)
to prove
$$\sum_{i=1}^n r_i^2 + 2\sum_{i=1}^n r_is_i+ \sum_{i=1}^n s_i^2\leq \sum_{i=1}^n r_i^2+ 2\sqrt{\sum_{i=1}^n r_i^2}\sqrt{\sum_{i=1}^n s_i^2}+\sum_{i=1}^n s_i^2,$$
which we can simplify to 
$$\sum_{i=1}^n r_is_i\leq \sqrt{\sum_{i=1}^n r_i^2}\sqrt{\sum_{i=1}^n s_i^2}.$$
Squaring this again we arrive at Cauchy's inequality
$$\left(\sum_{i=1}^n r_is_i\right)^2\leq \left(\sum_{i=1}^n r_i^2\right)\left(\sum_{i=1}^n s_i^2\right)$$
which is known to hold for all $n$-tuples of real numbers $(r_1,\ldots, r_n)$ and $(s_1,\ldots, s_n)$.
\end{example}

\begin{example}
Besides the Euclidean distance $d_2$ discussed above, there are many other choices of metric we can put on the $n$-dimensional real vector space $\mathbb R^n$. Let us give two more such examples: for two points $x=(x_1,\ldots, x_n)$ and $y=(y_1,\ldots, y_n)$ in $\mathbb R^n$ we define their \textbf{taxicab distance} $d_1$ by
 $$d_1(x,y) := \sum_{i=1}^n \vert x_i-y_i\vert.$$

 \noindent Another metric is the \textbf{maximum metric} $d_\infty$, which just measures the distance coordinate-wise and then returns the maximal value:
    $$d_\infty(x,y)=\max\{\vert x_i-y_i\vert\mid 1\leq i\leq n\}.$$
\end{example}

\begin{example}
    Let $X=\mathbb C^n$. Then we can define a metric on $X$ by setting
    $$d(z,w)=\sqrt{\sum_{i=1}^n \vert z_i-w_i\vert^2}$$
    When we express each entry of the complex tuple in terms of its real and imaginary parts, the triangle inequality for $\mathbb C^n$ coincides with the one for $(\mathbb R^{2n},d_2)$ discussed above.
\end{example}

\begin{example}[Discrete metric]
    On any set $X \neq\emptyset$ the function
\[
d(x,y) =
\begin{cases}
    1 & \hbox{ if } x \neq y, \\
    0 & \hbox{ if } x = y
\end{cases}
\]
defines a metric called the \textbf{discrete metric}. Such 'pathological'
examples, as they are nicknamed, are not normally used in applications
in analysis. They serve as a warning to check by rigorous proofs
that results suggested by intuition really hold in general metric spaces. In other words, they are potential counterexamples; they explore the boundaries of the concept of a metric space.
\end{example}

\begin{example}
   On the complex plane $\mathbb{C}$ the {\bf French Railway metric} is given as
\[
d_{f}(z_{1},z_{2})=\begin{cases}
    0 & \hbox{if } z_{1}=z_{2},\\
|z_{1}|+|z_{2}| & \hbox{if } z_{1}\neq z_{2}
\end{cases}
\]
is a metric (folklore suggests that the shortest rail journey between any two French towns is via Paris).
\end{example}


\begin{example}[Metric Subspaces]
If $(X,d)$ is a metric space and $Y\subseteq X$ is a subset of $X$, then we can define the \textbf{induced metric} $d_Y$ on $Y$ as the restriction of $d$ to $Y\times Y\subseteq X\times X$, i.e. $d_Y(x,y)=d(x,y)$ for all $x,y\in Y$.

\end{example}

If these were the only examples of metric spaces it is
doubtful whether general metric space theory would be worthwhile. The
examples below indicate the wide range of metric space theory (but do
not exhaust it).

\begin{example} The following metric plays an important role in number theory.
Let $p$ be a fixed prime number. Define a metric $$d_p:\mathbb Z\times \mathbb Z\to \mathbb R$$
by setting $d(m,m)=0$ and for $n\neq m$ set $d(m,n)=1/r$ where $p^{r-1}$ is the highest power of $p$ which divides $m-n$.
\end{example}

\begin{example}[The word metric on a finitely generated group]
This example will only make sense if you know about groups and generating sets. Suppose $G$ is a finitely generated group and $S$ is a generating set for $G$. That is every element $g\in G$ can be written as a product $g=g_1\cdots g_n$ of elements in $S$ (and their inverses). The shortest way to write $g$ in this way is called the length of $g$, denoted by $l(g)$. Now we can define the word-metric on $G$ by setting $d(g,h)=l(g^{-1}h).$
\end{example}

\begin{example}[Geodesic distance on a graph]
    Let $(V,E)$ be a connected graph (undirected, without multiple edges between vertices), with vertex set $V$ and edge set $E$. Then we can define a metric on $V$ by letting $d(v,w)$ be the length of the shortest path between the two vertices $v$ and $w$. This metric is important in the study of networks.
\end{example}

\begin{example}[Hamming distance]
     Let $\Sigma=\{a,b,c,\ldots, z\}$ be the modern Latin alphabet. Let $X$ be the set of all strings of letters in $\Sigma$ of length 4 (e.g. $abcd$ is an element in $X$, so are $math$ or $iosk$). The \textbf{Hamming distance} $d_H$ between two strings in $X$ is the number of positions at which the corresponding symbols are different. In other words, it measures the minimum number of substitutions required to change one string into the other. One can check that $d_H$ is indeed a metric on $X$. A major application of the Hamming distance is in coding theory.
\end{example}

Let us now also introduce a couple of the \emph{function spaces} that motivated Fr\'echet to study metric spaces in the first place. These will be studied in much more detail in Linear Analysis, so we keep our discussion here brief.

\begin{example}[Uniform metric]
   Let $A\neq \emptyset$ be a set. A function $f:A\rightarrow \mathbb R$ is called \textbf{bounded}, if there exists a constant $C>0$ such that $\vert f(a)\vert\leq C$ for all $a\in A$. Let $\ell^\infty (A)$ denote the set of all such bounded, complex valued functions on $A$. Then for $f,g\in \ell^\infty(A)$ we can define
$$d_\infty(f,g) := \sup_{a\in A} \vert f(a)-g(a)\vert.$$
We leave it as an exercise to show that this is indeed a metric.
\end{example}

\begin{example}[$L^1$ metric]
    Let $C[a,b]$ denote the set of all continuous functions $f:[a,b]\to \mathbb R$. Then we can define a metric $d_1$ on $C[a,b]$ by setting
    $$d_1(f,g):=\int_a^b \vert f(x)-g(x)\vert \ \mathrm d x.$$
\end{example}

\begin{example}[$L^2$ metric]
    Let $C[a,b]$ denote the set of all continuous functions $f:[a,b]\to \mathbb R$. Then we can define a metric $d_2$ on $C[a,b]$ by setting
    $$d_2(f,g):=\left( \int_a^b (f(x)-g(x))^2 \ \mathrm d x\right)^\frac{1}{2}.$$
\end{example}

%The following is an important result of this section, a proof can be found in the appendix.
%\begin{theorem}\label{Theorem:All norms equivalent}
%    Let $V$ be a finite-dimensional $\mathbb K$-vector space. Then any two norms $\nor{\cdot}$ and $\nor{\cdot}'$ on $V$ are equivalent.
%\end{theorem}

%In particular, convergence of sequences in $V$ does not depend on the choice of the norm. When we want to test for convergence we can choose the one which makes the task the easiest!

%\begin{corollary}\label{Cor: Norm convergence equivalent to entrywise convergence}
%    Let $\nor{\cdot}$ be an arbitrary norm on $\mathbb
%    K^m$ (where $\mathbb K=\mathbb R$, or $\mathbb C$). Let $(x_n)_n$ be a sequence in $\mathbb K^m$ and $y\in \mathbb K^m$. Then the following are equivalent:
%    \begin{enumerate}
%    \item $x_n\rightarrow y$ with respect to $\nor{\cdot}$;
%    \item $x_{n,i}\rightarrow y_i$ for all $1\leq i\leq m$ (where $x_{n,i}$ is the $i$-th entry of $x_n=(x_{n,1},\ldots, x_{n,m})$).
%    \end{enumerate}
%\end{corollary}
%\begin{proof}
%    The direction $(2)\Rightarrow (1)$ was already verified in Lemma \ref{Lemma:Entrywise implies Norm}.
%    For $(1)\Rightarrow (2)$ it is enough to find one concrete norm for which one can show the converse thanks to Theorem \ref{Theorem:All norms equivalent}. This has been done in Exercise \ref{Exercise:Norm implies entrywise for 1-norm}. 
%\end{proof}

\section{Sequences in Metric Spaces}
Now that we have formalised the notion of distance and a lot of examples to play with we can define convergence of sequences in any metric space:
\begin{definition}
    Let $(X,d)$ be a metric space and $(x_n)_{n\in \mathbb N}$ a sequence in $X$. We say that $(x_n)_{n\in \mathbb N}$ \textbf{converges to $x$} (shorthand notation $x_n\rightarrow x$, or $\lim_{n\rightarrow \infty} x_n=x$) if for every $\varepsilon>0$ there exists an $N\in\mathbb N$ such that $d(x_n,x)<\varepsilon$ for all $n\geq N$.
\end{definition}


Given a sequence $(x_n)_{n\in \mathbb N}$ in $X$ and $x\in X$ we can consider the sequence of distances $(d(x_n,x))_{n\in \mathbb N}$ in $[0,\infty)$. 
Comparing the definition above with the one from the intro it is clear that $(x_n)_{n\in \mathbb N}$ converges to $x$ in $(X,d)$ if and only if the sequence of distances $(d(x_n,x))_{n\in \mathbb N}$ converges to $0$ in the usual sense of convergence of sequences of real numbers!
    
  


We want to observe that if a sequence in a metric space converges, then its limit is unique. It might come as a surprise why this requires a proof at all, but we will later (in a more general context) see that this is indeed an important feature of metric spaces.

\begin{lemma}\label{Lemma: Metric spaces are Hausdorff}
    Let $(X,d)$ be a metric space and $(x_n)_{n\in \mathbb N}$ be a sequence in $X$ and $x,y\in X$. If $x_n\rightarrow x$ and $x_n\rightarrow y$, then $x=y$.
\end{lemma}
\begin{proof}
    Observe first that the conclusion $x=y$ is equivalent to $d(x,y) <\varepsilon$ for all $\varepsilon>0$. Thus, it suffices to show the latter.
    So let $\varepsilon>0$ be given. Then there exist $N_1,N_2\in \mathbb N$ such that $d(x_n,x)<\frac{\varepsilon}{2}$ for all $n\geq N_1$ and $d(x_n,y)<\frac{\varepsilon}{2}$ for all $n\geq N_2$. Let $N:=\max \{N_1,N_2\}$. Then using the triangle-inequality (M3) we have
    $$d(x,y)\leq d(x,x_N)+d(x_N,y)<\varepsilon$$
    Since $\varepsilon$ was aribtrary it follows that $d(x,y)=0$ and hence $x=y$ by axiom (M1).   
\end{proof}

\noindent Note also that this result justifies the notation $\lim_{n\rightarrow \infty} x_n$ for the limit.

\smallskip



From real analysis we know a lot of tools to check if a sequence in $\mathbb R$ converges, but checking if a sequence in a given metric space converges seems like a much more daunting task. It is helpful to observe that some metrics have the same convergent sequences. If that is the case, we can just chose the one that seems easier to us to check convergence. Formally we make the following definition:

%\begin{lemma}[entrywise convergence $\Rightarrow$ convergence]\label{Lemma:Entrywise implies Norm}
%    Let $d_i$ for $i=1,2,\infty$ be one of the metrics on $\mathbb
%    R^m$ discussed above. Let $(x_n)_n$ be a sequence in $\mathbb R^m$ and $y\in \mathbb R^m$ such that $x_{n,i}\rightarrow y_i$ for all $1\leq i\leq m$ (where $x_{n,i}$ is the $i$-th entry of $x_n$). Then $x_n\rightarrow y$ in $\mathbb R^m$ with respect to $d_i$.
%\end{lemma}

%\begin{proof}
%    The assumptions tell us that $\vert x_{n,i}- y_i\vert\rightarrow 0$ for all $1\leq i\leq m$.
%%    Let $\{e_1,\ldots, e_m\}$ denote the standard basis vectors for $\mathbb K^n$. Then we compute:
 %%   \begin{align*}
   %     \nor{x_n-y}&=\nor{\sum_{i=1}^m (x_{n,i}-y_i)e_i}\\
    %    &\stackrel{\Delta-ineq}{\leq}\sum_{i=1}^m \nor{(x_{n,i}-y_i)e_i}\\
     %   &=\sum_{i=1}^m \vert x_{n,i}-y_i\vert \nor{e_i}\\
      %  &\leq (\max_{1\leq i\leq m} \nor{e_i}) \sum_{i=1}^m \vert x_{n,i}-y_i\vert \rightarrow 0
    %\end{align*}    
       
%\end{proof}
  




%%%%%%%%%%%%%%%%%%%%
\begin{definition}
\item Two metrics $d$ and $d'$ on a set $X$ are  \textbf{Lipschitz equivalent} if there are constants $C,D>0$ such that
\[
d(x,y)\leq Cd'(x,y)\ \hbox{ and }\ d'(x,y) \leq D d(x,y)
\]
for all $x,y\in X$.
\end{definition}

\begin{example}
    The metrics $d_1, d_2$, and $d_\infty$ on $\mathbb R^n$ are pairwise Lipschitz equivalent.
    The proof proceeds in several steps.
\begin{enumerate}
    \item For all $x=(x_{1},x_{2},\ldots,x_{n})$ and $y=(y_{1},y_{2},\ldots,y_{n})$ in $\mathbb R^{n}$,
we have
\[
d_\infty(x,y)=\max\{|x_{i}-y_i|:1\leq i\leq n\}
\leq\sum_{i=1}^{n}|x_{i}-y_i|=d_1(x,y)
\]
and
\[
d_1(x,y)=\sum_{i=1}^{n}|x_{i}-y_i|
\leq \sum_{i=1}^{n}\max\{|x_{i}-y_i|:1\leq i\leq n\}
=\sum_{i=1}^{n} d_\infty(x,y)
=n \cdot d_\infty(x,y).
\]
In conclusion we have $d_\infty(x,y)\leq d_1(x,y)\leq nd_\infty(x,y)$ for all $x,y\in \mathbb R^n$.
Thus, the metrics $d_1$ and $d_\infty$ are Lipschitz equivalent.

\item For all $x=(x_{1},x_{2},\ldots,x_{n})$ in $\mathbb R^{n}$,
we have
\[
d_\infty(x,y)^2
=\left(\max\{|x_{i}-y_i|:1\leq i\leq n\}\right)^2
\leq\sum_{i=1}^{n}|x_{i}-y_i|^{2}=d_2(x,y)^2,
\]
and
\[
d_2(x,y)^2=\sum_{i=1}^{n}|x_{i}-y_i|^{2}
\leq\sum_{i=1}^{n}\max\{|x_{i}-y_i|^{2}:1\leq i\leq n\}
=n\cdot d_\infty(x,y)^2.
\]
Thus, taking square roots throughout we get
$$d_\infty(x,y)\leq d_2(x,y)\leq \sqrt{n}d_\infty(x,y) \ \forall x,y\in \mathbb R^n.$$

\item Combining (1) and (2) we can also prove that $d_1$ and $d_2$ are Lipschitz equivalent since for all $x,y\in \mathbb R^n$ we have
$$d_1(x,y)\stackrel{(1)}{\leq} nd_\infty(x,y)\stackrel{(2)}{\leq} nd_2(x,y)\stackrel{(2)}{\leq}n\sqrt{n}d_\infty(x,y)\stackrel{(1)}{\leq}n\sqrt{n}d_1(x,y).$$

\end{enumerate}
\end{example}



\begin{proposition}\label{Prop: equivalent metrics convergence}
     If $d$ and $d'$ are Lipschitz equivalent metrics on $X$, and $(x_n)_{n\in \mathbb N}$ is a sequence in $X$, then
        $x_n\rightarrow x$ with respect to $d$ if and only if $x_n\rightarrow x$ with respect to $d'$.
\end{proposition}
\begin{proof}
    The statement is clearly symmetric, so we only have to prove one direction and the other will work in exactly the same way with the roles of $d$ and $d'$ exchanged. 

    \noindent So suppose that $x_n\to x$ with respect to $d$. We want to show that $x_n\to x$ with respect to $d'$.
    In order to verify the definition we fix an arbitrary tolerance $\varepsilon>0$. We also know that $d$ and $d'$ are Lipschitz equivalent. So let us fix a $D>0$ such that
    $$d'(x,y)\leq D d(x,y) \ \forall x,y\in X.$$

    Since $x_n\to x$ with respect to $d$ we know that there must exist an $N\in \mathbb N$ such that $d(x_n,x)<\varepsilon/D$ for all $n\geq N$. 
    Thus, for all $n\geq N$ we have
    $$d'(x_n,x)\leq D\cdot d(x_n,x)<D \cdot \varepsilon/D=\varepsilon$$
    as desired.
\end{proof}



\begin{example}
Let $C[0,1]$ be the set of all continuous real-valued functions defined on the closed interval $[0,1]$, and consider the metrics
\[
d_\infty(f,g)=\sup\{|f(x)-g(x)|:0\leq x\leq 1\} \hbox{ and }  d_1(f,g)=\int_{0}^{1}\vert f(x)-g(x)\vert \ dx
\]
on $C[0,1]$.
Then $d_{\infty}$ and $d_{1}$ are NOT Lipschitz equivalent.
\begin{enumerate}
\item  The inequality $d_1(f,g)\leq d_\infty(f,g)$ still holds as in the discrete setting:
by definition of $d_\infty$, for all $x \in [0,1]$,
\[
\vert f(x)-g(x)\vert  \leq \sup_{y \in [0,1]} |f(y)-g(y)|= d_\infty(f,g).
\]
Hence by integration theory,
\[
d_1(f,g)=\int_{0}^{1} \vert f(x)-g(x)\vert dx \leq \int_{0}^{1}d_\infty(f,g)\ dx = d_\infty(f,g).
\]

\item The other direction however fails: for any $n\in \mathbb N$, consider the continuous function
\[
g_{n}(t)=\left\{\begin{array}{lc}
-nt +1 & \hbox{ if } t \in [0, \frac{1}{n}], \\
0 & \hbox{ if } t \in [\frac{1}{n},1], \end{array}\right\}
\]
The graph of $g_n$ is the union of the line segments connecting $(0,1)$ with $(\frac{1}{n},0)$ and $(\frac{1}{n},0)$ with $(1,0)$.
Then it is easy to see that
\[
d_1(g_n,0)=\int_{0}^{1}|g_{n}(x)|dx = \int_{0}^{\frac{1}{n}} (-nt +1)dt = \left[-\frac{n}{2}t^2+t\right]_{0}^{\frac{1}{n}}=\frac{1}{2n}
\]
and that
\[
d_\infty(g_n,0)=\sup_{t \in [0,1]}|g_{n}(t)| = 1.
\]

\noindent Suppose for contradiction, that there exists a constant $C>0$ such that $d_\infty \leq C d_1$. Then for all $n\in \mathbb N$ we would have
$$1=d_\infty(g_n,0) \leq C d_1(g_n,0)=C \frac{1}{2n},$$
a contradiction.
\end{enumerate}
\end{example}




%%%%%%%%%%%%%%%%%%%%


\begin{exercise}\label{Exercise:Norm implies entrywise for 1-norm}
    Consider the metrics $d_1,d_2,d_\infty$ on $\mathbb R^m$ from week 1. Show that a sequence $(x_n)_{n\in \mathbb N}$ in $\mathbb R^m$ converges to $x=(x(1),\ldots, x(m))\in\mathbb R^m$ with respect to $d_i$ if and only if for all $1\leq i\leq m$ the sequence of the $i$-th entries $(x_n(i))_{n\in \mathbb N}$ converges to $x(i)$ in $\mathbb R$.
\end{exercise}

\subsection*{Cauchy sequences}
Here is another useful concept that can be carried over from real analysis without any trouble.
\begin{definition}
    Let $(X,d)$ be a metric space. A sequence $(x_n)_{n\in \mathbb N}$ in $X$ is called a \textbf{Cauchy sequence} if for all $\varepsilon>0$ there exists an $N\in \mathbb N$ such that $d(x_n,x_m)<\varepsilon$ for all $n,m\geq N$.
\end{definition}
\noindent The proofs of the following two elementary facts about Cauchy sequences are also almost exactly the same as in calculus:
\begin{lemma} Let $(X,d)$ be a metric space.
\begin{enumerate}
    \item Every convergent sequence in $X$ is a Cauchy sequence. 
    \item Every Cauchy sequence in $X$ is bounded.
\end{enumerate}
    
\end{lemma}
\begin{proof}
    \begin{enumerate}
        \item Let $(x_n)_{n\in \mathbb N}$ be a convergent sequence with limit $x\in X$. Let furthermore $\varepsilon >0$ be given. Since $(x_n)_{n\in \mathbb N}$ converges to $x$, there exists an $N\in \mathbb N$ such that $d(x_n,x)<\varepsilon/2$ for all $n\geq N$. Using the triangle-inequality (M3) it follows that for all $n,m\geq N$ we have
        $$d(x_n,x_m)\leq d(x_n,x)+d(x,x_m)<\varepsilon/2 + \varepsilon/2 =\varepsilon.$$

        \item Let $(x_n)_{n\in \mathbb N}$ be a Cauchy sequence. We need to show that there exists a number $D\geq 0$ such that $d(x_n,x_m)\leq D$ for all $n,m\in \mathbb N$. Since $(x_n)_{n\in \mathbb N}$ is Cauchy, for $\varepsilon=1$ there exists an $N\in \mathbb N$ such that $d(x_n,x_m)\leq 1$ for all $n,m\geq N$. Hence $1$ works as an upper bound for the sequence $x_N,x_{N+1},x_{N+2},\ldots$. Moreover, by the triangle inequality we have
        $$d(x_1,x_n)\leq d(x_1,x_N)+d(x_N,x_n)\leq d(x_1,x_N)+1 \ \forall n\geq N.$$
        Similarly for $x_2, x_3,\ldots, x_{N-1}$.

        So if we set $\Tilde{D}=\max\{d(x_i,x_N)\mid 1\leq i\leq N-1\} +1$, then this almost works.   The only distances we have not yet taken care of are the distances $d(x_i,x_j)$ when $1\leq i,j\leq N-1$. But notice that by the triangle inequality (M3) again we have

        $$d(x_i,x_j)\leq d(x_i,x_N)+d(x_N,x_j)\leq 2\Tilde{D}.$$

        So if we set $D:=2\Tilde{D}$, then $d(x_n,x_m)\leq D$ for all $n,m\in \mathbb N$.
    \end{enumerate}
\end{proof}
The converse of (1) it not true as the following familiar example shows:
\begin{example}
    Consider the space $X=\mathbb Q$ with the standard metric $d(x,y)=\vert x-y\vert$. 
    Define a sequence $(x_n)_n$ by $x_1=1$ and $x_{n+1}=x_n/2+1/x_n$. Clearly, $x_n\in \mathbb Q$ for all $n\in \mathbb N$. We claim that the sequence converges, but only in the bigger set $\mathbb R$. Note that
    $$x_n-x_{n+1}=x_n-\frac12\Bigl(x_n+\frac 2{x_n}\Bigr)=\frac1{2x_n}(x_n^2-2).$$
    Focussing on the second factor we have
    \begin{align*}
x_n^2-2
	&=\frac14\Bigl(x_{n-1}+\frac 2{x_{n-1}}\Bigr)^2-2\\
	&=\frac{x_{n-1}^2}4-1+\frac{2^2}{4x_{n-1}^2}\\
	&=\frac14\Bigl(x_{n-1}^2-4+\frac{2^2}{x_{n-1}^2}\Bigr)\\
	&=\frac{1}{4}\Bigl(x_{n-1}-\frac 2{x_{n-1}}\Bigr)^2\\
	&\ge0.
\end{align*}
It follows that $(x_n)_n$ is decreasing and bounded below. Thus, the Monotone Convergence Theorem (from Stage 1 Real Analysis!) that the sequence converges to a point $x\in \mathbb R$. Using the algebra of limits, the point $x$ must satisfy $x=x/2 + 1/x$ which gives $x=\sqrt{2}$. Since the sequence is convergent, it must be a Cauchy sequence. So we have found a Cauchy sequence in $\mathbb Q$ which does not converge in $\mathbb Q$. 
\end{example}

The observation that Cauchy sequences do not necessarily converge in every metric space is a first major difference to what we know about sequences in $\mathbb R$. Thus, we see that ``all Cauchy sequences converge" is a property of a metric space, not an intrinsic feature. Since it is a very useful property, we give it a name:
\begin{definition}
    A metric space $(X,d)$ is called \textbf{complete} if every Cauchy sequence in $X$ converges in $X$.
\end{definition}

From Calculus we know that $\mathbb R$ is complete. In fact this is the fundamental property that distinguishes $\mathbb R$ from $\mathbb Q$! Using this we can also show that higher dimensional Euclidean space is complete:
\begin{example}
$(\mathbb R^k,d_2)$ is complete for all $k\in \mathbb N$. Consider a Cauchy sequence $(x_n)_{n\in \mathbb N}$ in $\mathbb R^k$. Note that $x_n\in \mathbb R^k$ for each $n\in \mathbb N$, i.e. $x_n$ is a vector with $k$ entries. We will write $x_n=(x_n(1),x_n(2),\ldots, x_d(k))$. Fix $i\in \{1,\ldots, k\}$. Then for each $x_n$ we look at it's $i$-th entry. This gives us a sequence $(x_n(i))_{n\in \mathbb N}$ in $\mathbb R$. We claim that this is a Cauchy sequence in $\mathbb R$. Indeed, let $\varepsilon >0$ be given. Since $(x_n)_n$ is a Cauchy sequence, there exists an $N\in \mathbb N$ such that $d_2(x_n,x_m)<\sqrt{\varepsilon}$ for all $n,m\geq N$. 
But then for all $n,m\geq N$ we have
$$
\vert x_n(i)-x_m(i)\vert ^2\leq \sum_{i=1}^d \vert x_n(i)-x_m(i)\vert ^2=d_2(x_n,x_m)^2<\varepsilon.
$$
Thus our claim follows. Using that $\mathbb R$ is complete, for each $i$, the sequence $(x_n(i))_{n\in \mathbb N}$ converges to some $x(i)\in \mathbb R$. Setting $x:=(x(1),x(2),\ldots, x(d))\in \mathbb R^d$ we conclude that $x_n\rightarrow x$ by Exercise \ref{Exercise:Norm implies entrywise for 1-norm}. Thus we have shown that every Cauchy sequence in $\mathbb R^k$ converges.
\end{example}

The following result shows that completeness is preserved under Lipschitz equivalence. We leave the proof as an exercise!
\begin{proposition}
    Let $d$ and $d'$ be Lipschitz-equivalent metrics on $X$. Then $(X,d)$ is complete if and only if $(X,d')$ is complete.
\end{proposition}
%\begin{proof}
%    An argument very similar to the proof of Proposition \ref{Prop: equivalent metrics convergence} shows that a sequence $(x_n)_{n\in \mathbb N}$ in $X$ is a Cauchy sequence with respect to $d$ if and only if it is a Cauchy sequence with respect to $d'$. 
    
%    Suppose now that $(X,d)$ is complete. We want to show that $(X,d')$ is complete. Given a Cauchy sequence $(x_n)_{n\in \mathbb N}$ in $X$ with respect to $d'$, the observation above shows that $(x_n)_{n\in \mathbb N}$ is also a Cauchy sequence with respect to $d$. Since $(X,d)$ is complete, there exists an $x\in X$ such that $x_n\to x$ with respect to $d$. But then applying Proposition \ref{Prop: equivalent metrics convergence} shows that $x_n\to x$ with respect to $d'$ as well. This shows that $(X,d')$ is complete as well. The converse direction works in exactly the same way by swapping the roles of $d$ and $d'$.
%\end{proof}



%The following is an important result of this section, a proof can be found in the appendix.
%\begin{theorem}\label{Theorem:All norms equivalent}
%    Let $V$ be a finite-dimensional $\mathbb K$-vector space. Then any two norms $\nor{\cdot}$ and $\nor{\cdot}'$ on $V$ are equivalent.
%\end{theorem}

%In particular, convergence of sequences in $V$ does not depend on the choice of the norm. When we want to test for convergence we can choose the one which makes the task the easiest!

%\begin{corollary}\label{Cor: Norm convergence equivalent to entrywise convergence}
%    Let $\nor{\cdot}$ be an arbitrary norm on $\mathbb
%    K^m$ (where $\mathbb K=\mathbb R$, or $\mathbb C$). Let $(x_n)_n$ be a sequence in $\mathbb K^m$ and $y\in \mathbb K^m$. Then the following are equivalent:
%    \begin{enumerate}
%    \item $x_n\rightarrow y$ with respect to $\nor{\cdot}$;
%    \item $x_{n,i}\rightarrow y_i$ for all $1\leq i\leq m$ (where $x_{n,i}$ is the $i$-th entry of $x_n=(x_{n,1},\ldots, x_{n,m})$).
%    \end{enumerate}
%\end{corollary}
%\begin{proof}
%    The direction $(2)\Rightarrow (1)$ was already verified in Lemma \ref{Lemma:Entrywise implies Norm}.
%    For $(1)\Rightarrow (2)$ it is enough to find one concrete norm for which one can show the converse thanks to Theorem \ref{Theorem:All norms equivalent}. This has been done in Exercise \ref{Exercise:Norm implies entrywise for 1-norm}. 
%\end{proof}

\section{Maps between metric spaces I}
Once we have a new mathematical object in the form of a set with some additional structure, we usually want to study functions between different instances of this object that preserve the given structure (e.g. group homomorphisms between groups, linear maps between vector spaces etc). The strongest way to preserve the structure of the metric space is by preserving distances on the nose:

\begin{definition} Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces. A map $f:X\to Y$ is called an \textbf{isometry} if $d_Y(f(x),f(y))=d_X(x,y)$ for all $x,y\in X$.
\end{definition}

\begin{examples}
    Consider $X=\mathbb R^n$ with the Euclidean metric $d_2$.
    \begin{enumerate}
        \item Given a fixed vector $b\in \mathbb R^n$ the translation map $f(x):=x+b$ is an isometry. Indeed
    $$d_2(f(x),f(y))=\sqrt{\sum_{i=1}^n (x_i+b_i-(y_i+b_i))^2}=\sqrt{\sum_{i=1}^n (x_i-y_i)^2}=d_2(x,y).$$
    A similar calculation works for the metrics $d_1$ and $d_\infty$.
    \item Let $Q\in M_n(\mathbb R)$ be an orthogonal matrix, i.e. $Q^TQ=I=QQ^T$. These matrices represent rotations about the origin, and reflections along a hyperplane. For example

    $$R_\theta=\begin{pmatrix}
        \cos(\theta) & -\sin(\theta)\\
        \sin(\theta) & \cos(\theta)
    \end{pmatrix}$$
    is the rotation with angle $\theta\in [0,2\pi]$ about the origin in the plane $\mathbb R^2$, and
    $$S=\begin{pmatrix}
        1 & 0\\
        0 & -1
    \end{pmatrix}$$
    is the reflection across the $x$-axis. 
    For any orthogonal matrix $Q$ the map $$f_Q:\mathbb R^n \to \mathbb R^n, \ f_Q(x)=Qx$$
    is an isometry with respect to $d_2$. To see this we make the observation that $d_2$ can be expressed in terms of the dot product on $\mathbb R^n$:    
      $$d_2(x,y)=\sqrt{\langle x-y,x-y\rangle}$$
      Using this we have
      \begin{align*}
          d_2(Qx,Qy)&=\sqrt{\langle Q(x-y),Q(x-y)\rangle}\\
          & = \sqrt{\langle Q^TQ(x-y),x-y\rangle}\\
          & = \sqrt{\langle x-y,x-y\rangle}\\
          & = d_2(x,y).
      \end{align*}
      \item Consider the canonical map $i:\mathbb Z\to \mathbb R$, $i(n)=n$. Then $i$ is isometric.
      
\end{enumerate}
\end{examples}
The following easy Lemma shows that being an isometry is quite a strong condition:
\begin{lemma}
    Let $f:X\to Y$ be an isometry. Then $f$ is injective.
\end{lemma}
\begin{proof}
    Let $x,x'\in X$ such that $f(x)=f(x')$. Then
    $d_X(x,x')=d_Y(f(x),f(x'))=0$ an hence (M1) implies that $x=x'$.
\end{proof}
This seems very restrictive when compared to other settings (e.g. not every linear map between vector spaces is automatically injective). In the following we also want to consider successively weaker concepts:

\begin{definition}
    Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces and let $f:X\to Y$ be a map. 
    \begin{enumerate}
        \item $f$ is called \textbf{Lipschitz continuous} if there exists a constant $C\geq 0$ such that
    $$d_Y(f(x),f(y))\leq C d_X(x,y) \hbox{ for all } x,y\in X.$$
            The constant $C$ is called a Lipschitz constant.
        \item $f$ is called \textbf{uniformly continuous} if for every $\varepsilon>0$ there exists $\delta>0$ such that for all $x,y\in X$ we have 
        $$d_X(x,y)<\delta \Rightarrow d_Y(f(x),f(y))<\varepsilon.$$
        \item $f$ is called \textbf{continuous} at $x_0$ if 
        for every $\varepsilon>0$ there exists $\delta>0$ such that for all $x\in X$ satisfying $d_X(x,x_0)<\delta$ we have  $d_Y(f(x),f(x_0))<\varepsilon$.
        $f$ is called \textbf{continuous} if it is continuous at all points $x_0\in X$.
    \end{enumerate}    
\end{definition}

Note that we the following implications hold true in general and are almost obvious from the definition:

\begin{center}
    $f$ isometry $\Rightarrow$ $f$ Lipschitz continuous $\Rightarrow$ $f$ uniformly continuous $\Rightarrow$ $f$ continuous.
\end{center}
The converse implications are all false. This can already be seen by looking at familiar examples of real functions.
\begin{examples}
\begin{enumerate}
    \item The sine function $\sin:\mathbb R\to \mathbb R$ is a Lipschitz continuous function with respect to the usual metric on $\mathbb R$. Let $x,y\in \mathbb R$ be given. We know that the sine function is differentiable everywhere, so by the mean value theorem, there exists a $c\in (x,y)$ such that
    $\cos(c)=\sin'(c)=\frac{\sin(y)-\sin(x)}{y-x}$.
    It follows that
    $$\vert \sin(x)-\sin(y)\vert=\vert \cos(c)\vert \vert x-y\vert\leq \vert x-y\vert.$$
    So we can choose the Lipschitz constant $C=1$. However, the sine function is not isometric since for example
    $$\vert \sin(\pi/2)-\sin(0)\vert=1\neq \vert \pi/2-0\vert.$$
    \item Consider the square root function $\sqrt{\cdot}:[0,\infty)\to \mathbb R$. This function is uniformly continuous but not Lipschitz continuous.
    It is uniformly continuous, because for any $\varepsilon >0$ we can set $\delta:=\varepsilon^2$ and then compute for any $x,y\geq 0$ with $\vert x-y\vert<\delta$:
    $$\vert \sqrt{x}-\sqrt y\vert^2\leq \vert \sqrt{x}-\sqrt y\vert\vert \sqrt{x}+\sqrt y\vert=\vert x-y\vert<\delta=\varepsilon^2.$$
    Taking square roots gives $\vert \sqrt{x}-\sqrt y\vert<\varepsilon$ as desired.
    
    However, the square root function is not Lipschitz continuous, since given any $C>0$ pick $0<x<1/C^2$ and $y=0$. Then
    $$\frac{\vert \sqrt{x}-\sqrt{y}\vert}{\vert x-y\vert}=\frac{\sqrt{x}}{x}=\frac{1}{\sqrt{x}}>C.$$
    \item The function $f:\mathbb R\to \mathbb R$, $f(x)=x^2$ is continuous but not uniformly continuous.
\end{enumerate}
\end{examples}

Uniform continuity will come up again later in the course. For now let us prove an important result on Lipschitz continuous functions with Lipschitz constant strictly less than one:

\begin{theorem}[Contraction Mapping Theorem/Banach Fixed-Point Theorem]
    Let $(X,d)$ be a non-empty complete metric space and let $T:X\to X$ be a Lipschitz continuous map with Lipschitz constant $C<1$. 
    Then $T$ admits a unique fixed point, i.e. there exists exactly one point $x^*\in X$ such that $T(x^*)=x^*$.
\end{theorem}
\begin{proof}
We will first proof the \textit{existence} of a fixed point.
    To start the proof, fix an arbitrary point $x_0\in X$. Then, define a sequence in $X$ inductively by setting $x_n:=T(x_{n-1})$ for all $n\geq 1$.

    Our goal is to show that $(x_n)_n$ is a Cauchy sequence. To do this we need an intermediate claim:
    \begin{equation}
        d(x_{n+1},x_n)\leq C^n d(x_1,x_0)\ \forall n\in \mathbb N
    \end{equation}
    We can prove this by induction on $n$ using the hypothesis in the theorem: for $n=1$ we have 
    $$d(x_2,x_1)=d(T(x_1),T(x_0))\leq Cd(x_1,x_0).$$
    For the induction step, suppose that the inequality is true for $n$. Then
    $$d(x_{n+2},x_{n+1})=d(T(x_{n+1}),T(x_n))\leq C d(x_{n+1},x_n)\leq C \cdot C^n d(x_1,x_0).$$

    Now let $m,n\in \mathbb N$. We may assume without loss of generality that $m>n$. Then we compute
    \begin{align}
        d(x_m,x_n) & \leq  d(x_m,x_{m-1})+d(x_{m-1},x_{m-2})+\ldots + d(x_{n+1},x_n)\\
        & \leq C^{m-1}d(x_1,x_0)+C^{m-2}d(x_1,x_0) +\ldots + C^n d(x_1,x_0)\\
        & = C^nd(x_1,x_0) \left(\sum_{k=0}^{m-n-1} C^k\right)\\
        & \leq  C^nd(x_1,x_0) \left(\sum_{k=0}^{\infty} C^k \right)\\
        & = C^nd(x_1,x_0) \frac{1}{1-C}
    \end{align}

It follows that $(x_n)_n$ is a Cauchy sequence. Since $X$ was assumed to be complete the sequence $(x_n)_n$ has a limit in $X$, call it $x^*$. Then $x^*$ is a fixed point for $T$. Indeed, since
$$d(T(x^*),x^*)\stackrel{(M3)}{\leq} d(T(x^*),T(x_n))+d(T(x_n),x^*)\leq Cd(x^*,x_n)+d(x_{n+1},x^*)\to 0,$$
we have $d(T(x^*),x^*)=0$ and hence $(M1)$ implies $T(x^*)=x^*$.
This concludes the proof of the existence of a fixed point. It remains to show that $x^*$ is the unique fixed point.
Let $y^*\in X$ be any point with $T(y^*)=y^*$. Then using the fact that $T$ is a conctraction we compute
$$d(x^*,y^*)=d(T(x^*),T(y^*))\leq C d(x^*,y^*).$$
But $0<C<1$, so the above inequality can only hold when $d(x^*,y^*)=0$, which implies $x^*=y^*$ by $(M1)$.
\end{proof}

For the theorem to work we really need a contraction. For example the translation maps $f_b(x)=x+b$ are isometries, but for $b\neq 0$ they clearly have no fixed point. 

\begin{definition}
    A map $f:X\to Y$ between two metric spaces $(X,d_X)$ and $(Y,d_Y)$ is called a \textbf{bi-Lipschitz equivalence} if there exist constants $c,C>0$ such that
    $$cd_X(x,y)\leq d_Y(f(x),f(y))\leq Cd_X(x,y) \ \forall x,y\in X.$$
\end{definition}
Clearly, every isometry is a bi-Lipschitz equivalence. If $d$ and $d'$ are two metrics on the same set $X$ then the identity map $\mathrm{id}_X:(X,d)\to (X,d')$ is a bi-Lipschitz equivalence if and only if the metrics are Lipschitz equivalent in the sense of section 2.

Again, a bi-Lipschitz equivalence is always injective (why?), but not necessarily surjective.

\begin{proposition}
    Let $f:X\to Y$ be a bi-Lipschitz equivalence. If $X$ is complete, then $f(X)$ is complete.
\end{proposition}
\begin{proof}
    Let $(y_n)_n$ be a Cauchy sequence in $f(X)$. Then for each $n\in \mathbb N$ we must have $y_n=f(x_n)$ for some $x_n\in X$. We claim that $(x_n)_n$ is also a Cauchy sequence. So let $\varepsilon>0$ be given. Then, since $(y_n)_n$ is Cauchy, there exists an $N\in \mathbb N$ such that $d(y_n,y_m)<c\varepsilon$ for all $n,m\geq N$. Then, for all $n,m\geq N$ we have
    $$d(x_n,x_m)\leq \frac{1}{c}d_Y(f(x_n),f(x_m))=\frac{1}{c}d_Y(y_n,y_m)<\varepsilon.$$
    So $(x_n)_n$ is indeed a Cauchy sequence. Using that $X$ is complete, there exists an element $x\in X$ such that $x_n\to x$. Let $y:=f(x)\in f(X)$. To finish the proof we show that $y_n\to y$. But this follows from the second inequality  in the bi-Lipschitz condition since
    $$d(y_n,y)=d(f(x_n),f(x))\leq Cd_X(x_n,x)\to 0,$$
    and hence $y_n\to y$ as desired.
    
\end{proof}

\begin{corollary}
    If $f:X\to Y$ is a surjective bi-Lipschitz equivalence, then $X$ is complete if and only if $Y$ is complete.
\end{corollary}
\begin{proof}
Suppose $X$ is complete. The previous proposition implies that $f(X)$ is complete, but since $f$ is surjective, we conclude that $Y=f(X)$ is complete.

For the converse, first observe that the hypothesis imply that $f$ is a bijection. We claim that $f^{-1}:Y\to X$ is also a bi-Lipschitz map. Let $c,C>0$ are the bi-Lipschitz constants for $f$ and let $y_1,y_2\in Y$ be arbitrary elements. Then we get
$$c d_X(f^{-1}(y_1),f^{-1}(y_2))\leq d_Y(f(f^{-1}(y_1)),f(f^{-1}(y_2)))=d_Y(y_1,y_2)\leq C d_X(f^{-1}(y_1),f^{-1}(y_2))$$
and manipulating the two inequalities we conclude that
$$\frac{1}{C}d_Y(y_1,y_2)\leq  d_X(f^{-1}(y_1),f^{-1}(y_2))\leq \frac{1}{c}d_Y(y_1,y_2).$$
Thus $f^{-1}$ is also bi-Lipschitz with constants $1/C$ and $1/c$. Applying Proposition 3.8 to $f^{-1}$ then implies that $X$ is complete whenever $Y$ is complete.
\end{proof}

\section{The metric topology}
We have already seen that the notions of convergence and continuity in the setting of metric spaces do only depend on the metric up to a certain extent. For example, if we replace $d$ by a Lipschitz-equivalent metric $d'$, then sequences converge with respect to $d$ if and only if they converge with respect to $d'$. In this section we will introduce the concepts on which convergence actually depends.
This will eventually lead us the definition of a topological space. 

\begin{definition}\label{Def:Open sets in metric space}
    Let $(X,d)$ be a metric space, $x\in X$ and $r>0$.
\begin{enumerate}
    \item The \textbf{open ball} of radius $r$ centered at $x$ is the set 
    $$U_r(x):=\{y\in X\mid d(x,y)<r\},$$
    and similarly, the \textbf{closed ball} of radius $r$ centered at $x$ is the set 
    $$B_r(x):=\{y\in X\mid d(x,y)\leq r\}.$$
%    \item A set $U\subseteq X$ is called a \textbf{neighbourhood} of $x$ (with respect to $d$) if there exists an $r>0$ such that $U_r(x)\subseteq U$.
    \item $U\subseteq X$ is called \textbf{open} if for every $y\in U$ there exists an $r>0$ such that $U_r(y)\subseteq U$. %This means that $U$ is a neighbourhood of all of its elements.
    \item $A\subseteq X$ is called \textbf{closed} if $X\setminus A$ is open.
\end{enumerate}
\end{definition}

%%%%%%%%%%%%%%%%%%%%
\begin{remark}
We use the word ``ball'' in a metric space, though these sets may not look very ball-like (depending on the chosen metric). See the exercise sheet for some examples. So the word ``ball'' is an abuse of terminology.
\end{remark}



\begin{examples} Let $(X,d)$ be a metric space, $x\in X$ and $r>0$.
  \begin{enumerate}
%      \item $B_r(x)$ is always a neighbourhood of $x$, since $U_r(x)\subseteq B_r(x)$.
      
      \item As the name suggests, the open ball $U_r(x)$ is always open in the sense of Definition 4.1(2): Indeed, let $y\in U_r(x)$. Then $\varepsilon:=r-d(x,y)>0$ and we claim that $U_\varepsilon(y)\subseteq U_r(x)$: For $z\in U_\varepsilon(y)$ we compute
      $$d(z,x)\stackrel{(M3)}{\leq} d(z,y)+d(y,x)<\varepsilon +d(y,x)=r-d(x,y)+d(y,x)\stackrel{(M2)}{=}r,$$ which proves the claim.

      \item Similarly, the closed ball $B_r(x)$ is always closed in the sense of Definition 4.1(3). This works in a very similar way to the above and is a good exercise!
      %To see this we have to show $X\setminus B_r(x)$ is open. So let $y\in X\setminus B_r(x)$. Then $d(x,y)>r$ and hence $\varepsilon:=d(x,y)-r>0$. Then for any $z\in U_\varepsilon (y)$ the triangle inequality (M3) implies that
      %$d(x,y)\leq d(x,z)+d(z,y)$, i.e. $$d(z,x)\geq d(x,y)-d(z,y)>d(x,y)-\varepsilon=r.$$ This shows that $U_\varepsilon(y)\subseteq X\setminus B_r(x)$ as desired.
      \item Every singleton set $\{y\}$ is closed. To see this we need to show that $X\setminus\{y\}$ is open. So let $x\in X\setminus \{y\}$. Then $r:=d(x,y)>0$ by (M1), and $U_r(x)\subseteq X\setminus \{y\}$.

  \end{enumerate}
\end{examples}

\begin{examples}Consider $\mathbb R$ with the Euclidean metric.
\begin{enumerate}
    \item The open balls in $\mathbb R$ are exactly the open intervals. Indeed, for $x\in\mathbb R$ we have $U_r(x)=(x-r,x+r)$. Conversely, given an open interval $(a,b)$ let $r:=\vert a-b\vert /2$. Then $(a,b)=U_r(\frac{a+b}{2})$.
    \item Similarly, the closed balls in $\mathbb R$ correspond to the closed intervals $[a,b]$.
\end{enumerate}
     
    
    \end{examples}


%%%%%%%%%%%%%%%%%%%%
\textbf{Warning:}
A common mistake is to say that if a set is not open then it is closed (or vice versa).
\textbf{THIS IS NOT TRUE!}

In metric spaces a set can be:
\begin{enumerate}
\item open \emph{and} closed, e.g., every point in $X$ with the discrete metric;

\item open \emph{but not} closed,  e.g., an open interval $(a, b)$ in $\mathbb R$
with the Euclidean metric;

\item closed \emph{but not} open,  e.g., a closed interval $[a, b]$ in $\mathbb R$
with the Euclidean metric; or

\item \emph{neither} open nor closed,  e.g., an interval $(a, b]$ in $\mathbb R$
with the Euclidean metric.
\end{enumerate}
In ``most'' spaces, ``most'' sets are neither open nor closed.

\subsection*{Sequences and Open/Closed sets}
In this subsection we want to prove two small results showing how the concepts of open and closed sets interact nicely with convergence of sequences. The first one is a characterisation of convergence in terms of open sets:

\begin{lemma}\label{Lemma:ConvergenceOfSequences}
    Let $(X,d)$ be a metric space. Let $(x_n)_n$ be a sequence in $X$ and $x\in X$. Then $x_n$ converges to $x$ with respect to $d$ if and only if for every open set $U$ containing $x$, there exists an $N\in \mathbb N$ such that $x_n\in U$ for all $n\geq N$.
\end{lemma}
\begin{proof}
    Suppose $x_n\rightarrow x$ and $U$ is an open set containing $x$. Then by definition (of being an open set), there exists an $\varepsilon>0$ such that $U_\varepsilon(x)\subseteq U$. Since $x_n\rightarrow x$, there also exists an $N\in \mathbb N$ such that $d(x_n,x)<\varepsilon$ for all $n\geq N$. But the latter just means that $x_n\in U_\varepsilon (x)\subseteq U$ for all $n\geq N$, which is what we wanted to show.

    \smallskip

    Conversely, suppose for every open set $U$ containing $x$ there exists an $N\in \mathbb N$ such that $x_n\in U$ for all $n\geq N$. We want to show that $x_n\rightarrow x$ with respect to $d$. So let $\varepsilon>0$. Then $U_\varepsilon(x)$ is a particular open set containing $x$. So we can apply our assumption to find an $N\in \mathbb N$ such that $x_n\in U_\varepsilon(x)$ for all $n\geq N$. But writing out what the latter means we get $d(x_n,x)<\varepsilon$ for all $n\geq N$.
\end{proof}

This result suggests, that all we need to know in order to meaningfully talk about convergence in $X$ is the collection of open sets. So once we know what the open sets are that $d$ gives rise to, we can just forget about $d$ and only work with the collection of open sets. This is the idea behind the general notion of a topology, and we will return to it in the second half of the course.

The following criterion gives a relation between closed sets and sequences. In fact, it shows that we can easily check whether or not a set is closed, by considering the convergent sequences it contains. The precise result reads as follows:
\begin{proposition}\label{Prop:A closed iff sequence closed}
    Let $(X,d)$ be a metric space and $A\subseteq X$ a subset. Then the following are equivalent:
    \begin{enumerate}
        \item $A$ is closed in $X$;
        \item whenever $(x_n)_n$ is a sequence in $A$ such that $x_n\rightarrow x$ for some $x\in X$, then $x\in A$.
    \end{enumerate}
\end{proposition}
\noindent Catch phrase: In a metric space, a set is closed if and only if it is \textbf{sequentially closed}.
\begin{proof}
    $(1)\Rightarrow (2)$: Let $(x_n)_n$ be a sequence in $A$ such that $x_n\rightarrow x$ for some $x\in X$. Suppose for contradiction, that $x\in X\setminus A$. Since $A$ is closed, $X\setminus A$ is open. Since $(x_n)_n$ converges to $x$, Lemma \ref{Lemma:ConvergenceOfSequences} implies that there exists an $N\in \mathbb N$ such that $x_n\in X\setminus A$ for all $n\geq N$. But we assumed that $x_n\in A$ for all $n\in \mathbb N$. Contradiction!

    $(2)\Rightarrow (1)$: We will show that $X\setminus A$ is open. Assume for contradiction that it is not. Then there exists a point $x\in X\setminus A$ such that $U_\varepsilon (x)\cap A\neq \emptyset$ for all $\varepsilon>0$.
    In particular, for each $n\in\mathbb N$ we can choose some element $x_n\in U_{1/n}(x)\cap A$. Then $(x_n)_n$ is a sequence in $A$ and $d(x,x_n)<\frac{1}{n}\rightarrow 0$, so $x_n\rightarrow x$. Applying (2) we conclude that $x\in A$ which contradicts our choice of $x$!

\end{proof}



\begin{example}
Let $f:\mathbb R\rightarrow \mathbb R$ be a continuous function. Then the graph of $f$
    $$G_f=\{(x,f(x))\in \mathbb R^2\mid x\in \mathbb R\}$$
is a closed subset of $\mathbb R^2$ with respect to the Euclidean metric.

Indeed, a sequence in $G_f$ is of the form $(x_n,f(x_n))_n$. Suppose now that $(x_n,f(x_n))\rightarrow (x,y)$ for some $(x,y)\in \mathbb R^2$. We have to show that $(x,y)\in G_f$. Since convergence in $\mathbb R^2$ is equivalent to convergence in each entry we must have $x_n\rightarrow x$ and $f(x_n)\rightarrow y$. But $f$ is continuous, so we also have $f(x_n)\rightarrow f(x)$. Finally, by Lemma 2.2 limits of sequences in metric spaces are unique, which allows us to conclude that $y=f(x)$ and hence $(x,y)=(x,f(x))\in G_f$.
\end{example}



\subsection*{Open/Closed sets and set theoretic operations}
We want to investigate how open sets interact with set-theoretic operations like taking unions and intersections. The main important result is the following:

%%%%%%%%%%%%%%%%%%%%
\begin{theorem}\label{Theorem:MetricInducesTopology}
The open sets of a metric space $(X,d)$ have the following properties:
\begin{enumerate}
\item $\emptyset$ and $X$ are open;
  \item arbitrary unions of open sets are open;
  \item finite intersections of open sets are open;
  \end{enumerate}
\end{theorem}
\begin{proof}
\begin{enumerate}
    \item If $E = \emptyset$, there is nothing to check, since there are no points.
On the other hand, if $E = X$, then $E$ contains all balls about all points, so it is obviously open.
\item Suppose that $\{U_\alpha\mid \alpha\in I\}$ is a collection of open sets. We want to show that $\bigcup_{\alpha \in I} U_\alpha$ is again an open set. So let $x\in \bigcup_{\alpha\in I} U_\alpha$.
Then $x\in U_{\alpha_0}$ for at least one $\alpha_0\in I$.
Since $U_{\alpha_0}$ is open, there is a radius $r>0$ such that $U_r(x) \subseteq U_{\alpha_0}$. But then we clearly have $$U_r(x) \subseteq U_{\alpha_0}\subseteq \bigcup_{\alpha\in I} U_\alpha,$$ showing that $\bigcup_{\alpha\in I} U_\alpha$ is open.

\item 
Now suppose that $\{U_1,\dots,U_n\}$ are open. We want to show that $\bigcap_{k=1}^n U_k$ is open again. So let $x\in \bigcap_{k=1}^n U_k$.
Then $x\in U_k$ for all $1\leq k\leq n$, and thus there are radii $r_k>0$ such that the corresponding balls satisfy $U_{r_k}(x) \subseteq U_k$ for all $1\leq k\leq n$.
Let $r := \mathrm{min}\,r_k > 0$.
Then $U_r(x) \subseteq U_{r_k}(x)$ for all $1\leq k\leq n$, and so $$U_r(x)\subseteq \bigcap_k U_{r_k}(x) \subseteq \bigcap_k U_k,$$ showing that $\bigcap_k U_k$ is open.
\end{enumerate}
\end{proof}

%%%%%%%%%%%%%%%%%%%%
\begin{remark}
Note that \textit{infinite} intersections of open sets need not be open. Consider for example the sets $U_{r}(0)$ in $\mathbb R^2$ with respect to the Euclidean metric (i.e. open discs of radius $r$). Each of the sets $U_r(0)$ is open, but $\bigcap_{r>0} U_r(0)=\{0\}$ and one point sets are not open with respect to the Euclidean metric.


In the discrete metric, one point sets, and hence all sets, are open!
We refer to sets which are both open and closed as \textbf{clopen} sets.
\end{remark}

There is a related result for closed sets:

%%%%%%%%%%%%%%%%%%%%
\begin{theorem}
The closed sets of a metric space $(X,d)$ have the following properties:
\begin{enumerate}
\item $\emptyset$ and $X$ are closed;
  \item Finite unions of closed sets are closed;
  \item Arbitrary intersections of closed sets are closed.
  
\end{enumerate}
\end{theorem}

\begin{proof}
The proof is left as an exercise (use the Theorem above and apply de~Morgan's laws).
\end{proof}



%%%%%%%%%%%%%%%%%%%%
%\begin{proposition}
%A subset of a metric space is open if and only if it is a union of open balls.
%\end{proposition}
%\ifsolutions 
%\begin{proof}
%$[\Longrightarrow]$: If $U$ is open then for each $u\in U$ there exists $r_u>0$ such that the open ball $U_{r_u}(u) \subseteq U$.
%It follows that
%\[
%U=\bigcup_{u\in U}U_{r_u}(u),
%\]
%a union of open balls.

%\smallskip

%[$\Longleftarrow$]: Any union of open balls is open by the previous Theorem.
%\end{proof}
%\else \newpage
%\fi 

%%%%%%%%%%%%%%%%%%%%
%\begin{example}
%Consider the metric space $({\Bbb C}^n, d_1)$, where
%\[
%d_1 ({\vec v}, {\vec w}) \; =\;\sum_{j=1}^n |v_j- w_j|,
%%\]
%for $\vec v =(v_1, \dots, v_n), \vec w =(w_1, \dots, w_n) \in {\mathbb C}^n$.
%Then the {\it open ball} in the metric space $({\mathbb C}^n, d_1)$ for ${\vec a} \in {\mathbb C}^n$ and $r>0$ is given by
%\[
%B({\vec a},r)=\{{\vec v} \in {\mathbb C}^n: d_1({\vec a},{\vec v})<r\}
%=\{{\vec v} =(v_1, \dots, v_n) \in {\Bbb C}^n:\; \sum_{j=1}^n  |v_j-a_j| <r\}.
%\]
%\end{example}

%%%%%%%%%%%%%%%%%%%%




%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\subsection*{Closure}
A general subset of a metric space $X$ is 
likely to be neither open nor closed in $X$. However, we can get from an 
arbitrary subset of $X$ to one that is closed in $X$ and also to one that is 
open in $X$, in rather natural ways. We shall explain first how to get from 
a general subset $A\subseteq X$ to a related set, called the closure of $A$ in $X$, 
which is closed in $X$. Intuitively, to get from $A$ to its closure, written $\overline{A}$, 
we add in all points of $X$ which are 'arbitrarily close to $A$'.

\begin{definition}
Suppose that $A$ is a subset of a metric space $(X,d)$, and $x\in X$. We say that $x$ is a \textbf{point of closure of $A$ in $X$} if for all $\varepsilon > 0$
we have $U_\varepsilon (x)\cap  A \neq \emptyset$. The \textbf{closure} of $A$ in $X$, written $\overline{A}$, is the set of all points of closure of $A$ in $X$. 
\end{definition}

\begin{examples}
\begin{enumerate}
    \item The closure of each of the intervals $(0, 1), [0, 1), (0, 1], 
[0, 1]$ in $\mathbb R$ is the interval $[0, 1]$.
\item The closure of $U_1((0, 0))$ in $\mathbb R^2$ is $B_1((0,0))$.
\item If $A$ is a non-empty hounded subset of $\mathbb R$ then $\sup A$ and $\inf A$ are in $\overline{A}$. 
\item {\bf Warning:}
Note that in a metric space $(X,d)$ there may be a difference between the closed ball $B_r(a)$ and the closure $\overline{U_r(a)}$ of the open ball $U_r(a)$.
Both sets are closed but they may not coincide!
\end{enumerate}
\end{examples}

\begin{proposition}
    Let $(X,d)$ be a metric space and let $A,B\subseteq X$ be two subsets. Then the following hold:
    \begin{enumerate}
         \item $\overline{A}$ is closed in $X$,
        \item $A\subseteq \overline{A}$,
        \item $A\subseteq B$ implies $\overline{A}\subseteq\overline{B}$,
        \item $A$ is closed in $X$ if and only if $A=\overline A$,
       
        \item $\overline{\overline{A}}=\overline{A}$,
        \item $\overline{A}$ is the smallest closed set in $X$ containing $A$,
        \item $\overline{A\cup B}=\overline{A}\cup \overline{B}$,
        \item $\overline{A\cap B}\subseteq \overline{A}\cap \overline{B}$, but the converse inclusion is not necessarily true.
    \end{enumerate}
\end{proposition}
\begin{proof}
\begin{enumerate}
\item We will show that $X\setminus \overline{A}$ is open. Suppose $x\in X\setminus \overline{A}$. Then there exists a radius $\varepsilon>0$ such that $U_\varepsilon (x)\cap A=\emptyset$. In other words, $U_\varepsilon (x)\subseteq X\setminus A$. We claim that in fact we must have $U_{\varepsilon/2} (x)\subseteq X\setminus \overline{A}$. Suppose for contradiction that there exists $y\in U_{\varepsilon/2} (x)\cap \overline{A}$. Then, since $y\in \overline{A}$ there exists $z\in U_{\varepsilon/2}(y)\cap A$. Using the triangle inequality it follows that 
$$d(z,x)\leq d(z,y)+d(y,x)=\varepsilon/2 + \varepsilon/2=\varepsilon.$$
It follows that $z\in U_\varepsilon (x)\cap A$, a contradiction, since we know that the latter intersection is empty!

    \item If $x\in A$, then $x\in U_\varepsilon (x)\cap A$ for all $\varepsilon>0$. Hence $x\in \overline{A}$.
    \item Let $x\in \overline{A}$ and $\varepsilon>0$ be given. Then $\emptyset\neq U_\varepsilon(x)\cap A\subseteq U_\varepsilon(x)\cap B$. It follows that the latter set cannot be empty either and thus $x\in \overline{B}$.
    \item Suppose that $A$ is closed in $X$. Since $A\subseteq \overline{A}$ by (2) we only have to show that $\overline{A}\subseteq A$. Suppose for contradiction that this is not the case, i.e. there exists an $x\in \overline{A}$ such that $x\notin A$. Then $x\in X\setminus A$ and since $A$ is closed, the latter set is open. Thus, by definition of being an open set, there exists a radius $\varepsilon >0$ such that $U_\varepsilon(x)\subseteq X\setminus A$. But this contradicts the fact that $x$ is a point of the closure of $A$!

    The converse is an immediate consequence of (1).
    \item Since $\overline{A}$ is closed by (1) this follows directly from (4).
    \item Suppose $C$ is any other closed set in $X$ such that $A\subseteq C$. Then (3) and $(4)$ imply $\overline{A}\subseteq \overline{C}=C$, i.e. the closure of $A$ is smaller than $C$.
    \item The union $\overline{A} \cup \overline{B}$ is a closed set since it is a union of two closed sets by (1).
Since $A \subseteq \overline{A}$ and $B \subseteq \overline{B}$ we get that $A \cup B \subseteq \overline{A} \cup \overline{B}$.
It follows from (3) and (4) that $\overline{A \cup B} \subseteq \overline{A} \cup \overline{B}$.
On the other hand $A \subseteq A \cup B$ hence $\overline{A} \subseteq \overline{A \cup B}$ by (3).
By the same argument we get $\overline{B} \subseteq \overline{A \cup B}$.
Therefore we conclude that $\overline{A} \cup \overline{B} \subseteq \overline{A \cup B}$.
\item Since $A \cap B \subseteq A$ we get $\overline{A\cap B}\subseteq \overline{A}$ by (3). Similarly, we have that $\overline{A \cap B} \subseteq \overline{B}$ and hence $\overline{A\cap B}\subseteq \overline{A}\cap \overline{B}$.
\end{enumerate}
\end{proof}

\section{Maps between metric spaces II}
In week 3 we focussed on isometries and Lipschitz maps. In this section we want to discuss continuous maps in more detail.

\subsection*{More on continuous functions}
Let us start with a couple of examples and non-examples that go beyond the examples from calculus:

\begin{examples}
    \begin{enumerate}
        \item Let $X$ be a set and $d_X$ be the discrete metric. If $(Y,d_Y)$ is any other metric space and $f:X\rightarrow Y$ is any function, then $f$ is continuous.

        To see this fix an arbitrary point $x_0\in X$. We will show that $f$ is continuous at $x_0$. So let $\varepsilon >0$ be given. Let $\delta:=1$. Since $d_X$ is the discrete metric, $d_X(x,x_0)<1$ if and only if $x=x_0$, and in that case $d_Y(f(x),f(x_0))=d_Y(f(x_0),f(x_0))=0<\varepsilon$.
        
        \item Let $\pi:\mathbb R^2\rightarrow \mathbb R$ be the first coordinate projection, i.e. $\pi(x,y)=x$. Then $\pi$ is continuous with respect to the Euclidean metrics on $\mathbb R$ and $\mathbb R^2$ respectively.
       
        \noindent To see this, fix an arbitrary point $(x_0,y_0)\in \mathbb R^2$. Now let $\varepsilon>0$ be given. Then let $\delta:=\varepsilon$. If $d_{\mathbb R^2}((x,y),(x_0,y_0))<\delta$ i.e. $\vert x-x_0\vert ^2+\vert y-y_0\vert^2<\varepsilon^2$, then
        $$d_\mathbb R(\pi(x,y),\pi(x_0,y_0))^2=d_\mathbb R(x,x_0)^2=\vert x-x_0\vert^2 < \varepsilon^2.$$ Taking square roots, we get 
        $$d_\mathbb R(\pi(x,y),\pi(x_0,y_0)) < \varepsilon$$
        as desired.
      
        \item The identity function $\mathrm{id}:(\mathbb R,d_{\vert\cdot \vert})\rightarrow (\mathbb R,d_{\mathrm{disc}})$, $\mathrm{id}(x)=x$ is NOT continuous at any point $x_0\in \mathbb R$.
       To see this consider $\varepsilon=1/2$. For all $\delta>0$, there exists a point $x\in \mathbb R$ such that $x\neq x_0$ and $d_{\vert \cdot \vert}(x,x_0)=\vert x-x_0\vert<\delta$. But then $d_{\mathrm{disc}}(x,x_0)=1> \varepsilon$. So $\mathrm{id}$ is not continuous.
       
    \end{enumerate}
\end{examples}

\begin{proposition}\label{sequential continuity}
     Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces, $x_0\in X$, and let $f:X\to Y$ be a map. Then $f$ is continuous at $x_0$ if and only if for every sequence $(x_n)_{n\in \mathbb N}$ in $X$ converging to $x_0$, the sequence $(f(x_n))_{n\in \mathbb N}$ converges to $f(x_0)$ in $(Y,d_Y)$.
\end{proposition}
\begin{proof}
    Suppose first that $f$ is continuous at $x_0$ and let $(x_n)_n$ be a sequence in $X$ converging to $x_0$. We have to show that $(f(x_n))_n$ converges to $f(x_0)$. So let $\varepsilon >0$ be given. By the definition of continuity of $f$ at $x_0$ we can find a $\delta>0$ such that whenever $d(x,x_0)<\delta$, then $d_Y(f(x),f(x_0))<\varepsilon$. Applying the fact $x_n\to x$ to this $\delta$ we can find $N\in \mathbb N$ such that $d(x_n,x_0)<\delta$ for all $n\geq N$. Combining both of these facts we see that for all $n\geq N$ we have
    $$d_Y(f(x_n),f(x_0))<\varepsilon.$$
    This completes the proof of the forward direction.

    \medskip

    \noindent For the converse, suppose for contradiction that $f$ was not continuous at $x_0$. Then there exists an $\varepsilon >0$ such that for all $\delta>0$ there exists an $x\in X$ such that $d_X(x,x_0)<\delta$ but $d_Y(f(x),f(x_0))\geq \varepsilon$. Apply this to $\delta_n:=1/n$ for all $n\in \mathbb N$: i.e. for each $n\in \mathbb N$ there exists $x_n\in X$ such that $d_X(x_n,x_0)<1/n$ but $d_Y(f(x),f(x_0))\geq \varepsilon$.
    Since $d(x_n,x)<1/n\to 0$ we see that $(x_n)_n$ converges to $x$. By our hypothesis, this implies that $(f(x_n))_n$ converges to $f(x_0)$. But the fact that $d_Y(f(x_n),f(x_0))\geq \varepsilon$ for all $n\in \mathbb N$ contradicts this!
\end{proof}

Next we want to prove some elementary results concerning continuous maps on metric spaces.

\noindent When $f,g:X\to \mathbb R$ are real-valued functions on $X$ we can define associated functions
\begin{align*}
    \vert f\vert:X\to \mathbb R, & \ \vert f\vert (x):=\vert f(x)\vert,\\
    f+g:X\to \mathbb R, & \ (f+g)(x):= f(x)+g(x)\\
    fg:X\to \mathbb R, & \ (fg)(x):=f(x)g(x).
\end{align*}
Also, if $g(x)\neq 0$ for all $x\in X$, then we can define the function
$$1/g:X\to \mathbb R, \ (1/g)(x):=1/g(x).$$

\begin{lemma}
    Suppose that $f,g:X\to \mathbb R$ are continuous functions on a metric space $(X,d)$. Then the functions $\vert f\vert$, $f+g$, and $fg$ are continuous. Moreover, if $g(x)\neq 0$ for all $x\in X$, then $1/g$ is also continuous. 
\end{lemma}
\begin{proof}
    These are really easy to prove using the sequential characterisation of continuity and the algebra of sequences in $\mathbb R$. For example, suppose we want to prove that $f+g$ is continuous. We will use the characterisation from Proposition \ref{sequential continuity}. Let $(x_n)_n$ be a sequence in $X$ converging to $x\in X$. By continuity $(f(x_n))_n$ converges to $f(x)$ and $(g(x_n))_n$ converges to $g(x)$. But then by the algebra of limits in $\mathbb R$ we have that $$(f+g)(x_n)=f(x_n)+g(x_n)\to f(x)+g(x)=(f+g)(x).$$
    Thus we can apply Proposition \ref{sequential continuity} again to obtain the result.
    The other statements follow in the same way.
\end{proof}

We leave the following result as an exercise:
\begin{lemma}
Let $(X,d_X)$, $(Y,d_Y)$ and $(Z,d_Z)$ be three metric spaces and let $f:X\to Y$ and $g:Y\to Z$ be continuous functions. Then $g\circ f:X\to Z$ is continuous. \end{lemma}

We can also use the new terminology from Week 4 to characterise continuity of a function at a point:
\begin{theorem} \label{Theorem:Continuity in Metric spaces}
Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces, $f:X\rightarrow Y$
a function and $x_0\in X$. Then the following are equivalent:
\begin{enumerate}
    \item $f$ is continuous at $x_0$;
    \item for every $\varepsilon>0$ there exists a $\delta>0$ such that
    $$f(U_\delta(x_0))\subseteq U_{\varepsilon}(f(x_0));$$
\end{enumerate}
\end{theorem}
\begin{proof}
 This is just a reformulation. Recall that $x\in U_\delta(x_0)$ precisely when $d(x,x_0)<\delta$ and $f(x)\in U_\varepsilon(f(x_0))$ precisely when $d(f(x),f(x_0))<\varepsilon$.    
\end{proof}

\begin{theorem}\label{theorem:characterisation of continuity}
    Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces and $f:X\rightarrow Y$ be a function. Then the following are equivalent:
    \begin{enumerate}
        \item $f$ is continuous;
        \item for every open set $U\subseteq Y$ the preimage $f^{-1}(U)$ is open in $X$;
        \item for every closed set $A\subseteq Y$ the preimage $f^{-1}(A)$ is closed in $X$ .
    \end{enumerate}
\end{theorem}
\begin{proof} 
(1) $\Rightarrow$ (2): Suppose that $f$ is continuous and let $U\subseteq Y$ be open. We have to show that $f^{-1}(U)$ is open in $X$. So let $x\in f^{-1}(U)$ be given. Then $f(x)\in U$. Since $U$ is open, there exists $\varepsilon >0$ such that $U_\varepsilon(f(x))\subseteq U$. Since $f$ is continuous at $x$, the previous Theorem gives us a $\delta>0$ (corresponding to this $\varepsilon$) such that 
$$f(U_\delta(x)) \subseteq U_\varepsilon(f(x))\subseteq U.$$
It follows that $U_\delta(x)\subseteq f^{-1}(U)$. This concludes the proof that $f^{-1}(U)$ is open in $(X,d_X)$.

\smallskip

(2) $\Rightarrow$ (3): Suppose that $K\subseteq Y$ is closed.
Then $Y \setminus K$ is open. We have that
 $X\setminus f^{-1}(K)=f^{-1}(Y \setminus K)$ which is open by (2).
It follows that $f^{-1}(K)$ is closed.

\smallskip

(3) $\Rightarrow$ (1): Let $x\in X$ be an arbitrary point and let $\varepsilon>0$ be given. Then $U_\varepsilon(f(x))$ is an open set and hence $Y\setminus U_\varepsilon(f(x))$ is closed. Applying (3) to this set we conclude that $f^{-1}(Y\setminus U_\varepsilon(f(x)))=X\setminus f^{-1}(U_\varepsilon(f(x)))$ is closed in $X$. Passing to the complement again we see that $U:=f^{-1}(U_\varepsilon(f(x)))$ is an open set in $X$ containing $x$. Hence, by the definition of being open, there exists some $\delta>0$ such that $U_\delta(x)\subseteq U=f^{-1}(U_\varepsilon(f(x)))$. In other words, $f(U_\delta(x))\subseteq U_\varepsilon(f(x))$. Thus, we have verified the condition for continuity from the previous Theorem.
\end{proof}

\subsection*{Homeomorphisms}

\begin{definition}
    Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces and $f:X\rightarrow Y$ be a function. We say that $f$ is a \textbf{homeomorphism} if $f$ is a continuous bijection and the inverse function $f^{-1}$ is also  continuous. If such a homeomorphism exists, then we say that $X$ and $Y$ are \textbf{homeomorphic}.
\end{definition}

\begin{examples}
    \begin{enumerate}
        \item Consider the function $f:\mathbb R\rightarrow (-1,1)$ given by $f(x)=\frac{x}{\sqrt{1+x^2}}$. Then $f$ is a continuous bijection with inverse $f^{-1}(x)=\frac{x}{\sqrt{1-x^2}}$. The map $f^{-1}$ is clearly continuous as well and hence $f$ is a homeomorphism. Thus we have proved $$\mathbb R\cong (-1,1).$$
        \item If $(a,b)\subseteq \mathbb R$ and $(c,d)\subseteq \mathbb R$ are any two open intervals, then $(a,b)$ and  $(c,d)$ are homeomorphic. To see this it is enough to show that every open interval $(a,b)$ is homeomorphic to $(0,1)$. A homeomorphism $g:(0,1)\rightarrow (a,b)$ is given by $g(t)= (1-t)a+tb$ (Check this!). Composing this with the homeomorphism above gives $\mathbb R\cong (-1,1)\cong (a,b)$ for all real numbers $a<b$;
        \item Similarly, we can show that $\mathbb C$ is homeomorphic to the open unit disc $U_1(0)=\{z\in \mathbb C\mid \vert z\vert<1\}$. Let $f:\mathbb C\rightarrow U_1(0)$ given by $f(z)=\frac{z}{1+\vert z \vert}$, Then $f$ is a homeomorphism with continuous inverse $g(z):=\frac{z}{1-\vert z \vert}$.
        \item We consider the \emph{stereographic projection}. Consider the unit sphere $S^2$ in $\mathbb R^3$. Concretely, $S^2$ is given as the set
        $$S^2:=\{(x,y,z)\in \mathbb R^3\mid x^2+y^2+z^2=1\}.$$
        Note that $(x,y,z)\in S^2$ iff $d_2((x,y,z),(0,0,0))=1$, where $d_2$ is the euclidean metric on $\mathbb R^3$. Let $N:=(0,0,1)$ denote the ``north pole" of the sphere. We claim that $S^2\setminus \{N\}$ (the sphere with the north pole removed) equipped with the induced metric from $d_2$ on $\mathbb R^3$, is homeomorphic to $(\mathbb R^2,d_2)$. Define a map
        $\pi:S^2\setminus\{N\}\to \mathbb R^2$ by $\pi(x,y,z)=(\frac{x}{1-z},\frac{y}{1-z})$. Not that this is well-defined since we removed the only point $(x,y,z)$ on the sphere with $z=1$ is the north pole $N$, which we removed from the domain of $\pi$.

        The map $\pi$ has a nice geometric interpretation: if $(x,y,z)\in S^2\setminus \{N\}$ is given, draw the unique straight line through $(x,y,z)$ and $N$. The image $\pi(x,y,z)$ is then exactly the point where the line intersects with the $z=0$-plane. 
        The map $\pi$ is clearly continuous coordinate-wise and hence it is continuous. Reversing the geometric process above, we see that $\pi$ is in fact bijective. For each point in the $z=0$-plane, we can draw the unique line through that point and $N$. This line will intersect the sphere $S^2$ in exactly one point. This procedure gives a way to find the inverse of $\pi$. Doing some elementary geometry one can then come up with the following formula for the inverse map $\psi:\mathbb R^2\to S^2\setminus\{N\}$: we set $\psi(x,y)=(\frac{2x}{1+x^2+y^2},\frac{2y}{1+x^2+y^2}, \frac{-1+x^2=y^2}{1+x^2+y^2})$. From this formula, it is again clear that $\psi$ is continuous, because it is entry-wise continuous. Moreover, one easily checks by direct computation that
        $$\pi\circ \psi=\mathrm{id}_{\mathbb R^2}\hbox{ and }\psi\circ \pi=\mathrm{id}_{S^2\setminus\{N\}}.$$

        The stereographic projection is applied in cartography, since it allows us to display the surface of the earth (minus a point) as a planar object. It is also applied in geology and crystallography.

        Of course $\pi$ distorts the distances between points on the sphere, but the fact that it is a homeomorphism at least means that $\pi$ preserves the qualitative features of the sphere, and we have a way to (continuously) reverse the process!
    \end{enumerate}
    \end{examples}

%\begin{definition}
%Let $(X,d)$ and $(Y,d)$ be metric spaces and let $f:X \rightarrow Y$ be a map.
%\begin{enumerate}
%    \item $f$ is called \textbf{open} if $f(U)$ is open in $Y$ for all open sets $U\subseteq X$.
%    \item Similarly, $f$ is called \textbf{closed} if whenever $f(A)$ is closed in $Y$ for all closed sets $A\subseteq X$.
%\end{enumerate}
%\end{definition}

%Note that a continuous map need not be open or closed!

%%%%%%%%%%%%%%%%%%%%
%\begin{examples}
%\begin{enumerate}
%    \item Let $\pi_1:\mathbb R^2 \rightarrow \mathbb R$ be the first coordinate projection $\pi_1(x, y) = x$, where $\mathbb R$ and $\mathbb R^2$ are endowed with the Euclidean metric. We have already seen that $\pi_1$ is continuous. We want to see that it is also open, but not closed.
    
%    To see that $\pi_1$ is open, let $U\subseteq \mathbb R^2$ be an open set. We need to show that $\pi_1(U)$ is open in $\mathbb R$. To this end let $x\in \pi_1(U)$ be given. Then there exists $y\in \mathbb R$ such that $(x,y)\in U$. Since $U$ is open, there exists some radius $\varepsilon>0$ such that the open ball of radius $\varepsilon$ centered at $(x,y)$ is contained in $U$, in symbols: $U_\varepsilon(x,y)\subseteq U$. But then for every $x'\in \mathbb R$ such that $\vert x-x'\vert<\varepsilon$ we have $d_2((x,y),(x',y))=\vert x-x'\vert<\varepsilon$ as well, which means that $(x',y)\in U_\varepsilon(x,y)\subseteq U$, i.e. $U_\varepsilon(x)\subseteq \pi_1(U)$.
%    This shows that $\pi_1$ is open. 

%    Finally, to see that $\pi_1$ is not closed consider the set $F=\{(\frac{1}{n},n)\mid n\in \mathbb N\}$. Then $F$ is closed (because $\mathbb R^2\setminus F$ is open) but $\pi_1(F)=\{\frac{1}{n}\mid n\in \mathbb N\rbrace$ is not closed since $\frac{1}{n}\rightarrow 0$ but $0\notin \pi(F)$.
%\item Let $I= [0, 2\pi]$ and $S^1 := \{(x,y) \in \mathbb R^2 : x^2 + y^2 = 1\}$ endowed with the subspace metric of the Euclidean metrics on $\mathbb R$ and $\mathbb R^2$, respectively.
%Consider the function $f:I \rightarrow Y$ given by $f(x) = (\sin(x), \cos(x))$.
%We claim that $f$ is continuous and closed, but not open. 
%To check continuity, we can use the sequential continuity criterion. If $(x_n)_n$ is a sequence in $I$ such that $x_n\rightarrow x\in I$, then we know from real analysis that $\sin$ and $\cos$ are continuous and hence it follows that $\sin(x_n)\rightarrow \sin(x)$ and $\cos(x_n)\rightarrow \cos(x)$. Since convergence in $(\mathbb R^2,d_2)$ is equivalent to entry-wise convergence we conclude that
%$$(\sin(x_n),\cos(x_n))\rightarrow (\sin(x),\cos(x))$$ and hence $f$ is continuous.

%Let us check that $f$ is closed. So let $A\subseteq I$ be a closed subset. We need to check that $f(A)$ is closed in $S^1$. To see this suppose $(y_n)_n$ is a sequence in $f(A)$ such that $y_n\rightarrow y\in S^1$.
%Since $y_n\in f(A)$ there exists $x_n\in A$ such that $f(x_n)=y_n$. Now $x_n\in A\subseteq [0,2\pi]$ for all $n\in \mathbb N$ so $(x_n)_n$ is a bounded sequence. By the Bolzano-Weiterstrass-Theorem, there exists a convergent subsequence $(x_{n_m})_m$, i.e. $x_{n_m}\rightarrow x$ as $m\rightarrow\infty$ for some $x\in [0,2\pi]$. Since $A$ is closed we must actually have $x\in A$. Applying that $f$ is continuous, we get $y_{n_m}=f(x_{n_m})\rightarrow f(x)$. But $y_{n_m}\rightarrow y$ as well and hence $y=f(x)\in f(A)$. 

%Finally, to see that $f$ is not open, consider the set $U=(\pi,2\pi]$. Then $U$ is open in $I$ (since $U=I\cap (\pi,3\pi)$). Then every open ball $U_\varepsilon (1,0)$ about $f(2\pi)=(1,0)$ will contain some element in the upper half circle and hence $U_\varepsilon (1,0)\not\subseteq f(U)$ for all $\varepsilon>0$ and hence $f(U)$ is not open.
%\end{enumerate}
%\end{examples}

%However, we have the following corollary of Theorem \ref{theorem:characterisation of continuity}.

%%%%%%%%%%%%%%%%%%%%
\begin{corollary}
Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces and let $f:X\rightarrow Y$ be a continuous bijection. Then the following are equivalent:
\begin{enumerate}
    \item $f$ is a homeomorphism,
    \item for every open set $U\subseteq X$, its image $f(U)$ is open in $Y$,
    \item for every closed set $A\subseteq X$, its image $f(A)$ is closed in $Y$.
\end{enumerate}
\end{corollary}

\begin{proof}
We prove the implications separately.
\begin{itemize}
    \item[``$(1)\Rightarrow (2)/(3)$"] If $f$ is a homeomorphism, $f^{-1}$ is continuous and so $f(W)=(f^{-1})^{-1}(W)$ for any set $W\subseteq X$. If $W$ was open, continuity of $f^{-1}$ thus implies that $f(W)$ is open. Similarly, if $W$ was closed, continuity of $f^{-1}$ implies that $f(W)$ is closed.
    \item[``$(2)\Rightarrow (1)$"] We need only prove that $f^{-1}$ is continuous (it is a well-defined function since $f$ is a bijection).
The assumption implies that $(f^{-1})^{-1} = f$ takes open sets to open sets.
Therefore $f^{-1}$ is continuous by Theorem \ref{theorem:characterisation of continuity}.
\item[``$(3)\Rightarrow (1)$"]
This works identical to the previous item, just replace \emph{open} by \emph{closed} everywhere.
\end{itemize}
\end{proof}

\section{Connected Spaces}

In this section we want to study two important notions of connectedness of a space. It turns out that if $X$ and $Y$ are homeomorphic metric spaces then $X$ is (path-)connected, if and only if is $Y$ (path-)connected. This a basic instance of a \emph{topological invariant} which can help us tell metric spaces apart in the following way: if we are given two spaces $X$ and $Y$ and we can show that $X$ is (path)-connected and $Y$ is not, then they cannot be homeomorphic to each other.

\begin{definition}
Let $(X,d)$ be a metric space. 
\begin{enumerate}
    \item A subset $A\subseteq X$ is called \textbf{connected}, if whenever $U$ and $V$ are open subsets of $X$ such that $A\subseteq U\cup V$ and $U\cap V\cap A=\emptyset$, then $U\cap A=\emptyset$ or $V\cap A=\emptyset$.
    \item Let $x,y\in X$. A continuous map $\gamma:[0,1]\rightarrow X$ such that $\gamma(0)=x$ and $\gamma(1)=y$ is called a \textbf{path} from $x$ to $y$.
    \item A subset $A\subseteq X$ is called \textbf{path-connected} if for every pair $x,y\in A$ there exists a path $\gamma:[0,1]\rightarrow A$ from $x$ to $y$.
\end{enumerate}
\end{definition}
Slightly more informally speaking, $X$ is connected if $X$ cannot be decomposed into two non-empty disjoint open subsets.

\begin{examples}
\begin{enumerate}
    \item Every interval $I\subseteq \mathbb R$ is path-connected with respect to the Euclidean metric. Indeed, given $x,y\in I$ we can define a path $\gamma:[0,1]\rightarrow I$ from $x$ to $y$ by $\gamma(t):=(1-t)x+ty$. 
    \item If $X$ is a set with at least two elements and $X$ is equipped with the discrete metric, then $X$ is not connected. If we fix $x\in X$, then $U:=X\setminus \{x\}$ and $V:=\{x\}$ are both non-empty open sets satisfying $X=U\cup V$ and $U\cap V=\emptyset$. But the definition says that this cannot happen in a connected space.
\end{enumerate}
\end{examples}

\begin{remark}\label{Remark:Paths} It is useful to keep in mind the following observations about paths in a metric space $X$:
\begin{enumerate}
    \item If $\gamma:[0,1]\rightarrow A$ is a path in $A\subseteq X$ from $x$ to $y$, then there is also a path from $y$ to $x$ given by $\tilde{\gamma}(t):=\gamma(1-t)$. The path $\tilde{\gamma}$ just runs through $\gamma$ backwards.
    \item If $\gamma_1:[0,1]\rightarrow A$ is a path in $A\subseteq X$ from $x$ to $y$ and $\gamma_2:[0,1]\rightarrow A$ is a path in $A$ from $y$ to $z$, then we can build the concatenation $\gamma_1\ast \gamma_2$ of these paths
    $$(\gamma_1\ast \gamma_2)(t)=\left\{\begin{array}{lc}
        \gamma_1(2t) & ,t\in[0,1/2] \\
        \gamma_2(2t-1) & ,t\in [1/2,1] 
    \end{array}\right\}$$
    to obtain a path in $A$ from $x$ to $z$.
\end{enumerate}
\end{remark}

\begin{theorem} \label{Theorem:Basics on connected sets}
Let $(X,d)$ be a metric space. Then the following hold:
\begin{enumerate}
    \item If $A\subseteq X$ is connected and $A\subseteq B\subseteq \overline A$ is another set. Then $B$ is connected. In particular $\overline A$ is connected.
    \item For each $i\in I$ let $A_i\subseteq X$ be a (path-)connected subspace of $X$ such that $\bigcap_{i\in I} A_i\neq \emptyset$. Then $\bigcup_{i\in I} A_i$ is (path-)connected.
    \item If $A_1,\ldots, A_n\subseteq X$ are finitely many (path-)connected subspaces of $X$ such that $A_i\cap A_{i+1}\neq \emptyset$ for each $1\leq i\leq n-1$, then $\bigcup_{n=1}^n A_i$ is connected.
    \item If $f:X\rightarrow Y$ is a continuous map and $A\subseteq X$ is (path)-connected, then $f(A)\subseteq Y$ is (path-)connected.
\end{enumerate}
\end{theorem}
\begin{proof}
    \begin{enumerate}
        \item Let $B$ be as in the statement. Suppose $U$ and $V$ are open sets in $X$ such that $B\subseteq U\cup V$ and $U\cap V\cap B=\emptyset$. Then $A\subseteq B\subseteq U\cup V$ and $U\cap V\cap A\subseteq U\cap V\cap B=\emptyset$ as well. Since $A$ is connected either $A\cap U$ or $A\cap V$ must be empty. Let us assume that $A\cap U=\emptyset$ (the other case works in the same way). Then $A\subseteq X\setminus U$ and since $X\setminus U$ is closed, we have $B\subseteq \overline{A}\subseteq X\setminus U$ as well, which shows that $B\cap U=\emptyset$ as desired.
        \item Let $A$ denote the union $A:=\bigcup_{i\in I} A_i$. We need to show that $A$ is connected. Let $U,V\subseteq X$ be open sets such that $A\subseteq U\cup V$ and $U\cap V\cap A=\emptyset$. By assumption there exists $x\in \bigcap_{i\in I} A_i$. Since $U$ and $V$ cover $A$ we can assume without loss of generality that $x\in U$ (if $x\in V$ we can proceed by the same argument, just interchanging the roles of $U$ and $V$ in everything that follows).
        We claim that then $A\subseteq U$. Since $U\cap V\cap A=\emptyset$ this will imply that $A\cap V=\emptyset$.
        So let $a\in A$. Our goal is to show that $a\in U$. Since $A$ is the union of the sets $A_i$, there exists $j\in I$ such that $a\in A_j$.
        Note that we also have
        $$A_j\subseteq A\subseteq U\cup V \hbox{ and }U\cap V\cap A_j\subseteq U\cap V\cap A=\emptyset$$
        So connectedness of $A_j$ implies that either $A_j\cap U=\emptyset$ or $A_j\cap V=\emptyset$. But we assumed above that $x\in U\cap A_j$, so we must in fact have $A_j\cap V=\emptyset$. But then we must have $a\in A_j\subseteq U$ as desired.
        \item This follows from (2) by induction. 
        \item Let $U$ and $V$ be open subsets in $Y$ such that $f(A)\subseteq U\cup V$ and $U\cap V\cap f(A)=\emptyset$. Since $f$ is continuous, $f^{-1}(U)$ and $f^{-1}(V)$ are open sets in $X$ such that
        $$A\subseteq f^{-1}(U\cup V)=f^{-1}(U)\cup f^{-1}(V)$$ and $$f^{-1}(U)\cap f^{-1}(V)\cap A\subseteq f^{-1}(U)\cap f^{-1}(V)\cap f^{-1}(f(A))= f^{-1}(U\cap V\cap f(A))= \emptyset.$$
        Since $A$ is connected, this implies that either $f^{-1}(U)\cap A=\emptyset$ or $f^{-1}(V)\cap A=\emptyset$. But this implies that either $U\cap f(A)\subseteq f(f^{-1}(U)\cap A)=f(\emptyset)=\emptyset$ or (by the same reasoning) $V\cap f(A)=\emptyset$ as desired. 
    \end{enumerate}

    The corresponding statements about path-connectedness can be proven easily by applying the constructions in Remark \ref{Remark:Paths}.
\end{proof}

Note that we did not forget the ``(path-)" in item (1) above. Indeed, this statement is not correct for path-connectedness in general as the following example shows:
\begin{examples} (Topologist's sine curve)
    Let $A=\{(x,\sin(1/x))\mid x\in (0,1]\}\subseteq \mathbb R^2$ be equipped with the metric induced from the Euclidean metric. 
    Then $A$ is path-connected. Indeed, given any two points $(x,\sin(1/x))$ and $(y,\sin(1/y))$ with $x,y\in (0,1]$ we can define a continuous path in $A$ between the two by $$\gamma(t)=\left((1-t)x+ty,\sin(\frac{1}{(1-t)x+ty})\right).$$


    On the other hand one can show that $A\cup \{(0,0)\}\subseteq \overline{A}$, hence $A\cup \{(0,0)\}$ is connected by Theorem \ref{Theorem:Basics on connected sets}(1), but there is no continuous path in $A\cup \{(0,0)\}$ between $(0,0)$ and $(1,\sin(1))$. 
\end{examples}

\begin{proposition}
Every closed interval $[a,b]$ in $(\mathbb R,d_{\vert\cdot\vert})$ is connected.
\end{proposition}

\begin{proof}
Suppose $U,V$ are open subsets in $[a,b]$ such that 
$U\cap V =\emptyset$ and $[a,b]=U\cup V$.
We may suppose without loss of generality that $a\in U$ (if it is not do the following argument with $V$ instead of $U$). We claim that this already implies $[a,b]\subseteq U$.
First note that $U=[a,b]\setminus V$ and hence $U$ is also closed in $[a,b]$. Consider the set $S:=\{t\in [a,b]\mid [a,t]\subseteq U\}$ and let
$s:=\sup S.$
Since $U$ is closed we have
$$[a,s]\subseteq \overline{\bigcup_{t\in S} [a,t]}\subseteq U.$$
Suppose for contradiction that $s\neq b$. Since $s\in U$ and $U$ is open, there exists a $\varepsilon>0$ such that $[s-\varepsilon,s+\varepsilon]\cap [a,b]\subseteq U$. In particular $[s,s+\varepsilon]\cap [a,b]\subseteq U$. But then $[a,s+\varepsilon]=[a,s]\cup [s,s+\varepsilon]\subseteq U$. This contradicts the definition of $s$!
Hence we conclude that $s=b$ and hence $[a,b]=U$.
\end{proof}

This proof shows that even in seemingly obvious cases it is not trivial to verify the definition of connectedness. For many geometric spaces like circles, spheres, the torus etc it is however rather easy to check that they are path-connected. Hence the following result is very helpful to identify more connected spaces:

\begin{corollary}
    Let $(X,d)$ be a metric space. If $X$ is path-connected, then $X$ is connected.
\end{corollary}
\begin{proof}
Suppose for contradiction that there exist open subsets $\emptyset\neq U,V\subseteq X$ such that $X=U\cup V$ and $U\cap V=\emptyset$. Pick points $x\in U$ and $y\in V$. Since $X$ is path-connected, we can find a continuous path $\gamma:[0,1]\rightarrow X$ such that $\gamma(0)=x$ and $\gamma(1)=y$. But then $\gamma^{-1}(U)$ and $\gamma^{-1}(V)$ are non-empty open subsets of $[0,1]$ such that $\gamma^{-1}(U)\cup\gamma^{-1}(V)=[0,1]$ and $\gamma^{-1}(U)\cap\gamma^{-1}(V)=\emptyset$. This contradicts the fact that $[0,1]$ is connected!
\end{proof}

This implies for example that all intervals, not just the closed ones, are connected, since they are clearly path-connected.
Combining all these results we can now show the following result which sounds obvious, but is not that easy to prove without the methods presented here.
\begin{corollary}
    $(\mathbb R,d_{\vert \cdot\vert})$ and $(\mathbb R^n,d_2)$ for $n>1$ are not homeomorphic 
\end{corollary}
\begin{proof}
     Suppose for contradiction that there exists a homeomorphism $f:\mathbb R^n\rightarrow \mathbb R$. Let $x_0:=f(0)\in \mathbb R$. Since $f$ is a bijection we have $f(\mathbb R^n\setminus \{0\})=\mathbb R\setminus \{x_0\}$. Note that $\mathbb R^n\setminus \{0\}$ is easily seen to be path-connected (draw a picture) and hence connected. Thus, $f(\mathbb R^n\setminus \{0\})=\mathbb R\setminus \{x_0\}$ should be connected as well by Theorem \ref{Theorem:Basics on connected sets}(4), but it is not (take $U=(-\infty,x_0)$ and $V=(x_0,\infty)$ to obtain a partition of $\mathbb R\setminus\{x_0\}$ into open sets). Contradiction!
\end{proof}

We will use similar ideas on the exercise sheet to distinguish some more spaces!

%%%%%%%%%%%%%%%%%%%%
\begin{definition}
Let $(X,d)$ be a non-empty metric space.
A \textbf{connected component} of a metric space $X$ is a connected subset $C$ of $X$ with the property that if $A\subseteq X$ is another connected subset of $X$ with $C\subseteq A$, then $A=C$.
A space in which all of the connected components are singleton sets is said to be \textbf{totally disconnected}.
\end{definition}
A connected component is a maximal (with respect to $\subseteq$) connected subspace of $X$.

\begin{lemma} Let $(X,d)$ be a metric space. Then the following hold:
\begin{enumerate}
    \item The connected components of $X$ form a partition of $X$: they are pairwise disjoint, non-empty and their union is the whole space.
    \item If $C\subseteq X$ is a connected component, then $C$ is closed.
    \item If the number of connected components of $X$ is finite, then every connected component $C\subseteq X$ is also open.
\end{enumerate}
\end{lemma}
\begin{proof}
    \begin{enumerate}
        \item Let $C_1$ and $C_2$ be two connected components of $X$. Suppose that there exists an element $x\in C_1\cap C_2$. Then by \ref{Theorem:Basics on connected sets} their union $C_1\cup C_2$ is also connected. But $C_i\subseteq C_1\cup C_2$ for $i=1,2$ and hence the maximality of $C_1$ and $C_2$ forces $C_1=C_1\cup C_2=C_2$. This shows that distinct components are disjoint. It is also clear that every $x\in X$ is contained in some connected component.
        \item Suppose $C$ is a connected component. Then $C\subseteq \overline{C}$ and by \ref{Theorem:Basics on connected sets} we have that $\overline{C}$ must be connected as well. Maximality of $C$ then implies $C=\overline{C}$ which is to say that $C$ is closed.
        \item By (1) we can partition $X$ as $X=C_1\sqcup \ldots \sqcup C_n$ where the $C_i$ are the connected components of $X$. Fix $i\in \{1,\ldots, n\}$. Since each $C_j$ is closed, the finite union $\bigcup_{j\neq i} C_j$ is closed as well and hence $C_i=X\setminus \bigcup_{j\neq i} C_j$ is open.
    \end{enumerate}
\end{proof}
%%%%%%%%%%%%%%%%%%%%
\begin{example}
If $X$ has the discrete metric, then every set is open.
Hence the largest connected set containing a point $x$ is $\{x\}$. It follows that $X$ is totally disconnected.
\end{example}

%%%%%%%%%%%%%%%%%%%%
\begin{example}
Consider $\mathbb Q \subseteq \mathbb R$ with the usual metric.
Note that $\mathbb Q$ is \emph{not} connected.
For instance, $U = (-\infty,\sqrt{2})\cap \mathbb Q$ and $V = (\sqrt{2}, \infty)\cap \mathbb Q$ are two disjoint open subsets of $\mathbb Q$ such that $\mathbb Q=U\cup V$.
Since any two rational numbers have an irrational number between them, one can repeat the argument above to see that any two rational numbers must lie in separate connected components of $\mathbb Q$.
Hence the connected components of $\mathbb Q$ are singleton sets, i.e. $(\mathbb Q,d_{\vert\cdot\vert})$ is totally disconnected. This gives an example of a totally disconnected space which does not have the discrete metric.
\end{example}


\subsection{The Cantor Set}
The Cantor set is an important example that appears in many areas of pure mathematics providing interesting examples and counterexamples. 
We construct the Cantor Set inductively as a subset of the unit interval $[0,1]$. 
Let $C_0 := [0,1]$.
To obtain $C_1$ from $C_0$, remove the open middle third of $C_0$ so that 
\[
C_1 := [0,1/3] \sqcup [2/3,1]
\]
For $C_2$, remove the open middle thirds of the  two intervals constituting $C_1$, i.e. 
\[
C_2 := [0, 1/9] \sqcup [2/9, 3/9] \sqcup [6/9, 7/9] \sqcup [8/9, 1]
\]
Repeat this process to obtain
\[
C_3:=[0, \frac{1}{27}] \sqcup [\frac{2}{27}, \frac{3}{27}] \sqcup [\frac{6}{27},\frac{7}{27}] \sqcup [\frac{8}{27},\frac{9}{27}] \sqcup [\frac{18}{27},\frac{19}{27}] \sqcup [\frac{20}{27},\frac{21}{27}] \sqcup [\frac{24}{27},\frac{25}{27}] \sqcup [\frac{26}{27},1]
\]
and so on. 
The first three steps can be seen in the following diagram.

\vspace{.5cm}

\begin{center}
\begin{minipage}{\textwidth}
\centering
\xymatrix{
{0} \ar@{|-|}[rrrrrrrrr]& & &  & & & & & & {1}
\\
{0} \ar@{|-|}[rrr] & & & \frac{1}{3} & & & \frac{2}{3} \ar@{|-|}[rrr] & & & {1}
\\
{0}\ar@{|-|}[r] & \frac{1}{9} & \frac{2}{9} \ar@{|-|}[r] & \frac{3}{9} & & & \frac{6}{9} \ar@{|-|}[r] & \frac{7}{9}& \frac{8}{9} \ar@{|-|}[r]& {1}
}

\end{minipage}
\end{center}

\vspace{.5cm}

\textbf{Cantor's set} is then defined as $C := \bigcap_{n \in \mathbb N} C_n$.
From the construction it is clear that $0,1\in C$ so it is non-empty. We equip $C$ with the metric it inherits from the Euclidean metric on $[0,1]$.

\begin{lemma}
    Let $C$ be the Cantor set as defined above. Then the following hold:
    \begin{enumerate}
\item $C$ does not contain any open subset of $([0,1],d_{\vert\cdot\vert})$,
\item $C$ is totally disconnected.
    \end{enumerate}
\end{lemma}
\begin{proof}
    \begin{enumerate}
\item Fix $\varepsilon > 0$ and choose $n$ such that $3^{-n} < \varepsilon$. 
Then $C_n$ is the disjoint union of intervals of length equal to $3^{-n}$ and it cannot contain an open interval of radius bigger than $\varepsilon$. 
Since $C \subset C_n$ the same applies for $C$.
As $\varepsilon$ is arbitrary we cannot find an open interval in $C$.
So $C$ contains no open sets. 
\item We show that any two distinct points $x,y\in C$ lie in separate connected components. Given distinct points $x,y\in C$ the Archimedean property implies that there exists an $n\in \mathbb N$ such that $3^{-n}<\vert x-y\vert$, and as $x,y\in C_n$ it follows that they belong to different closed intervals making up $C_n$. Let $I$ be the closed interval in $C_n$ containing $x$. It follows that $x\in C\cap I$ and $y\in C\setminus I$, and these sets are separated.
    \end{enumerate}
\end{proof}

\section{Compact Metric spaces I}
Compactness is a finiteness property for metric spaces.
To motivate this concept let us first consider a finite set $X$ (we do not view $X$ as a metric space, just as a set).
Finite sets have a number of nice properties, that distinguish them from infinite sets. For example, when $X$ is a finite set, then
\begin{itemize}
    \item every function $f:X\rightarrow \mathbb R$ is bounded, meaning that there exists a constant $M>0$ such that $\vert f(x)\vert\leq M$ for all $x\in X$;
    \item every function $f:X\rightarrow \mathbb R$ attains its maximum, meaning that there exists an $x_0\in X$ such that $f(x_0)\geq f(x)$ for all $x\in X$;
    \item every sequence $(x_n)_n$ in $X$ has a constant sub-sequence.
\end{itemize}
All of these properties are not terribly hard to prove when $X$ is finite, but they will become false, when $X$ is an infinite set like the natural numbers $\mathbb N$.

\smallskip

Now we want to turn to metric spaces. Most interesting metric spaces are infinite as sets, but some of them still exhibit properties similar to those of finite sets. From calculus you may remember that a
\emph{continuous} function $f:[0,1]\rightarrow \mathbb R$ is bounded and attains its maximum. So despite $[0,1]$ being infinite, once we require our function to be continuous, it does somehow behave very similar to a function defined on a finite set. 
There is also an analogue of the third item in the list above: The Bolzano-Weierstraß theorem says that every sequence in $[0,1]$ has a \emph{convergent} sub-sequence. 

\smallskip

We will see that the reason for all this is that $[0,1]$ is an example of a \emph{compact space} and hence `small' in some sense. 
The rough idea is that spaces which are ‘infinitely large’ such as $\mathbb R$ or $[0,\infty)$ are not compact. However, we want compactness to depend just on the open sets of the space, so it will have to be defined purely in terms of open sets. This means that
any space homeomorphic to a non-compact space will also be non-compact. In particular compactness does \emph{not} say that the rigid size (like the length, or area) will be small. For example the intervals $(0, 1)$ and $[0, 1)$ will also be non-compact (despite being subsets of the compact set $[0,1]$), since they are homeomorphic to $\mathbb R$ and $[0,\infty)$ respectively.

So how can this idea be expressed just in terms of open sets rather than in some numerical measure of size? This would seem to be difficult since open sets themselves can be large or small. But large open sets can be expressed as unions of small open
sets, so the idea is to count how many small open sets are needed
when a large open set in a space X, such as the whole space $X$ itself, is expressed as a union of small open sets. The most basic question in this situation is whether the
number of small open sets needed is finite or infinite. For example, if $X$ is a metric
space, then $X$ is the union of all its balls $U_r(x)$ of fixed radius $r>0$, so we could
ask whether $X$ is in fact the union of a \emph{finite} collection of these balls $U_r(x)$ of fixed
radius. This is still not quite general enough: we need to replace balls by arbitrary open sets, and this leads to the following general definition:

\begin{definition}
Let $(X,d)$ be a metric space and $K\subseteq X$ a subset.
\begin{enumerate}
    \item An \textbf{open cover} of $K$ in  $X$ is a collection of open subsets $\mathcal{U}$ such that $K\subseteq \bigcup_{U\in \mathcal{U}} U$;
    \item if $\mathcal{V}\subseteq \mathcal{U}$ such that $\mathcal{V}$ is still a cover of $K$, then we call $\mathcal{V}$ a \textbf{subcover} of $\mathcal{U}$;
    \item we say that $K$ is \textbf{compact} if every open cover $\mathcal{U}$ of $K$ admits a finite subcover, i.e. there exists a finite subset $\mathcal{V}\subseteq \mathcal{U}$ such that $K\subseteq \bigcup_{U\in \mathcal{V}} U$.
\end{enumerate}
\end{definition}

\begin{examples}
\begin{enumerate}
    \item $\mathbb R$ itself with the Euclidean metric is not compact. Take for example the collection of open intervals $\{(-n,n)\mid n\in \mathbb N\}$. This is an open cover of $\mathbb R$ since $\mathbb R=\bigcup_{n\in\mathbb N} (-n,n)$, but it does not admit a finite subcover since we really need all the intervals $(-n,n)$ to cover $\mathbb R$.
    \item In the same spirit we can show that $(0,1)$ is not compact: Consider the collection of open intervals $\{(\frac{1}{n},1)\mid n\in \mathbb N\}$. Again we have $(0,1)=\bigcup_{n\in\mathbb N} (\frac{1}{n},1)$ so we do indeed have an open cover. But no finite sub-collection of  $\{(\frac{1}{n},1)\mid n\in \mathbb N\}$ will be sufficient to cover all of $(0,1)$: we would always miss a tiny bit near zero.
    \item Let $(X,d)$ be any metric space, and let $F\subseteq X$ be a finite subset. Then $F$ is compact.
    To see this, write $F=\{x_1,\ldots, x_n\}$ and let $\mathcal{U}$ be an open cover of $F$. This means that for each $x_i\in F$ there exists an $U_i\in \mathcal{U}$ such that $x_i\in U_i$. But then $\{U_i\mid 1\leq i\leq n\}$ is a finite subcover of $\mathcal{U}$. Hence $F$ is compact.
    \item If $X$ is equipped with the discrete metric then the converse is true, i.e. compact sets are finite.

    To see this let $K$ be a compact subset of the discrete space $X$. Then $K=\bigcup_{x\in K} \{x\}$ and since singleton sets are open with respect to the discrete metric this means that $(\{x\})_{x\in K}$ is an open cover of $K$. Since $K$ is compact, there must exist a finite subcover $\{x_1\},\ldots, \{x_n\}$ of this cover. This means that $K\subseteq \bigcup_{i=1}^n \{x_i\}=\{x_1,\ldots, x_n\}$ and hence $K$ must be finite.
\end{enumerate}
\end{examples}

%\textbf{Warning:} A common mistake is to think that compactness means that there exists a finite cover. But this is wrong! In fact every space admits \emph{some} finite cover (e.g. just take $X$ itself). The point is, that \textbf{every} cover should admit a finite subcover.
%\smallskip

Showing that a given space is compact from the definition is not always easy. Hence we want to develop some theory to identify a lot more examples of compact spaces. Let us start with the following result:
\begin{proposition}\label{Prop:Unit interval is compact}
The closed interval $[0,1]\subseteq \mathbb R$ is compact with respect to the Euclidean metric.
\end{proposition}

\begin{proof}
Let $\mathcal U$ be an open cover of $[0,1]$.
Consider the set
$$C:=\{c\in [0,1]\mid [0,c] \hbox{ is covered by finitely many elements in }\mathcal{U}\}.$$
$C$ is bounded, and hence it has a least upper bound $c_0:=\sup C$.

We first claim that $c_0 > 0$. Since $0\in [0,1]$ and $\mathcal{U}$ covers $[0,1]$, there exists $V_0\in \mathcal{U}$ such that $0\in V_0$. Using that $V_0$ is open, there exists $\varepsilon>0$ such that $(-\varepsilon,\varepsilon)\subseteq V_0$. In particular, $[0,\varepsilon/2] \subseteq V_0\in \mathcal{U}$. Thus, $c:=\varepsilon/2\in C$ and $c>0$. Thus $c_0\geq c>0$ as well.

\smallskip

Next, we claim that $c_0\in C$. Since $c_0\in [0,1]$ there exists $V$ such that $(c_0-\varepsilon,c_0+\varepsilon)\subseteq V$. Since $c_0-\varepsilon/2\in C$ there exist $V_1,\ldots, V_n\in \mathcal{U}$ covering $[0,c_0-\varepsilon/2]$. But then $\{V_1,\ldots, V_n,V\}\subseteq \mathcal{U}$ covers $[0,c_0]$. Thus, $c_0\in C$ as desired.

\smallskip

Finally, we claim that $c_0=1$. Suppose for contradiction that $c_0 < 1$. Since $\mathcal{U}$ is a cover, there exists an open set $U\in \mathcal{U}$ such that $c_0\in U$. Using that $U$ is open, there exists $\varepsilon>0$ such that $[c_0-\varepsilon,c_0+\varepsilon]\subseteq U\cap (0,1)$. But by our choice of $c_0$, $[0,c_0-\varepsilon]$ has a finite subcover, i.e. there exist $U_1,\ldots, U_n\in \mathcal{U}$ such that $[0,c_0-\varepsilon]\subseteq U_1\cup\ldots\cup U_n$. But then $[0,c_0+\varepsilon]$ also has a finite subcover, namely $\{U_1,\ldots, U_n,U\}$. This contradicts the definition of $c_0$. Hence it must be the case that $c_0 = 1$, and so $[0,1]$ is compact.
\end{proof}

We now want to learn a couple of important facts about compact spaces. First, we will see that compactness of $K\subseteq X$ only depends on the metric of $K$ and not on the ambient space $X$ that we choose.
\begin{lemma}
    Let $(X,d)$ be a metric space and $K\subseteq X$. Then $K$ is compact in $X$ as defined above if and only if $K$ is compact (viewed as a subset of itself) with respect to the induced metric on $K$.
\end{lemma}
\begin{proof}
   Suppose first that $K$ is compact as a subset of $X$. We want to show that $K$ is compact in $(K,d_K)$. So let $\mathcal{U}$ be a collection of open sets in $K$ such that $K= \bigcup_{U\in \mathcal{U}} U$.
   Using the fact that every open set in the induced metric is an intersection of an open set in $X$ with $K$, there exists open sets $V_U$ in $X$ such that $U=V_U\cap X$ for every $U\in \mathcal{U}$. But then $K=\bigcup_{U\in \mathcal{U}} U\subseteq \bigcup_{U\in \mathcal{U}} V_U$, so $\{V_U\mid U\in \mathcal{U}\}$ is an open cover of $K$ in $X$. Since $K$ is compact, this cover admits a finite subcover, i.e. there exists a finite subset $\mathcal{V}\subseteq \{V_U\mid U\in \mathcal{U}\}$ such that $K\subseteq \bigcup_{V\in \mathcal{V}} V$. Write $\mathcal{V}=\{V_{U_1},\ldots, V_{U_n}\}$. Then also $K\subseteq (\bigcup_{i\in F} V_i)\cap K=\bigcup_{i\in F} (V_i\cap K)=\bigcup_{i\in F} U_i$.
    So $\{U_i\mid i\in F\}$ is a finite subcover of our original cover.

    \smallskip

    Conversely, suppose that $K$ is compact in $(K,\tau_K)$. Let $\{U_i\mid i\in I\}$ be a collection of open sets in $X$ such that $K\subseteq \bigcup_{i\in I} U_i$. Then $V_i:=K\cap U_i$ is open in $K$ for every $i\in I$ and $K\subseteq  (\bigcup_{i\in I} U_i)\cap K=\bigcup_{i\in I} V_i$. Since $K$ is compact (as a subset of itself) there exists a finite set $F\subseteq I$ such that $K\subseteq \bigcup_{i\in F} V_i$. But
    since $V_i\subseteq U_i$ for all $i\in F$ we get that $K\subseteq \bigcup_{i\in F} U_i$, so $\{U_i\mid i\in F\}$ is a finite subcover of our original cover, which concludes the proof.    
\end{proof}

We now list some basic results regarding compactness.

%%%%%%%%%%%%%%%%%%%%
\begin{theorem}\label{Theorem:Properties of compact spaces} Let $(X,d)$ be a metric space and $E\subseteq X$. Then the following hold:
\begin{enumerate}
    \item If $X$ is compact and $E$ is closed in $X$, then $E$ is compact;
    \item if $E$ is compact, then $E$ is closed;
    \item if $f:X\rightarrow Y$ is a continuous map and $K\subseteq X$ is compact, then $f(K)\subseteq Y$ is compact;
    \item if $E_1,\ldots, E_n\subseteq X$ are finitely many compact sets, then their union $E=E_1\cup\ldots \cup E_n$ is also compact. (warning: this does not hold in general for infinite unions!)
\end{enumerate}
\end{theorem}
\begin{proof}
For (1) let $X$ be a compact space and $E$ a subspace.
Let $\mathcal{U}$ be an open cover of $E$.
Since $E$ is closed, its complement $X \setminus E$ is open, so that $\mathcal{U} \cup \{X \setminus E\}$ is an open cover of $X$.
By compactness, this has a finite subcover $\{U_0,U_1,\dots,U_n\}$, where we can take $U_0 = X \setminus E$ and the rest of the sets from $\mathcal{U}$.
Since $U_0\cap E = \emptyset$ then $\{U_1,\dots,U_n\}$ is a finite subcover of $\mathcal{U}$ covering $E$.
Hence $E$ is compact.

\medskip

For (2) let $E$ be a compact subset of $X$.
For $x\notin E$ and for each $y\in E$, there are open subsets which we call $U_y$ and $V_y$ containing $x$ and $y$, respectively, such that $U_y\cap V_y = \emptyset$.
Then $\{V_y\}_{y \in E}$ is an open cover of $E$, and so has a finite subcover $\{V_{y_1},\dots, V_{y_n}\}$.
Since this collection is finite, the intersection of the corresponding sets containing $x$ then $W_x := \bigcap_j U_{y_j}$ is a finite intersection of open sets, and so is open.
Furthermore, since $W_x\cap V_{y_j} = \emptyset$ for all $j$, it follows that $W_x\cap E = \emptyset$.
Furthermore we have that $X \setminus E = \bigcup_{x\notin E} W_x$, being the union of open sets, is open.
Hence $E$ is closed.

\medskip

For (3) let $f \colon X\rightarrow Y$ be continuous, and let $\mathcal{V}$ be an open cover of $f(X)$.
By continuity, $f^{-1}(V)$ is open in $X$ for all $V\in \mathcal{V}$, and so $ \{f^{-1}(V)\mid V\in \mathcal{V}\}$ is an open cover of $X$.
By compactness, $ \{f^{-1}(V)\mid V\in \mathcal{V}\}$ has a finite subcover, i.e. there exists a finite set $\mathcal{F}\subseteq \mathcal{V}$ such that $\{f^{-1}(V)\mid V\in \mathcal{F}\}$ covers $X$.
The corresponding sets $\{V\mid V\in \mathcal F\}$ then cover $f(X)$, so we have found our subcover of $\mathcal{V}$. Since $\mathcal{V}$ was an arbitrary cover, $f(X)$ is compact.

\medskip

To prove (4) let $\{U_i\mid i\in I\}$ be an open cover of $E=E_1\cup\ldots \cup E_n$. Then $\{U_i\mid i\in I\}$ is also an open cover for each $E_j$ individually. Hence for each $1\leq j\leq n$ there exists a finite set $F_j\subseteq I$ such that $\{U_i\mid i\in F_j\}$ covers $E_j$. Set $F:=F_1\cup\ldots \cup F_n$. Then $F$ is still a finite subset of $I$ and $\{U_i\mid i\in F\}$ covers $E$. Hence this is the finite subcover we were looking for.

\end{proof}



\begin{example}
\begin{enumerate}
\item The Cantor set $C\subseteq [0,1]$ is compact. Indeed, we defined $C$ as $C=\bigcap_{n\in \mathbb N} C_n$. Since each $C_n$ is a finite union of closed intervals, $C_n$ is closed in $[0,1]$. Hence $C=\bigcap_{n\in \mathbb N} C_n$ is closed in $[0,1]$ and hence compact by Theorem \ref{Theorem:Properties of compact spaces}(1).
    \item Since the interval $[a,b]$ is the image of $[0,1]$ under the continuous map $f(x) = (b-a)x + a$, Theorem \ref{Theorem:Properties of compact spaces}(3) implies that $[a,b]$ is compact for $-\infty < a \leq b < \infty$.    
    \item  Let $S^1$ be the unit circle in $\mathbb C$. With respect to the usual metrics on $S^1$ and $[0,1]$ we have a continuous surjective map $f:[0,1]\rightarrow S^1$ given by $f(t)=\exp(2\pi i t)$. Thus, Theorem \ref{Theorem:Properties of compact spaces}(3) implies that $S^1=f([0,1])$ is compact.
\end{enumerate}
    
\end{example}

These results have a number of important applications:

%%%%%%%%%%%%%%%%%%%%
\begin{corollary} Let $(X,d)$ be a compact metric space. Then the following hold:
\begin{enumerate}
    \item If $Y$ is homeomorphic to $X$, then $Y$ is compact (that is, compactness is a topological property).
%    \item If $\sim$ is an equivalence relation on $X$, then the quotient space $X/{\sim}$ is compact.
    \item If $Y$ is another metric space and $f \colon X\to Y$ is a continuous bijection, then $f$ is a homeomorphism.
\end{enumerate}
\end{corollary}
\begin{proof} For $(1)$ note that if $X$ and $Y$ are homeomorphic, then there exists a continuous and bijection $f:X\rightarrow Y$. Hence $Y=f(X)$ is the continuous image of the compact space $X$, and hence compact as well.

\smallskip

%For part (2) just apply Theorem \ref{Theorem:Properties of compact spaces}(3) to the canonical quotient map $X\rightarrow X/{\sim}$.

%\smallskip

Finally, for (2) it suffices to show that $f$ is a closed map.
Let $C\subseteq X$ be an arbitrary closed subset of $X$.
Then $C$ is compact and so $f(C)$ is compact in $Y$ by Theorem 6.5(3). Finally, Theorem 6.5(2) implies that $f(C)$ is closed, which is what we wanted to show.
\end{proof}

\section{Compact Metric Spaces II}
We continue our discussion of compactness. Let us recall the definition and some of the basic results we proved last week:

\begin{definition}
Let $(X,d)$ be a metric space and $K\subseteq X$ a subset.
\begin{enumerate}
    \item An \textbf{open cover} of $K$ in  $X$ is a collection of open subsets $\mathcal{U}$ such that $K\subseteq \bigcup_{U\in \mathcal{U}} U$;
    \item if $\mathcal{V}\subseteq \mathcal{U}$ such that $\mathcal{V}$ is still a cover of $K$, then we call $\mathcal{V}$ a \textbf{subcover} of $\mathcal{U}$;
    \item we say that $K$ is \textbf{compact} if every open cover $\mathcal{U}$ of $K$ admits a finite subcover, i.e. there exists a finite subset $\mathcal{V}\subseteq \mathcal{U}$ such that $K\subseteq \bigcup_{U\in \mathcal{V}} U$.
\end{enumerate}
\end{definition}

The following is a list of facts we proved last week. They are copied in here again for ease of reference. We always consider a set $X$ with a fixed metric $d$.
\begin{enumerate}
    \item If $X$ is a compact metric space and $E$ is closed in $X$, then $E$ is compact;
    \item if $E\subseteq X$ is compact, then $E$ is closed in $X$;
    \item if $E_1,\ldots, E_n\subseteq X$ are finitely many compact sets, then their union $E=E_1\cup\ldots \cup E_n$ is also compact. (warning: this does not hold in general for infinite unions!)
     \item if $f:X\rightarrow Y$ is a continuous map between two metric spaces and $K\subseteq X$ is compact, then $f(K)\subseteq Y$ is compact;
     \item if $X$ and $Y$ are homeomorphic metric spaces, then $X$ is compact if and only if $Y$ is compact;
    \item every closed interval $[a,b]\subseteq \mathbb R$ is compact with respect to the Euclidean metric.
\end{enumerate}

In this section we want to prove a couple of important theorems regarding compact metric spaces.


\subsection{Compactness of products}
Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces and let $X\times Y=\{(x,y)\mid x\in X, y\in Y\}$ be their Cartesian product. We can define a metric on $X\times Y$ by the formula
$$d_\infty((x,y),(x',y'))=\max\{d_X(x,x'),d_Y(y,y')\}.$$ 
Note, that an open ball $U_r^{d_\infty}(x,y)$ in $(X\times Y, d_\infty)$ looks like $$U_r^{d_\infty}(x,y)=U^{d_X}_r(x)\times U^{d_Y}_r(y).$$

We have already looked at the particular example $(X,d_X)=(Y,d_Y)=(\mathbb R,d_{\vert\cdot\vert})$ before. 
\begin{theorem}\label{thm: products of compact spaces}
    Let $(X,d_X)$ and $(Y,d_Y)$ be two metric spaces and let $X\times Y$ have the metric $d_\infty$ defined above. Then we have
$$(X\times Y,d_\infty) \hbox{ is compact }\Leftrightarrow (X,d_X)\hbox{ and }(Y,d_Y)\hbox{ are both compact}.$$
\end{theorem}
\begin{proof}
    The statement is an equivalence, so we have to prove two directions. 
\begin{itemize}
    \item[``$\Rightarrow$"] Consider the projection maps $\pi_X:X\times Y\to  X$ and $\pi_Y:X\times Y\to Y$. It is easy to see that $\pi_X$ and $\pi_Y$ are both continuous maps. Since $\pi_X(X\times Y)=X$ and $\pi_Y(X\times Y)=Y$, the claim follows from (iv).
    \item[``$\Leftarrow$"] This direction is much trickier to prove. Let $\mathcal{W}$ be an arbitrary open cover of $X\times Y$. We will call a subset $A\subseteq X$ \emph{good} (for $\mathcal{W}$) if $A\times Y$ can be covered by a finite subcollection of $\mathcal{W}$. Thus, rephrasing our goal in this language, we want to show that $X$ is good. We shall need two intermediate claims to complete the proof:
    \begin{enumerate}
        \item[\underline{Claim 1:}] If $A_1,\ldots, A_n\subseteq K$ are all good, then $A_1\cup\ldots\cup A_n$ is also good.
        \begin{proof}[Proof of Claim 1.]
            The proof is almost identical with the proof of (iii) above, which we did last week. So we will leave it as an exercise.
        \end{proof}
        \item[\underline{Claim 2:}] For every $x\in X$ there exists an open set $U_x\subseteq X$ such that $x\in U_x$ and $U_x$ is good. 
        \begin{proof}[Proof of Claim 2.]
            Fix $x\in X$. For each $y\in Y$ there exists a set $W_y\in \mathcal{W}$ such that $(x,y)\in W_y$, since $\mathcal{W}$ covers $X\times Y$. Since $W_y$ is open in $X\times Y$, there exists a radius $r_y>0$ such that 
            $$U^{d_X}_{r_y}(x)\times U^{d_Y}_{r_y}(y)=U_{r_y}^{d_\infty}(x,y)\subseteq W_y.$$
            Then the family $\{U^{d_Y}_{r_y}(y)\mid y\in Y\}$ is an open cover of $Y$. By compactness of $Y$, we can find a finite subcover, say $\{U^{d_Y}_{r_{y_1}}(y_1),\ldots,U^{d_Y}_{r_{y_m}}(y_m)\}$.
            Define
            $$U_x:=U^{d_X}_{r_{y_1}}(x)\cap \ldots \cap U^{d_X}_{r_{y_m}}(x).$$
            For each $i=1,\ldots, m$ we have
            $$U_x\times U^{d_Y}_{r_{y_i}}(y_i)\subseteq U^{d_X}_{r_{y_i}}(x)\times U^{d_Y}_{r_{y_i}}(y_i)=U_{r_{y_i}}^{d_\infty}(x,y_i)\subseteq W_{y_i},$$
            and hence
            $$U_x\times Y=U_x\times \left(\bigcup_{i=1}^m U^{d_Y}_{r_{y_i}}(y_i)\right)= \bigcup_{i=1}^m \left(U_x \times U^{d_Y}_{r_{y_i}}(y_i)\right) \subseteq \bigcup_{i=1}^m W_{y_i}.$$
            This shows that $U_x$ is good. Moreover, $x\in U_x$ and as a finite intersection of open sets, $U_x$ is open. 
        \end{proof}
        
    \end{enumerate}
    We can now complete the proof that $X$ is good: for each $x\in X$ let $U_x$ be a good open set as provided by Step 2. Since $x\in U_x$ for all $x\in X$, the family $\{U_x\mid x\in X\}$ is an open cover of $X$. So by compactness of $X$ there is a finite subcover, say $\{U_{x_1},\ldots, U_{x_n}\}$. But this means that
        $X=U_{x_1}\cup\ldots\cup U_{x_n}$ is a finite union of good sets, i.e. it is good itself by Step 1. This is what we wanted to show.
\end{itemize}
\end{proof}

Applying the product theorem above in conjunction with the fact that $[a,b]$ is compact with respect to the Euclidean metric $d_{\vert\cdot\vert}$, we conclude that the square $[a,b]^2$ is compact with respect to $d_\infty$. Applying the product theorem inductively, we see that the $n$-dimensional cube $[a,b]^n$ is compact with respect to $d_\infty$ for all $n\geq 1$.
Since the identity map gives rise to a homeomorphism $([a,b]^n,d_\infty)\to ([a,b]^n, d)$ whenever $d$ is a metric that is Lipschitz equivalent to $d_\infty$, we conclude that $[a,b]^n$ is in fact compact with respect the metrics $d_1$ and $d_2$ as well.

\subsection{Compact subsets of $\mathbb R^n$}
In this section we are going to determine exactly which subsets of $\mathbb R^n$ are compact. To do this we start with the following observation:
\begin{proposition}\label{Prop: Compact spaces are bounded}
    Let $(X,d)$ a metric space. If $K\subseteq X$ is compact, then $K$ is bounded in the sense that there exists a constant $C\geq 0$ such that $d(x,y)\leq C$ for all $x,y\in K$.
\end{proposition}
\begin{proof}
    The result is obvious when $K=\emptyset$. So let us assume there exists $x\in K$. Then $\{U_n(x)\mid n\in\mathbb N\}$ is an open cover of $K$. Since $K$ is compact, there exists a finite subcover, i.e. there exist $n_1,\ldots, n_l$ such that $K\subseteq \bigcup_{i=1}^l U_{n_i}(x)$. Let $n=\max_{1\leq i\leq l} n_i$ and $C:=2n$. Then for each pair $y,z\in K$ we have $$d(y,z)\leq d(y,x)+d(x,z)\leq n+n=C.$$
\end{proof}

The converse is not necessarily true: consider $\mathbb N$ with the discrete metric. Then $d(n,m)\leq 1$ for all $n,m\in \mathbb N$ so $\mathbb N$ is bounded in this metric but not compact.

In $\mathbb R^n$ equipped with the Euclidean metric however it turns out that the converse does hold:
\begin{theorem}[Heine-Borel] Consider the space $(\mathbb R^n,d_2)$,
A subset $K\subseteq \mathbb R^n$ is compact if and only if it is closed and bounded.
\end{theorem}
\begin{proof} The statement is an equivalence, so we have to prove both implications.
\begin{itemize}
    \item[``$\Rightarrow$":]   If $K\subseteq \mathbb R^n$ is compact, then Proposition 8.4 shows that $K$ is bounded, and (ii) shows that $K$ is closed.
    \item[``$\Leftarrow$":]   Suppose conversely, that $K\subseteq \mathbb R^n$ is closed and bounded. We want to show that $K$ is compact. Since $K$ is bounded, there must exist some $L>0$ such that $K\subseteq [-L,L]^n$. As a product of compact intervals, $[-L,L]^n$ is itself compact with respect to the Euclidean metric. But this shows that $K$ is a closed subset of a compact set, and hence (i) implies that $K$ must be compact itself.
\end{itemize}
  



  
\end{proof}

\subsection{The Bolzano-Weierstraß Theorem}
The goal of this section is to prove the following important result:
\begin{theorem}[Bolzano-Weierstraß] \label{Theorem:BW}
    Let $(X,d)$ be a metric space. Then the following are equivalent:
\begin{enumerate}
\item $(X,d)$ is compact;
\item Every sequence in $(X,d)$ has a convergent subsequence.
\end{enumerate}
\end{theorem}

To prove the theorem we need the following reformulation of compactness in terms of closed sets. We leave its proof as an exercise.
\begin{lemma}\label{Lemma:Finite intersection property}
    Let $(X,d)$ be a metric space. Then the following are equivalent:
    \begin{enumerate}
        \item $X$ is compact;
        \item whenever $\{A_i\mid i\in I\}$ is a collection of closed sets in $X$ with the property that $\bigcap_{i\in F} A_i\neq \emptyset$ for all finite subsets $F\subseteq I$, then we must have $\bigcap_{i\in I} A_i\neq \emptyset$.
        (in words: if any finite subcollection of the $A_i$ shares a common point, then all the $A_i$ must share a common point)
    \end{enumerate}
\end{lemma}


Using the lemma, we can already prove one implication of the Bolzano-Weierstraß Theorem:
\begin{proof}[Proof of Theorem \ref{Theorem:BW} $(1)\Rightarrow (2)$] Suppose $X$ is compact and let $(x_n)_n$ be a sequence in $X$. Our goal is to construct a convergent subsequence of $(x_n)_n$. For every $n\in \mathbb N$ let
$$
A_n:=\overline{\{x_m\mid m\geq n\}}=\overline{\{x_n,x_{n+1},x_{n+2},\ldots\}}.
$$
Then $\{A_n\mid n\in \mathbb N\}$ is a family of closed sets. Suppose $F\subseteq \mathbb N$ is an arbitrary finite subset. Let $N:=\max F$. Then we have 
$$x_N\in \bigcap_{n \in F} \{x_m\mid m\geq n\}\subseteq \bigcap_{n\in F} A_n.$$
In particular, $\bigcap_{n\in F} A_n\neq \emptyset$. Applying the characterisation of compactness from Lemma \ref{Lemma:Finite intersection property}, we conclude that $\bigcap_{n\in\mathbb N} A_n\neq \emptyset$. 
So let $x\in \bigcap_{n\in\mathbb N} A_n$. We are going to construct a subsequence of $(x_n)_n$ which converges to $x$.
Since $x\in A_n$ for all $n\in \mathbb N$ and by definition of the closure, we have $U_{1/m}(x)\cap A_n\neq \emptyset$ for all $n,m\in \mathbb N$. 
We define a strictly increasing sequence of natural numbers $n_1<n_2<n_3<\ldots$ inductively as follows: 
Since $U_1(x)\cap \{x_1,x_2,x_3,\ldots\}\neq \emptyset$ there exists an index $n_1\geq 1$ such that $x_{n_1}\in U_1(x)$.
Inductively, assume that we have found natural numbers $n_1<\ldots <n_{k-1}$ such that $x_{n_l}\in U_{1/l}(x)$ for all $1\leq l\leq k-1$. Then, since $$U_{1/k}(x)\cap \{x_{n_{k-1}+1}, x_{n_{k-1}+2},\ldots\}\neq \emptyset,$$
there exists $n_k\geq n_{k-1}+1>n_{k-1}$ such that $x_{n_k}\in U_{1/k}(x)$.

Since the sequence of natural numbers $n_1<n_2<n_3<\ldots $ defined in this way is strictly increasing we obtain a subsequence $(x_{n_k})_{k\in \mathbb N}$ of $(x_n)_{n\in \mathbb N}$. Moreover, we have
$$d(x_{n_k},x)<\frac{1}{k}\to 0 \hbox{ as }k\to \infty,$$
in other words: $(x_{n_k})_{k\in \mathbb N}$ converges to $x$.
\end{proof}

For the other implication we need even more intermediate results, which we collect in the following Lemma:
\begin{lemma}\label{Lemma: Lebesgue number and total boundedness}
    Suppose $(X,d)$ is a metric space such that every sequence in $(x_n)_n$ in $X$ has a convergent subsequence. Then the following hold:
    \begin{enumerate}
        \item[(a)] If $\mathcal{U}$ is an open cover of $X$, then there exists a positive real number $\delta>0$ such that for every $x\in X$ there exists a $U\in \mathcal{U}$ such that $U_\delta(x)\subseteq U$.
        \item[(b)] For every $\varepsilon>0$ there exists a finite subset $F\subseteq X$ such that $X=\bigcup_{x\in F} U_\varepsilon(x)$.
    \end{enumerate}
\end{lemma}
\begin{proof}
    \begin{enumerate}
        \item[(a)] Suppose for contradiction that there exists no such $\delta>0$. Then in particular, for any $n\in \mathbb N$ the number $1/n$ does not have this property. So for each $n\in \mathbb N$ there exists an $x_n\in X$ such that 
        \begin{equation}\label{eq:contra}
        U_{1/n}(x_n) \hbox{ is not contained in a single element of }\mathcal{U}.
        \end{equation}
        By our standing assumption on $X$, the sequence $(x_n)_n$ that we have just found must have a convergent subsequence, say $(x_{n_m})_m$ is the subsequence and it converges to $x\in X$. Since $\mathcal{U}$ is an open cover of $X$, there exists a $U\in \mathcal{U}$ such that $x\in U$. Since $U$ is open, there exists an $\varepsilon>0$ such that $U_{2\varepsilon}(x)\subseteq U$. Moreover, since $x_{n_m}\to x$, there exists an $M\in \mathbb N$ such that $x_{n_m}\in U_\varepsilon(x)$ for all $m\geq M$. Choose $k\geq M$ large enough so that $1/{n_{k}}<\varepsilon$.
        We claim that $U_{1/n_k}(x_{n_k})\subseteq U_{2\varepsilon}(x)$. Indeed,
        given $y\in U_{1/n_k}(x_{n_k})$ we have that
        $$d(y,x)\stackrel{(M3)}{\leq} d(y,x_{n_k})+d(x_{n_k},x)<1/n_k + \varepsilon<2\varepsilon.$$
        But then we have $U_{1/n_k}(x_{n_k})\subseteq U_{2\varepsilon}(x)\subseteq U$. But this contradicts our choice of sequence (compare line (\ref{eq:contra})).
        
        \item[(b)] Suppose for contradiction that there exists some $\varepsilon>0$ such that 
        \begin{equation}\label{eq 1}
            X\setminus \bigcup_{x\in F} U_\varepsilon(x)\neq \emptyset \hbox{ for every finite set } F\subseteq X.
        \end{equation}
         We are going to construct a sequence $(x_n)_n$ which admits no Cauchy subsequence. To do this we are going to inductively define a sequence $(x_n)_n$ satisfying $d(x_n,x_m)\geq \varepsilon$ for all $n,m\in \mathbb N$ as follows: to start the construction, pick any element $x_1\in X$. Since $\{x_1\}$ is a finite subset of $X$, our assumption from line (\ref{eq 1}) implies that there exists an element $x_2\in X\setminus U_\varepsilon(x_1)$, i.e. satisfying $d(x_1,x_2)\geq \varepsilon$. Suppose now that $x_1,\ldots, x_n$ satisfying $d(x_i,x_j)\geq \varepsilon$ for all $i\neq j\in \{1,\ldots, n\}$ have already been constructed. Since $\{x_1,\ldots, x_n\}$ is a finite subset of $X$, our assumption from line (\ref{eq 1}) implies that there exists an element $x_{n+1}\in X\setminus \bigcup_{i=1}^n U_\varepsilon(x_i)$. But being in this complement just translates to $d(x_{n+1},x_i)\geq\varepsilon$ for all $i=1,\ldots, n$. 
         Thus, we have inductively constructed a sequence $(x_n)_n$ such that $d(x_n,x_m)\geq \varepsilon$ for all $n,m\in \mathbb N$. Such a sequence is clearly not a Cauchy sequence. In particular, it cannot have a convergent subsequence, since every convergent sequence is a Cauchy sequence. But this then contradicts our standing assumption that every sequence in $X$ has a convergent subsequence.
    \end{enumerate}
\end{proof}

With these observations in hand, we can finally complete the proof of the Bolzano-Weierstraß Theorem.

\begin{proof}[Proof of Theorem \ref{Theorem:BW} $(2)\Rightarrow (1)$]
    Suppose that every sequence in $(x_n)_n$ in $X$ has a convergent subsequence. We want to show that $X$ is compact. So let $\mathcal{U}$ be an arbitrary open cover of $X$. Our goal is to produce a finite subcover of $\mathcal{U}$. 
    By the first part of Lemma \ref{Lemma: Lebesgue number and total boundedness} there exists a $\delta>0$ such that for every $x\in X$ there exists a $U\in \mathcal{U}$ such that $U_\delta(x)\subseteq U$. Apply the second part of the Lemma to this $\delta$, i.e. we can find a finite subset $F\subseteq X$ such that $X=\bigcup_{x\in F} U_\delta(x)$.
    Putting things together, we can find for each $x\in F$ a $U_x\in \mathcal{U}$ such that $U_\delta(x)\subseteq U$. But then $X=\bigcup_{x\in F} U_\delta(x)\subseteq \bigcup_{x\in F} U_x$, so that $\{U_x\mid x\in F\}$ is a finite cover of $X$ which is contained in $\mathcal{U}$.    
\end{proof}

\section{Topological Spaces}
We have seen that metric spaces allow us to talk about convergence of sequences, the most fundamental notion of analysis. Curiously, in week $4$ we were able to reformulate this into a condition that does no longer explicitly depends on the actual metric, but only on the collection of open sets that the metric defines. Similarly, in section 5 we observed that continuity of functions between metric spaces can be equivalently formulated purely in terms of the open subsets of the domain and range of the function. The concepts of being connected (week 6) and compact (weeks 7 and 8) were even just defined in terms of open sets and made no explicit reference to the underlying metric anymore. The idea of topology is to build on this observation and make a \textbf{paradigm shift}, by declaring the collection of \textbf{open sets} to be the central object of interest.

%%%%%%%%%%%%%%%%%%%%
\begin{definition}
A \textbf{topology} on a set $X$ is a collection $\tau$ of subsets of $X$ satisfying the following conditions:
\begin{enumerate}
\item[(T1)] $\emptyset\in \tau$ and $X\in \tau$;
\item[(T2)] $\tau$ is closed under arbitrary unions: whenever $I$ is an index set and $U_i \in \tau$ for all $i \in I$ then also $\bigcup_{i \in I} U_i \in \tau$;
\item[(T3)] $\tau$ is closed under finite intersections: whenever $U_1, \dots, U_n \in \tau$ then also $\bigcap_{i=1}^n U_i \in \tau$.
\end{enumerate}
We write $(X,\tau)$ for a topological space, or simply $X$ if $\tau$ is understood.
The sets in the family $\tau$ are called \textbf{the open sets} of $X$.
\end{definition}

%%%%%%%%%%%%%%%%%%%%
\begin{examples}
\begin{enumerate}
\item On every set $X\neq \emptyset$ there are always two `extreme' topologies:
The \textbf{discrete topology} $\tau = \mathcal P (X)$ (recall that $\mathcal{P}(X)$ denotes the power set of $X$, i.e. the set of all subsets of $X$), in which every set is open, and the \textbf{trivial topology} $\tau = \{\emptyset, X\}$. The interesting topologies lie somewhere between these two. 
\item Let $(X,d)$ be a metric space, and let
$$\tau_d=\{U\subseteq X\mid \forall x\in U \exists \varepsilon>0: U_\varepsilon(x)\subseteq U\}$$ be the collection of sets defined as open sets in a metric space (see Definition 4.1).
Then $(X,\tau_d)$ is a topological space. We have already proved this as Theorem 4.6 (of course without using the terminology). We say that $\tau_d$ is the topology generated by the metric $d$.

\smallskip

\noindent In the special case $X=\mathbb R^n$ and $d_2(x,y):=(\sum_{i=1}^n \vert x_i- y_i\vert^2)^\frac{1}{2}$, we call the resulting topology $\tau_{d_2}$ on $\mathbb R^n$ the \textbf{Euclidean topology}.

\smallskip

\noindent A topological space $(X,\tau)$ is called \textbf{metrisable}, if $\tau=\tau_d$ for \emph{some} metric $d$ on $X$.
As we shall see, not all topological spaces have this property, so they are a more general concept.

\item Let $X = \{a,b\}$, $\tau = \{\emptyset, \{a\}, X\}$.
Then $(X, \tau)$ is a topological space (check!).
This topology is not metrisable.
To reach a contradiction, suppose there was a metric $d$ such that $$\{U\subseteq X\mid \forall x\in U\ \exists \varepsilon>0: U_\varepsilon(x)\subseteq U\}=\tau.$$
Since $\{a\}$ is open, there is an $\varepsilon>0$ such that $U_\varepsilon(a) \subseteq \{a\}$.
Since $b\notin \{a\}$, it follows that $d(a,b) > \varepsilon$.
Hence $a\notin U_\varepsilon(b)$.
But the set $U_\varepsilon(b)$ is open, and the only open set containing $b$ is $X$, so $U_\varepsilon(b) = X$.
But then $a\in U_\varepsilon(b)$, giving a contradiction.

\item Let $X$ be any nonempty set, so $X$ has at least one element $p$.
Let $\tau_p$ consist of the empty set plus all subsets of $X$ which have $p$ as a member:
\[
\tau_p = \{\emptyset\} \cup\{S\subseteq X:p\in S\}.
\]
Then $\tau_p$ is a topology on $X$.
It is called a {\bf particular point topology}.
\item On $X = \mathbb R$ define
$$\tau_{s.i.}:=\{\mathbb R, \emptyset\}\cup \{(a,\infty)\mid a\in\mathbb R\}.$$


We check that $\tau_{s.i.}$ satisfies the axioms one by one:
\begin{enumerate}
    \item[(T1)] By definition, we have that $\emptyset, \mathbb R \in \tau_{s.i.}$.
    \item[(T2)]Now, $(U_i)_i$ be a collection of sets in $\tau_{s.i.}$. 
            If at least one of the sets $U_i$ is equal to $\mathbb R$, then $\bigcup_{i\in I} U_i=\mathbb R\in \tau_{s.i.}$ and we are done. So let us assume $U_i\neq \mathbb R$ for all $i\in I$. Since taking a union with the empty set does not affect the union at all, we may as well also assume that $U_i\neq \emptyset$ for all $i\in I$. Then there must exist $a_i\in \mathbb R$ for each $i\in I$ such that $U_i=(a_{i},\infty)$. Then we have two cases:
\begin{enumerate}
\item if the set $\{a_{i}\mid i\in I\}$ is bounded below, then $\inf_{i\in I} a_{i}$ exists and we have 
$$\bigcup_{i\in I}(a_i,\infty)=(\inf_{i\in I} a_{i},\infty)\in\tau_{s.i.};$$

\item if $\{a_{i}\mid i\in I\}$ is not bounded below, then $\bigcup_{i\in I}(a_i,\infty)=\mathbb R\in\tau_{s.i.}$.
\end{enumerate}
    \item[(T3)] Finally suppose we are given finitely many elements $U_1,\ldots, U_n\in \tau_{s.i.}$. If at least one of the $U_i$ is equal to the empty set, then $\bigcap U_i=\emptyset\in \tau_{s.i.}$ as well and we are done. So let us assume that $U_i\neq \emptyset$ for all $i=1,\ldots, n$. Moreover, taking an intersection with $\mathbb R$ does not affect the intersection at all, so we may as well assume that $U_i\neq \mathbb R$ for all $i=1,\ldots, n$. Thus, we must have $U_i=(a_i,\infty)$ for some $a_i\in \mathbb R$, $i=1, \dots, n$. Then we get:
\[
\bigcap_{i=1}^{n}(a_{i},\infty)=(\max\{a_{1},a_{2},\ldots,a_{n}\},\infty)
\in\tau_{s.i.}.
\]
\end{enumerate}
Thus $\tau_{s.i.}$ is a topology on $\mathbb R$.\\
Note that every semi-infinite open interval $(a,\infty)$ is also open with respect to the Euclidean topology on $\mathbb R$. Hence we have
\[
\tau_{s.i.} \subseteq \tau_{d{\vert\cdot\vert}}.
\]
On the other hand, finite open intervals of the form $(a,b)$ for $a<b$ are not members of $\tau_{s.i.}$.
Thus the two topological spaces $(\mathbb R,\tau_{d{\vert\cdot\vert}}) $ and $(\mathbb R,\tau_{s.i.}) $ are different.


\end{enumerate}
\end{examples}

%\begin{exercise}
%Let $X$ be a set and let $d$ and $d'$ be equivalent metrics on $X$. Show that $\tau_d=\tau_{d'}$.
%\end{exercise}



Similar to what we did in the case of metric spaces, we can always restrict a topology to a subset. We leave the proof as an exercise.
\begin{lemma}
    Let $(X,\tau)$ be a topological space and $Y\subseteq X$ a subset. Then 
    $$\tau|_Y:=\{U\cap Y\mid U\in \tau\}$$
    is a topology on $Y$. It is called the \textbf{induced topology} on $Y$.
\end{lemma}

One has to be very careful when working with induced topologies. For example consider $X=\mathbb R$ with the usual topology and let $Y=(0,1]\subseteq \mathbb R$. Then $Y\in \tau|_Y$, i.e. $Y$ is open in itself, but $Y$ is neither open nor closed in $X$. So being open or closed depends very much on the ambient space!

%%%%%%%%%%%%%%%%%

\begin{lemma}
    Let $X,I\neq \emptyset$ be sets. Suppose for each $i\in I$ we have a topology $\tau_i$ on $X$. Then $\tau:=\bigcap_{i\in I}\tau_i$ is also a topology on $X$.    
\end{lemma}
\begin{proof}
    We verify the three axioms for $\tau$, using that $\tau_i$ satisfies them for every $i\in I$.
    \begin{enumerate}
        \item[(T1)] Since $\emptyset,X\in \tau_i$ for all $i\in I$, $\emptyset$ and $X$ are also in $\tau$.
        \item[(T2)] Now let $J$ be another index set and $U_j\in \tau$ for all $j\in J$. But then each $U_j$ must be contained in $\tau_i$ for all $i\in I$. 
    Since each $\tau_i$ is a topology, it follows that $\bigcup_{j\in J} U_j\in \tau_i$. Since this holds for all $i\in I$ we conclude that $\bigcup_{j\in J} U_j\in \tau$ as desired.
        \item[(T3)]  Finally, let $U_1,\ldots, U_n$ be finitely many elements in $\tau$. As before, this means that $U_j\in \tau_i$ for all $1\leq j\leq n$ and $i\in I$. Since $\tau_i$ is a topology, we conclude that $\bigcap_{j=1}^n U_j\in \tau_i$ for all $i\in I$ and hence $\bigcap_{j=1}^n U_j\in \tau$. This concludes the proof.
    \end{enumerate}    
\end{proof}

\begin{definition}
    Let $X$ be a set and $\mathcal{S}\subseteq \mathcal{P}(X)$ a collection of subsets of $X$. Then $$\tau(\mathcal S):=\bigcap \{\tau\mid \tau \hbox{ topology on }X\hbox{ with }\mathcal{S}\subseteq \tau\}$$
    is a new topology on $X$ by the previous Lemma. It is called the \textbf{topology generated by} $\mathcal{S}$.
\end{definition}
Note that by construction, $\tau(\mathcal S)$ is the smallest topology on $X$ containing $\mathcal{S}$.
%%%%%%%%%%%%%%%%%%%%
\begin{example}
Let $X= \mathbb R$ with the topology generated by half open intervals of the form $[x,y)$ with $x< y$ (i.e. the topology generated by $\mathcal{S}=\{[x,y)\mid x,y\in \mathbb R:x<y\}$).
Note that we have $(x,y) = \bigcup_{n\in\mathbb N} [x+1/n,y)\in \tau(\mathcal{S})$. Since the Euclidean topology $\tau_{\vert \cdot\vert}$ on $\mathbb R$ is generated by the open intervals, we conclude that $\tau_{\vert \cdot\vert}\subseteq \tau(\mathcal{S})$.
\end{example}

We can also make the same definition as in the case of metric spaces for closed sets:

%%%%%%%%%%%%%%%%%%%%
\begin{definition} Let $(X,\tau)$ be a topological space.
A set $C\subseteq X$ is said to be \textbf{closed} if its complement $X \setminus C$ is open (i.e. $X\setminus C\in \tau$).
\end{definition}

%%%%%%%%%%%%%%%%%%%%
\begin{examples} \begin{enumerate}
%    \item Consider $X=\mathbb R$ with the Euclidean topology $\tau_{\vert \cdot\vert}$. Every closed interval $[a,b]$ of $\mathbb R$ is a closed set with respect to this topology since its complement $\mathbb R\setminus [a,b]$ is the union $(-\infty,a)\cup(b,\infty)$ of two open sets and hence open.
    
%    \noindent An open interval $(a,b)$ of $\mathbb R$ is  not  closed in the usual topology. Its complement $(a,b)^c$ is the union $(-\infty,a]\cup[b,\infty)$ which is not an open subset of $\mathbb R$ (why?).
    \item Let $X\neq \emptyset$ and $p\in X$. Consider again the particular point topology $\tau_p:=\{U\subseteq X\mid p\in U\}\cup \{\emptyset\}$. A set $A\subseteq X$ is closed in this topology if $p\notin A$ or if $A=X$.
    \item Let $X=\mathbb R$ with the topology $\tau(\mathcal{S})$ from Example 9.6. Then every set that is closed with respect to the Euclidean topology is also closed with respect to $\tau(\mathcal{S})$ since we saw in 9.6 that $\tau_{\vert\cdot\vert}\subseteq \tau(\mathcal{S})$. In particular $[a,b]$ for $a\leq b$ is closed in $(\mathbb R,\tau(\mathcal{S})$. What about the sets $[a,b)$ for $a<b$? To check whether or not they are closed we need to check whether or not the complement $\mathbb R\setminus [a,b)=(-\infty,a)\cup [b,\infty)$ is open. But $[b,\infty)=\bigcup_{n\in \mathbb N} [b,b+n)\in \tau(\mathcal{S})$ by axiom $(T2)$, and we have already seen that $(-\infty,a)\in \tau(\mathcal{S})$. Hence $\mathbb R\setminus [a,b)=(-\infty,a)\cup [b,\infty)$ is a union of two open sets and hence open.

    Conclusion: In $(\mathbb R,\tau(\mathcal{S}))$ the sets $[a,b)$ are both open and closed, while in $(\mathbb R,\tau_{\vert \cdot\vert})$ they are neither open nor closed.
\end{enumerate}

\end{examples}

%%%%%%%%%%%%%%%%%%%%


%%%%%%%%%%%%%%%%%%%%
\begin{proposition}
Let $(X,\tau)$ be a topological space.
Then the following hold:
\begin{enumerate}
\item $\emptyset$ and $X$ are closed.
\item Arbitrary intersections of closed sets are closed;
\item Finite unions of closed sets are closed;
\end{enumerate}
\end{proposition}

\begin{proof}
The proof is left as an exercise.
\end{proof}

Every statement involving open sets can be translated into a corresponding statement involving closed sets, simply by taking complements.
For example, we could equally well have defined topological spaces in terms of closed sets using (1)-(3) as in the proposition above.

%%%%%%%%%%%%%%%%%%%%
\subsection*{Closure-Interior-Boundary}
%%%%%%%%%%%%%%%%%%%%

The notions of the closure, interior and a boundary that we know from the setting of metric spaces also extend to the realm of general topological spaces. Although the following formal definition looks a bit different at first sight:

%%%%%%%%%%%%%%%%%%%%
\begin{definition} Let $(X,\tau)$ be a topological space and $E\subseteq X$ a subset. Then
\begin{enumerate}
    \item the \textbf{interior} of $E$ (denoted by $E^\circ$) is the union of all open subsets contained in $E$, in symbols
$$
E^\circ := \bigcup \{U\subseteq E: U\hbox{ is open}\}.
$$
Some authors use the notation $\mathrm{Int}(E)$ instead of $E^\circ$.
\item the \textbf{closure} of $E$ (denoted $\overline{E}$) is the intersection of all closed subsets containing $E$, in symbols
$$
\overline{E} := \bigcap \{A\supseteq E: A \hbox{ is closed}\}.
$$
We sometimes use the notation $\mathrm{Cl}(E)$ or $\mathrm{Cl}_X(E)$ if we want to ensure that the ambient space $X$ is understood.
\item The \textbf{boundary} of $E$ is defined as
$$
\partial E := \overline{E}\cap \overline{(X \setminus E)} = \overline{E} \setminus E^\circ.
$$
\end{enumerate}
\end{definition}

The same rules that we proved in the case of metric spaces, still hold for general topological spaces.
\begin{proposition}
    Let $(X,\tau)$ be a topological space and let $A,B\subseteq X$ be two subsets. Then the following hold:
    \begin{enumerate}
        \item $\overline{A}$ is the smallest closed set in $X$ containing $A$,        
        \item $A\subseteq B$ implies $\overline{A}\subseteq\overline{B}$,
        \item $A$ is closed in $X$ if and only if $A=\overline A$,
       
        \item $\overline{\overline{A}}=\overline{A}$,
        
        \item $\overline{A\cup B}=\overline{A}\cup \overline{B}$,
        \item $\overline{A\cap B}\subseteq \overline{A}\cap \overline{B}$, but the converse inclusion is not necessarily true.
    \end{enumerate}
\end{proposition}
\begin{proof}
    \begin{enumerate}
        \item By definition, $\overline{A}$ is the intersection of a family of closed sets. As such, it is closed by Proposition 9.9.
       Moreover, since each of the sets that we are intersecting to form $\overline{A}$ contains $A$, so does $\overline{A}$.
        To see that $\overline{A}$ is the smallest set with these properties, suppose that $C$ is another closed set such that $A\subseteq C$. Then $C\in \{E\supseteq A\mid E \hbox{ is closed}\}$ and hence
        $\overline{A}=\bigcap\{E\supseteq A\mid E \hbox{ is closed}\}\subseteq C$.
       
        \item By (1) we have $$A\subseteq B\subseteq \overline{B}.$$ Since $\overline{B}$ is a closed subset containing $A$ and $\overline{A}$ is the smallest closed subset containing $A$ by (1), we must have $\overline{A}\subseteq \overline{B}$.
        \item If $A$ is closed itself, then $A \in \{E\supseteq A\mid E \hbox{ is closed}\}$ and hence 
        $$\overline{A}=\bigcap \{E\supseteq A\mid E \hbox{ is closed}\}\subseteq A.$$
        Since we always have $A\subseteq \overline{A}$ we get equality. 

        Conversely, if $\overline{A}=A$, then $A$ is closed since $\overline{A}$ is always a closed set. 
        \item Since $\overline{A}$ is always closed, this follows from (3). 
        \item For (5) recall that $\overline{A} \cup \overline{B}$ is a closed set as a finite union of two closed sets.
Since $A \subseteq \overline{A}$ and $B \subseteq \overline{B}$ we get that $A \cup B \subseteq \overline{A} \cup \overline{B}$.
By definition then $\overline{A \cup B} \subseteq \overline{A} \cup \overline{B}$.
On the other hand $A \subseteq A \cup B$ implies $\overline{A} \subseteq \overline{A \cup B}$ by (2).
By the same argument we get $\overline{B} \subseteq \overline{A \cup B}$.
Therefore we conclude that $\overline{A} \cup \overline{B} \subseteq \overline{A \cup B}$.


\item For (5) we have that $\overline{A}$ is a closed set that contains $A$.
Since $A \cap B \subseteq A$, we get $\overline{A\cap B}\subseteq \overline{A}$ by (2). Similarly, we have that $\overline{A \cap B} \subseteq \overline{B}$ and hence $\overline{A\cap B}\subseteq \overline{A}\cap \overline{B}$.
    \end{enumerate}
\end{proof}


%%%%%%%%%%%%%%%%%%%%
\begin{examples} Let us compute the closure, interior and boundary in a few examples.
Let $X = \{a, b, c, ,d, e\}$ and consider
\[
\tau = \{\emptyset, X, \{a\}, \{c, d\}, \{a, c, d\}, \{b, c, d, e\}\}.
\]
Then $\tau$ is a topology on $X$ (check!) and the closed sets in $X$ are
\[
\{ X, \emptyset, \{b,c,d,e\}, \{a,b,e\},\{b,e\},\{a\}\}.
\]
For $A = \{a,c\}$ we get that
\[
A^\circ = \{a\},\ \overline{A} = X,\ \partial A = \{b, c, d, e\}.
\]
On the other hand for $B = \{b,d\}$ we have that
\[
B^\circ=\emptyset,\ \overline{B}=\{b,c,d,e\},\ \partial B = \overline{B}\setminus \emptyset =\{b,c,d,e\}.
\]
\end{examples}




%%%%%%%%%%%%%%%%%%%%


%%%%%%%%%%%%%%%%%%%%
%\begin{exercise}
%\begin{enumerate}
%    \item Let $(X,d)$ be a metric space.
%Show that $\overline{U_r(a)} \subseteq B_r(a)$ for all $a \in X$ and $r \in \mathbb R$.
%    \item Give a counterexample where these two sets are not the same.
%(Consider the discrete metric on a space with at least two points and see what happens for $r=1$.)
%\item Show that $B_r(a) = \overline{U_r(a)}$ in any normed vector-space $(V,\nor{\cdot})$ (Hint: Use that a set in a metric space is closed  if and only if is sequentially closed).
%\end{enumerate}
%\end{exercise}

%%%%%%%%%%%%%%%%%%%%%%%%%%





%%%%%%%%%%%%%%%%%%%%
%\begin{exercise}
%Let $(X,\tau)$ be a topological space. Formulate and prove an analogue of Lemma 2.16 for the interior operator, i.e. how does "taking interior" behave with respect to inclusions, unions, and intersections?
%\end{exercise}

\section{Bases in topological spaces and the Hausdorff property}
\subsection*{Bases in topological spaces}
%%%%%%%%%%%%%%%%%%%%

In a metric space, there is a canonical collection of open sets, namely the open balls of some radius, centered at some point. Now this concept no longer makes sense in an arbitrary topological space. The following concepts are a kind of replacement for them:

%%%%%%%%%%%%%%%%%%%%
\begin{definition}
Let $(X,\tau)$ be a topological space and $x\in X$.
\begin{enumerate}
\item A \textbf{neighbourhood} (\textbf{n'hood}) of $x$ is a set $A\subseteq X$ such that there exists an open set $U\subseteq X$ with $x\in U\subseteq A$.

\item A \textbf{neighbourhood base} $\mathcal U_x$ about $x$ is a collection of n'hoods of $x$ with the property that for every n'hood $V$ of $x$ there exists an element $U\in \mathcal U_x$ such that $U\subseteq V$.

\item We say that $(X,\tau)$ is \textbf{first-countable} if every point $x\in X$ admits a countable n'hood base $\mathcal{U}_x=\{U_n\mid n\in \mathbb N\}$.
\end{enumerate}
\end{definition}
%%%%%%%%%%%%%%%%%%%%

Note that n'hoods (and so elements of n'hood bases) need not be open.
In case they are, we will specifically say so. 

\begin{examples}
Let $X = \mathbb R$ with the usual topology.
An example of a n'hood base for $x\in \mathbb R$ is $$\mathcal{U}_x=\{[x-\varepsilon,x+\varepsilon]\mid \varepsilon\in (0,\infty)\}.$$
An example of an open n'hood base is $$\mathcal{V}_x=\{(x-\varepsilon,x+\varepsilon)\mid\varepsilon\in (0,\infty)\}.$$ These are examples of uncountable neighbourhood bases (since $(0,\infty)$ is uncountable).
However, we can find smaller ones as well:
For each $x\in \mathbb R$ consider $$\mathcal{W}_x=\{[x-\frac{1}{n},x+\frac{1}{n}]\mid n\in\mathbb N\}.$$ Then $\mathcal{W}_x$ is a countable neighbourhood base for $x$. This shows that $(\mathbb R,\tau_{\vert\cdot\vert})$ is first-countable.
\end{examples}

Expanding on the previous example we have:
\begin{theorem}
    Let $(X,\tau)$ be a metrisable topological space. Then $(X,\tau)$ is first-countable.
\end{theorem}
\begin{proof}

    Since $\tau$ is metrisable, there exists a metric $d$ on $X$ such that $\tau=\tau_d$. For each $x\in X$ consider the collection
    $$\mathcal{U}_x:=\{U_{\frac{1}{n}}(x)\mid n\in\mathbb N\}$$
    of open balls of radius $1/n$.
    The collection $\mathcal{U}_x$ is clearly countable so we only have to show that it is an open neighbourhood base for $x$.
    So let $U$ be an arbitrary neighbourhood of $x$. Then there exists an open set $V$ such that $x\in V\subseteq U$. But $V$ being open in a metric space means that there exists an $\varepsilon>0$ such that $U_\varepsilon(x)\subseteq V\subseteq U$.
    Now find $n\in\mathbb N$ such that $1/n<\varepsilon$. Then 
    $U_{\frac{1}{n}}(x)\subseteq U_\varepsilon(x)\subseteq V\subseteq U$, which concludes the proof.
    
\end{proof}

Here is an example of a topology that is not first-countable:
\begin{example}
    Let $X=\mathbb R$ and $\tau=\{\emptyset\}\cup \{U\subseteq \mathbb R\mid \mathbb R\setminus U \hbox{ is finite}\}$.
    Then $(X,\tau)$ is not first-countable.

    Suppose for contradiction that it was. Then for $x\in \mathbb R$ we could find a countable neighbourhood base $\mathcal{U}=\{U_n\mid n\in\mathbb N\}$. Then $F_n:=\mathbb R\setminus U_n$ is finite and hence $F:=\bigcup_{n\in\mathbb N} F_n$ is countable. Since $\mathbb R$ is uncountable there exists a $y\in \mathbb R\setminus F$ . In particular $y\neq x$ and by definition of the topology, the set $U_y:=\mathbb R\setminus \{y\}$ is an open neighbourhood of $x$.
    Since $\mathcal{U}$ is a neighbourhood basis for $x$, there must exist an $n\in \mathbb N$ such that $x\in U_n\subseteq U_y$. But then $y\not\in U_n$ (since $y\not\in U_y$) and hence $y\in F_n\subseteq F$. This contradicts our choice of $y$!
\end{example}
%%%%%%%%%%%%%%%%%%%%
Many arguments with open sets in $(\mathbb R, \tau_{\vert \cdot \vert})$ reduce to looking at what happens with open intervals since open sets in the Euclidean topology are defined in terms of open intervals. A similar statement
holds for $\mathbb R^2$ and $\mathbb R^n$ with open disks and balls in place of open intervals. In each
case a general open set is a union of the special open sets given by open intervals,
disks, or balls. This idea is expressed by the following terminology:
\begin{definition}
Let $(X,\tau)$ be a topological space.
\begin{enumerate}
\item A \textbf{base} $\mathcal U$ for the topology on $X$ is a collection of \underline{open} subsets of $X$ (i.e. $\mathcal{U}\subseteq \tau$) such that every open set in $X$ (that is, every element of $\tau$) can be written as a union of elements of $\mathcal U$.

%\item A \textbf{subbase} $\mathcal S$ for the topology on $X$ is a collection of \underline{open} subsets of $X$ such that 
%\[\{S_1\cap\ldots\cap S_n\mid n\in \mathbb N, S_1,\ldots, S_n\in\mathcal S\}\]
%is a base for the topology on $X$.
\item We say that $(X,\tau)$ is \textbf{second-countable} if $(X,\tau)$ admits a countable base.
\end{enumerate}
\end{definition}



%%%%%%%%%%%%%%%%%%%%
\begin{examples}

\begin{enumerate}
    \item A base for the Euclidean topology on $\mathbb R$ is the collection $\mathcal{I}=\{(a,b)\mid a,b\in \mathbb R, a<b\}\cup\{\emptyset\}$ of all open intervals in $\mathbb R$.
Another base is the collection $\mathcal{I}_{rat}:=\{(a,b)\mid a,b\in \mathbb Q, a<b\}\cup\{\emptyset\}$ of all open intervals with rational endpoints. Since $\mathbb Q$ is countable, so is $\mathcal{I}_{rat}$ and hence the Euclidean topology on $\mathbb R$ is second-countable!

A subbase for the Euclidean topology is the collection of intervals of the form $(-\infty,a)$ or $(a,\infty)$.
\item If $(X,d)$ is a metric space, then $\mathcal{U}:=\{U_\varepsilon (x)\mid x\in X, \varepsilon>0\}$ is a base for the topology $\tau_d$ (the topology induced by $d$). If $Y\subseteq X$ is a countable subspace such that $\overline{Y}=X$ (e.g. $\mathbb Q^n\subseteq \mathbb R^n$) then $$\mathcal{V}:=\{U_{\frac{1}{n}} (x)\mid x\in Y, n\in \mathbb N\}$$ 
is a countable base for $\tau_d$, hence $(X,\tau_d)$ is second countable.
\end{enumerate}

\end{examples}

%%%%%%%%%%%%%%%%%%%%


Suppose we are now in the situation that we have a set $X$ and we want to define a topology on $X$. It is then often easier to specify a base or a subbase rather then the topology itself.
To do this it is important to know when a given collection of sets $\mathcal{U}$ is a base for some topology on $X$:
\begin{proposition}
    Let $X$ be a set and $\mathcal{U}\subseteq \mathcal{P}(X)$ a collection of sets. Then there exists a topology $\tau$ on $X$ for which $\mathcal{U}$ is a base if and only if $\mathcal{U}$ satisfies the following two conditions:
   \begin{enumerate}
       \item For all $x\in X$ there exists $U\in\mathcal{U}$ such that $x\in U$, and
       \item if $U_1,U_2\in \mathcal{U}$ and $x\in U_1\cap U_2$, then there exists $U\in \mathcal{U}$ such that $x\in U\subseteq U_1\cap U_2$.
   \end{enumerate}
\end{proposition}
\begin{proof}
    Suppose first that there exists a topology $\tau$ on $X$ for which  $\mathcal{U}$ is a base. Since $X\in\tau$ and $\mathcal{U}$ is a base we can write $X=\bigcup_{U\in\mathcal{U}} U$ which implies (1). Suppose now that $U_1,U_2\in\mathcal{U}$ and $x\in U_1\cap U_2$. Since base members are open, $U_1$ and $U_2$ are open and hence $U_1\cap U_2$ must also be open by (T3). Since $\mathcal{U}$ is a basis we can write  $U_1\cap U_2$ as a union of sets in $\mathcal{U}$, so there exist an index set $I$ and $V_i\in \mathcal U$ for all $i\in I$ such that $U_1\cap U_2=\bigcup_{i\in I} V_i$. But then there must exist an $i\in I$ such that $x\in V_i$ and hence $x\in V_i\subseteq U_1\cap U_2$ as desired.

    Conversely, suppose $\mathcal{U}$ satisfies $(1)$ and $(2)$. Set
    $$\tau:=\left\{ \bigcup_{i\in I} U_i\mid I \hbox{ a set and } U_i\in \mathcal{U}\ \forall i\in I\right\},$$
    i.e. $\tau$ consists of all arbitrary unions of elements in $\mathcal{U}$. We claim that $\tau$ is a topology, so we need to check the axioms:
    \begin{enumerate}
        \item[(T1)] If we choose $I=\emptyset$, then $\bigcup_{i\in I}U_i=\emptyset$ and hence $\emptyset\in \tau$. 
        To see that $X\in \tau$ let $I:=\mathcal{U}$. Then $X=\bigcup_{U\in \mathcal{U}}U\in \tau$ by (1).
        \item[(T2)] An arbitrary union of unions of elements of $\mathcal{U}$ is obviously again a union of elements of $\mathcal{U}$.
        \item[(T3)] By induction it is enough to show that $W_1\cap W_2\in \tau$ for all $W_1,W_2\in \tau$. To see the latter write
        $$W_1=\bigcup_{i\in I} U_i, \textit{ and }W_2=\bigcup_{j\in J}V_j,$$
        where $U_i,V_j\in \mathcal{U}$ for all $i\in I, j\in J$.
        Now for each $x\in W_1\cap W_j$ there exist an $i_x\in I$ and a $j_x\in J$ such that $x\in U_{i_x}\cap U_{j_x}$. By item (2) we can find $U_x\in \mathcal{U}$ such that $x\in U_x\subseteq U_{i_x}\cap V_{j_x}\subseteq W_1\cap W_2$. It follows that
        $$W_1\cap W_2=\bigcup_{x\in W_1\cap W_2} U_x\in \tau.$$
    \end{enumerate}
\end{proof}

\begin{example}
    Consider the set $\mathcal{F}(\mathbb R):=\{f:\mathbb R\rightarrow \mathbb C\}$ the set of all functions from $\mathbb R$ to $\mathbb C$. For $f\in \mathcal{F}(\mathbb R),\ x_1,\ldots x_n\in \mathbb R,$ and $\varepsilon>0$, let
    $$U_\varepsilon(f;x_1,\ldots, x_n):=\{ g\in\mathcal{F}(\mathbb R)\mid \vert f(x_i)-g(x_i)\vert<\varepsilon \ \forall 1\leq i\leq n\},$$
    and let
    $$\mathcal{U}=\{U_\varepsilon(f;x_1,\ldots, x_n)\mid f\in \mathcal{F}(\mathbb R),\ n\in\mathbb N,\ x_1,\ldots, x_n\in\mathbb R,\ \varepsilon>0\}.$$
    We claim that $\mathcal{U}$ is the base of a topology on $\mathcal{F}(\mathbb R)$. 
 
    To see this we check items (1) and (2) from the Proposition above:
    \begin{enumerate}
        \item Given $f\in \mathcal{F}(\mathbb R)$ find any $x\in\mathbb R$. Then $f\in U_1(f,x)\in \mathcal{U}$.
        \item Now suppose $f\in U_{\varepsilon_1}(f_1;x_1,\ldots, x_n)\cap U_{\varepsilon_2}(f_2;y_1,\ldots, y_m)$. Set 
        $$\varepsilon:=\min \{\varepsilon_1-\vert f_1(x_i)-f(x_i)\vert, \varepsilon_2-\vert f_2(y_j)-f(y_j)\vert \mid 1\leq i\leq n, 1\leq j\leq m\} $$
        Then $$f\in U_\varepsilon(f;x_1,\ldots, x_n,y_1,\ldots, y_m)\subseteq U_{\varepsilon_1}(f_1;x_1,\ldots, x_n)\cap U_{\varepsilon_2}(f_2;y_1,\ldots, y_m).$$
    \end{enumerate}

    We will see later that $\mathcal{F}(\mathbb R)$ with this topology is neither first- nor second-countable. It follows in particular, that $\mathcal{F}(\mathbb R)$ is not metrisable.
\end{example}

The following Lemma explains the relation between a basis and a neighbourhood basis for a point. We leave the proof of the lemma and its corollary as an exercise.
\begin{lemma}
    Let $(X,\tau)$ be a topological space and $\mathcal{U}\subseteq \mathcal{P}(X)$. Then the following are equivalent:
    \begin{enumerate}
        \item $\mathcal{U}$ is a base for $\tau$;
        \item For all $x\in X$ the collection $\mathcal{U}_x:=\{U\in \mathcal{U}\mid x\in U\}$ is a neighbourhood base of $x$.
    \end{enumerate}
\end{lemma}
\begin{corollary}
    Let $(X,\tau)$ be a topological space. If $(X,\tau)$ is second countable, then $(X,\tau)$ is also first countable.
\end{corollary}

%%%%%%%%%%%%%%%%%%%%
\subsection*{Convergence of sequences}
%%%%%%%%%%%%%%%%%%%%

Abstracting from the metric space case (compare Lemma 4.5) we can define what it means for a sequence to converge in a topological space:
\begin{definition}
    Let $(X,\tau)$ be a topological space and $(x_n)_n$ be a sequence in $X$. We say that {\bf $(x_n)_n$ converges to an element $x\in X$} if for every open set $U$ with $x\in U$ there exists an $N\in\mathbb N$ such that $x_n\in U$ for all $n\geq N$.
\end{definition}







%\begin{example}
%Let $(X,\rho)$ be a metric space and let $x_0\in X$.
%Define $\Lambda = X \setminus \{x_0\}$ as a directed set, where $x\leq y$ if and only if $\rho(y,x_0) \leq \rho(x,x_0)$ (note that the order on this directed set is \textbf{not} antisymmetric!).
%If $f \colon X \to N$ then $f$ restricted to $\Lambda$ defines a net in $N$.
%This net converges to $z_0$ if and only if given any open ball $U(z_0,\varepsilon)$ about $z_0$, there is a $y_0$ such that for all $y > y_0$ with $f(y)\in U(z_0,\varepsilon)$.
%If $\delta = \rho(x_0,y_0)$, then this is equivalent to saying that $y\in U(x_0,\delta)$.  That is, $z_0 = \lim_{x\to x_0} f(x)$ in the usual sense.
%\end{example}






%%%%%%%%%%%%%%%%%%%%
\begin{lemma}\label{Lemma:Closed is limit closed}
Let $(X,\tau)$ be a topological space, let $E \subseteq X$, and let $x\in X$. Consider the following statements:
\begin{enumerate}
    \item there is a sequence $(x_n)_n$ in $E$ such that $x_n \rightarrow  x$.
    \item $x\in \overline{E}$
    \item $U\cap E\neq \emptyset$ for every open neighbourhood $U$ of $x$.
    
\end{enumerate}
Then $(1)\Rightarrow (2)\Leftrightarrow (3)$ and if $X$ is first-countable, then all three conditions are equivalent.
\end{lemma}
The lemma shows that beyond the first-countable setting, sequences are no longer enough to characterise if a given element is in the closure of a set or not. There is a solution to this problem. The idea is to replace \emph{sequences} by a more general concept, where we replace our index set $\mathbb N$ by larger (i.e. uncountable) sets. We will not cover this topic in detail and leave it as an appendix for the interested reader.
\begin{proof}
$(1)\Rightarrow (2)$: suppose that there is a sequence $(x_n)_n$ in $E$ so that $x_n\to  x$. Suppose for contradiction that $x\notin \overline{E}$, or in other words, $x\in X\setminus \overline{E}$. Since $\overline{E}$ is closed, $X\setminus \overline{E}$ is open. Thus, using that $x_n \to x$ we can find an $N\in \mathbb N$ such that $x_n\in X\setminus \overline{E}\subseteq X\setminus E$ for all $n\geq N$. But then $x_N\in E\cap X\setminus E=\emptyset$, a contradiction!

\smallskip

$(2)\Rightarrow (3)$: Suppose for contradiction that $E\cap U=\emptyset$ for some open neighbourhood of $x$. Then $X\setminus U$ is closed and $E\subseteq X\setminus U$. It follows that $\overline{E}\subseteq \overline{X\setminus U}=X\setminus U$. But since $x\in \overline{E}$, this implies that $x\notin U$, a contradiction to the fact that $U$ was a neighbourhood of $x$.

\smallskip 

$(3)\Rightarrow (2)$: Suppose for contradiction that $x\notin \overline{E}$, i.e. $x\in X\setminus \overline{E}$. Since $X\setminus\overline{E}$ is open, $X\setminus \overline{E}\cap E\neq \emptyset$ by $(3)$. So there exists an element $y\in E$ such that also $y\in X\setminus \overline{E}\subseteq X\setminus E$. A contradiction!

\smallskip

Finally, let us show $(3)\Rightarrow (1)$ under the additional hypothesis that $X$ is first-countable: let $\mathcal{U}_x=\{U_n\mid n\in \mathbb N\}$ be a countable neighbourhood base for $x$. We may assume without loss of generality that $U_{n+1}\subseteq U_n$ for all $n\in \mathbb N$. By $(3)$ $U_n\cap E\neq \emptyset$ for all $n\in \mathbb N$. Hence we can choose a point $x_n\in U_n\cap E$ for each $n\in \mathbb N$. But then $x_n\rightarrow x$. Indeed, if $V$ is any open set containing $x$, then by virtue of being a neighbourhood base, there exists an $N\in \mathbb N$ such that $x\in U_N\subseteq V$ and since $\mathcal{U}_x$ is nested we get that $x\in U_n\subseteq U_N\subseteq V$ for all $n\geq N$. Since $x_n\in U_n$ for all $n\in \mathbb N$ this shows that $x_n\in V$ for all $n\geq N$ as desired.
\end{proof}

Convergence of sequences proved useful in a metric space to check whether a given set is closed. We do have an analogue of this for certain topological spaces, which we leave as an exercise.

\begin{proposition}
    Let $(X,\tau)$ be a topological space and $A\subseteq X$ a subset. Consider the following statements:
    \begin{enumerate}
        \item $A$ is closed in $X$;
        \item whenever $(x_n)_n$ is a sequence in $A$ such that $x_n\rightarrow x$ for some $x\in X$, then $x\in A$.
    \end{enumerate}
    The implication $(1)\Rightarrow (2)$ is always true. If $X$ is first-countable, then we also have $(2)\Rightarrow (1)$.
\end{proposition}





%We remark that if $(X,\tau)$ is first-countable, then we can replace nets by sequences in item (3) of the previous lemma.
The following example shows that in a space that is not first-countable, item (3) in the Lemma \ref{Lemma:Closed is limit closed} is not sufficient to guarantee that $x\in \overline{E}$:
%%%%%%%%%%%%%%%%%%%%
\begin{example}
Let $X = \mathcal{F}(\mathbb R)$ be the set of all functions $f:\mathbb R\rightarrow \mathbb C$ with the topology defined in Example 2.25. Consider the subset $E\subseteq \mathcal{F}(\mathbb R)$ given by
$$
E = \{f:\mathbb R\rightarrow \mathbb C\mid f(x)\in \{0,1\} \forall x\in \mathbb R,\hbox{ and the set }f^{-1}(0)\hbox{ is finite}\}.
$$
Let $g\equiv 0$ be the constant function.
A basic open n'hood of $g$ is
$$
U_\varepsilon(g,F) = \{h:\mathbb R\rightarrow \mathbb C\mid |h(x)| < \varepsilon,\forall x\in F\}, \hbox{ where } \varepsilon>0,\ F\subseteq  \mathbb R \hbox{ finite}.
$$
For every finite subset $F\subseteq \mathbb R$ the function $h_F$ defined by
$$
h_F(x) =
\begin{cases}
0 & x\in F,\\
1 & \hbox{otherwise},
\end{cases}
$$
is in $U_\varepsilon(g,F) \cap E$ for all $\varepsilon>0$.
Hence this intersection is nonempty.
Consequently, we get that $g\in \overline{E}$ by the previous lemma.

\smallskip

Now suppose that $(f_n)_n$ is a sequence in $E$ that converges to some $f\in X$.
Each $f_n$ is zero on a finite set, and so the union of all of these zero sets is countable.
Hence $f$ can be zero on at most a countable set; that is, it is not zero everywhere.
Hence $g$ is not the limit of any sequence in $E$.
\end{example}
%We now arrive at the fundamental notion of limit points.

%%%%%%%%%%%%%%%%%%%%
%\begin{definition}
%Let $E$ be a subset of a topological space $X$.
%Then $x$ is a \textbf{limit point} or \textbf{cluster point} of $E$ if and only if every open n'hood of $x$ contains a point $y\neq x$ in $E$.
%\end{definition}

%Note here that a cluster point of $E$ need not be in $E$.
%As we will see later, this happens for specific sets $E$.

%%%%%%%%%%%%%%%%%%%%
%\begin{example}
%The point $0$ is a limit point of both $\{1/n\}_{n\in\mathbb N}$ and $\{-1/n\}_{n\in\mathbb N}$ in $\mathbb R$ with the usual topology.
%On the other hand in the Sorgenfrey line, $0$ is also a limit point of $\{1/n\}_{n\in\mathbb N}$ though it is \textbf{not} a limit point of $\{-1/n\}_{n\in\mathbb N}$.
%\end{example}

%%%%%%%%%%%%%%%%%%%%
%\begin{example}
%For $[0,1] \cup \{2\}$ in $\mathbb R$ with the usual topology, the limit points include everything \textbf{except} $2$.
%\end{example}

%%%%%%%%%%%%%%%%%%%%
%\begin{theorem}
%%Let $(X,\tau)$ be a topological space and let $E \subseteq X$. Then
%\[
%\overline{E} = E \cup \{\text{the cluster points of }E\}.
%\]
%\end{theorem}

%\begin{proof}
%Suppose that $x\notin\overline{E}$.
%In particular we have that $x \notin E$.
%Also $X \setminus \overline{E}$ is an open n'hood of $x$, and so $x$ is not a cluster point of $E$.

%\smallskip

%Now suppose that $x\notin E \cup \{\text{the cluster points of }E\}$.
%Then there is open n'hood $U$ of $x$ such that $U\cap E = \emptyset$.
%By definition of the closure, $\overline{E}$ is contained in the closed set $X \setminus U$.  Hence $x\notin\overline{E}$.
%\end{proof}

\subsection*{Uniqueness of limits and Hausdorff spaces}
The following example shows that limits of sequences in a topological space may no longer be unique.
\begin{example}
    
Consider $X=\{a,b,c\}$ and
$\tau=\{ \emptyset, X, \{a,b\}\}$. It is routine to check that $\tau$ is a topology on $X$.
Define the sequence
\[
x_n = \begin{cases}
a & n \hbox{ is even},\\
b & n \hbox{ is odd}.
\end{cases}
\]
Then we have
\begin{enumerate}
    \item $x_n\rightarrow a$ because whenever $A\subseteq X$ is a neighbourhood of $a$, then it must contain $\{a,b\}$. But then $x_n\in \{a,b\}\subseteq A$ for all $n\in \mathbb N$, and
    \item $x_n\rightarrow b$ because whenever $B\subseteq X$ is a neighbourhood of $b$, then it must contain $\{a,b\}$. But then $x_n\in \{a,b\}\subseteq B$ for all $n\in \mathbb N$.
\end{enumerate}
\end{example}

The problem in this minimal example is that there are not enough open sets to distinguish the points $a$ and $b$, i.e. we cannot find any neighbourhood of $a$ that does not also contain $b$ and vice versa.
Now that we have isolated the problem, the following definition will hopefully seem reasonable:

\begin{definition}
    Let $(X,\tau)$ be a topological space. Then $(X,\tau)$ is called a \textbf{Hausdorff space} (also $T_2$ space) if for any two distinct points $x,y\in X$ there exist open sets $U,V\in \tau$ such that $x\in U$, $y\in V$, and  $U\cap V=\emptyset$.
\end{definition}
The definition says that in a Hausdorff space any two distinct points can be separated by (open) neighbourhoods. It means that the topology contains enough information about $X$ to distinguish between distinct elements.

\begin{examples}
\begin{enumerate}
    \item Let $X$ be a set with at least two points. Then the trivial topology $\tau=\{\emptyset, X\}$ is \textbf{not} a Hausdorff topology.
    \item Let $X$ be any set equipped with the discrete topology $\tau=\mathcal{P}(X)$. Then $(X,\tau)$ is a Hausdorff space since the singleton set $\{x\}$ is itself a neighbourhood of $x$.
    \item Let $(X,d)$ be a metric space. Then $(X,\tau_d)$ is a Hausdorff space. Indeed, if $x\neq y$ then $d(x,y)>0$. So if we set $\varepsilon:=d(x,y)/2$, then $U_\varepsilon (x)\cap U_{\varepsilon}(y)=\emptyset$.
    \item The space $\mathcal{F}(\mathbb R)$ with the topology of pointwise convergence is a Hausdorff space. If $f\neq g$, then there exists a point $x\in \mathbb R$ such that $f(x)\neq g(x)$. Let $\varepsilon:=\frac{\vert f(x)-g(x)\vert}{2}$. Then 
    $$U_\varepsilon(f;x)\cap U_{\varepsilon}(g;x)=\emptyset.$$
    \end{enumerate}
\end{examples}
We have the following important result:

\begin{theorem}
    Let $X$ be a first-countable topological space. Then the following are equivalent:
    \begin{enumerate}
        \item $X$ is a Hausdorff space;
        \item every convergent sequence in $X$ has a unique limit.
    \end{enumerate}
\end{theorem}
\begin{proof}

    Suppose first that $X$ is a Hausdorff space. Let $(x_n)_n$ be a net in $X$ such that $x_n\rightarrow x$ and $x_n\rightarrow y$. Suppose for contradiction, that $x\neq y$. Then the Hausdorff property lets us find neighbourhoods $U$ of $x$ and $V$ of $y$ such that $U\cap V=\emptyset$. On the other hand, since $x_n\rightarrow x$, there exists $n_0$ such that $x_n\in U$ for all $n\geq n_0$. Similarly, since $x_n\rightarrow y$ there exists $n_1$ such that $x_n\in V$ for all $n\geq n_1$. Let $N:=\max \{n_0,n_1\}$. Then $x_n\in U\cap V$ for all $n\geq N$, a contradiction to the fact that $U\cap V=\emptyset$!

    \smallskip

    Suppose now that limits of sequences in $X$ are unique. We want to show that $X$ is Hausdorff. Suppose for contradiction that there exist $x\neq y$ such that $U\cap V\neq \emptyset$ for \underline{every} neighbourhood $U$ of $x$ and every neighbourhood $V$ of $y$. To reach a contradiction, we are going to construct a sequence that converges to both $x$ and $y$.
    Using that $X$ is first countable, find a countable neighbourhood base $\mathcal{U}=\{U_1,U_2,\ldots\}$ of $x$ and $\mathcal{V}=\{V_1,V_2,\ldots\}$ one for $y$. Replacing $\mathcal{U}=\{U_1,U_2,\ldots\}$ by $\mathcal{U}'=\{U_1,U_1\cap U_2,U_1\cap U_2\cap U_3,\ldots\}$ and similarly for $\mathcal{V}$, we may assume without loss of generality that $U_{n+1}\subseteq U_n$ and $V_{n+1}\subseteq V_n$ for all $n\in \mathbb N$.
    
    By our assumption we can find an element $x_n\in U_n\cap V_n$ for every $n\in\mathbb N$. Then $(x_n)_{n\in \mathbb N}$ is a sequence in $X$ such that $x_n\rightarrow x$ and $x_n\rightarrow y$ (verify!). Contradiction!
\end{proof}
\end{document}
