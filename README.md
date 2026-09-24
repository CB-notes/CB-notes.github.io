<!-- HTML script to load MathJax engine on the live GitHub Pages website -->
<script type="text/javascript">
  window.MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']],
      displayMath: [['$$', '$$'], ['\\[', '\\]']]
    }
  };
</script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

***Week 1***

Metric spaces were introduced by Fréchet in his PhD dissertation in 1906. The mathematicians of that time were studying various spaces
(mainly spaces of functions) and they had various notions of
*convergence* in such spaces. For each space its own notion of
convergence was introduced, and studied. Of course, similarities were
noticed and Fréchet realised that these arguments can be unified by
introducing an abstract concept of a *metric* or *distance function*. He
could show that many of these spaces were instances of his new concept
of a metric space. Then, by proving one result axiomatically from the
metric axioms, it automatically holds for all instances.

In the modern view, the concept of a metric space is just an
axiomatisation of the notion of distance. As we will see, different
notions of distance are very important since they occur all the time in
mathematics, statistics and physics. Many geometric objects rely on a
notion of distance (e.g. the unit sphere in $\mathbb R^n$ is exactly the
set of points at distance $1$ from the origin). So, it is natural to
distil some common properties of distances in various contexts and set
them as axioms.

As already mentioned above, distance plays a fundamental role in the
definition of convergence. Let us recall that definition from calculus:

**Definition 1**. Let $(x_n)_n$ be a sequence of real numbers and
$x\in \mathbb R$. Then $(x_n)_n$ **converges to $x$**, if for every
$\varepsilon>0$ there exists an $N\in \mathbb{N}$ such that
$\vert x-x_n\vert<\varepsilon$ for all $n\geq N$.

In other words: for every error tolerance (the $\varepsilon$) the
*distance* between $x_n$ and $x$ is eventually (i.e. past the the index
$N$) less than the error tolerance.

Our first goal is to formalise the concept of *distance*. This is the
content of the following definition:

**Definition 2**. Let $X$ be a non-empty set. A **metric** (or distance
function) on $X$ is a function
$$d \colon X \times X \to \mathbb R, \ (x,y)\mapsto d(x,y)$$ satisfying
the following three properties:

1.  $d(x,y) = 0$ if and only if $x=y$;

2.  $d(x,y) = d(y,x)$ for all $x,y \in X$;

3.  $d(x,y) \leq d(x,z) + d(z,y)$ for all $x,y,z \in X$.

The pair $(X,d)$ is called a **metric space**.

Let us record a few remarks on the axioms in the definition above:

-   (M1) says that each point has zero distance from itself, and that
    distinct points must have a non-zero distance.

-   (M2) says that the distance from $x$ to $y$ is the same as the
    distance from $y$ to $x$. We say that $d$ is **symmetric**.

-   (M3) is called the **triangle inequality** and gets its name from
    the fact that the length of any side of a triangle is at most the
    sum of the lengths of the other two sides. It says that a journey
    from $x$ to $y$ doesn't get any shorter if you take a detour via
    $z$, but may possibly get longer.

-   We can combine the axioms to prove that the distance between any two
    points must be non-negative: indeed, for all $x,y\in X$ we have
    $$2d(x,y)=d(x,y)+d(x,y)\stackrel{(M2)}{=}d(x,y)+d(y,x)\stackrel{(M3)}{\geq} d(x,x)\stackrel{(M1)}{=}0,$$
    so dividing by $2$ gives $d(x,y)\geq 0$.

Let us now consider some examples:

**Example 3** (Euclidean space). The first example is the
$n$-dimensional **Euclidean space** $(\mathbb R^n, d_2)$ where for two
points $x=(x_1,\ldots, x_n)$ and $y=(y_1,\ldots, y_n)$ in $\mathbb R^n$
we define their **Euclidean distance** by
$$d_2(x,y) := \sqrt{\sum_{i=1}^n (x_i-y_i) ^2}.$$

