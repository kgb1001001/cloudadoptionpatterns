# Strangler
(aka Strangle the Monolith, Evolve System with Microservices)
   
You have a monolith that has been providing value to your organization for some time. The software requirements are changing more rapidly than your organization can accommodate; adapting the software, adding features, and managing existing features in the monolith are difficult due to: (i) significant coupling between components in the monolith, or (ii) significant synchronization complexity in the deployment process among the teams working on the monolith. Sometimes the need for rapid changes to the software comes with a need for the organization to evolve and grow. The decision has been made to evolve to using the microservice architecture style.

**How can we start evolving the overall architecture to better meet the needs of the organization, specifically an evolution to microservices?**

A legacy monolith is used by several client applications; the monolith and those applications are still providing value to the organization. There is a lot of code and tight coupling within the monolith that make rewriting it expensive. Adding functionality to the monolith is becoming harder and sometimes creates bugs. 

There is a desire and sometimes potential benefit to use new protocols and technologies. However, client applications make use of the monolith by calling services that use old protocols and technologies (e.g., SOAP, EJB) or by adding module dependencies to the monolith and directly calling the logic inside it. 
New applications being developed use different technologies, programming languages, frameworks, and API design standards from those used for the monolith, thus limiting reuse of the monolith by these new applications.

Deployment becomes difficult—it requires testing the whole system because the changes might have affected other functionality. You also have to redeploy the whole system with downtime that is increasing with the size of the deployment unit.

Therefore,

**Gradually create microservices that are independent of the monolith, growing them in number over time until the monolith is replaced (strangled) by the new microservices.**

You have a useful legacy system that is a monolith. There is the need to develop new applications that use different programming languages, different frameworks, or simply newer incompatible versions of languages or frameworks. Consequently, these new applications cannot directly call components in the monolith. Perhaps the software needs to evolve or grow rapidly, but it is getting harder to evolve the current system. The following situations can complicate the process of transforming a monolith to microservices:
* A monolith uses old versions of libraries and frameworks. Developers want to upgrade to the latest versions, but the upgrades are not fully backward compatible and require updating a lot of code in the monolith. These upgrades have been postponed time and again over the years, and now the discrepancy between the old version and the latest makes the upgrades costly and risky. 
* The monolith was written in a programming language that is no longer the best choice for the current context at the organization. 

Extracting logic out of the monolith into microservices may create a situation where the same logic needs to be accessed by both old and new client components. Existing clients need to access the logic the old way, and new clients will access the logic the new way, using current protocols and API standards. A general approach is to create a proxy or façade for old external systems or client components (see Figure 3). This façade sits between the client components and the logic that exists in the monolith which is being moved to microservices. 

<p align="center"><img src="../assets/StranglerFacadeOverview.png" width="90%";/><br>
#insert FIG here...Figure 3—Strangler Evolution</p>

Initially, this façade doesn’t do anything but pass all traffic, unmodified, between old client components and the legacy application (monolith). This approach is a way to Wrap the Monolith to protect old clients from change. As microservices replace monolith components, this façade transcodes protocols from old clients into the protocols, technologies, and contracts used by the new system being created. Note this could be a two-way façade as there could be communication coming back from the monolith to the old client components.

Eventually the legacy monolith becomes strangled and can be removed. This evolution is notionally represented in Figure 3. Note that even when the strangling is complete, there could be some old client components that might not be updated thus still needing the façade.

