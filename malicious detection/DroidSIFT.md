###<center>Semantics-Aware Android Malware Classification USing Weighted Contextual API Dependency Graph###

　Existing automated Android malware detection and classification can be divided into two general catageries: signature-based and machine learning-based. The former one can be easily evaded by bytecode-level transformation attacks. And prior learning-based works extract features from application syntax instead of program semantics, which are also subject to evasion. So this paper proposed a method to extract a weighted contextual API dependency graph similarity metrics to uncover homogeneous application behaviors.

__________________
####Introduction####
　To directly address malware that evades automated detection, prior works distill program semantics into graph representations, such as control-flow graph, data dependency graphs, and permission event graphs. These graphs are checked against manually-crafted specifications to detect malware. However, these method can potentially be evaded by polymorphic variants. Furthermore, the specifications used for detection are produced from known malware families and cannot be used to battle zero-day malware.
In google paly market, they use Bouncer vetting system to discovere malicious software. Bouncer performs a dynamic analysis to examine apps within an emulated android envionment for a limited period time. So, this method can be easily evaded by apps that perform emulaot detection, contain hidden behaviors during the short time period when the app is being vetted.
_____
####Implementation####
#####1, Behavior graph generation#####
They just considered the following aspects as essential when describing the semantic-level behaviors of an Android malware:
	1. API dependency: API call indicate how a app interacts with android framework. It is essential to capture the API calls an app makes and the dependencies among those calls.
	2. Context: The entry point that directly or indirectly trigger the call can reflect some sensitive information.
	3. Constant: Constands convey sematic information by revealing the calues of critical parameters and uncovering fine-grained API semantics.
Based on these three perspectives, they perform similarity checking, rather than seeking an exact match on the behavioral graphs. Since each API call plays a different role in an app, it contributes differently to the graph similarity. They emphasize security-sensitive APIs conbined with critical contexts or constant parameters. That is, giving different node with a weights.

Graph generation can be divided into two phases: entry point discovery, constant analysis and dataflow analyses.
In the entry point discovery phase, they have considered the asynchronous calls and recognized callbacks. Such as Thread.run() and onClick().
As for the constant analysis, they performed backward dataflow analysis on selected parameters and collect all possible constant values on the backward trace.
Then, they perform a globle dataflow analysis for security-sensitive APIs to discover data dependencies between API modes and build the edges on WC-ADG.

#####2, Scalable Graph Similarity Query#####
In the first step, they mentioned that they will assign a weight for each node. Instead of manually specify the weights on different APIs, they wish to see a near-optimal weight assignment. Intuitively, if two graph come from the same malware family and share one or more critical API labels, we must maximize the similarity between the two. They call such a pair as "homogeneous pair". If one graph is malicious and the other one is benign, even if they share one or more critical critical API labels, we must minimize the similarity between the two.  They call such a pair as "heterogeneous pair". Therefore, they cast the problem of weight assignment to be an optimization problem.
To quantify the similarity of two graphs, we first compute a graph edit distance. In this paper, they use the following formular:
![](./capture.PNG)

Given an app, the number of graphs in the database can be fairly large, so the design of the graph query must be scalable. In this paper, they insert graphs into indicidual buckets, with each bucket labeled according to the presence of critical APIs.

#####3, Malware Classification#####
Based on the graph similarity results, they conduct anomaly detection and sigature detection. In anomaly detection, they build a graph database for benign apps, and attempt to match the WC-ADGs of the given app against the ones in database. If no sufficiently similar one is found, an anomaly is reported. As for sigature detection, they build a database for malicious apps, if a sufficiently similar one is found, then a potential malware is reported.



















