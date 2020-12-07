# Day 7
###### Advent of Code

The problem outlined in part 1 of day 7 is to find all of the bags where the
"shiny gold" bag is some descendant of it. Since the data we are working with is
assumed to be directed and acylcic, the most optimal solution would be to
perform either a BFS or DFS on the input data, after structuring it as a
directed graph $G = (V, E)$.
