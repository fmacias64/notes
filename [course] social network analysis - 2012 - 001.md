z# Social Network Analysis - 2012 - 001

(via Coursera)

## Lecture notes

### 1A Why Social Network Analysis?

-	Can use Gephi to do auto community and clustering detection.
-	Organisation hierarchies often reflected in clustered graphs, but shortcuts present too.
-	Characterising networks and nodes.
	-	Are nodes connected?
	-	How far apart are nodes?
	-	Are some nodes more important due to position?
	-	Are there communities in the network?
-	Modelling networks (where structure comes from).
	-	Randomly generated.
	-	Small-world structures.
-	How network structure affects processes.

###  1B Software Tools

-	In this course:
	-	Gephi - visualization and basic network metrics
		-	http://gephi.org, download dining.gephi.
	-	NetLogo - modelling network dynamics
	-	iGraph - programming
-	Alternatives:
	-	Pajek (http://pajek.iimfm.si/doku.php), Windows only
	-	UINet (not free, Windows)
	-	NodeXL (http://nodexl.codeplex.com) (Windows, free, beta)
	-	NetworkX (Python)
	-	sna package for R (http://cran.r-project.org/web/packages/sna/index.html)
		-	Test hypotheses
	-	SoNIA (Social Network Image Animator) (http://www.stanford.edu/group/sonia)
-	Using Gephi
	-	Load dataset.
	-	Select Layout -> ForceAtlas 2. Want to put nodes into communities.
	-	Right click on colour/size, select, close dialog, then left click on the button again to apply.
	-	Layout -> Label adjust to adjust labels.
	-	Partition -> Edges, then reload, then select a parameter, then click run. Edges coloured by parameter.
	-	Buttons at top (Overview, Data Laboratory, Preview)
		-	Can explore data in Data Laboratory.
		-	Can export using Preview.
	-	(bottom) big T to show node labels.

### 1C Degree and Connected Components

-	Tufte principles
	-	Above all else show the data.
	-	Maximise the data-ink ratio, within reason.
	-	Erase non-data ink, within reason.
	-	Erase redundant data-ink.
	-	Revise and edit.
-	Aesthetic criteria for network visualisations.
	-	Minimise edge crossings.
	-	Uniform edge lengths (but not if edges have weight).
	-	Don't allow nodes to overlap with edges that's aren't incident on them.
-	Edge attributes
	-	Weight (positive and negative)
	-	Ranking  (1st, 2nd, ...)
	-	Type
	-	Properties depending on the rest of the graph, e.g. betweenness.
-	Data representation
	-	**Adjacency matrix**
		-	N x N for N nodes. Row 1 is node 1, ...
		-	A_ij is 1 if node i has edge to node j.
		-	A_ii = 0, unless there are self loops.
		-	A_ij = A_ji if undirected.
	-	**Edge list**
		-	[2,3], [2,4], ...
	-	**Adjacency list**
		-	If graph very large and very sparse.
		-	For each node a list of neighbours.
-	**Node degree** - number of edges incident to node
	-	Indegree, outdegree, or degree (in and out).
-	Graph properties: betweenness, centrality.
-	**Outdegree** = Sum of row in adjacency matrix.
-	**Indegree** = Sum of column in adjacency matrix.
-	**Indegree sequence** = ordered list of indegree of each node.
-	**Outdegree sequence** = ordered list of outdegree of each node.
-	**Degree sequence** = order list of degree of each node.
-	**Degree distribution** = freqency count of each degree.
-	**Strongly connected components** - each node can reach every other node by following directed edges.
-	**Weakly connected components** - each node can be reached from every other node by following edges in either direction (even if directed).
-	**Giant component** - if largest component encompasss a significant fraction of graph.

### 1D Gephi demo

-	(top left) Ranking -> Nodes -> Indegree, set min/max size by clicking on the red ruby icon, spline, apply. Nodes sized by indegree.
-	(right) Statistics -> Network Overview -> Average degree -> Run.
	-	Not only visual but will put new columns in Data Laboratory.
-	(right) Statistics -> Network Overview -> Connected Components -> Run. Then should be able to Partition -> Edges -> refresh, choose strongly connected ID.

### 2A Introduction to random graph models

-	simple representation to test and predict properties.
-	a strawman: how is the real world different, what insights are there?
-	Erdos and Renyi, random network model.
-	Assumptions:
	-	Nodes connect at random.
	-	Undirected.
-	Two parameters:
	-	N: number of nodes.
	-	p: probability that any two nodes share an edge, OR
	-	M: total number of edges.
-	(N, p) model is binomial (review this). p = node, (1 - p) = no node.
-	Average degree = (N - 1) * p.
	-	Each node has (N - 1) tries to get an edge. 
-	Binomial cofficient
	-	N choose k. = n! / (k!) * (n - k)!
-	B(7;4;p) = 7_C_4 * p^4 * (1-p)^3.
-	In general average degree is the mean, expected(x) = sum(x) * p(x).
-	Variance in degree = (n-1) * p * (1-p)
-	In general variance = E[(X-u)^2] = sum(X-u)^2 * p(x).
-	Binomial approximations:
	-	Small p => Poisson. p_k = z^k * e^(-z) / k!
	-	Large n => Normal.
-	Insights:
	-	No hubs, no nodes with very high degrees.

### 2B: Random graphs and alternative models

-	For a growing random graph there's a marked increase in the giant component size when average degree = 1.
	-	NetLogo -> Sample Models -> Network -> Giant Component.
	-	Imagine network of friends. If average degree = 1 there's a chain of a friend to a friend to a …, hence giant component.
-	Lattice percolation.
	-	2D grid, each point has a probability p of being occupied.
	-	How far can infinite liquid starting at origin travel?
	-	Critical point at p = 0.5 - 0.55
-	In general: at what average degree (i.e. density) to giant components appear?
-	In random graphs degree distribution has an exponential distribution.
-	In random graphs size of giant components ~ N, whereas size of other components ~ log(n).
	-	Given two very large components any additional random edges are very likely to join them, hence intuitively only one giant component likely.
-	Given Erdos-Renyi graph with nodes N, average degree z, => average shortest path ~= log(N) / log(z).
	-	Very hard to derive.
	-	Intuitively N^l = z^l. i.e. the number of friends distance l away from you is z^l.
-	Closed triad: A -> B -> C -> A.
-	**Introduction model**
	-	Like ER except only (1 - p_intro) chance of random edge. Else we ask an adjacent node for one of their edges (friend of a friend).
	-	Relative to ER the **introduction model** has:
		-	more closed triads (friends introduce you to friends)
		-	longer average shortest path (instead of randomly connecting to distant nodes edges kept more local).
		-	more uneven degree distribution (people with more connections get more edges, increasing returns)
		-	smaller giant component at low p.
-	**Static geographical model**
	-	Randomly place nodes on a 2D grid. Each node tries to connect to M neighbours.
	-	Relative to ER:
		-	narrower degree distribution (each node is aiming for the same number of neighbours).
		-	longer average shortest path (geographically localised)
		-	smaller giant component (less chance of random connections)
-	**Random encounter model**
	-	Nodes at random on 2D grid. Then each node moves randomly until it encounters a node, and then makes an edge.
	-	Relative to ER:
		-	longer average shortest path.
		-	smaller giant component.
		-	more closed triads.
-	**Growth model**
	-	Nodes added over time.
	-	Compared to ER:
		-	More nodes with degree 1, as there are more younger nodes.
		-	No more closed triads, because of yound nodes.
		-	Smaller giant component.
		
### 2C: Models of network growth

-	In real networks degree distribution is highly skewed.
	-	Question/answer forums, sexual contact.
-	The Poisson distribution of Erdos-Renyi has very fey high degree nodes.
-	The Power Law of real networks have log(n) high degree nodes.
	- p(k) (probability of degree k) = C * k ^ (-alpha).
	- C is constant such that probabilities of all k sum to 1.
	- i.e. log(p(k)) = c - alpha * log(k).
	- alpha > 3 => no longer heavy tailed distribution.
-	Preferential attachment / cumulative advantage is increasing returns, those with many edges get more edges.
-	Power law model networks **grow over time**, nodes make m edges per tick. (first ingredient)
	-	If at time t there are t nodes, k_i is degree of node i born at time i, then dk_i(t) / dt = m / t.
	-	k_i(t) = m * (log(t) + c)
	-	At t = i, k_i(t) = m, => m = m * (log(i) + c), => c = 1 - log(i)
	-	=> **k_i(t) = m * (1 + log(t/i))**
	
	-	If tau(100) is time when node of degree 100 is born, fraction of nodes that have degree <= 100 is (t - tau) / t, or 1 - tau/t.
	-	log(t/tau) = k/m - 1
	-	t/tau = e^(k/m - 1)
	-	tau/t = e^(-(k/m - 1)))
	-	P(k < k') = 1 - e^(-(k/m - 1))
-	Power law model networks show **preferential attachment** (second ingredient).
	-	Price [65] model for citations.
		-	Papers start with m citations.
		-	Probability of citing a paper with degree k proportional to k + 1.
		-	Power law, alpha = 2 + 1/m.
-	Barbasi-Albert model
	-	New nodes form m attachments. Form to nodes in proportion to vertex degree / sum of all degrees of all vertices.
	-	dk_i(t) / dt = m * (k_i/2tm) = k_i/2t, and k_i(i) = m.
	-	k_i(t) = m * (t/i) ^ (1/2)
	-	p(k) = 2m^2 / k^3
	-	Distribution is scale free (i.e. power law) with alpha = 3.
	-	Graph is connected.
	-	Older are richer.

### 3A: Centrality

-	www.moviegalaxies.com
-	Indegree/outdegree, discussed before.
-	Trade in petroleum, source: NBER / UN Trade Doha
-	Ask yourself what your network represents and what its scope is.
-	Common tactic - size node by in-degree, colour node by out-degree or ratio of in/out degree.
-	**Normalization**
	-	Divide degree by maximum possible degree, $$N-1$$.
-	**Skew in distribution of degree centrality**
	-	Could just do stdev of degree.
	-	Freeman's general formula.
		-	Sum over all nodes of difference between maximum centrality and this node's centrality, divided by number of pairs [(N-1)(N-2)].

		sum[i = 1 to g](C_D(n*) - C_D(i)) / [(N-1)(N-2)]

-	**Brokerage**: how nodes lie between other nodes.
	-	Having to go through other key nodes to each everyone.
	-	How many pairs of nodes do you have to go through to reach one another in a minimum number of hops?
-	Degree centralization doesn't capture brokerage.
-	**Constraint**: how dependent on other nodes are you to communicate.
	-	In a brokerage position you experience low constraint.
-	**Betweenness** definition:

$$ C_B(i) = /sum{j<k} \frac{g_jk(i)}{g_jk} $$

-	$$g_jk(i)$$ is number of shortest paths node $$i$$ is on between $$j$$ and $$k$$.
-	$$g_jk$$ is the total number of shortest paths between $$j$$ and $$k$$.
-	**Normalized betweenness**:

$$ C_B(i) = \frac{C_B(i)}{[(n-1)(n-2)/2]} $$

-	Denominator is number of pairs of nodes excluding the node itself.
-	Size nodes by degree, colour by betweenness.
	-	Notice low degree nodes with high betweenness, bridge networks.
-	What if it's not important to have many direct edges, but just to be "not too far"?
-	**Closenesss**: length of average shortest path between a node and all other nodes in the graph.

$$ C_c(i) = [\sum{j=1}^{N} d(i,j)]^(-1) $$

-	**Normalized closeness centrality**

$$ C'_C(i) = \frac{C_C(i)}{(N-1)} $$

-	Sometimes the graph isn't fully connected, so some distances are infinite. Instead can invert each distance and then sum those.

### 3B: Eigenvector and directed networks

-	**Eigenvector centrality**: you are as central as your neighbours, recursively.
	-	Solving for eigenvector of adjacency matrix with eigvenvalue = 1.
-	**Bonacich eigenvector centrality**
	-	Tunable via beta.

$$ c_i(\Beta) = \sum{j} (\alpha + \Beta c_j)A_(ji) $$

$$ c(\Beta) = \alpha(I - \Beta A)^-1 \times A \times 1 $$

-	Meaning:
	-	alpha: normalization constant.
	-	beta: how important the centrality of your neighbours is.
	-	A: adjacency matrix (can be weighted)
	-	I: identity matrix
	-	1: matrix of all ones.

-	Beta:
	-	0 yields simple degree centrality.
	-	Small beta => high attenuation. Only your immediate friends matter.
	-	High beta => low atteuation. Global network structure matters.
	-	Negative => node is more central when connected to less central nodes.
	
-	**Betweenness centrality in directed networks**
	-	Watch out which paths you're actually on.
	-	Normalization denominator changes, loses factor of 2:
	
$$ C'_B(i) = \frac{C_B(i)}{[(N-1)(N-2)]} $$

-	**Directed closeness centrality**
	-	In-closeness (prestige in citation networks)
	-	Out-closeness.
	-	Only consider nodes you can reach.
	
-	**Eigenvector centrality in directed networks**
	-	**PageRank.**
	-	Recursive, directed. Difficult to artificially inflate it because it's recursive.
-	**Random walk** is like the eigenvector centrality measure.
	-	Just walk randomly, measure time you spend at each node.
	-	More time => more important.
	-	But could get trapped in circles!
	-	PageRank allows random teleportation to work around cycles.
	-	As you increase random teleportation probability PageRank score distribution flattens. Not walking, just jumping around.

### 3C: Centrality applications (optional)

-	**Hospital patient transfers**, simulation.
	-	Patients transfer, take diseases.
	-	Hospitals could collaborate to find hubs of key disease transfer points.
	-	Want to allocate money to hospitals to fight disease, but who to give money to?
	-	Strategies, and how they affect probability of getting infected:
		-	Random, no effective.
		-	Degree (some hospitals have more transfers than others), geometric mean (sqrt(indegree + outdegree)), a bit effective.
		-	Betweenness, even more effective.
		-	Greedy (simulation based), most effective.
		-	Eigenvector (as effective as greedy).
-	**Identifying expertise** in an expertise network
	-	Response time gap between the questions you ask and when they're answered.
	-	Directed edges.
		-	A -> thread => A asked the question.
		-	Thread -> B and C => B and C answered.
		-	Could weigh edges by:
			-	number of threads.
			-	shared credit (all responders get equal weight)
			-	backflow (questions that are answered get a backward edge).
	-	**Bow tie model** of web and forums
		-	Core: strongly connected component, everyone asks and answers.
		-	In: mostly askers
		-	Out: mostly helpers.
		-	Forums are skewed; indegree is much higher, small core. Not a community as such.
		-	Question: what is the indegree/outdegree of the largest connected component?
	-	Is centrality, using various measures, a good measure of expertise?
		-	Compared with human evaluation: yes.
	-	Very interesting is that recursive PageRank wasn't the best!
		-	To investigate, simulated two models:
			-	'Best' preferred. Experts answer questions that are high enough quality to be worth answering.
			-	'Just better' preferred: people answer questions just a bit more challenging than their expertise level.
			-	Centrality measure perform differently depending on model.


#### Readings:

-	Week 1
	-	Network Science - Chapter 1
		-	Networks have predictive power.
		-	Networks are remarkably stable.
		-	The choice of network we focus on makes a huge difference.
		-	Cascading faliures - where nodes depend on each other. Network structure critical.
		-	Behind each complex system is an intricate network.
		-	There are fundamental principles and reproducible mechanisms behind all networks.
		-	Interdisciplinary.
		-	Empirical, data driven.
		-	Quantitative and mathematical nature. Physics, engineering, statistics, etc.
		-	Computational nature. Big databases, algorithms, data mining.
		
-	Week 2
	-	Giant component (Wikipedia)
		-	For n nodes, p = 1 / n, size of giant component is likely to be proportional to n^(2/3).

-	Week 3
	-	**The Social Organization of Conspiracy - Illegal Networks in the Heavy Electrical Equipment Industry (Baker / Faulkner)**
		-	Price fixing.
		-	Conclusion: maximise concealment rather than efficiency.
		-	In switchgear "phase of the moon" price scheduling, i.e. decentralized. Product standardized, flow of orders predictable, easy to synchronize price fixing. Not true of more complex products like turbines.
		-	In transformers also decentralized price fixing.
		-	In turbines very lumpy market, low volume, non-standardized. High information processing requirements for conspirators.
		-	Industrial organization economics examines effects of market system imperfections on behaviour of producers, and how producers satisfy society's economic needs.
			-	Collusion likely in certain industry structures; few sellers, high seller concentration, homogenous products.
			-	Number of two-way flows is N(N-1)/2, so fewer sellers => easier to coordinate.
			-	Treat the internals of the conspiracy as a black box.
		-	Organizational crime examines individuals as agents, representing their organization and themselves.
			-	Makes many simplifications about conspirator social organization, almost a black box as well.
		-	Expect *sparse, decentralized networks* if secrecy is only factor. But also need to communicate efficiently.
		-	Small group research applies here: more routine tasks are more efficiently performed in centralized structures, more complex tasks in decentralized structures.
		-	Organizational theorists have similar conclusions - more information-processing requires more decentralization.
		-	Concealment vs. coordination.
		-	Centrality: more central => can get better illegal deals for your company, but also mean more personal culpability.
		-	Executives can delegate so can afford to be less central, hence predict less likely to get fined or prosectured.
		-	Degree => legal culpability, where betweenness and closensess amounts to hearsay.
		-	Undirected graph of Senate testimony where witnesses mention someone else. Also measure organizational rank.
		-	Freeman's three point centrality measures used. Also could have used Bonacich's measures of sociometric status (Bonacich 1972) and influence (Bonacich 1987), Coleman's measure of power (Coleman 1973), Burt's measure of prestige (1980).
		-	Also Stephenson and Zelen (1989)'s measure of point centrality where shortest paths are deliberately avoided.
		-	Graph density => observed number of edges as percentage of maximum possible.
		-	p849, figure 2: decentralized and centralized networks.
		-	Graph centralization => ratio of centrality of most central point to maxmium possible centrality.
		-	Results.
		-	Turbines (recall, most information processing) had highest density and most centralization, contradicting small group and organizational theory.
		-	Network decentralization did not protect against successful prosection; in turbine network less likely to be found guilty.
		-	Top executives in decentralized conspiracies able to shield themselves from prosection, but when found guilty had larger fines.
		-	Top executives in centralized conspiracies could not shield themselves, but when found guilty had smaller fines.
		-	Middle managers more vulnerable than junior managers.
		-	Degree centrality increases vulnerability. Not betweenness or closeness. However, degree does not affect penalities.
		-	In centralized networks, e.g. turbines, small connected core and large periphery. Core dominated by top executives, who need to be hands on. Hence lower conviction rate but more top executives found guilty.
	-	**Network Structure and Information Advantage (Aral / Alstyne)**
		-	How and why social structure affects economic outcomes.
		-	Burt (1992) shows that structurally diverse networks (low in cohesion and structural equivalence) are more successful in e.g. wages, promotion, job placement, creativity (Burt 2004a). Other studies show similar. More novel information.
			-	See p11 figure 1 for diagram of cohesion and structural equivalence.
			-	p12 => sructural equivalence of two actors is Euclidean distance of their contact vectors.
		-	Conclusion: total amount and diversity of novel information increases at decreasing rate with network size and network diversity.
		-	Weak ties to other parts of network important source of inormation (Granovetter 1973: 1371). Get redudant information from well connected local network (Burt 1992).
		-	Burt (2004b): "creativity is an import-export game, not a creation game".
		-	Do diverse networks actually provide access to more novel information? No.
			-	Less diverse, stronger connected links have less novel information but higher bandwidth, so maybe more information.
			-	Nodes aware of more redundant information in local network so they adjust their transmission to avoid redundancy.
		-	Even with new information does productivity necessarily rise? No.
		-	p19, vector space model of communication content. Emails categorized into set of topic vectors, individuals' email's diversity is variance of topic vectors.
		-	Results.
		-	Total and diversity of novel information increasing with node's network size and network diversity, but marginal increase decreses with network size.

## Assignment notes

## General notes