It is easy to see that $(M1)$ and $(M2)$ are satisfied. To see that
$(M3)$ holds let $z=(z_1,\ldots, z_n)$ be a third point in
$\mathbb R^n$. Then writing out the inequality
$d_2(x,z)\leq d_2(x,y) + d_2(y,z)$ we have to prove
$$\sqrt{\sum_{i=1}^n (x_i-z_i) ^2}\leq \sqrt{\sum_{i=1}^n (x_i-y_i) ^2}+\sqrt{\sum_{i=1}^n (y_i-z_i) ^2}$$
To simplify things introduce auxiliary variables $r_i:=x_i-y_i$ and
$s_i:=y_i-z_i$. Plugging these in, the above inequality becomes
$$\sqrt{\sum_{i=1}^n (r_i+s_i) ^2}\leq \sqrt{\sum_{i=1}^n r_i^2}+\sqrt{\sum_{i=1}^n s_i^2}$$
Since both sides arc non-negative, it is equivalent (squaring both
sides) to prove
$$\sum_{i=1}^n r_i^2 + 2\sum_{i=1}^n r_is_i+ \sum_{i=1}^n s_i^2\leq \sum_{i=1}^n r_i^2+ 2\sqrt{\sum_{i=1}^n r_i^2}\sqrt{\sum_{i=1}^n s_i^2}+\sum_{i=1}^n s_i^2,$$
which we can simplify to
$$\sum_{i=1}^n r_is_i\leq \sqrt{\sum_{i=1}^n r_i^2}\sqrt{\sum_{i=1}^n s_i^2}.$$
Squaring this again we arrive at Cauchy's inequality
$$\left(\sum_{i=1}^n r_is_i\right)^2\leq \left(\sum_{i=1}^n r_i^2\right)\left(\sum_{i=1}^n s_i^2\right)$$
which is known to hold for all $n$-tuples of real numbers
$(r_1,\ldots, r_n)$ and $(s_1,\ldots, s_n)$.
:::

**Example 4**. Besides the Euclidean distance $d_2$ discussed above,
there are many other choices of metric we can put on the $n$-dimensional
real vector space $\mathbb R^n$. Let us give two more such examples: for
two points $x=(x_1,\ldots, x_n)$ and $y=(y_1,\ldots, y_n)$ in
$\mathbb R^n$ we define their **taxicab distance** $d_1$ by
$$d_1(x,y) := \sum_{i=1}^n \vert x_i-y_i\vert.$$

Another metric is the **maximum metric** $d_\infty$, which just measures
the distance coordinate-wise and then returns the maximal value:
$$d_\infty(x,y)=\max\{\vert x_i-y_i\vert\mid 1\leq i\leq n\}.$$

**Example 5**. Let $X=\mathbb C^n$. Then we can define a metric on $X$
by setting $$d(z,w)=\sqrt{\sum_{i=1}^n \vert z_i-w_i\vert^2}$$ When we
express each entry of the complex tuple in terms of its real and
imaginary parts, the triangle inequality for $\mathbb C^n$ coincides
with the one for $(\mathbb R^{2n},d_2)$ discussed above.



**Example 6** (Discrete metric). On any set $X \neq\emptyset$ the
function $$d(x,y) =
\begin{cases}
    1 & \hbox{ if } x \neq y, \\
    0 & \hbox{ if } x = y
\end{cases}$$ defines a metric called the **discrete metric**. Such
'pathological' examples, as they are nicknamed, are not normally used in
applications in analysis. They serve as a warning to check by rigorous
proofs that results suggested by intuition really hold in general metric
spaces. In other words, they are potential counterexamples; they explore
the boundaries of the concept of a metric space.



**Example 7**. On the complex plane $\mathbb{C}$ the **French Railway
metric** is given as $$d_{f}(z_{1},z_{2})=\begin{cases}
    0 & \hbox{if } z_{1}=z_{2},\\
|z_{1}|+|z_{2}| & \hbox{if } z_{1}\neq z_{2}
\end{cases}$$ is a metric (folklore suggests that the shortest rail
journey between any two French towns is via Paris).



**Example 8** (Metric Subspaces). If $(X,d)$ is a metric space and
$Y\subseteq X$ is a subset of $X$, then we can define the **induced
metric** $d_Y$ on $Y$ as the restriction of $d$ to
$Y\times Y\subseteq X\times X$, i.e. $d_Y(x,y)=d(x,y)$ for all
$x,y\in Y$.


