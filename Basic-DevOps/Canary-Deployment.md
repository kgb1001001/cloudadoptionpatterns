---
parent: Basoc DevOps
title: Canary Deployment
---
# Canary Deployment 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(aka Staged Deployment)

You are doing continuous delivery as part of DevOps by making deployment to different environments as automated and as quick as possible. You are releasing to a live environment that has potentially many users.

** How can we get feedback on the new release, verify if it is working properly, and get early reactions from users? **

Building and releasing into production environments can be tedious and error prone.

Automating the testing and deployment process is challenging and requires a lot of expertise.

Lack of validation or testing of your release can be dangerous and costly.

New releases have various risks that are important to validate before release to all users.

New releases made available to all users can can severely hurt the confidence on the application and negatively impact the business if they are flawed, 

Therefore, 

**First deploy the change to a limited number of users or servers to test and validate the release. This could include verifying the release works properly and/or getting acceptance feedback from your users. After you have validated the release, then roll the change out to all servers or users.**

This limited release is called canary deployment. Canaries used to be used in coal mining as a warning system making sure there were no toxic gases before miners entered the mine. In a sense we are doing the same thing with canary deployment. Before releasing to a wide audience, the system is first deployed to one or more canary servers (see figure 2). These might be for trusted internal users. After the release is validated, make it available to other users and servers. Validation includes getting feedback from canary users and also monitoring runtime properties of the new version. If significant flaws are found, the release of the new version to all users is cancelled.

Figure 2: Canary Deployment

**Advantages of Canary Deployments**

Canary deployment allows finding problems before they are pushed out to all users. These problems can be bugs in the new release, unsatisfactory latency or throughput, poor user experience, security breaches, among others. The final result is improved quality of new releases.

**Disadvantages of Canary Deployments**

Canary deployments require you to control what users see the canary release and hence requires a supporting infrastructure for moving users from the main system to the canary system, and vice-versa. This supporting infrastructure has to be configured and governed, and may include routers, network proxies, authentication mechanisms,  and configuration files.

The canary deployment represents a delay on the rollout of the new release to general users. 

Similar to blue-green deployment, canary deployment incurs the cost of having two production environments.

**Alternatives to Canary Deployments**
An alternative to canary deployment is to deploy the new version to everyone with feature toggles turned off for the new features. Then you selectively enable features to different users. As you validate the release, you increase the number of users access to the new features. This approach requires a special implementation using “feature toggles” combined with canary user identification.

*   *   *

You can also use blue-green deployment to push the release out to the green server for example, and then only move a few users from the blue server to the green server for the canary deployment. Then as you validate the release you can move more and more users to the green server.
