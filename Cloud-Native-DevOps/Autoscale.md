Autoscaling
===

You’d like your application’s capacity to adjust elastically based on load.  You are using a Stateless Runtime.

**How do you plan for handling unpredictable load while at the same time minimizing the per-unit cost of application hosting?**

Development teams are notoriously bad at predicting demand on their applications.  

What's more it takes time to gather real customer usage data to develop a capaciity model that is based on actual usage.  By the time you realize when your peaks are, it may be too late for the application because it may have crashed from overuse.

Therefore,

**Use Autoscaling to dynamically adjust the number of identical runtime instances to only the number required by current traffic loads.**

For example, Kubernetes supports the [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) that will automatically adjust the number of replicas running in your cluster, likewise [Amazon Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/) scales web applications written in a variety of languages to deal with shifting load conditions.

One issue that all autoscaling frameworks have is that they depend on good baselines for application performance in order for the scaling policies to be set correctly.  Performance Testing early is critical to be able to set that baseline and to understand when changes to the application affect the baseline.
