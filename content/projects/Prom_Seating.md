---
title: "Prom_Seating"
date: 2024-06-21T18:26:56-04:00
draft: false 
---

![image2](https://github.com/blucardin/blucardin.github.io/assets/55935207/03998e34-8eca-4ddb-9518-017696911c4d)

 
# An exercise in social networks, mathematical graphs, and community detection algorithms. 
 
 
As I prepare to go to Prom, I find myself faced with the most challenging question of my high school career: Who will I sit with? From this initial question, we can derive a general problem: How do you optimally partition a given population people into tables of fixed size so that each person is seated around people who they like?  
 
This problem is more difficult than it seems. Let’s say you have a population of 200 individuals to assign to 20 tables of 10 people each. You could start by simply asking each person for a ranked list of the top 20 people they want to sit with. This would give you 20*200 = 4000 data points, each one expressing the strength of a relationship from one person to another. But what do you do with this massive amount of data? Where do you go from here? 
 
This is where graphs come into play. In discrete mathematics, and more specifically graph theory and network analysis, a graph is a collection of objects in which some pairs of objects are related. In nomenclature, each object is abstracted (generalized) as a “node”, and each relationship is abstracted as an “edge”.  
 
Graphs are fun because they allow you to represent and analyze complex data in a uniquely freeform way. Because of this property, they are used everywhere in computer science. Think of the last time you used Google maps to find the most optimal route to school: Google has represented the entire street system as a graph, with the nodes being intersections and the edges being roads. Then, your phone executes an algorithm (in this case the A* search algorithm) to find the shortest distance between two nodes.  
 
We can represent our data as a directed weighted graph network. A directed graph has some direction encoded in its edges, not a real physical direction, but more like each edge is pointing away from an origin node and towards a destination node. A weighted graph also assigns a numerical value, called a “weight”, to each edge. In our case the direction of an edge shows whether person A selected person B or person B selected person A, and the weight shows the strength of the relationship (the level of ranking). 
 
If Noah really wanted to sit with Luca and ranked him first, this would be represented as a strong edge (shown as a thick arrow) from the “Noah” node to the “Luca” node. If Luca didn’t like Noah in return, there would be a very thin arrow from Luca to Noah. Note how the sum of the weights of all edges directly connecting two nodes is proportional to the “strength” of the relationship between the two people. Also note how this reformats our original dataset into a sort of map of our social network.  
 
![image4](https://github.com/blucardin/blucardin.github.io/assets/55935207/215a2e87-f651-4358-9bad-30faeba4a441)

 
Ok, we have our graph, but now what?  
 
Since we now have a bunch of nodes that are connected by a bunch of edges, we can begin to formalize our problem: We need to find 20 groups of tightly connected nodes within our graph, where “tightly connected” refers to a high density and strength of edges between the nodes in each group. In short, we need to create partitions of our graph such that we maximize the connections within the groups and, consequently, minimize connections between different groups. As it turns out, this problem of tight group recognition from graphs has been done before and is known as “community detection”.  
 
Community detection is used in all sorts of fields. Biologists use it to study the relationships between different biological protein structures and functional groups. Advertisers and social media networks use it to deliver targeted ads and recommend engaging content. Epidemiologists use it to study the spread of disease. And even the police use it to map criminal networks. Most notably however, community detection is helpful in machine learning with graph-based neural networks where you can use it to extract useful insights from a seemingly random graph.  
 
But how do we concretely measure communities? How do we know if a community is more tightly internally connected than externally connected? How do we know if we have found the crime ring, or a collection of unrelated criminals? The answer: Modularity! 
 
Modularity is a function that determines how “modular” communities are within a graph. Modularity is defined as the sum of the number of edges within a group subtract the expected number of edges within that group.  
 
If you don’t like math, skip two paragraphs.  
Imagine we have a node “i” with “ki” edges and another node “j” with “kj” edges in a non-directed non-weighted graph with “m” edges (counting each edge twice, once for the sender, and once for the receiver). We can say node i has ki “opportunities” to connect with node j, and for each opportunity, there is a kj / 2m probability that the edge will connect with node v. So, node u has ki (kj / 2m) expected connections with node v. We can then subtract the actual number of connections between i and j (represented by Aij) to find how “modular” the connection between i and j is. If we repeat and sum this method for all pairs of nodes in a given community “s”, and all communities “S”, in the graph “G”, and normalize with 1/(2m) to prevent double counting edges, we get the following formula.  

![image5](https://github.com/blucardin/blucardin.github.io/assets/55935207/729318a8-2a56-47ee-8bce-76ebd3a7e88b)

Formula for the modularity of a graph G with communities S. (Leskovec, Jure)  
 
Notice how if the actual number of edges is greater than the expected number of edges, modularity is positive, and vice versa – this is how we implicitly detect tightly connected communities as they, by definition, have a higher density of edges than we would expect if all edges were distributed evenly. Adapting this formula to work for weighted directed graphs is left as an exercise for the reader. 
 
Confused yet? Just think of modularity as a measure of how close we are to optimal table assignment. A modularity of 1 means that we have perfectly fit our data into tables such that there are no connections between tables and lots of connections within tables. A modularity of -1 means that there are no connections within tables, but lots of connections between tables.  
 
Modularity acts as what is called a “heuristic” function, sort of like that hot-or-cold game: Modularity tells us if we are hot or cold relative to where we want to be but cannot tell us where to go. Now, our job is simplified, all we have to do is create an algorithm to find the input to the modularity function that produces the highest number, and we get our tables for free.  
 
The most famous algorithm to this is the Louvain method: First, assume each node is in its own community, then test if merging any of the communities would result in an increase in modularity, perform the merges that increase modularity, simplify the graph by condensing each community into its own node, and repeat until no more increases in modularity can occur. This method works very well; however, it often produces communities of varying sizes as the most optimal community arrangement to maximize modularity is not necessarily the one in which all communities have the same number of members. Remember, we need exactly 20 communities of 10 nodes each.  
 
So, we are forced to invent our own algorithm: First assume every node is in one big community, then select a random node to be in a separate community, determine the change modularity if each neighbor of the new community was added to it, move the node that increases modularity the most into the new community, repeat until we have 10 nodes in a community, then remove those nodes from the graph, and repeat until we have 20 groups. 
 
This technique (always making a small step in the right direction) is known as a “greedy algorithm”, and they are also found everywhere in computer science (A* is a greedy algorithm). The downside of this method is that it will most likely only ever achieve a local maximum of modularity, as there is a possibility that a node that yields the highest modularity for one group would result in a higher modularity if put in a different group. A possible solution to this would be to start with 20 random communities and expand them simultaneously, however, we then encounter the problem that we don’t know which 20 nodes to select to guarantee that none of them fall within the same table if everything is most optimally assigned.  
 
To fix this, we can run the algorithm multiple times starting with random nodes for each table selection, then use the trial that produced the highest modularity value. But how do we know how many times to run the algorithm? Well, we can run it a few times and use what is called a collector’s curve.  
 
A collector’s curve is a “traditional” graph of discoveries over time, with the discovery on the x-axis and the “difference” (in this case the modularity value) on the y-axis. It is primarily used in biology to predict the number of undiscovered species in an environment. In our case, the undiscovered species is a better modularity value.  
 
 <img alt="image" src="https://github.com/blucardin/blucardin.github.io/assets/55935207/d5554e37-6b89-4f0c-8636-00217b12c0d4">

 
This is a collector’s curve generated by the analysis of the graph below. As you can see, after one improvement in modularity values on the third attempt, we can’t find any more improvements after 17 subsequent attempts. This implies that after 3 tries, we have found a modularity value close to the best possible, such that it would take too much effort to discover anything better and said discovery would only have a marginal improvement. Also note how all modularities produced varied from 0.285 to 0.306 (only 0.021 difference) this shows us that our new algorithm is very good at finding high modularity tables regardless of the starting conditions.  
 
 <img  alt="image" src="https://github.com/blucardin/blucardin.github.io/assets/55935207/2091ab1e-1c87-46cc-9472-71042d5228b2">

 
Compare this to a collector’s curve generated while I was still working out the best number of tries. Here, the scale of improvements is increasing rapidly, telling us that there are likely worthwhile discoveries to be found if we make just a few more attempts.   
 
Finally, we are left with our perfect tables:  
 
 
This is a sample graph created by using excel to manually (but also randomly) generate each person’s preferences so that groups are formed. Notice how the weak edges are thinner and longer, and the strong edges are shorter and thicker. Also notice how the algorithm split the nodes into tables, each table presented as a different colour. As you can see, the colours are roughly grouped together, YAY.  
  
Now I can rest peacefully knowing that everyone at prom is optimally seated. 
 
Believe it or not, these same graph-based techniques can be used for more fun, and malicious, insights. For example, by taking the shortest distance between nodes using the A* algorithm, you can determine the degree of friendship between two non-directly connected individuals.  
 
If you add in gender data into the graph, you could determine who is dating who, forecast which couples are likely to get together, and which are likely to split up by measuring the degree of friendship between all pairs of males and females. 
 
If you really wanted to, you could find all available bachelorettes that have relatively high connectivity to you and your friend group and low connectivity to all other males. Who said computer science would never help me get a girlfriend?  
 
You could also use the Louvain-partitioning algorithm to find communities within the network. This could be used for campaigning: If you wanted to run for student council president (or valedictorian) and need to advertise, you don’t have to talk to everyone at the school, you only need to advertise to the most well-connected members of the largest communities, then wait for word of mouth to do its thing.  
 
Finally, a graph approach could also be useful for the Amy Reston Compliment Project. At graduation, each student is given the name of another student to compliment. If we organize all students in a graph, we can construct a chain of people to optimize the connection between individuals. This would ensure you get the name of someone you know.  
 
But in the end, the prom committee took the easy way out, and decreed that students must decide who is at their tables and everyone at each table must submit the same list of the other students at the table. Maybe they just lack my appreciation for lines and dots.  
 
All code can be found here: https://github.com/blucardin/Prom-Seating  

Leskovec, Jure. “Lecture 13.2 - Network Communities.” CS224W: Machine Learning with Graphs, Stanford University, 25 May 2021, www.youtube.com/watch?v=mJQrtXZT5pw&list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn&index=40.  

Leskovec, Jure. “Lecture 13.3 - Louvain Algorithm.” CS224W: Machine Learning with Graphs , Stanford University, 25 May 2021, https://www.youtube.com/watch?v=0zuiLBOIcsw&list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn&index=40.  

"Modularity — NetworkX 2.5 Documentation." NetworkX, 25 September 2020, https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.community.quality.modularity.html. 
