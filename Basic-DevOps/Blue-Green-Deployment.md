---
parent: Basoc DevOps
title: Blue-Green Deployment
---
# Blue-Green Deployment 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(aka Red-Black or A/B Deployment)

You are doing continuous delivery [Humble10] as part of DevOps by making deployment as automated and quick as possible. You are releasing to a live environment that has potentially many users.

**How can we deploy reliably and with confidence of not negatively impacting many users?((

Building and releasing into production environments may require several steps, such as transferring and replacing deployment artifacts (e.g., executable files, JAR files, Docker images), updating property files, altering database structures, reconfiguring infrastructure elements (e.g., message routing in an API gateway). This process can be tedious and error prone.

Automating the testing and deployment process is challenging, due to its complexity and uncertainty, thus requiring a lot of expertise and effort.

Lack of validation or testing of your release can be dangerous and costly.

It can be expensive to duplicate the entire production environment. Any other alternatives will be only a simpler replica, possibly not emulating all the issues of production.

New releases have various risks that can negatively impact the business (e.g., loss of funds), if problems arise. New releases that cause problems need to be rolled back quickly and reliably.

Therefore,

**When releasing, have two environments that are nearly identical. One is the live environment. Release into the non-live environment, after validating the release, switch all network traffic to the new environment disabling the previous live environment.**

This type of deployment process is referred to as “blue-green deployment”. Blue-green deployments require two nearly identical production environments (called "blue" and "green") where deployments are made The two environments can be, for example, two physical or virtual machines, two nodes on a Kubernetes cluster, to mention a few.

At any time only one of the blue-green environments is live. For example (see Figure 1), let's say the green environment is currently being used for live production. When you have a new release, you deploy your system and do your final testing in the other (blue) environment. Once the software is working in the new environment (blue), you switch all live access so that all incoming requests now go to the new tested (blue) environment. The previous production environment (green) is now idle and ready either for a rollback, for emergency use, or for the next release. As you have new releases, you continue to switch back and forth between the blue and the green environment. 
            
Figure 1: Blue-Green Deployment

Switching the live version from v1 to v2, or rolling back from v2 to v1 can still be complicated, as we should allow requests currently being processed to finish successfully before the transition. Your design might handle this through some replication and ramped release strategy, or possibly putting the systems into a read only stage during the transition.

**Advantages of Blue-Green Deployments**

Foremost, blue-green deployment significantly decreases the downtime for rolling out a new version. 
Blue-green deployment enables quick version rollback: after deploying to one environment, if a problem is discovered you can easily switchback and start using the previous environment. You may have to cleanup some transactions that happened during the rollout of the failed environment.

With blue-green deployments you always have a backup environment ready in case the production environment becomes unavailable. Having the two environments may also allow independent maintenance in the infrastructure. For example, let’s say blue and green environment are two separate VMs. When blue is active, you may perform upgrades to the green environment VM. Then when green becomes active, you can perform the upgrades on the blue environment VM. The application is not affected. 

**Disadvantages of Blue-Green Deployments**

Blue-green deployments require organizations to have two identical sets of production environments, which can lead to significant added costs and overhead without actually adding capacity or improving utilization. As an alternative, there are other strategies that can help such as canary or rolling deployments. Canary deployment releases the new system to a small limited number of users, while rolling deployment staggers the rollout of new code across servers, usually to a server with limited number of users first.

When the new version requires database schema changes and/or data migration, employing blue-green poses an additional design challenge. There are two main alternatives:
*When there is a single centralized database. make the database structure changes backward compatible, that is, the old code will be able to access the new database structure. Complementarily, the new version code should be backward compatible, that is, the new code will be able to access the old database structure.   
*Make each version access a separate database (separate DB server or separate logical space/owner within the same DB server). In this case, the data is replicated across the old version DB and the new version DB. Therefore, a data synchronization mechanism must be established. This is an eventual consistency setting that has the additional drawback that an application may consume stale data.

Blue-green deployment can be problematic when the new version contains API changes that make old client applications incompatible. In this case, we might need an interceptor placed between the clients and the old and new application to perform message transformations to deal with the API changes.

Blue-green deployment can use feature toggles to emulate a form of canary deployment, by toggling on/off certain features for certain users roles.

Blue-green deployment can be used in conjunction with canary deployment. In other words you can push the new release completely to the second environment. And then route selected users from the first environment to the second environment in a canary fashion. 



