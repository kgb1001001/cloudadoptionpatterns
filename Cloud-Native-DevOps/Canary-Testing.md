# Canary Testing

You are following a Cloud-Native DevOps approach and may be deploying an application with a [Microservices Architecture](../Microservices/Microservices-Architecture.md). You are deploying new and improved services at an ever increasing rate, but you have a large number of users that can only withstand a minimal amount of disruption during the process. 

**How do you determine that a new service version can be put into production without undue risk of disruption to the production system users?** 

The Microservices idea brings along with it the fact that each service can be deployed through its own pipeline, but importantly at its own rate.  That means that as a team becomes more proficient and higher-performing, that the time it takes to develop and deploy new service versions decreases, which could increase the number of times that a user could be disrupted by a bad rollout.

At one level, the reduced blast radius of decisions within a Microservice means that each change would be smaller, and thus potentially less disruptive, but the possibility of disruption, at an increased rate remains.  What is needed is a way to not only minimize the potential scope of decisions, but also minimize the potential number of users that could be disrupted by a change.

Therefore,

**Employ a Canary Testing Approach through which a new service or service version is only rolled out to a small number of users initially.  If the change does not prove to be disruptive, then roll out the service to the remaining user population.**

This approach is called "Canary Testing" because of the analogy to the way canaries were taken in cages down into mines in the 19th century.  If the canary died, the miners knew that the air in the mine was no longer breathable, and left as quickly as they could before they were overcome by poisonous gases. In this analogy, a small group of users (possibly just internal users) are treated as canaries - if they have a bad experience, the rollout is stopped and the problem is mitigated while leaving the larger group unaffected.  If the test is successful, then the rollout continues to the larger group.

Canary tests can be used in conjunction with [Red-Black Deploys](Red-Black-Deploy.md) in that often you would start with a Canary test before rolling out to a progressively larger set of groups. Canary Tests can be automated and made part of a standard CI/CD Pipeline and are built into many CI/CD products such as [CloudBees](https://www.cloudbees.com/) as well as being part of Service Mesh open source projects like [Istio](https://istio.io/latest/blog/2017/0.1-canary/). Products such as [LaunchDarkly](https://launchdarkly.com/) combine Canary Tests with Feature Flags and other rollout approaches. 