If these were the only examples of metric spaces it is doubtful whether
general metric space theory would be worthwhile. The examples below
indicate the wide range of metric space theory (but do not exhaust it).


**Example 9**. The following metric plays an important role in number
theory. Let $p$ be a fixed prime number. Define a metric
$$d_p:\mathbb Z\times \mathbb Z\to \mathbb R$$ by setting $d(m,m)=0$ and
for $n\neq m$ set $d(m,n)=1/r$ where $p^{r-1}$ is the highest power of
$p$ which divides $m-n$.



**Example 10** (The word metric on a finitely generated group). This
example will only make sense if you know about groups and generating
sets. Suppose $G$ is a finitely generated group and $S$ is a generating
set for $G$. That is every element $g\in G$ can be written as a product
$g=g_1\cdots g_n$ of elements in $S$ (and their inverses). The shortest
way to write $g$ in this way is called the length of $g$, denoted by
$l(g)$. Now we can define the word-metric on $G$ by setting
$d(g,h)=l(g^{-1}h).$

**Example 11** (Geodesic distance on a graph). Let $(V,E)$ be a
connected graph (undirected, without multiple edges between vertices),
with vertex set $V$ and edge set $E$. Then we can define a metric on $V$
by letting $d(v,w)$ be the length of the shortest path between the two
vertices $v$ and $w$. This metric is important in the study of networks.

**Example 12** (Hamming distance). Let $\Sigma=\{a,b,c,\ldots, z\}$ be
the modern Latin alphabet. Let $X$ be the set of all strings of letters
in $\Sigma$ of length 4 (e.g. $abcd$ is an element in $X$, so are $math$
or $iosk$). The **Hamming distance** $d_H$ between two strings in $X$ is
the number of positions at which the corresponding symbols are
different. In other words, it measures the minimum number of
substitutions required to change one string into the other. One can
check that $d_H$ is indeed a metric on $X$. A major application of the
Hamming distance is in coding theory.

Let us now also introduce a couple of the *function spaces* that
motivated Fréchet to study metric spaces in the first place. These will
be studied in much more detail in Linear Analysis, so we keep our
discussion here brief.


**Example 13** (Uniform metric). Let $A\neq \emptyset$ be a set. A
function $f:A\rightarrow \mathbb R$ is called **bounded**, if there
exists a constant $C>0$ such that $\vert f(a)\vert\leq C$ for all
$a\in A$. Let $\ell^\infty (A)$ denote the set of all such bounded,
complex valued functions on $A$. Then for $f,g\in \ell^\infty(A)$ we can
define $$d_\infty(f,g) := \sup_{a\in A} \vert f(a)-g(a)\vert.$$ We leave
it as an exercise to show that this is indeed a metric.


**Example 14** ($L^1$ metric). Let $C[a,b]$ denote the set of all
continuous functions $f:[a,b]\to \mathbb R$. Then we can define a metric
$d_1$ on $C[a,b]$ by setting
$$d_1(f,g):=\int_a^b \vert f(x)-g(x)\vert \ \mathrm d x.$$



**Example 15** ($L^2$ metric). Let $C[a,b]$ denote the set of all
continuous functions $f:[a,b]\to \mathbb R$. Then we can define a metric
$d_2$ on $C[a,b]$ by setting
$$d_2(f,g):=\left( \int_a^b (f(x)-g(x))^2 \ \mathrm d x\right)^\frac{1}{2}.$$

***Week 2: Sequences and convergence in metric spaces***

Now that we have formalised the notion of distance and a lot of examples
to play with we can define convergence of sequences in any metric space:


**Definition 1**. Let $(X,d)$ be a metric space and
$(x_n)_{n\in \mathbb N}$ a sequence in $X$. We say that
$(x_n)_{n\in \mathbb N}$ **converges to $x$** (shorthand notation
$x_n\rightarrow x$, or $\lim_{n\rightarrow \infty} x_n=x$) if for every
$\varepsilon>0$ there exists an $N\in\mathbb N$ such that
$d(x_n,x)<\varepsilon$ for all $n\geq N$.


