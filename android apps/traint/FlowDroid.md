###<center>FlowDroid###

FlowDroid is a novel and highly precise **static taint analysis tool** for android apps. FlowDroid handles the callbacks invoked by the android framework while keep low false positive rate.

On the other hand, this paper proposed an **open test suite DROIDBENCH** for evaluating the effectivemess and accurancy of taint-analysis tools for android. FlowDroid achieved better results than **IBM AppScan Source and Fortify SCA**.



####Intruduction####

Android sensetive data includes **location information, contact data, pictures, SMS messages**, etc. Even application thar are not malicious and were carefully programmed may suffer from attacks, too. Because many developers include **third party libraries**.

the challenges of static analysis:

	1. Static analyse must not only model this lifecycle, but also intergrate further callbacks for system-event handling, UI interaction, and others.

	2. This detection requires a model of auxiliary information storeed in the manifest and layout XML files, for example, button can be defined in XML.

	3. Aliasing system



####FlowDroid Modelling of Lifecycle####

#####Multiple enrty poings#####

Unlike jaca programs, android applications do not have a main method. Apps comprise **many entry points** such as methods that are implicityly called by the Android framework. There are four components: activites, services, content providers and broadcast receivers. Those components can be called by the android framework.

#####Asynchronouly executing components#####

An application can contain multiple components, e.g., three activities and one service. The executed **order of activities** is arbitrary, and the services can be excuted **in parallel**. So, considering each possible ordergings would be very expensive. FlowDroid bases its analysis on **IFDS**, an analysis framework which is not path sensitive.

#####Callbacks#####

Callback is a function that can be incvoked under certain conditions and events, for example, a button click. In android, there are two methods to register callback handlers. Firstly, callbacks can be defined declaretively in the **XML** files of an activity. Secondly, the can also be registered using well-know call to **specific system method**, such as addListener.

To find the callbacks registered in the application code, FlowDroid first computers one call gragh, and then used to scan for calls to specific Android system method. As for callbacks defined in the layout XML files, the respective XML file is **mapped to one or more application components** using the respective layout controls.



####precise Flow-sensitive Analysis####

#####Taint analysis#####

	1. taint left-hand side if any of the operands on the right-hand side is tainted;

	2. taint all array if one array elements are tainted(conservatively);

	3. clear all path rooted from x(x.f, x.f.g, etc) if x if cleared;

	4. call function, replace actual with formal parameters;

	5. inverse translation when method return;

#####Alias analysis#####

Whenever a tainted value is assigned to a heap location such as a firld or an array, FlowDroid search backwards for aliases of thr target variable. To maintain context sensitivity, when triggering a backwards or forwards analysis, FlowDroid insert the original context into the analysis. To maintain flow sensitivity, FlowDroid uses activation statements. Only the statement excuted after source can be regarded as a sink.





























