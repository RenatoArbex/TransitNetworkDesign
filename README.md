# Transit Network Design Instances

TransitNetworkDesign is a public transit networks repository for research. Here you will find transit network instances and solution route sets proposed by authors in specialized academic literature and practitioners to benchmark new algorithms. Suggestions, additional instances and proposed new solutions route sets for any instance are always welcome.

The Transit Network Design Problem (TNDP) involves finding a set of routes to operate in an urban public transport system. This is a hard combinatorial optimization problem, with multiple constraints and conflicting objective functions such as minimizing passenger generalized costs and operator costs. 

User costs generally corresponds to total travel time, including waiting time, in-vehicle travel time and transfer penalties, while operator costs may correspond to total bus routes length or fleet size. The multi-objective transit network design and frequency setting problem (TNDFSP) also includes finding those routes associates frequencies. This problem must also considerer capacity constraints as passenger demand may exceed supply.

A known issue in this field of Transit Network Design is the lack of instances to apply methodologies, mainly larger instances and real-sized transit networks. The most used benchmark instance is Mandl, which is rather small compared to real-world cities, but nonetheless already brings quite a challenge for new researchers in the field. Larger instances, however, have more operational constraints to tackle, such as limitations on route start and stop locations, existing infrastructure such as terminals, rail lines and a high number of real bus stop locations. This site aims to fill this void and promote transit network design research and algorithms.

## How to Download Transit Network Design Instances

Each instance is stored in a separate folder. In each folder you will find several files containing information on nodes, links and demand. Details on Data format are described in Format section.

  - (For all data) Clone the repository to your computer using the "Clone or Download" button
  - (For a single file) Click on a file, click view as Raw, and then save the file
  
## How to Add Instances