Given a sequence $(x_n)_{n\in \mathbb N}$ in $X$ and $x\in X$ we can
consider the sequence of distances $(d(x_n,x))_{n\in \mathbb N}$ in
$[0,\infty)$. Comparing the definition above with the one from the intro
it is clear that $(x_n)_{n\in \mathbb N}$ converges to $x$ in $(X,d)$ if
and only if the sequence of distances $(d(x_n,x))_{n\in \mathbb N}$
converges to $0$ in the usual sense of convergence of sequences of real
numbers!

We want to observe that if a sequence in a metric space converges, then
its limit is unique. It might come as a surprise why this requires a
proof at all, but we will later (in a more general context) see that
this is indeed an important feature of metric spaces.

**Lemma 2**. *Let $(X,d)$ be a metric space and $(x_n)_{n\in \mathbb N}$
be a sequence in $X$ and $x,y\in X$. If $x_n\rightarrow x$ and
$x_n\rightarrow y$, then $x=y$.*

*Proof.* Observe first that the conclusion $x=y$ is equivalent to
$d(x,y) <\varepsilon$ for all $\varepsilon>0$. Thus, it suffices to show
the latter. So let $\varepsilon>0$ be given. Then there exist
$N_1,N_2\in \mathbb N$ such that $d(x_n,x)<\frac{\varepsilon}{2}$ for
all $n\geq N_1$ and $d(x_n,y)<\frac{\varepsilon}{2}$ for all
$n\geq N_2$. Let $N:=\max \{N_1,N_2\}$. Then using the
triangle-inequality (M3) we have
$$d(x,y)\leq d(x,x_N)+d(x_N,y)<\varepsilon$$ Since $\varepsilon$ was
aribtrary it follows that $d(x,y)=0$ and hence $x=y$ by axiom (M1). ◻


Note also that this result justifies the notation
$\lim_{n\rightarrow \infty} x_n$ for the limit.

From real analysis we know a lot of tools to check if a sequence in
$\mathbb R$ converges, but checking if a sequence in a given metric
space converges seems like a much more daunting task. It is helpful to
observe that some metrics have the same convergent sequences. If that is
the case, we can just chose the one that seems easier to us to check
convergence. Formally we make the following definition:


**Definition 3**. Two metrics $d$ and $d'$ on a set $X$ are **Lipschitz
equivalent** if there are constants $C,D>0$ such that
$$d(x,y)\leq Cd'(x,y)\ \hbox{ and }\ d'(x,y) \leq D d(x,y)$$ for all
$x,y\in X$.



**Example 4**. The metrics $d_1, d_2$, and $d_\infty$ on $\mathbb R^n$
are pairwise Lipschitz equivalent. The proof proceeds in several steps.

1.  For all $x=(x_{1},x_{2},\ldots,x_{n})$ and
    $y=(y_{1},y_{2},\ldots,y_{n})$ in $\mathbb R^{n}$, we have
    $$d_\infty(x,y)=\max\{|x_{i}-y_i|:1\leq i\leq n\}
    \leq\sum_{i=1}^{n}|x_{i}-y_i|=d_1(x,y)$$ and
    $$d_1(x,y)=\sum_{i=1}^{n}|x_{i}-y_i|
    \leq \sum_{i=1}^{n}\max\{|x_{i}-y_i|:1\leq i\leq n\}
    =\sum_{i=1}^{n} d_\infty(x,y)
    =n \cdot d_\infty(x,y).$$ In conclusion we have
    $d_\infty(x,y)\leq d_1(x,y)\leq nd_\infty(x,y)$ for all
    $x,y\in \mathbb R^n$. Thus, the metrics $d_1$ and $d_\infty$ are
    Lipschitz equivalent.

2.  For all $x=(x_{1},x_{2},\ldots,x_{n})$ in $\mathbb R^{n}$, we have
    $$d_\infty(x,y)^2
    =\left(\max\{|x_{i}-y_i|:1\leq i\leq n\}\right)^2
    \leq\sum_{i=1}^{n}|x_{i}-y_i|^{2}=d_2(x,y)^2,$$ and
    $$d_2(x,y)^2=\sum_{i=1}^{n}|x_{i}-y_i|^{2}
    \leq\sum_{i=1}^{n}\max\{|x_{i}-y_i|^{2}:1\leq i\leq n\}
    =n\cdot d_\infty(x,y)^2.$$ Thus, taking square roots throughout we
    get
    $$d_\infty(x,y)\leq d_2(x,y)\leq \sqrt{n}d_\infty(x,y) \ \forall x,y\in \mathbb R^n.$$

