# DuckDuckGo_JmeterProject_PlanIT

****1. You have a requirement which states
"The system should scale to 2000 users".

a.) What other questions would you need to ask in order to get enough information to create
a workload model.****

- Get the application architecture and the components involved for testing (In Scope and Out of Scope). Also, ask if the application is already in PROD or a new one (which needs to be baselined)
- Ask for the peak load, TPS/TPH, users, SLAs for Response time, Business/Performance critical transactions to be performance tested
- Gather PROD environment details  for the number of application servers and peak load observed in PROD, if it's an existing application already deployed in PROD.
- Understand the PROD behavior to analyze if 2000 users a rethe maximum users or they all are accessing the application all time 
		
**b.) Can you re-write the requirement so that it is more descriptive and testable. (You can use
made up values.)**

Number of users = 2000
Total test duration = 1 hour
Number of Transactions = 2

Total number of transactions for the entire test duration (Transactions per hour) = 4000 Txns (2000 vusers * 2 Txns)

TPS (Transaction per second) = 4000/ 3600 = 1.11 

**2. Please provide and example of when you were involved the resolution of a
performance / scalability defect.
a. How was the defect found
b. How was it diagnosed
c. How was it resolved
d. How was the resolution proven
Please state your involvement in each of the processes.**

	Example 1:

While testing an application that has been deployed on the AWS AutoScaling Group, I observed poor performance and scalability issue.

- The Auto Scaling Group was defined with 12 initial application instances (active) and can scale up to 60 application instances based on the incoming load and treshold has been set at 40% resource utilization to scale down and 60% utilization to scale up. This was defined in a way that the instances can scale up/ down based on the traffic/load, where AWS lambda functions have been implemented to support this functionality. There was a step function that will be triggered if an instance scales up or down.

- To execute this test scenario, the load has been increased/decreased eventually in order to scale up (to 60 insatnces) or down the application instances and also run at steady state TPS whenever a new instance is up/down to observe the behavior of the individual instance and all the active instances of Auto Scaling Group as a whole.

- There is a time delay of 5 mins between each step function. Each instance takes upto ~10-15 mins to scale up and ~5 mins to scale down. (These time delays between that functions have been identified during testing). 

- At 48th instance under load, applcication started crashing as it was unable to handle the load and each instance took around ~15 minutes to be active to take in traffic which had put other instances under huge load. So, AutoscalingGroup was able to handle only 48 instances at max and found the breaking point. 

- This made to cover another test scenario (Spike testing), to observe the behavior when there is an expected peak usage of the application. For example, flights booking during peak season or e-shopping sales day. to execute this scenario, huge load (>100% of actual load) was induced and observed the performance. As suspected, application had less performance and was unable to handle the load and scale up to take in the additional load. 

- This helped the Clients to be prepared for the peak load to set the required number of instances, instances with high specifications and adjust accordingly in PROD to overcome the peak load.

	Example 2:

- An application had performance issues with respect to the resource utilization, as it couldn't handle the expected load. As part of performance, I suggested to either have high-spec application server or to add another application server to handle and balance the expected load. This is because there were no functionality or code took too long for processing.


**3. As well as creating a script in a tool to do the performance testing, what other factors would
need to be considered for a performance testing engagement?**

- As part of performance testing engagement, we have to the stages of performance testing life cycle. 

- Gather and understand Non functional requirements (NFR) from the business team/analyst for the application infrastructure details, performance critical txns, peak load, SLAs for Response time, etc. Analyze these NFRs and create a NFR document consisting of these details. Also, get the project timelines to estimate the testing efforts. If working in an Agile model, ensure that we need to understand the complexity of application testing and efforts are to be planned accordingly with the number of resources (performance tester available to test in order to complete the testing and having some buffer period allocated to handle unknown risks/defects associated with the application under test or with the testing tools, etc. 
	
- Based on the complexity of testing, we can breakdown the feature into user stories with story points defined, mapping them to the sprint and executing and delivering the work.
	
- Once NFRs are gathered, determine the test plan/strategy that includes the application architecture, environment details, resources needed, tools to be used, test data, workload modelling, identifying the dependencies and risks associated, test types to be performed (Ex. load test, stress test, endurance test, etc) , scope of testing, etc.

- Create the test scripts and execute the test using the performance testing tools with the appropriate workload and ensure that we have covered the necessary test types (Ex. load test, stress test, endurance test, etc) as defined in the test plan. Monitor the test using monitoring tools and collect the results for further analysis to determine the application's performance.

- We need to keep the Client updated with the testing status and make sure that we don't give any surprises at the end. Deliver the outcomes on the work done at each PTLC phase, so that everyone remains on the same page and discuss	for any dependencies or risks that might affect the testing cycle. Provide the detailed analysis indicating the Key performance indicators (KPIs) and identify if there could be any perfromance issues that might occur and provide performance suggestions to overcome the issue.

 







