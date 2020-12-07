# Day 7
###### Advent of Code

The problem outlined in part 1 of day 7 is to find all of the bags where the
"shiny gold" bag is some descendant of it. We can structure the input as a
directed graph, where each line constitues a vertex $v$ with out-edges $e_1, e_2,
\dots, e_n$ that indicate $v$ *contains* $v_i$ if and only if there is a path $v
\leadsto v_i$. This format creates a directed graph $G = (V, E)$. We may also
find it convenient to weight the edges so that $w(e_i)$ is the amount of bags
that $v$ contains of $v_i$.