3.  Combining (1) and (2) we can also prove that $d_1$ and $d_2$ are
    Lipschitz equivalent since for all $x,y\in \mathbb R^n$ we have
    $$d_1(x,y)\stackrel{(1)}{\leq} nd_\infty(x,y)\stackrel{(2)}{\leq} nd_2(x,y)\stackrel{(2)}{\leq}n\sqrt{n}d_\infty(x,y)\stackrel{(1)}{\leq}n\sqrt{n}d_1(x,y).$$



**Proposition 5**. *If $d$ and $d'$ are Lipschitz equivalent metrics on
$X$, and $(x_n)_{n\in \mathbb N}$ is a sequence in $X$, then
$x_n\rightarrow x$ with respect to $d$ if and only if $x_n\rightarrow x$
with respect to $d'$.*



*Proof.* The statement is clearly symmetric, so we only have to prove
one direction and the other will work in exactly the same way with the
roles of $d$ and $d'$ exchanged.

So suppose that $x_n\to x$ with respect to $d$. We want to show that
$x_n\to x$ with respect to $d'$. In order to verify the definition we
fix an arbitrary tolerance $\varepsilon>0$. We also know that $d$ and
$d'$ are Lipschitz equivalent. So let us fix a $D>0$ such that
$$d'(x,y)\leq D d(x,y) \ \forall x,y\in X.$$

Since $x_n\to x$ with respect to $d$ we know that there must exist an
$N\in \mathbb N$ such that $d(x_n,x)<\varepsilon/D$ for all $n\geq N$.
Thus, for all $n\geq N$ we have
$$d'(x_n,x)\leq D\cdot d(x_n,x)<D \cdot \varepsilon/D=\varepsilon$$ as
desired. ◻



**Example 6**. Let $C[0,1]$ be the set of all continuous real-valued
functions defined on the closed interval $[0,1]$, and consider the
metrics
$$d_\infty(f,g)=\sup\{|f(x)-g(x)|:0\leq x\leq 1\} \hbox{ and }  d_1(f,g)=\int_{0}^{1}\vert f(x)-g(x)\vert \ dx$$
on $C[0,1]$. Then $d_{\infty}$ and $d_{1}$ are NOT Lipschitz equivalent.

1.  The inequality $d_1(f,g)\leq d_\infty(f,g)$ still holds as in the
    discrete setting: by definition of $d_\infty$, for all
    $x \in [0,1]$,
    $$\vert f(x)-g(x)\vert  \leq \sup_{y \in [0,1]} |f(y)-g(y)|= d_\infty(f,g).$$
    Hence by integration theory,
    $$d_1(f,g)=\int_{0}^{1} \vert f(x)-g(x)\vert dx \leq \int_{0}^{1}d_\infty(f,g)\ dx = d_\infty(f,g).$$

2.  The other direction however fails: for any $n\in \mathbb N$,
    consider the continuous function $$g_{n}(t)=\left\{\begin{array}{lc}
    -nt +1 & \hbox{ if } t \in [0, \frac{1}{n}], \\
    0 & \hbox{ if } t \in [\frac{1}{n},1], \end{array}\right\}$$ The
    graph of $g_n$ is the union of the line segments connecting $(0,1)$
    with $(\frac{1}{n},0)$ and $(\frac{1}{n},0)$ with $(1,0)$. Then it
    is easy to see that
    $$d_1(g_n,0)=\int_{0}^{1}|g_{n}(x)|dx = \int_{0}^{\frac{1}{n}} (-nt +1)dt = \left[-\frac{n}{2}t^2+t\right]_{0}^{\frac{1}{n}}=\frac{1}{2n}$$
    and that $$d_\infty(g_n,0)=\sup_{t \in [0,1]}|g_{n}(t)| = 1.$$

    Suppose for contradiction, that there exists a constant $C>0$ such
    that $d_\infty \leq C d_1$. Then for all $n\in \mathbb N$ we would
    have $$1=d_\infty(g_n,0) \leq C d_1(g_n,0)=C \frac{1}{2n},$$ a
    contradiction.



