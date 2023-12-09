# Graphs

The idea of this project is to find the shortest way to see all the animals in a parc and come back to the entry at the end of the day. 

It's clearly a trading salesman problem but we would allow to get back to nodes we've already seen or edges (roads) we've already walked. 

The ultimate goal is to say : To see all the animals from the entry of the parc, you must see them in this order and you'll have to walk this much. 

The immediate upgrade of the problem could be adding some time constraints like queues in amusement parc like Disneyland,... or some PMR constraints for people that can't use stairs. 

The above and more general problem is to find the optimal walk on already existing edges to visit all the nodes at least once and come back to where we started. It has applications for buses, cars (Waze, maps), for planes (if we admit that the aerial traffic is already fixed) and more generally in all problems in which we wish to see all the nodes of a graph for a minimum total weight.

This will lead to the analysis of existing algorithms and upgrading of some of them hopefully. We can also explore the existing methods in packages like NetworkX or external software like concorde to see if some of them could be upgraded. 

Here's how the programm works : 

