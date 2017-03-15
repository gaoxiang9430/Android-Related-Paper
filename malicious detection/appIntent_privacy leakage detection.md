###<center>AppIntent: Analyzing sensitive data transmission in Android for privacy leakage detection###
Android phones carry much personal information, attracting malicious developers to embed code in Android applications to steal sensitive data. Transmission of sensitive data in itself does not indicate privacy leakage, a better indicator may be whether the transmission is by user intention or not. When transmission is not user-intended, it is more likely a privacy leakage.
AppIntent first apply static analysis to the target app to identify the possible execution under analysis. And then, AppIntent generate event-based constraints for these paths, which  presents all the possible event sequencess for a given path. Finally, AppIntent collects the input data and user interaction that lead to the transmission, and shows them to analyst.
####Background####
Unlike java or c program language, android do not have a main entry point. And android apps are event-drived program, which bring much more challenges to symbolic execution. There are two major events in android: callbacks to manipulate the state transition and listeners to handle system events and user interactions with GUI component. We can not determine the time which event will be triggered, even the order of the events, which further worsen the already notorious search space explosion problem of symbolic excution.

####Event-space constraint guided symbolic excution####
To reduce the search space, AppIntent only consider the event that may trigger the instruction in the sensetive data transmision path. So, the first step is to get the transmision path using static analysis. Than, construct the event-space constraint graph according to the path infomation.
Event-space constraint graph contains two type of nodes: critical node and essential node. Critical node represents an event of which the event handler method contains at least one instrction of a given data propagation. And essential node represents the event which is a prerequisite for a critical event.
To find the critical events, for each instruction in the path, AppIntent traverse the call graph to find all events that might trigger it. As for essential events, AppIntent also use call graph and backward analysis to get it.
The next step is symbolic excution, AppIntent just focuses on the event-space constraint graph which can reduce the search space significantly. After symbolic excution, we can get the event sequences and origin inputs.


####Possible Weakness####
	1. User-intended behavior can also result in data leakage(eg. save file, malicious behavior in the user-intended path);
	2. Not all data leakage is relevant to GUI;
	3. unintended transmission may not cause data leakage(eg. automate update OS).