---
title: Basic DevOps
nav_order: 15
has_children: true
---
# Basic DevOps Introduction
Continuous Integration and Delivery has become the de-facto standard for most Agile and Lean processes. Many of these development processes help teams respond to unpredictability through incremental, iterative work cadences and through empirical feedback. Regular delivery of reliable working software that has the highest value to those using or benefiting from the software is becoming more important for the success of many companies. Actually, the first principle behind the Agile manifesto is: "our highest priority is to satisfy the customer through early and continuous delivery of valuable software.” That has led to the acceptance of DevOps, which advocates automation and monitoring at all steps of software construction, from integration, testing, releasing to deployment. 

<!--

FIGURE TO BE UPDATED SOON
Figure 1: DevOps

NOTE I'M STILL EVOLVING THIS SO IT's NOT QUITE THERE YET.

However, blindly following Agile practices isn’t sufficient to help sustain delivering quality software at a good pace with confidence. Quite often system qualities, such as reliability, scalability, or performance, are overlooked or simplified until late in the development process, thus causing time delays due to extensive refactoring and rework of the software design required to correct quality flaws. There are other practices (patterns) that can help with this, such as reflection time, finding ways to improve, and building quality into the process and product from the start [YWA, YW, YWW14, YWW15, YWW16a, YWW16b]. 
The goal is to be able to safely and quickly release our software in a sustainable way. Continuous Delivery and DevOps focus on both automation and team practices that can help with delivering more quickly and reliably. Automation and a good pipeline that includes quality steps has proven invaluable for raising confidence in the release. This paper will focus on the “Quality Delivery Pipeline” as a practice that can help sustain delivering with confidence by addressing important qualities in the pipeline.

Nowadays, applications are released more frequently, sometimes many times per day. Deploying frequently helps organizations to be more agile by making changes that deliver business value faster, which includes ways to rapidly experiment with new ideas, testing the impact on the business, and quickly addressing any issues that arise.
DevOps as a software engineering practice unifies software development (Dev) and software operation (Ops). To assist with quality delivery in these practices you need to provide a “Quality Delivery Pipeline” [Yoder18] to help assure the delivery meets the requirements and proper validation and checks are done before releasing into full production. At the end of the pipeline the validated system will be deployed into production. There are various deployment techniques to help successfully and reliably deploy more quickly. The goal is to give confidence by providing "reliable, working software" to the user (making the user confident in the system). Also, the teams will have more confidence the system is working.

Monolith architectures generally use a “big bang” deployment approach that updates most of the application at one time, sometimes including database updates as well. This has been the de facto release approach for decades. Big bang deployment approaches requires development and operations teams to do extensive development and testing before release, following a ceremonial deployment process that often took several days. For example, day 1 of the deployment process could have a deadline for code commit, then code would be built and deployed on a staging environment, acceptance tests would take place until day 3, then a new build and deployment with all fixes would happen on the staging environment, followed by final tests, and finally on day 4 we would have a go/no-go decision and deployment in production. This big bang approach can be slow, error-prone because of cumbersome branching and tagging, thus being less agile.

Feature toggles have become popular with “big bang” deployment to help address some of these problems, especially with reliability. With feature toggles you can enable or disable features at runtime. This is especially useful for releases where new features might cause issues, thus you can turn off a specific feature and address the eventual issues more quickly. However, this approach is limited to features that can be disabled temporarily, and there are still maintenance issues with using feature toggles and quite often the toggles become a legacy to the system. This is often because the toggles are not prioritized to be removed from the system after they are no longer needed.

The challenges in any type of deployment is that if you break something, the deployment could negatively affect reliability or customer experience. Another scenario would be that you are testing new features with end users and unstable new features would negatively affect regular users while power users would want to have them (e.g. stable versus beta versions), so you have parallel development streams. Therefore having alternative deployment techniques for releasing can provide many benefits. Deployment techniques in modern software development that have recently become more popular are blue-green deployment and canary deployment.

-->
