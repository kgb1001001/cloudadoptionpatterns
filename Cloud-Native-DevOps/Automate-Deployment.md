[//]: # (This is Cees' "Automate" pattern, which probably needs work)

# Automate VM Deployment

You are building a cloud-native system that will be deployed across several cloud datacenters, probably across more than one cloud vendor, or across public and private clouds.

**How can you effectively manage deploying the VM's that a container or PaaS solution (such as Cloud Foundry, or Kubernetes) run on in a multi-vendor, multi-cloud environment?**

Managing base images for multiple cloud vendors by hand is error prone as the various base images can diverge. When relying on a single cloud vendor, maintaining a base image (in AWS speak, an “AMI”) is still workable; with multiple cloud vendors and the networking differences they often bring, this becomes impossible even at a small scale.

Therefore,

**Use an automation tool like Chef or Puppet to configure machines; in fact, you should prefer to use cloud vendor-independent orchestration tools such as TerraForm to help up bringing them up.**

Automation is not unique to this set of patterns, but it becomes extra important when using multiple vendors. Instead of relying on vendor-dependent tooling to manage and protect networks of machines, machines need to be interconnected with an  [Overlay Network](Overlay-Network.md), machines in different vendors’ datacenters get slightly different settings because networks and available memory/cpu sizes differ, and so on.

Even with a handful of machines, this quickly becomes very error prone when doing manually. Whereas many good DevOps practices can be postponed by teams for a while, when applying the patterns in this language, VM Automation becomes critical very quickly.
