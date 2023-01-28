# ml_courses
Some interesting assignments and projects I did for ML courses

### normalized_random_dot

When getting a distribution of dot products between two uniform, random, and normalized vectors, there's a trend that occurs where the variance of this distribution is $\sigma^2 = \frac{1}{n}$ where $n$ is the dimension of the vectors. Why is this?

Let's use vectors $A$ and $B$ as example, each with dimension $n$.

First we start with the definition of variance using the expectation value which is

$\text{Var}(X) = \mathbb{E}[X^2] - \mathbb{E}[X]^2$ for arbitrary $X$

Knowing the variance means we need to know these two expectation values. Since these values are all independent, then they can be treated as a linear system where $\mathbb{E}[X+Y] = \mathbb{E}[X] + \mathbb{E}[Y]$. 

With this in mind, we can now apply principals of linearity to $\text{Var}(A\cdot B)$.

First, we can trivially set $\mathbb{E}[X] = 0$ since the distributions must range from $-1$ to $1$ symmetrically due to uniformity and independence. So $\text{Var}(A\cdot B) = \mathbb{E}[(A\cdot B)^2]$.

Next, we can notice that since $A$ and $B$ are uniformly distributed unit vectors, we can set one of them as any basis vector to our liking and the distribution of $A$ would not be impacted. Letting $A = (a_1,a_2,\dots,a_n)$ and $B = (1,0,\dots,0)$, then $A\cdot B = a_1$ (wolog).

This property is important because now we can apply the top two results to see that $\text{Var}(A\cdot B) = \mathbb{E}[(A\cdot B)^2] = \mathbb{E}[a_1^2]$.

Another property we can can exploit is the dot product of the single vector with itself. Since $A$ is a unit vector, then $A\cdot A = 1$. From this, we can note that $\mathbb{E}[A\cdot A] = \mathbb{E}[1] = 1$ and that $\mathbb{E}[A\cdot A] = \mathbb{E}(\sum^na_i^2)$. The second relation can be further extended by invoking the linearity of $\mathbb{E}$ as stated on the top then uniformity and independence (iid) of each dimensional term, so $\mathbb{E}[\sum^na_i^2] = \sum^n\mathbb{E}[a_i^2] = n\mathbb{E}[a_i^2] = n\mathbb{E}[a_1^2]$.

Finally, this can all be combined to show that $\text{Var}(A\cdot B) = \mathbb{E}[a_1^2] = \frac{1}{n}\mathbb{E}[A\cdot A] = \frac{1}{n} = \sigma^2$.

Then taking the square root, we get the standard deviation $\sigma = \frac{1}{\sqrt{n}}$

How can this be shown computationally? We can do this by looking at this in terms of its geometric or algebreic significance.

Algebrically, if we let $A = (a_1,\dots,a_n)$ and $B = (b_1,\dots,b_n)$, then $(A\cdot B)^2 = (\sum(a_ib_i))^2 = \sum a_i^2 + \sum b_i^2 + 2\sum \sum a_i b_j$. Putting this into the expectation value, we can see that all the complicated terms go to 0 since they're expectation values of single variables. This makes $\mathbb{E}[(A\cdot B)^2] = \sum a_i^2 + \sum b_i^2. = \sum(a_i^2 + b_i^2)$. Since each term is uniformly identical, we can treat them as the same so it equals $\mathbb{E}[n(a_i^2 + b_i^2)] = n\mathbb{E}[a_i^2 + b_i^2]$. And the rest copies the previous proof.

Geometrically is harder. We'll have to use hyperspheres. But if we keep this at low dimensions, we can directly compute with simple knowledge of calculus.

2D Case. Let $A$ and $B$ be normalized vectors. $A\cdot B = |A||B|\cos\theta = \cos\theta$ on a 2D unit circle. Therefore $\text{Var}(A\cdot B) = \mathbb{E}[\cos^2\theta] - \mathbb{E}[\cos\theta]^2 = \frac{1}{2\pi}\int^{2\pi}_{0}\cos^2\theta\,d\theta - \frac{1}{2\pi}\int^{2\pi}_{0}\cos\theta\,d\theta = \frac{1}{2} - 0 = \frac{1}{2}$. Then $\sigma = \sqrt{\text{Var}} = \frac{1}{\sqrt{2}}$.

3D Case. Using the same argument, this is now 3D so all the possible vector combinations will lie on a 3D unit sphere. $\text{Var}(A\cdot B) = \mathbb{E}[\cos^2\theta] - \mathbb{E}[\cos\theta]^2 = \frac{1}{4\pi}\int^{\pi}_{0}\cos^2\theta\sin\theta\,d\theta\int^{2\pi}_0\,d\phi - \frac{1}{4\pi}\int^{\pi}_{0}\cos\theta\sin\theta\,d\theta\int^{2\pi}_0\,d\phi = \frac{1}{3} - 0 = \frac{1}{3}$. Then $\sigma = \sqrt{\text{Var}} = \frac{1}{\sqrt{3}}$.
