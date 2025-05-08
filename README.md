# DuckDuckGo_JmeterProject_PlanIT

**1. You have a requirement which states
"The system should scale to 2000 users".

a.) What other questions would you need to ask in order to get enough information to create
a workload model.**

	--> Get the application architecture and the components involved for testing (In Scope and Out of Scope). Also, ask if the application is already in PROD or a new one (which needs to be baselined)
	--> Ask for the peak load, TPS/TPH, users, SLAs for Response time, Business/Performance critical transactions to be performance tested
	--> Gather PROD environment details  for the number of application servers and peak load observed in PROD, if it's an existing application already deployed in PROD.
	--> Understand the PROD behavior to analyze if 2000 users a rethe maximum users or they all are accessing the application all time 
		
b.) Can you re-write the requirement so that it is more descriptive and testable. (You can use
made up values.)

Number of users = 2000
Total test duration = 1 hour
Number of Transactions = 2

Total number of transactions for the entire test duration (Transactions per hour) = 4000 Txns (2000 vusers * 2 Txns)

TPS (Transaction per second) = 4000/ 3600 = 1.11 


 







