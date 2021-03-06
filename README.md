kpath-centrality
================

This repository includes code and datasets to test the kpath centrality
algorithm and other randomized betweenness approximation algorithms
(randomized brandes and adaptive sampling)

---------------------------------------------------------------------------
Copyright (c) 2014 Nicolas Kourtellis (extensions)

Copyright (c) 2012 Tharaka Alahakoon, Rahul Tripathi, Nicolas Kourtellis

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

----------------------------------------------------------------------------
Additional Disclaimer:

This code was tested on Linux and Mac-based systems and works appropriately.
As mentioned above, please use at your own risk. We cannot provide any sort 
of guarantees that it will work on your platform and specific settings.
Also, we cannot provide any support for you to make it work in case of
compilation problems.

If you use this software and its relevant feeatures, please make sure to
acknowledge the appropriate studies, by citing:

[1]	Tharaka Alahakoon, Rahul Tripathi, Nicolas Kourtellis, Ramanuja Simha,
	and Adriana Iamnitchi. 2011. K-path centrality: a new centrality measure
	in social networks. In Proceedings of the 4th Workshop on Social Network
	Systems (SNS '11). ACM, New York, NY, USA, Article 1.
	DOI=10.1145/1989656.1989657, http://doi.acm.org/10.1145/1989656.1989657

[2]	Nicolas Kourtellis, Tharaka Alahakoon, Ramanuja Simha, Adriana Iamnitchi
	and Rahul Tripathi. 2013. Identifying high betweenness centrality nodes
	in large social networks. Social Network Analysis and Mining (SNAM).
	Volume 3, Number 4, Pages 899-914, Springer-Vienna.
	DOI=10.1007/s13278-012-0076-6, http://dx.doi.org/10.1007/s13278-012-0076-6

---------------------------------------------------------------------------

This zip contains three directories:

-------------
1. kpath-code
-------------

In the kpath-code directory there are c++ files and libraries to compile and 
be able to execute the kpath-centrality randomized approximation algorithm.
For your convenience there is also a Makefile in this directory that will
help you compile the necessary code and produce a single executable. If this
makefile does not work on your platform, you can also compile the various
modules at once:

g++ betweenness.o fibheap.o kpath.o readgml.o main_kpath.o -o kpath_centrality

User input:

The user input for these algorithms is shown when the executable is called
without the appropriate arguments:

$ ./kpath_centrality
Usage: ./Centrality <infile.gml> <outfile.csv> <k-path alpha> <k-path length>

Example of a correct execution:

$ ./kpath_centrality ../test-datasets/1K.gml ../test-datasets/1K.csv 0.2 20

In case that wrong values are given for the two parameters (alpha and length),
the software picks typical values.

If the input graph is unweighted, the value "1" should be used to signify this.
A weighted graph with integer valued weights is recognized by the software and
the appropriate routines are called.

The output will be stored in the file given as the second argument and will 
be in the csv format. For easiness, the brandes algorithm is also executed
first, to produce the real betweenness centrality values for vertices.
Besides some simple time counts reported in the beginning of the output file,
a list of results is printed at tuples: <vertex,betweenness,kpath-score> 

-------------------------------
2. rand-brandes_adap-sampl-code
-------------------------------

In the rand-brandes_adap-sampl-code directory there are c++ files and libraries
to compile and be able to execute two other betweenness approximation algorithms:
the randomized brandes and the adaptive sampling approximation algorithms.
For your convenience there is also a Makefile in this directory that will
help you compile the necessary code and produce a single executable.

User input:

The user input for these algorithms is shown when the executable is called without
the appropriate arguments:

$ ./rand-brandes_adap-sampl_centrality
Usage: ./rand-brandes_adap-sampl_centrality <infile.gml> <outfile.csv>
<epsilon for rand-bet> <c-threshold for adap-sampl> <pivots for adap-sampl>

Example of a correct execution:

$ ./rand-brandes_adap-sampl_centrality ../test-datasets/1K.gml ../test-datasets/1K.csv 0.05 5 20

If the input graph is unweighted, the value "1" should be used to signify this.
A weighted graph with integer valued weights is recognized by the software and
the appropriate routines are called.

The output will be stored in the file given as the second argument and will 
be in the csv format. For easiness, the brandes algorithm is also executed
first, to produce the real betweenness centrality values for vertices.
Besides some simple time counts reported in the beginning of the output file,
a list of results is printed at tuples: <vertex,betweenness,rand-brandes-score,adap-sampl-score>

----------------
3. test-datesets
----------------

In the test-datasets directory there are some small datasets in .gml format that allow
you to test the algorithm and get some results. In case you have other datasets in a
text-based format of 3 columns as an edge-list (first two columns) with integer weights
(3rd column), you can use the code in "fileToGML.cpp" to transform these datasets into
.gml format files.

Example execution (after successful compilation):

./fileToGML 1K.txt 1K.gml
