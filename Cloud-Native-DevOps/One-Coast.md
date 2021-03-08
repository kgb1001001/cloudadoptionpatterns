One Region
===

You want multiple datacenters and have settled on the number you need from [Three Datacenters](Three-Data-Centers.md). Now you need to select which locations to use. 

**What is the best selection algorithm for determining hwo to site your datacenters in a cloud environment?**

There are two clear and opposite forces influencing your decision:

-   Having your instances too close to each other does not protect against natural disasters;

-   Having your instances too far apart from each other makes round trip times too long;

Therefore,

**Make round-trip time between datacenters the primary selection tool. Stay within one region (which defaults to one coast (if in the USA)), and when using datacenters from multiple vendors, assume the worst about routing between the vendors–launch a virtual machine at each site and measure. Testing this is very cheap.**

We have noticed that datacenters of various vendors do tend to be clustered (local governments may give incentives, or local hydro-electric power generation may make it easy to obtain the coveted “green” label), but usually not so close that all but the worst natural disasters will have an impact.

Different cloud vendors tend to have very low latencies between their datacenters. With fiber optic WAN connections, packets travel at a significant fraction of the speed of light, which means that intermediate routers often introduce most of the latency. Private WAN interconnections minimize these “hops“, resulting in round-trip delays of modern WANs that come close to LAN delays ten or twenty years ago. Geographically separate datacenters of the same cloud vendor may therefore have, due to the use of private WANs, a lower latency than close datacenters of different providers which usually get routed over the public Internet. For example, we observed lower and more consitent round-trip times between AWS regions in Oregon and Southen California than between Azure and AWS regions that are both located in Fresno, CA.

Again, there’s a natural tension here: using all infrastructure from a single vendor will offer the best connectivity between datacenters. However, there may be shared components in a vendor’s infrastructure that can cause widespread outages, so adding more vendors may be an attractive option. Don’t forget though that there’s a clear financial drawback of using multiple vendors: one vendor will mean larger volume discounts, so there is an insurance premium to be paid for placing capacity among multiple providers.

