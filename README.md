# Graphs

The idea of this project is to find the shortest way to see all the animals in a parc and come back to the entry at the end of the day. 

It's clearly a trading salesman problem but we would allow to get back to nodes we've already seen or edges (roads) we've already walked. 

The ultimate goal is to say : To see all the animals from the entry of the parc, you must see them in this order and you'll have to walk this much. 

The immediate upgrade of the problem could be adding some time constraints like queues in amusement parc like Disneyland,... or some PMR constraints for people that can't use stairs. 

The above and more general problem is to find the optimal walk on already existing edges to visit all the nodes at least once and come back to where we started. It has applications for buses, cars (Waze, maps), for planes (if we admit that the aerial traffic is already fixed) and more generally in all problems in which we wish to see all the nodes of a graph for a minimum total weight.

This will lead to the analysis of existing algorithms and upgrading of some of them hopefully. We can also explore the existing methods in packages like NetworkX or external software like concorde to see if some of them could be upgraded. 

#--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Here's how the programm works : 

#--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

There's a first section dedicated to creating by ourselves our graph based on scale map. 
The idea is to get a scale map of our subject (a parc, a road map, ...) and add manually the points of interest and the paths linking them. 

When you run, a window with the map appear. On this image, you can do several actions using the key board but those keys may depend on your keyboard architecture. 

        - You can zoom and dezoom : It's '+' and '-' keys on my keyboard. 
        - You can move on the image : up = 'z', down = 'w', left = 'q', right = 's' 

The main action is to add points : you can do it by hitting the right-click on your pad or your mouse. When you do it, this happens : 

        - A window opens and asks the user to select a name for the node. In my application, those are animals. 
        - And when you validate, a red dot appears on the map. This point is however not saved yet. 

As it may not be suitable to add all points at once, you can do it in multiple steps : 

        - When you want to save the red points you added, press 'p'. 
        - A new window opens and the red points became blue, meaning that they've been saved. 

You can do it as many times as you want. 

        - When you finished adding all points, press 'y' and the window closes. 

It's now time to add the paths between the points we added. 

        - You have to maintain the left-click pushed while drawing the path between the 2 nodes you want to link. 

When it's done, a new window open and you must choose the 2 ends of the path among the points you added previously and validate your answer. 
If you misclick, just press cancel and the curve won't be kept. 

You can add multiple paths between the same 2 nodes. Only the shortest one will be kept for computations. 

Drawing a path linking the node to hitself is kinda weird in this application because this will never be used in the optimal path. 

Once again, press 'p' to save the current curves in red (and they become blue) and 'y' when you finished addind paths. 

We have some created files : 

        - points.txt : the added points with their positions 
        - curves.txt : the added curves (the number of the curve and the 2 ends) with their length 

        - Map_with_points.JPG : the map with the added points
        - Map_with_curves.JPG : the map with the added curves

And it also prints the points and curves in the notebook. 

#--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The second section is about trying to find the shortest paths using known algorithms. 

#--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

First, you see a distance matrix between the nodes. 
The i,j entry of this matrix is the shortest distance between nodes i and j. If there's no edge between the nodes, the entry is infinity. 

#--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

You then see 2 graphs : 

        - Left graph : the graph corresponding to the nodes and edges we added previously. The positions of the nodes respect their positions on the map. 
        - Right graph : The same graph with an automatic display so we can see clearly all the names and weights. 

#--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Then, we use algorithms defined in the package networkx : 

#--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

        - 1. a test of the Christofides algorithm. By the time I'm writing this, it passes through infinity edges so it doesn't work well. But I didn't deeply read the description. 

        - 2. the kruskal algorithm to retrieve the minimum cost spanning (linking all points) subgraph. It's displayed in red. This subgraph leads to a bound. 
        
        Indeed, I can't obtain a worst cost than the total weight of this subgraph 2 times. It means that our walk is just getting to every node using an edge in this subgraph and then take it in the opposite direction. 

        - 3. a test for the Dijkstra algorithm to find the shortest path between 2 points in the graph. Of course, if we try start == end, then the result is 0. It doesn't take in account that we have to visit all nodes. 

        Notice that the result of Dijkstra doesn't necessary follow edges in the subgraph found with kruskal ! 

        - 4. a try for an augmented version of Dijkstra that passes through all points. IT DOESN'T WORK. 
        - 5. a try for an held_karp algorithm but IT DOESN'T WORK and I'm not sure it's suited for this kind of problem.    

#--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The next steps are to : 

        - Seek for the algorithms and methods in litterature that could be useful (and networkx documentation)
        - Try to understand the functionning of apps such as Waze, maps, etc...