###<center>Safe Memory-Leak Fixing for C Programs###
Automate repair has become a promising direction for reducing manual effort in debugging. However, general apporaches to automatic bug fixing may face some fundamental difficulties. This paper just concentrate on specific fixing of  memory-leak bugs.
####Introduction####
Memory-leak fixing may also face several challeges. For example, we cannot easily **specify the condition of "no leak"** because there is no test case or an assertion can trigger those bugs apparently. To fix memory-leak problem, we need to insert a deallocation statement satisfying the following three conditions:
	1. In any execution, the memory chunk has to be allocated before the deallocation.
	2. There is no double free: no other deallocation will free this memory chunk.
	3. The memory chunk will not be used after the deallocation.
Besides, a further requirement is that we should insert the deallocation as early as possible.
Leak detection is strongly interrelated with pointer analysis. And recently, there are significant improvements on the efficiency of point analysis. This paper reuse existing pointer analysis algotithm as black boxes.

####Approch Overview####
#####Basic Idea#####
	1. Building a piont-to graph using pointer analysis, each node in the point to gragh is a memory object, and each edge represents the relationship between objects.
	2. identify the alloction procedures, use procedures and deallocation procedures.
	3. find an edge e where start from a memory allocation m, without deallocation and outgoing path from e does not contains Use(m)
#####Challenge#####
	1. point analysis enhencement: may contains some null point
	2. procedure identification
	3. Global variable: can be allocated, used or freed everywhere
	4. multiple allocation: each allocation should be followed a deallocation
	5. Loops: may contain a set of allocation and deallocation. extract loop procedure