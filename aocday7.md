---
usemathjax: true
---
{% include head.html %}

# Day 7
###### Advent of Code

The problem outlined in part 1 of day 7 is to find all of the bags where the
"shiny gold" bag is some descendant of it. We can structure the input as a
directed graph, where each bag constitues a vertex $$v$$ and there is an edge <span>$$(v,
v_k)$$</span> whenever <span>$$v$$</span> *contains* <span>$$v_k$$</span>. This produces a directed graph <span>$$G = (V,
E)$$</span>. A bag, call this vertex <span>$$b$$</span>, can then contain at least one "shiny gold"
bag, call this vertex <span>$$s$$</span>, if there exists a path <span>$$b \leadsto s$$</span>. The job of the
programmer is then to find out just how many <span>$$v \in V$$</span> have a path <span>$$v \leadsto
s$$</span>. We may also find it convenient to weight the edges by the quantity being
contained.

The simplest solution for this would be to take $$G^T$$ and run a BFS from the
source $$s$$, counting all the ancestors encountered. This will give us the
desired results since all vertices where there previously existed a path $$v
\leadsto s$$, there will now exist the path $$s \leadsto v$$, which means they will
all be counted after the BFS is run.

For part 2, a similar logic applies. Instead of running the BFS on $$G^T$$, we
instead run a DFS on $$G$$, additionally we keep an auxialiary stack $$A$$ for maintaining the
overall weight that has been calculated. When a vertex $$v_i$$ has begun being explored,
$$w_i = w(v_i.\pi, v_i)$$ is pushed onto $$A$$. It then queues each of the bags it
contains $$b_1, \dots, b_n$$ for DFS traversal. When $$v_i$$ is ending its
exploration, it pops and adds the weights $$w_b = \sum_{j=1}^n w(v_i, b_j)$$ from
the top of the stack, then appends the value $$w_i + (w_i * w_b)$$ to $$A$$, as was
specified by the problem description. This then gives us the amount of
individual bags required inside of the "shiny gold" bag.

Thanks for reading!