**Exercise 7**. Consider the metrics $d_1,d_2,d_\infty$ on $\mathbb R^m$
from week 1. Show that a sequence $(x_n)_{n\in \mathbb N}$ in
$\mathbb R^m$ converges to $x=(x(1),\ldots, x(m))\in\mathbb R^m$ with
respect to $d_i$ if and only if for all $1\leq i\leq m$ the sequence of
the $i$-th entries $(x_n(i))_{n\in \mathbb N}$ converges to $x(i)$ in
$\mathbb R$.
:::

## Cauchy sequences {#cauchy-sequences .unnumbered}

Here is another useful concept that can be carried over from real
analysis without any trouble.


**Definition 8**. Let $(X,d)$ be a metric space. A sequence
$(x_n)_{n\in \mathbb N}$ in $X$ is called a **Cauchy sequence** if for
all $\varepsilon>0$ there exists an $N\in \mathbb N$ such that
$d(x_n,x_m)<\varepsilon$ for all $n,m\geq N$.
:::

The proofs of the following two elementary facts about Cauchy sequences
are also almost exactly the same as in calculus:


**Lemma 9**. *Let $(X,d)$ be a metric space.*

1.  *Every convergent sequence in $X$ is a Cauchy sequence.*

2.  *Every Cauchy sequence in $X$ is bounded.*



*Proof.*

1.  Let $(x_n)_{n\in \mathbb N}$ be a convergent sequence with limit
    $x\in X$. Let furthermore $\varepsilon >0$ be given. Since
    $(x_n)_{n\in \mathbb N}$ converges to $x$, there exists an
    $N\in \mathbb N$ such that $d(x_n,x)<\varepsilon/2$ for all
    $n\geq N$. Using the triangle-inequality (M3) it follows that for
    all $n,m\geq N$ we have
    $$d(x_n,x_m)\leq d(x_n,x)+d(x,x_m)<\varepsilon/2 + \varepsilon/2 =\varepsilon.$$

2.  Let $(x_n)_{n\in \mathbb N}$ be a Cauchy sequence. We need to show
    that there exists a number $D\geq 0$ such that $d(x_n,x_m)\leq D$
    for all $n,m\in \mathbb N$. Since $(x_n)_{n\in \mathbb N}$ is
    Cauchy, for $\varepsilon=1$ there exists an $N\in \mathbb N$ such
    that $d(x_n,x_m)\leq 1$ for all $n,m\geq N$. Hence $1$ works as an
    upper bound for the sequence $x_N,x_{N+1},x_{N+2},\ldots$. Moreover,
    by the triangle inequality we have
    $$d(x_1,x_n)\leq d(x_1,x_N)+d(x_N,x_n)\leq d(x_1,x_N)+1 \ \forall n\geq N.$$
    Similarly for $x_2, x_3,\ldots, x_{N-1}$.

    So if we set $\Tilde{D}=\max\{d(x_i,x_N)\mid 1\leq i\leq N-1\} +1$,
    then this almost works. The only distances we have not yet taken
    care of are the distances $d(x_i,x_j)$ when $1\leq i,j\leq N-1$. But
    notice that by the triangle inequality (M3) again we have

    $$d(x_i,x_j)\leq d(x_i,x_N)+d(x_N,x_j)\leq 2\Tilde{D}.$$

    So if we set $D:=2\Tilde{D}$, then $d(x_n,x_m)\leq D$ for all
    $n,m\in \mathbb N$.

 ◻


The converse of (1) it not true as the following familiar example shows:


