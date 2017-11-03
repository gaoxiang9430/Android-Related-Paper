![android](others/ANDROID.png)
______

<h2 id="1">Content</h2>

* [Android Repair](#1)
* [Android Malicious Behavior Detection](#2)
* [Crash Testing](#3)
* [Others](#4)
* [Tools](#5)

<h2 id="1">Android Repair</h2>

#### 1. [FixDroid(CCS'17)](http://eprints.lancs.ac.uk/88075/1/CCS_FixDroid_CR.pdf) ####

FixDroid is a plug-in of android studio, which help inexperienced developer to develop applications with less security problems (security and privacy). Many Android apps have poorly implemented security mechanisms resulting from developer who are inexperienced, distracted or overwhelmed. Android Lint has many disadvantages. This paper introduces several operators for automitically fixing android vulneribilities.


<h2 id="2">Android Malicious Behavior Detection</h2>

#### 1. [Detecting Passive Content Leak and Pollution in Android Application(NDSS'13)](https://www.internetsociety.org/sites/default/files/02_3_0.pdf) ####

This paper studied two vulnerabilities rooted in an unprotected Android component. To share data with other apps, the interface of **content provider** is open by default, which provides an opportunity for other apps to access its sensitive data or modify its configuration. This paper proposed to use **static analysis** (combining CFG and DFG) to find the potential vulnerabilities. They found **2% and 1.4%** of apps they tested are susceptible to these two vulnerabilities.

#### 2. [Analyzing Inter-Application Communication in Android(MobiSys'11)](https://dl.acm.org/citation.cfm?id=2000018) ####

test content

#### 3. [Toward a Framework for Detecting Privacy Policy Violation in Android Application Code(FSE'16)](https://dl.acm.org/citation.cfm?id=2884855) ####
Software developers are entrusted by end users to not only care for their data, but disclose what exactly is being collected. So this paper proposes a semi-automated framework that consistss of a policy terminology-API method map and information flow analysis to detect misalignments. Firstly, they extract the API Terminology manually, which is a map from API method to policy phrases. Secondly, extracting the privacy policy terminology of the app from related documents. Finally, detect the voilation between the privacy policy provided by the developers and real implementation.


<h2 id="3">Crash Testing</h2>

#### 1. [IntelliDroid(NDSS'16)](https://pdfs.semanticscholar.org/4861/5e390327ca5218aef018c60938f0f2dc482b.pdf) ####

The **goal** of IntelliDroid is to generate input that specifically exercises malicious path in an application. IntelliDroid combined static and dynamic analysis. **Static phase**: To find the malicious path, they targeted **specific APIs** and generated inputs to trigger them. Firstly, they identified the event handlers that invoke the targeted APIs, and find the **call path** to those APIs within the event. Then, extract the **path constraints**. Those path constraints may depend on heap variables that are set in other event handlers. So, IntelliDroid extracted a **supporting event-chain**. **Dynamic phase**: IntelliDroid will solve the **path constraint** just before input value **injection** and inject the input into the device-framework interface that calls the event handler.

#### 2. [DART: Directed Automated Random Testing](https://dl.acm.org/citation.cfm?id=1065036) ####

Unit testing applies to the individual components of a software system. In practice, it is so hard and expensive to perform because it need a test driver and extral code to test function correctness, meanwhile, some software bugs depend on global field. DART first produced concolic execution.

#### 3. [Testing Android Apps Through Symbolic Execution](https://dl.acm.org/citation.cfm?id=2382798) ####

The goal the this paper is to **symbolic executing Android program** in [JPF](http://babelfish.arc.nasa.gov/trac/jpf/wiki/projects/jpf-symbc)(Java PathFinder). To symbolic execute android program, there are some chanlleges. Firstly, Android apps depend on a lot of **libs** that are not available outside the device or emulator. Secondly, Android programs have more **path-divergence** problems than traditional Java program, because of the multiple components and communication between them. Finally, Android is an event driven system and test inputs depend on **user interaction**. So this paper proposed a method to convert android program into java program that can be executed in JVM. First they developed a **model to simulate the behaviors** of actual Android lib. And secondly, they leveraged program analysis to **correlate events with their handler** for generating Android-specific drivers.

#### 4. [A Guided Genetic Algorithm for Automated Crash Reproduction (ICSE'17)]() ####

Manual crash relication is a labor-intensive task. Automated crash reproducation techniques have been proposed in the literature. Record-reply monitor software behavior via instrumentation to collect crash information when crash happend. Such technique suffer from practival limitation (performance, privacy issues). Post-failure approaches try to replicate crashes by exploiting data after crash.
The problems of current techniques is practical limitation, such as environment dependencies, performance overhead and so on. This paper proposed EvoCrash, a novel guided genetic algorithm(GGA). It first gived a **fitness function**, which is related to the (1)distance between executed statements and target statement, (2)distance between generated stack and the expected trace (3)whether the target exception is thrown or not. Secondly, it will make a initial population by insert at least one method of the crash is inserted in each initial test. And then **mutate or crossover** original test suite, and choose *K* fittest individuals as the tests suite in next iterations. After finite number of iterations, the **fittest test** case will be directly given to developer as starting point for crash replication and debugging.



<font color=#FF0000>Edsger Dijkstra "program testing can at best show the presence of errors but never their absence"</font>
<h2 id="4">Others</h2>
<font color=#FF0000> Hard to make enforcement both secure and backwards compatible with unmodified legacy applications on Android</font>

<h2 id="5">Tools</h2>

| Tools  |	purpose	| methodology |	rely on	|
| :----: |  -----   |   -----     | :-----: |
|FlowDroid|	flow analysis	|static analysis|	soot|	500(google play)+1000(virusShare)|
|dare|	retargeting to java Bytecode|	constraint solving and translate based on 9 rules |	|
|MFFA|	Media Fuzzing Framework for Android	||	FuzzBox	||
|Dynodroid	|Input generation	|observe-select-execute(dynamic and static analysis)|		|
|IntelliDroid|	Targeted Input Generator|	Dynamic and static analysis|	TaintDroid 	|
|Multi-Flows|	malware detection	|Analyze structure of information flow	|soot|
|DroidSIFT|	Semantics-aware malware detection|	static analysis|	soot|	|
|AppIntent|	extract context information for malicious behavior detection|	static analysis & dynamic analysis	|DED, soot, JPF, InstrumentationTestRunner	|
|AppContext|	extract context information and use machine learning to detect malware	|static analysis	|soot	|
|TriggerScope|	detect logic bombs |	Static analysis, symbolic execution, path predicate reconstruction and minimization|
|appSealer|	automatic generation of security-related patches	|static analysis & slicing & dynamic analysis|	Soot & TaintDroid||
|Automated Patching|	self-healing smartphone software to avoid further crash	|detection and bytecode rewriting||
|Reference Hijacking|	adopt enhancement on off-the-shelf devices	|||
|Pegasus|	enforce API and permission use|	static analysis & model checking & runtime monitoring|		|
|POSTER	|separate third-party lib with trusted code	| |	ARTist|
|Reliable Third-Party Library Detection|	third party lib detection|	Signature-based detection|||
