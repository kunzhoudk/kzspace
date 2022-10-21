# Distance from a point to a line
The distance between a point and a line, is defined as the shortest distance between a fixed point and any point on the line. It is the length of the line segment that is perpendicular to the line and passes through the poin.

<div style="text-align:center"><img src="./images/Vectorpoint-to-line.png" /></div>

Let $P$ be the point with coordinates $(x_{0}, y_{0})$ and let the given line have equation $ax + by + c = 0$. Also, let $Q = (x_{1}, y_{1})$ be any point on this line and $n$ the vector $(a, b)$ starting at point $Q$. The vector $n$ is perpendicular to the line, and the distance $d$ from point $P$ to the line is equal to the length of the orthogonal projection of $\overrightarrow{QP}$ on $n$. Thus we have from trigonometry:

$$
d= \lVert \overrightarrow{QP} \rVert cos\theta 
$$

Now, multiply both the numerator and the denominator of the right hand side of the equation by the magnitude of the normal vector $\overrightarrow{n}$:

$$
d= \frac{\lVert \overrightarrow{QP} \rVert \lVert \overrightarrow{n} \rVert cos\theta }{\lVert \overrightarrow{n} \rVert}
$$

we know from the definition of dot product that $\lVert \overrightarrow{QP} \rVert \lVert \overrightarrow{n} \rVert cos\theta $ ust means the dot product of the vector $\overrightarrow{QP}$ and the normal vector  $\overrightarrow{n}$:

$$
d= \frac{ \overrightarrow{QP} \cdot \overrightarrow{n}  }{\lVert \overrightarrow{n} \rVert}
$$

$$
\overrightarrow{QP}  = (x_{0} - x_{1}, y_{0} - y_{1})
$$

so 

$$
\overrightarrow{QP} \cdot \overrightarrow{n} = (x_{0} - x_{1}, y_{0} - y_{1}) \cdot(a,b) = a (x_{0} - x_{1}) + b(y_{0} - y_{1})
$$

And we also have $\overrightarrow{n} = \sqrt{a^2 + b^2}$, thus 

$$
 d= \frac{\lvert a (x_{0} - x_{1}) + b(y_{0} - y_{1}) \rvert}{\sqrt{a^2 + b^2}} = \frac{\lvert a(x_{0}) -a(x_{1}) + b(y_{0}) - b(y_{1})) \rvert}{\sqrt{a^2 + b^2}}
$$

From the equation of the line ve have $c = -a(x_{1}) -b(y_{1})$, which implies 

$$
 d= \frac{\lvert a (x_{0}) + b(y_{0}) +c \rvert}{\sqrt{a^2 + b^2}}
$$

So given a line of the form $ax + by + c$ abd a point $(x_{0},y_{0})$, the perpendicular distance can be found by the above formula.


