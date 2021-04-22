# Pave the Road
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(aka Make Microservices Development Easier)

The decision has been made to evolve an existing monolith to use the microservices architecture style. This has organizational consequences.

**How can we encourage teams and make it easier to write microservices?**

Some developers are excited about creating microservices and hence experimenting with microservice-related frameworks and technologies that are new to them. However, the organization has little or no experience building cloud-native or microservice-based applications.

The monolith is deployed through a ceremonial process that requires the coordination of different development teams and operators. This process hinders organizational agility.

The practices, policies and technologies for establishing a DevOps environment are not in place. Developers are not familiar with containerization, continuous delivery, log consolidation, and other recommended practices for microservice solutions.

Therefore, 

**Make it easier to develop microservices by providing templates, training, policies, and infrastructure elements that set the fundamental environment for creating microservices.**

There are many ways to Pave the Road. The first thing is to get the infrastructure up and running. To be successful with microservices it is important to have a good DevOps environment. This includes an automated pipeline of building, good tests, deployment, and monitoring as part of the process. Documenting this process and sharing the best practices with examples is another good early practice to help Pave the Road.

Another thing beneficial for teams is to provide a way to generate or build the core of a new microservice. Sometimes this is through code generation or using some descriptive data that can be interpreted. Other times it is useful to have templates or examples. A combination of these techniques can be used. Following are a list of several potential solutions that can be applied to ease the tedious programming tasks for creating new microservices: 
* Define processes and set up tools that provide the infrastructure for automating the pipeline for building, testing, and deploying the microservices.
* Create simple examples, templates, and/or scripts to show developers how to write the microservice.
* Develop a tool that generates the core microservice from a higher-level specification or a wizard tool such as a DSL for microservices. This requires a lot of effort and is done only when an organization is growing a lot and is mature in microservices development.
* Design and document a reference architecture for microservices. This should include a description of the various components and connectors, and any implementation details. 
Hire experienced people and provide training and/or mentoring.

There are many things to consider when deciding on an appropriate solution. Our advice is to do the simplest thing possible that minimizes your maintenance effort and evolve as you learn. This includes both the effort required to develop your microservice including building the pipeline and deploying (DevOps). 

Paving the road for microservice projects includes several technology elements related to the microservice runtime environment, such as containerization, container orchestration, log consolidation, monitoring, and distributed tracing. It also includes DevOps practices, some of which require infrastructure and tool automation; for example: continuous delivery [7], Externalized configuration [2], and infrastructure as code [8]. Many organizations hire microservice experts to avoid risks and expedite the learning of the new environment. With or without an expert in the ranks, the organization will typically launch a pilot microservice project. The team for this project should have ace developers that are also good at transferring knowledge. They shall pave the road while building the pilot project and documenting what is needed for other teams to follow their steps. The documentation can take the form of README files, instructions on a wiki, architecture decision records [9], a template for microservice projects, a reference architecture, and more.

Another important consideration is to rethink the way applications deal with persisted data, as they move from a more centralized database approach to the typical data decentralization used in microservice architectures. For example, there might be the need to use the Saga pattern [2] in place of the original single-connection transaction in the monolith.

<p align="center">* * *</p>

This pattern goes hand in hand with [Start Small](Start-Small.md). An initial small microservice project might be the pilot project that will shed light on the various new technologies and tools that get to be adopted for microservice development. This pattern is similar to Paving the Wagon Trail [10] from the perspective of creating templates, scripts, or DSLs. However this pattern also talks about other things that help, such as building the infrastructure, documentation, training, and hiring good people.

One of the main benefits of Paving the Road is that it creates an Easier Path [6] for developing microservices. New teams or people can roll out their first microservices quicker, by learning from the examples, documents, and templates created by the pioneer teams that Paved the Road. On the other hand it requires a lot of time and effort for building the software, process, template, docs, etc. Some of these can be difficult such as DSLs. Also there are maintenance issues associated with these items. The initial microservice projects that will Pave the Road will take longer and require a high upfront investment that will only pay off later.
