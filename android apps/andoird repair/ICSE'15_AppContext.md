###<center>AppContext: Differentiating Malicious and Benign Mobile App Behaviors Using Context###
　  Mobile malware attempts to evade detection during app analysis by mimicking security-sensitive behaviors of benigh apps that provide similar functionality, making it much more difficult to detect. This paper propose that the malicious and benign behaviors within apps can be differentialted based on the context that trigger security sensitive behaviors, ie., the event and conditions that cause the security-sensitive behaviors to occur. And they introduced AppContext, an approch of static program analysis that extracts the contexts of security-sensitive behaviors to assist app analysis.

####Introcuction####
---
　Similar to PC malware, mobile malware has begun taking steps to evade detection by camouflaging as benign apps, whichh make it more difficult to by detected by analysis tools. In android, a large portion of behaviors are triggered by system events, which is much hard to be detected by users. And on the other hand, it is very likely that the reviewers and tools cannot detect the malware when the environmrntal conditions that trigger the malicious behaviors are not met.
　Based on above abservation, AppContext produced to use the context to determine whether the behavior is benign or not. So, expressing contexts in mobile apps is a non-trivial task. They define a context for a security-sensitive behavior as a tuple containing an activation event and a series of context factors.

####AppContext####
---
#####Security-sensitive Behavior#####
　AppContext consider security-sensitive behavior as an invocation of a security-sensitive method. They divided security-sensitive methods into 3 categories:
	1. permission-protected methods
	2. sources or sinks in information flow
	3. reflection methods or dynamic loading methods

#####Activation Events#####
　The activation events are the external event that trigger the security-sensitive methods, including UI events(user interaction), system events hardware events(pressing HOME). After geting the extended call graph(including ICC) and security-sensitive method, activation events can be easily determined.

#####Context Factor#####
　From the ECG, we can fing all the path from activation event to security-sensitive methods. AppContext extracts those paths and forms RICFG(reduced inter-procedure control-flow graph). For statement Si in the path, if it is a conditional statement, its conditional vaules will be considered as the context factor.