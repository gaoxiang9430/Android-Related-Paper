![android](others/ANDROID.png)
_______
###Content
* [Android Repair](#1)
* [Android Malicious Behavior Detection](#2)
* [Crash Testing](#3)

<h2 id="1">Android Repair</h2>

####1. [paper1]()####
testhaloow
####2. [paper1]()####
test content



<h2 id="2">Android Malicious Behavior Detection</h2>

####1. [paper1]()####
testhaloow
####2. [paper1]()####
test content


<h2 id="3">Crash Testing</h2>

####1. [IntelliDroid(NDSS 2016)](android\ apps/crash\ testing/intellidroid-targeted-input-generator-dynamic-analysis-android-malware.pdf)####
The **goal** of IntelliDroid is to generate input that specifically exercises malicious path in an application. IntelliDroid combined static and dynamic analysis. **Static phase**: To find the malicious path, they targeted **specific APIs** and generated inputs to trigger them. Firstly, they identified the event handlers that invoke the targeted APIs, and find the **call path** to those APIs within the event. Then, extract the **path constraints**. Those path constraints may depend on heap variables that are set in other event handlers. So, IntelliDroid extracted a **supporting event-chain**. **Dynamic phase**: IntelliDroid will solve the **path constraint** just before input value **injection** and inject the input into the device-framework interface that calls the event handler.
####2. [paper1]()####
test content