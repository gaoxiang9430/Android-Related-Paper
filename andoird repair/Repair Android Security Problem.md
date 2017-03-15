###<center>Repair Android Security Problem###
####Fixing android security problems####
#####Potential Challenges#####
	1. target source code or apk? source code seems not significant
	2. how to determine a data leak (according to the return data? Event sequence?)
	3. keep original property
	4. how to repair (remove, modify?)
#####Potential Idea#####
	1. build a sensitive data flow gragh
	2. test user-intended data transmission(users are unaware of this kind of transmission because the malicious apps always do that in a stealthy manner.)

#####Target SMS#####
######Basic Idea######
	1. build control flow graph using static analysis
	2. get the events along with the tainted path

######SMS operation######
	1. User composes the SMS body and sends it instantly using the UI of the subject app
	2. User composes the SMS body and schedules the time when SMS should be sent. Then, the subject app will send SMS out automatically at that time point.
	3. User composes the SMS body and configures the subject app to automatically send that SMS as a response to an incoming SMS or phone call when he/she is busy (e.g., meeting, driving).
	4. User inputs the forward number and configures the subject app to automatically forward every incoming SMS to that number.
	5. User configures the subject app to send SMS with appended signature.