**Example 10**. Consider the space $X=\mathbb Q$ with the standard
metric $d(x,y)=\vert x-y\vert$. Define a sequence $(x_n)_n$ by $x_1=1$
and $x_{n+1}=x_n/2+1/x_n$. Clearly, $x_n\in \mathbb Q$ for all
$n\in \mathbb N$. We claim that the sequence converges, but only in the
bigger set $\mathbb R$. Note that
$$x_n-x_{n+1}=x_n-\frac12\Bigl(x_n+\frac 2{x_n}\Bigr)=\frac1{2x_n}(x_n^2-2).$$
Focussing on the second factor we have $$\begin{aligned}
x_n^2-2
    &=\frac14\Bigl(x_{n-1}+\frac 2{x_{n-1}}\Bigr)^2-2\\
    &=\frac{x_{n-1}^2}4-1+\frac{2^2}{4x_{n-1}^2}\\
    &=\frac14\Bigl(x_{n-1}^2-4+\frac{2^2}{x_{n-1}^2}\Bigr)\\
    &=\frac{1}{4}\Bigl(x_{n-1}-\frac 2{x_{n-1}}\Bigr)^2\\
    &\ge0.
\end{aligned}$$ It follows that $(x_n)_n$ is decreasing and bounded
below. Thus, the Monotone Convergence Theorem (from Stage 1 Real
Analysis!) that the sequence converges to a point $x\in \mathbb R$.
Using the algebra of limits, the point $x$ must satisfy $x=x/2 + 1/x$
which gives $x=\sqrt{2}$. Since the sequence is convergent, it must be a
Cauchy sequence. So we have found a Cauchy sequence in $\mathbb Q$ which
does not converge in $\mathbb Q$.


The observation that Cauchy sequences do not necessarily converge in
every metric space is a first major difference to what we know about
sequences in $\mathbb R$. Thus, we see that "all Cauchy sequences
converge\" is a property of a metric space, not an intrinsic feature.
Since it is a very useful property, we give it a name:


**Definition 11**. A metric space $(X,d)$ is called **complete** if
every Cauchy sequence in $X$ converges in $X$.


From Calculus we know that $\mathbb R$ is complete. In fact this is the
fundamental property that distinguishes $\mathbb R$ from $\mathbb Q$!
Using this we can also show that higher dimensional Euclidean space is
complete:


**Example 12**. $(\mathbb R^k,d_2)$ is complete for all
$k\in \mathbb N$. Consider a Cauchy sequence $(x_n)_{n\in \mathbb N}$ in
$\mathbb R^k$. Note that $x_n\in \mathbb R^k$ for each $n\in \mathbb N$,
i.e. $x_n$ is a vector with $k$ entries. We will write
$x_n=(x_n(1),x_n(2),\ldots, x_d(k))$. Fix $i\in \{1,\ldots, k\}$. Then
for each $x_n$ we look at it's $i$-th entry. This gives us a sequence
$(x_n(i))_{n\in \mathbb N}$ in $\mathbb R$. We claim that this is a
Cauchy sequence in $\mathbb R$. Indeed, let $\varepsilon >0$ be given.
Since $(x_n)_n$ is a Cauchy sequence, there exists an $N\in \mathbb N$
such that $d_2(x_n,x_m)<\sqrt{\varepsilon}$ for all $n,m\geq N$. But
then for all $n,m\geq N$ we have
$$\vert x_n(i)-x_m(i)\vert ^2\leq \sum_{i=1}^d \vert x_n(i)-x_m(i)\vert ^2=d_2(x_n,x_m)^2<\varepsilon.$$
Thus our claim follows. Using that $\mathbb R$ is complete, for each
$i$, the sequence $(x_n(i))_{n\in \mathbb N}$ converges to some
$x(i)\in \mathbb R$. Setting
$x:=(x(1),x(2),\ldots, x(d))\in \mathbb R^d$ we conclude that
$x_n\rightarrow x$ by Exercise
[7](#Exercise:Norm implies entrywise for 1-norm){reference-type="ref"
reference="Exercise:Norm implies entrywise for 1-norm"}. Thus we have
shown that every Cauchy sequence in $\mathbb R^k$ converges.


The following result shows that completeness is preserved under
Lipschitz equivalence. We leave the proof as an exercise!


**Proposition 13**. *Let $d$ and $d'$ be Lipschitz-equivalent metrics on
$X$. Then $(X,d)$ is complete if and only if $(X,d')$ is complete.*


