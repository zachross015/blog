{% include head.html %}

# Day 7
###### Advent of Code

## Theory

The problem outlined in part 1 of day 7 is to find all of the bags where the
"shiny gold" bag is some descendant of it. We can structure the input as a
directed graph, where each bag constitues a vertex $$v$$ and there is an edge $$(v,
v_k)$$ whenever $$v$$ *contains* $$v_k$$. This produces a directed graph $$G = (V,
E)$$. A bag, call this vertex $$b$$, can then contain at least one "shiny gold"
bag, call this vertex $$s$$, if there exists a path $$b \leadsto s$$. The job of the
programmer is then to find out just how many $$v \in V$$ have a path $$v \leadsto
s$$. We may also find it convenient to weight the edges by the quantity being
contained.

The simplest solution for this would be to take $$G^T$$ and run a either a BFS
or a DFS from the source $$s$$, counting all the unique ancestors encountered.
This will give us the desired results since all vertices where there previously
existed a path $$v \leadsto s$$, there will now exist the path $$s \leadsto v$$,
which means they will all be counted after the search is run.

For part 2, a similar logic applies. The problem for this is to instead find
amount of bags that the "shiny gold" one can hold. In this case however, it may
be simpler to run a DFS will be discussed, and we do this just on $$G$$.
Additionally we keep an auxialiary stack $$A$$ for maintaining the overall
weight that has been calculated. When a vertex $$v_i$$ has begun being explored,
$$w_i = w(v_i.\pi, v_i)$$ is pushed onto $$A$$. It then queues each of the bags
it contains $$b_1, \dots, b_n$$ for DFS traversal. When $$v_i$$ is ending its
exploration, it pops and adds the weights $$w_b = \sum_{j=1}^n w(v_i, b_j)$$
from the top of the stack, then appends the value $$w_i + (w_i * w_b)$$ to
$$A$$, as was specified by the problem description. This then gives us the
amount of individual bags required inside of the "shiny gold" bag.

DFS is more important for this problem since we need to know the value of a vertex
prior to adding it to its parent. For example, if we tried to run BFS with this
stack idea, the auxiliary stack would be a jumble of different weights that all
corresponded to different parents, which would simply not do.

## Program

Thanks for reading!
