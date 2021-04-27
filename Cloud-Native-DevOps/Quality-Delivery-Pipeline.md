# Quality Delivery Pipeline

Continuous Integration has become a key factor for most software development teams as a means to safely evolve the code ensuring that we have not broken anything that we have to interact with. A step to be successful with this is to setup servers and scripts for continuous integration. Continuous Delivery [Humble] is an extension of this by taking the automatic or semi-automatic promotion of builds and process them into something that can be delivered. The goal is to take changes from version control to production by making deployment to different environments as automated and as reliably as possible.

**How can we create a process that helps us deploy while ensuring the desired qualities are met?**

Automating the testing and deployment process is challenging and requires a lot of expertise. Building and releasing into production environments can be tedious and error prone.

Businesses can get very busy trying to meet the requirements where there is barely time, resources or people to do what is needed to keep a project afloat.

Lack of quality validation or testing of your release can be dangerous and costly.

Therefore,

**Develop and automate a delivery pipeline composed of steps to get and build the current version, run various quality validations on the build, and when successfully validated, push the build into a staging or production environment.**

Figure 3 outlines the core of what a minimum pipeline should be. In a sense it is analogous to pipes and filters where each step in the pipeline is a quality filter such as code quality, technical debt, security, etc. It is important that the pipeline be small and fast, instead of long and slow. Automating As you Go [YWW16b] makes the process quicker and more reliable.

The minimum pipeline must first get the code and build it. Then there is a step for some form of minimum quality testing such as unit and/or integration testing. If the build and test steps are successful, the system can be pushed into a staging environment for QA testing. Finally, if all steps were successful, the system can then be pushed into the production environment. Although this minimum pipeline works, it may not be “ideal” for gaining confidence as there can be many other critical qualities that need to be validated before releasing into production. 

### “Ideal” Quality Pipeline 
A pipeline that offers more confidence would add more involved testing steps and also validate many other important qualities. Some of these qualities might be code quality while others might be reliability, security, performance, or other architectural qualities. The following (Figure 4) is an example of a more complete quality pipeline.

This pipeline has steps for building the system (clone/clean/build), unit and integration tests, security checks through Fortify, and other code quality checks through Sonar. Additional architectural checks can be included in Sonar such as those outlined through Continuous Inspection [Merson]. Validating the dependencies are healthy through a pre-health test before release minimized potential issues when going into a production environment. Building monitors as part of the release and include as part of the pipeline is key and can help teams “monitor” the results of the release.

<p align="center">* * *</p>

The following is a set of related practices to gain confidence and assist with a quality pipeline:
* Small Incremental Releases - keep releasing small changes into production.
* Automate as you go - automate what you can as soon as you can.
* Continuous Inspection - getting regular feedback.
* Blue-Green Deployment - separate deployment from release.
* Staged Releases - first in a safe environment and spread out.
* Canary and Rolling Deployments - gradually roll out your release..
* Health Checks - Smoke Tests to make sure things are ok, etc.

The following are some advantages of Quality Delivery Pipeline: 
* Freeing teams up from needing to think about delivering quality makes them more productive as important quality validations are built into the pipeline; 
* Some important critical tasks can be done more quickly and with confidence.
* You can ensure that what gets delivered meets a minimum quality.

There are also some potential disadvantages to Quality Delivery Pipeline:
* Automating all quality checks might be very difficult,.
* Creating a quality pipeline can require a lot of technical expertise.

Automate as you Go can helps ensure the Quality Delivery Pipeline is run frequently, and error prone steps are avoided. The Quality Delivery Pipeline becomes a form of Continuous Inspection during the release cycle. 

Note these patterns were first introduced and evolved from a SugarLoaf PLoP 2018 paper by Joseph Yoder, Ademar Aguiar, and Hironori Washizaki.
