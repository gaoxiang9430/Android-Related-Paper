![android](others/ANDROID.png)
_______
###Content
* [Android Repair](#1)
* [Android Malicious Behavior Detection](#2)
* [Crash Testing](#3)
* [Others](#4)

<h2 id="1">Android Repair</h2>

####1. [paper1]()####
testhaloow
####2. [paper1]()####
test content



<h2 id="2">Android Malicious Behavior Detection</h2>

####1. [Detecting Passive Content Leak and Pollution in Android Application(NDSS'13)](https://www.internetsociety.org/sites/default/files/02_3_0.pdf)####
This paper studied two vulnerabilities rooted in an unprotected Android component. To share data with other apps, the interface of **content provider** is open by default, which provides an opportunity for other apps to access its sensitive data or modify its configuration. This paper proposed to use **static analysis** (combining CFG and DFG) to find the potential vulnerabilities. They found **2% and 1.4%** of apps they tested are susceptible to these two vulnerabilities.

####2. [Analyzing Inter-Application Communication in Android(MobiSys'11)](https://dl.acm.org/citation.cfm?id=2000018)####
test content


<h2 id="3">Crash Testing</h2>

####1. [IntelliDroid(NDSS'16)](android\ apps/crash\ testing/intellidroid-targeted-input-generator-dynamic-analysis-android-malware.pdf)####
The **goal** of IntelliDroid is to generate input that specifically exercises malicious path in an application. IntelliDroid combined static and dynamic analysis. **Static phase**: To find the malicious path, they targeted **specific APIs** and generated inputs to trigger them. Firstly, they identified the event handlers that invoke the targeted APIs, and find the **call path** to those APIs within the event. Then, extract the **path constraints**. Those path constraints may depend on heap variables that are set in other event handlers. So, IntelliDroid extracted a **supporting event-chain**. **Dynamic phase**: IntelliDroid will solve the **path constraint** just before input value **injection** and inject the input into the device-framework interface that calls the event handler.
####2. [DART: Directed Automated Random Testing](android\ apps/crash\ testing/dart-godefroid.pdf)####
Unit testing applies to the individual components of a software system. In practice, it is so hard and expensive to perform because it need a test driver and extral code to test function correctness, meanwhile, some software bugs depend on global field.

####3. [Testing Android Apps Through Symbolic Execution](https://dl.acm.org/citation.cfm?id=2382798)####
The goal the this paper is to **symbolic executing Android program** in [JPF](http://babelfish.arc.nasa.gov/trac/jpf/wiki/projects/jpf-symbc)(Java PathFinder). To symbolic execute android program, there are some chanlleges. Firstly, Android apps depend on a lot of **libs** that are not available outside the device or emulator. Secondly, Android programs have more **path-divergence** problems than traditional Java program, because of the multiple components and communication between them. Finally, Android is an event driven system and test inputs depend on **user interaction**. So this paper proposed a method to convert android program into java program that can be executed in JVM. First they developed a **model to simulate the behaviors** of actual Android lib. And secondly, they leveraged program analysis to **correlate events with their handler** for generating Android-specific drivers.

<h2 id="4">Others</h2>