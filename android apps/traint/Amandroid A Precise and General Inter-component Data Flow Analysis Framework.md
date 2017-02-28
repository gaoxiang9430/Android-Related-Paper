###<center>Amandroid A Precise and General Inter-component Data Flow Analysis Framework###
Amandroid actually is an extension of FlowDroid. Both Amandroid and FlowDroid are static analysis method in order to find the sensitive data transmision path. The difference is that Amandroid had taken the inter-component control and data flow into account.

####Introduction####
Current solution to android security problems is mostly reactive, for instance, pulling an app off the market after potential damage may have already been done. To find the vulnerabilities, app market may conduct static or dynamic analysis. For dynamic analysis, they run an app in a testing environment with the hope of identifying the problemativ behaviors. Analysis precision can be characterized as metrics on:
	1. false negatives(missed behaviors)
	2. false positive(false alarm)
There are some challenges in android static analysis:
	1. Android is an event-based system.
	2. The Android runtime consists of a large base of library code that an app depends upon.
	3. Android is a component-based system and makes extensive use of inter-component communication(ICC). And capturing all ICC flows accurately is a major challenge in static analysis.

####Main Step####
	1. Build precise inter-procedural control flow gragh(ICFG) of the whole app, that is both flow and context sensitive.
	2. Amandroid treats ICC just like method calls, the both control and data can flow on the edge. So, according to the ICFG, inter-procedure Data Flow Graph can be extablished.
	3. Amandroid builds the data dependence graph(DDG) of the app from the IDFG.