---
parent: Basic DevOps
title: Automate As You Go
---
# Automate As You Go 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(aka Red-Black or A/B Deployment)

“The first rule of any technology used in a business is that automation applied to an efficient operation will magnify the efficiency. The second is that automation applied to an inefficient operation will magnify the inefficiency.”— Bill Gates

At the start of agile projects there are many pressures to get something out to the end-user and to get initial reactions and feedback. It is important to establish a frequent delivery cadence and tools to make that possible. In creating this environment, quality-related items need to be considered as well. As a system evolves, it is essential to regularly evaluate the system to make sure that key qualities are being met.

**How can agile teams create tooling and an environment to assist with quick feedback about important qualities of the system and make their current status accessible and visible to the team?**

❖ ❖ ❖
Not focusing on important qualities early enough can cause significant problems, delays and rework. Remedying performance or scalability deficiencies can require significant changes and modifications to the system’s architecture. However, focusing too early on system qualities in the development cycle can lead to overdesign and premature optimization [Knuth]. 

Agile teams primarily focus early in a project implementing functional requirements. There is often a priority to doing the minimal necessary to getting something working so as to get customer’s reaction to the system’s functionality as soon as possible. This can lead to taking shortcuts or a lot of quick and dirty manual tasks such as testing to quickly get the product out. Although there are benefits to getting fast feedback, as the project grows, a growing number of manual tasks slows the team down, making it harder to safely validate and evolve the system.

There is often a temptation to use the latest and greatest tool that has been recently hyped. However, you have limited time and resources and there is a lot of pressure to get something out as soon as possible. Automation takes time and energy to set up and sometimes the payoff is not immediately apparent. Some tasks, specifically quality testing and validation, can be hard to automate if the architecture was never designed to be testable.

There is a risk that focusing too much on automation could cause the team to get caught up in tooling and spend too much effort and time on automation. Another risk is that by automating too many tasks you consequently slow down your build and deploy pipeline by testing too frequently or at the wrong time in the pipeline. 

Setting up environments and automating the testing of system qualities can require specialized skills and expertise. Also, you may not know what to measure about qualities until you have sufficiently defined the functionality. You want to avoid automating or putting effort into tasks that may not add value later. Being agile, you want to do things just in time.

❖ ❖ ❖
Therefore, 

**Create an environment and use tools to automate fundamental things that add value as soon as you can. Do not put off automation tasks until late in development.**

Some automations are important to do from the start. Early on the most essential things to automate are the build, integration and test environment configuration. Then automate functional tests and system quality tests. But that’s only the start. There are other things you can automate such as acceptance tests, performance metrics, code smell detection, application security checks, and architectural conformance. Also if you have repetitive, tedious or error prone tasks, and if you can automate those as well. As you automate tasks, they become part of the cadence of your project.

The more you automate repetitive manual tasks, the more time it frees you up to do more. It also allows time to spend on exploratory testing. Automation also allow you to more safely evolve the system. Automation lets you do work in smaller batches, making fewer mistakes and getting quicker feedback. With automated tests, you will know when something goes wrong with those items you are testing. You can run automated tasks more often making sure that important qualities are still being satisfied.

If you need to validate performance under load before you release, you might need to spin up and create a specific environment to test the system performance. This could require setup of databases and networks, etc. Doing this by hand every time can be error prone and take time. By creating a virtual environment with scripts that automate this setup, you can make performing this task much easier. As you see you are having to repeat manual tasks and that automation can help, it is time to add an automation task to your backlog.

When making a decision to automate, it is helpful to think about how long a particular automated task takes to execute and how frequently it is performed. You should consider automating infrequently performed tasks as well, especially if they are error prone or involve a lot of steps. If a task is expensive to automate and you do it infrequently, a manual checklist script might be the better alternative. For example, if you have a manual task that you perform once a year that takes one day but can be automated in five days, your return on time spent to automate will come only after five years.

The time it takes to perform any automated task figures into your consideration of whether to install it into your normal build and deploy process or to take it off of that workflow. If you can get early, quick feedback using less time-consuming automated tasks, those automations may prove as valuable as more thorough, longer running tests or automations. For example, a security scan that runs penetration testing against a deployed app can be automated, but might be too slow to be part of your automated build process. A static code analysis that includes looking for some security defects might not be as comprehensive as the penetration scan but can still provide useful feedback.

There are different testing cycles, especially for system qualities. Some tests, such as unit tests, will be run frequently, maybe hourly. When you check-in code, there will be some simple integration tests that will run. But other tests, if run at that time, might slow down the check-in process too much. So these quality or regression tests might be run nightly or even less frequently.

Automation considerations will influence your architecture style, your choice of frameworks, interface design, and many design details. For example if you decide that you will have many automated tests, you will want to design your system so these can be easily added. And while you will want to make parts of you system testable in isolation, you also need to consider how to perform meaningful integration tests.

Knowing what automation is necessary, and when automated tests and tasks should be run, is important. System Quality Specialists can provide expertise to assist with automation. Some quality tests are hard to set up and take a lot of time to run. Sometimes you have to be clever to set these up correctly and decide when good times are to run them. It is important that the results of the automation is visible to the team. This can be done via System Quality Dashboards and System Quality Radiators. However, you do not want to be overwhelmed with too much information that can be overlooked and ignored. The teams needs to decide what feedback is useful and the frequency that it gets updated.

There are a broader set of activities, beyond simply building and running tests continuously that need to be part of a continuous integration pipeline, such as deployment and IDE integration [Duv]. One of these activities that is valuable during continuous integration is Continuous Inspection. Continuous Inspection includes ways of running automated code analysis to find common problems before integration. Continuous Inspection also describes many additional automated tasks that can help insure that certain qualities and architecture constraints are being met [MYGA]. 

Automation tools are highly dependent upon the architecture and platform that is being used. For example if you are developing with Java, you might consider SonarQube, PMD, Checkstyle, FindBugs, JaCoCo, Jenkins, Maven and Eclipse with various plugins such as JUnit and code analysis tools.

When selecting tools, it is also useful to evaluate and select one or more tools that can perform static analysis on your code base. Tool evaluation criteria should include the programming and scripting languages used in your software projects versus the ones supported by the tool; whether the tool provides an API for developing customized verifications; integration with your IDE; integration with your continuous integration server; and the appropriateness to your project of the built-in verifications provided by the tool. Specialists can assist with tool selection.
