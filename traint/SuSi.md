###<center>SuSi:A tool to fully automated classification of android sources and sinks###
Many security testing tools are as good as the privacy policies they are configured with. Policies typically refer to a list of sources and sinks which may leak data to untrusted observers. However, sources and sinks are moving target, new version operating system may introduce new methods.SuSi is a novel and fully automated machine-learning approach for indentifying sources and sinks directly from **Android source code**.

####Introduction####
Smartphones are widely used to store and process highly sensitive information such as **text messages, private and business contacts, calendar data**, and more. Furthermore, while a large variety of **sensors** like GPS allow a contextsensitive user experience, they also create additional privacy concerns if used for tracking or monitoring.
Some previous works consider methods as sources and sinks that require a permission to execute. However, this method is imprecice, because some data leak may not need additional permissions. For example, if we write sensitive datas into a file, and make it publicly accessible, it will result in sensitive data leak.

####Definition of Sources and Sinks####
	1. Android Sources: Sources are calls into resource methods returning non-constant value into the application code. For instance, getDeviceId() is regarded as a source, because this method will return a different value on every phone.
	2. Android Sinks: Sinks are calls into resource methods accepting at least one non-constant data value from the application code as parameter, iff a new value is written or an existing one is overwritten on the resource.
A milicious app can try to call the official android framework API as well as the code of pre-installed apps. So, SuSi does not only analuze the framework API but also the per-installed apps.

####Fully Automated Classification####
This machine-learning method contains two rounds, the first one is to classify methods as sources and sinks or neither. and the second one is to further classify sources and sinks into categories.
To perform the machine-learning, some features should be extract from training set and test set. For identifying sources and sinks, SuSi uses the following classes of features. For instance:
	1. Method Name The method name contains or starts with a specific string, e.g., “get”, which can be an indicator for a source.
	2. Method has Parameters The method has at least one parameter. Sinks usually have parameters, while sources might not.
	3. ......

This paper chosed 14 different kinds of source-categories that we identified as being sufficiently meaningful for the different Android API methods: account, bluetooth, browser, calendar, contact, database, file, image, location, network, nfc, settings, sync, and uniqueidentifier.For the sinks, we defined 17 different kinds of categories: account, audio, browser, calendar, contact, email, file, location, log, network, nfc, phone-connection, phone-state, sms/mms, sync, system, and voip.

#####DataFlow Features#####
Considering a method’s signature and the syntax of its method body alone is insufficient to reliably detect sources and sinks. So SuSi perform a data flow analysis, that is, to find a data flow from the source to sink.
#####Prefiltering#####
Because abstract methods have no own behavior, SuSi remove such method from consideration. SuSi also prune all private methods and all methods in private classes.