Overlay network
===

You are building an application and the associated infrastructure for deployment into either a public cloud, or a hybrid cloud crossing multiple public and private clouds.

**How do you manage the network connectivity between all of the different nodes running in these disparate cloud environments?**

Multiple cloud vendors have their own flavors of what is called “virtual private clouds” (VPCs), which basically lets customers group clusters of virtual machines onto protected private networks. These tools are often very vendor-specific (so if you end up with multiple vendors, you need to learn multiple tools), and also require you to trust vendors to “do the right thing” on the network configuration. Furthermore, these tools only work within a single datacenter, which means that you still need firewalls and VPN connections between your VPCs. Systems running such “gateway to other datacenter” services will quickly become bottlenecks as more and more services need to go through them, loading the VPN nodes and making the central firewalls very complex.

Therefore,

**Don’t rely on VPCs, firewalls and VPNs to connect systems between multiple datacenters. IPsec can make a mesh encrypted network that connect each node to each other node it needs to talk to, securing communication between each and every node whether local or remote; OS-level packet filters can then allow only inbound traffic from other nodes known to require communication, essentially acting as one firewall per node.**

There is a reason that firewalls are often implemented in hardware, or at least as optimized appliances - all of the traffic between “inside” and “outside” flows through them, so they need to be very fast. As a system grows larger, both the traffic through the firewall increases and the complexity of the firewall’s rule base grows, making it very hard to keep up. Traffic between datacenters often is routed through VPN connections that add encryption, which is computationally expensive. Spreading work over multiple VPN endpoints is possible, but further complicates configuration.

With good DevOps practices, it becomes feasible to automate nodes to the extent that each and every node keeps an encrypted connection to every other node it needs to talk to. An IPsec Key Exchange daemon like Racoon[@racoon:online] can be instructed by DevOps automation tools to provide the IPsec kernel with keys for the right set of nodes. In this way, each system in the cluster participates in its own protection against the outside world (usually supported by kernel firewall rules on the node that prevent communication outside of the IPsec network), and each system contributes a bit of CPU power to do the necessary encryption and decryption of packets, eliminating central firewall/VPN machines as bottlenecks.

Furthermore, the resulting overlay network becomes transparent between datacenters; there is no difference, in terms of addressing and routing, between accessing local nodes or remote nodes. This makes it very easy to bind systems in different datacenters into WAN-spanning clusters.

The most important caveat of this solution is that it will only work when there is a tool to [Automate VM Deployment](Automate-Deployment.md) and make this kind of infrastructure setup available. Without it, maintaining the complex configuration required for such a setup becomes infeasible.