There are several ways to add a network:
  - Fork the repository
     - Create a GitHub account if needed
     - Fork (copy) the repo to your account
     - Organize files in the suggested format (below) and create a README file in [Markdown](https://guides.github.com/features/mastering-markdown) for your addition as well.  Take a look at some of the existing README files in the existing network folders to see what is expected.
     - Make changes such as adding a new folder and committing your data
     - Issue a pull request for us to review the changes and to merge your changes into the master     
  - Create an issue, which will notify us (me).  We will then reply to coordinate adding your instance/solutions to the site.
  
  - Or Email me: renatoarbex@usp.br

## How to Add Solution Route Sets and Objective Functions

Solution route sets are proposed solutions for the network with some other necessary data. Route sets contain the number of routes proposed and their sequence of nodes.
  - Prepare your route sets using the same format described in Formats below.
  - Upload the data to the repository in the folder of that instance using instructions above
  
*Objective functions*: several objective functions are proposed for this problem. You can either add just your solution route sets and/or additional files with complementary data. Suggested objective functions based on recent literature:
  - Total network user generalized cost
  - Fleet size required to operate solution with vehicle sizes
  - Average in-vehicle travel time
  - Total number of transfers in the network
  - Percentage of demand served with zero, one, two and two or more transfers
  - Empty seat hours
  - Accessibility to opportunities enabled by solution
  
While several objective functions are suggested in the literature, total network user generalized cost and fleet size are already a good measure to compare algorithm solution route sets.

*Complementary data suggested*: 
  - Objective functions results
  - Routes frequencies
  - Vehicle(s) size used
  - Assignment procedure used
  - Transfer penalty adopted, as well as waiting time and access time perception factors

# Formats

To facilitate automation on reading/comparing solutions and inputting data for algorithms, a data format is suggested. For now, only file format for instances and solution route sets is encouraged. Other files should contain necessary information on objective functions and above complementary data, but no fixed format is enforced.

## Instance

Instances are composed of *three main files: Nodes, Links and Demand*. While complex larger instances will need additional information, those 3 files already define the basic information for designing routes:

### Nodes
Nodes are points that represent a possible location for vehicles to board/alight. They may also represent an aggregation of real-world bus stops, representing a traffic zone, for example.

Format:
A CSV file with node ID, latitude, longitude and an indication if the node is also a bus/transit terminal. The last "terminal" column accepts 0 or 1 values. If 0, only passing through routes are allowed in that node. This is necessary to represent real-world conditions of existing possible terminal locations and/or nodes which may not be able to serve as a route terminal, such as a highway node.

Authors are encouraged to use node location in latitude and longitudes (EPSG 4326). If the instance does not represent a real-world location, location may be somewhere in the ocean. The will help further visualization tools that aim to provide insights over the proposed solution, such as routes and transit assignment visualizations.

Node file should start from 1 and continue with unique continuous +1 ID until last node, as some graph libraries implementations might not work well if a number is missing.

Example (Rivera instance):
```
id,lat,lon,terminal
1,-30.875393,-55.60165,1
2,-30.876683,-55.591102,1
3,-30.889253,-55.586219,1
4,-30.885728,-55.577737,1
(...)
```

### Links
Links are connection between nodes in the network.

Format:
A CSV file with i node ID, j node ID and travel time in minutes.

Example (Rivera instance):
```
from,to,travel_time
1,2,10.384615
2,1,10.384615
2,3,4.5
2,7,5.893847
2,11,7.901538
3,2,4.5
3,4,2.833846
(...)
```

### Demand
Demand file represents the number of users that wants to travel between two nodes. Demand represents travel in a *1 hour period* (unless otherwise mentioned). While the value is encouraged be an integer, real values are accepted as this depends on how trip data was collected and expanded.

Example
```
from,to,demand
1,3,4.90908
1,8,1.63638
1,18,1.27272
1,23,4.09092
1,31,2.8182
1,38,1.63638
1,39,3.2727
(...)
```

## Solution Route Sets
Route sets should be presented as Solution Title, number of routes and, for each route, the sequence of nodes.
Authors may include frequency information below, but it is not mandatory, as some papers don't deal with frequency setting.
References to published paper will appear in README.ml inside each instance folder.

Example (Mandl solution):
```
Arbex (2015) Best Compromising 10 routes
10
1-2-3-6-8-10-11-13
9-15-7-10-11-12
7-15-8-6-3-2-4-5
2-4-6-8-10-11-13-14
13-14-10-8-6-3-2-4
1-2-5-4-12
11-10-7-15-6-3-2-1
5-4-6-8-10-11
13-11-12-4-5-2-1
9-15-8-6-3-2-4-12
```

Example (Mandl solution, with frequencies (trips per hour) for each line):
```
Arbex (2015) Best Compromising 10 routes
10
1-2-3-6-8-10-11-13
9-15-7-10-11-12
7-15-8-6-3-2-4-5
2-4-6-8-10-11-13-14
13-14-10-8-6-3-2-4
1-2-5-4-12
11-10-7-15-6-3-2-1
5-4-6-8-10-11
13-11-12-4-5-2-1
9-15-8-6-3-2-4-12
10.91
8.44
6.67
9.31
8.57
3.21
13.00
11.74
3.49
4.00
```

File names:
Files should be named as to include Instance Name, Number of Solutions and/or if it comprises multiple Pareto Solutions. It is encouraged to include multiple solutions in a single file if this represents a Pareto solution set and/or the same methodology/algorithm route sets. Different methodologies applied to the same instance from the same paper/author can be presented in two different files. If frequencies are available, it should be clear in file name txt for automation purposes.

Examples:
```
instance_author_4to8_routes_solutions_route_sets.txt
Mandl_Arbex(2015)_compromising_route_sets_frequencies.txt
Mandl_Arbex(2014)_67_pareto_solutions_route_sets.txt
Mumford0_Mumford(2013)_4to8_best_passenger_route_sets.txt
Mumford1_Mumford(2013)_55_pareto_solutions_route_sets.txt
```

This is an initial suggestion for file formats, thus we can further adapt from here if needed. 

## Objective Functions and Additional Data

This will vary depending on whether you are also calculating frequencies or dealing with large scale instances that require additional information. Authors are strongly encouraged to submit information described above in "How to Add Solution Route Sets and Objective Functions" to ease comparisons of results.

# Summary of Instances

As of October 2018, instances in TransitNetworkDesign repository are:

| ﻿Network  	| Source                  	| Nodes 	| Links 	| Terminal Nodes 	|
|----------	|-------------------------	|-------	|-------	|----------------	|
| Ceder1   	| Ceder (2016) Chapter 15 	| 4     	| 4     	| 1              	|
| Ceder2   	| Ceder (2016) Chapter 15 	| 8     	| 14    	| 2              	|
| Mandl1   	| Mandl (1979)            	| 15    	| 21    	| All            	|
| Mandl2   	| Mandl (1979) adapted    	| 15    	| 21    	| 10             	|
| Mumford0 	| Mumford (2013)          	| 30    	| 90    	| All            	|
| Mumford1 	| Mumford (2013)          	| 70    	| 210   	| All            	|
| Mumford2 	| Mumford (2013)          	| 110   	| 385   	| All            	|
| Mumford3 	| Mumford (2013)          	| 127   	| 425   	| All            	|
| Rivera1  	| Mautonne (2005)         	| 84    	| 143   	| All            	|
| Rivera2  	| Mautonne (2005) adapted 	| 84    	| 143   	| 12             	|

Instances general comments:

*Ceder1/2*: small networks for researchers starting with this problem. While Ceder1 may be solved by hand, Ceder2 already has millions of possible solutions. Those networks are used by Avishai Ceder in Chapter 15 (Network Design) of his well-known Public Transit Planning and Operation book.

*Mandl*: the most solved instance in the literature. Usually solved with 4-12 routes.

*Mumford0,1,2,3*: instances proposed by Mumford(2013) to bridge the gap of instances scarcity. Generated randomly based on real sized networks.

*Rivera*: instance proposed by Mautonne (2005) using data from Rivera city in Uruguay.

More details for instances are available within each folder.

## Instances References

[Ceder(2016)](https://www.crcpress.com/Public-Transit-Planning-and-Operation-Modeling-Practice-and-Behavior/Ceder/p/book/9781466563919)
[Mandl(1979)](https://books.google.com.br/books/about/Applied_network_optimization.html?id=xGJRAAAAMAAJ&redir_esc=y)
[Mumford(2013)](https://ieeexplore.ieee.org/abstract/document/6557668)
[Mautonne(2005)](http://www.fing.edu.uy/inco/pedeciba/bibliote/tesis/tesis-mauttone.pdf)

# Transit Assignment

To evaluate solution route sets calculating total generalized costs and fleet size, a transit assignment procedure should be applied to assign demand to the network. This a crucial step which opens several possibilities and challenges for evaluation. The aim of this step is to represent users' choices in real-world scenarios so that the maximum passenger load per route can be calculated, which enables calculation of frequencies. But as user choices depends on route frequencies, this assignment procedure should be done until convergence. Also, whenever multiple lines serve an OD pair, demand is split between routes depending on their travel time to the destination and their frequencies, a problem known as the Common Lines Problem.
  
Ideally, a complex assignment procedure should be used; however, simplifications are made to enable a fast objective function calculation. Care should be taken for this not affect quality of final results, as the best solutions are those that aim to realistically represent passenger behaviors when choosing routes.
  
## License

  - Data sets are for academic research purposes only and all data is donated from contributors. 
  - Users of this repository are fully responsible for any results or conclusions obtained by using these data sets. 
  - Users must indicate the source of any dataset they are using in any publication that relies on any of the datasets provided in this web site. Users may indicate the original location of instances if they are available elsewhere.
  - The organizer of this repository is not responsible for the content of the data sets. 
  - Agencies, organizations, institutions and individuals acknowledged in this web site for their contribution to the datasets are not responsible for the content or the correctness of the datasets.

## How to Cite

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1473545.svg)](https://doi.org/10.5281/zenodo.1473545)

Public Transit Networks for Research. *Transit Network Design Instances for Research*. https://github.com/RenatoArbex/TransitNetworkDesign.  Accessed Month, Day, Year.

## Team
This repository is currently maintained by Public Transit Networks for Research. The current members are:
 - Renato Arbex, PhD Candidate at University of São Paulo. [GitHub](https://github.com/RenatoArbex) [Scholar](https://scholar.google.com.br/citations?user=Y3cAEhYAAAAJ&hl=en-US)
 
This initiative also aims to be help researchers organize input data and route sets in a similar format for aid for further research.

This repository was inspired by a similar compendium for Traffic Assignment Problem by the [Transportation Networks for Research Core Team](https://github.com/bstabler/TransportationNetworks). The author congratulates the Transportation Networks for Research Core Team for this great initiative and inspiration. 

## Other Related Projects

Transit Network Design research sites
  - Research on the Urban Transit Routing Problem (Bus Routing) Christine Mumford (https://users.cs.cf.ac.uk/C.L.Mumford/Research%20Topics/UTRP/Outline.html)
  - Antonio Mauttone research group on Transit Network Design Problem (https://www.fing.edu.uy/~mauttone/tndp/)

Traffic Assignment
  - [Transportation Networks for Research Core Team](https://github.com/bstabler/TransportationNetworks) Transportation Networks is a networks repository for transportation research. Aims to congregate network instances for the traffic assignment problem.

## Roadmap

  - Proposing in this site a methodology to evaluate route sets using the same assignment algorithm and objective functions using multiple languages such as Python, C++, Java (for comparison purposes)
  - Publishing a large instance of São Paulo main trunk transit network (~300 nodes/600 links) once ready
  - Organizing results with visualization tools
  - Incorporating GTFS as possible instances for transit network design and discussing the differences when dealing with real stop locations

This site aims to bring together transit network design researchers and practitioners interested in exchanging instances, methodologies and results. Contact me if you would like to contribute more! Help to continue this effort will be greatly appreciated!
