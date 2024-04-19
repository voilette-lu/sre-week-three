#### Problem Statement

Ticketing System Challenges: The ticketing system for alert management had been a major point of contention among engineers. Complaints included recurring obsolete issues and a lack of clear prioritization for incoming issues. An example of the ticketing system's output is as follows:

Zone XQ: EndpointRegistrationTransientFailure
Zone OH-1: EndpointRegistrationTransientFailure
Zone OH-1: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone OH-1: EndpointRegistrationTransientFailure
Zone OH-1: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone AB: EndpointRegistrationTransientFailure
Zone AB: LLMBatchProcessingJobFailures
Zone AB: EndpointRegistrationFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone OH-1: EndpointRegistrationTransientFailure
Zone OH-1: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone AB: EndpointRegistrationTransientFailure
Zone AB: LLMBatchProcessingJobFailures
Zone AB: TooFewEndpointsRegistered
Zone AB: LLMModelStale
Zone OH-1: EndpointRegistrationTransientFailure
Zone OH-1: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone XQ: EndpointRegistrationTransientFailure
Zone AB: EndpointRegistrationTransientFailure
Zone AB: LLMBatchProcessingJobFailures
Zone AB: EndpointRegistrationFailure
Zone AB: LLMModelVeryStale

#### Solutions

Identify potential solutions or products, whether free or commercial, to address the toil in the ticketing system.

##### recurring obsolete issues

1. Group the occurening issues and count how many occurences:
- EndpointRegistrationTransientFailure, 23;
- LLMBatchProcessingJobFailures, 3;
- EndpointRegistrationFailure, 2;
- LLMModelStale, 1;
- LLMModelVeryStale, 1;
- TooFewEndpointsRegistered, 1;

Above data points can assist us to proritize the toil reduction. For example, we can see that EndpointRegistrationTransientFailure happens 23 times so this could be the first issue to reduct toil by introducting automations.

2. the other observation is that one issue was alerted multiple times. The timestamp of the alerts should be added to the alert payload and group into the same incident if possible to reduce the number of alerts. 

##### lack of clear prioritization

As we can see from the alert information, the alerts took place in different zones:
- XQ;
- AB;
- OH-1;

Combining the above 6 issue types, we can build a severity matrix, taking into consideration of the business impact of each issue and the criticality of the zones. So that each alert comes with a severity of INFO, LOW, MEDIUM, HIGH, or CRITICAL. 

PagerDuty could be a potential product to set up the alerts routing to a PagerDuty group, and configure if the alert severity logic to trigger a phone call.