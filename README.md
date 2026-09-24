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

