# spark-on-k8s

## Key Requirements
* Autoscaling spark cluster for long-live jobs (dynamic resource allocation, achieved with Kubernetes Autoscaler)
* Create & Destroy spark clusters on premise for short batch jobs

## Objectives
* Scalability.
The new solution should provide the ability to scale Apache Spark cluster out and in as computing needs change.
* Reliability:
The new solution should monitor compute nodes and automatically terminate and replace instances in case of failure.
* Portability:
The new solution should eliminate the dependency on the underlying infrastructure.
* Cost-effectiveness:
The new solution should reduce the cost of managed services.

## Technology
* Kubernets (>=1.8.1)
* Spark Operator

## Observations on Industry
* Companys are using spark on k8s in production: Data Bricks, Data Mechanics 
* Hybrid cluster (spark is deployed together with other products) is a bad practice. Spark is usually deployed in a standandalone k8s cluster, serving as a resilient computational cluster
* Copmanys are moving from EMR to EKS
* Spark operator over spark submit
* Palantir's gang scheduling matters


## Design Trade-off 1: EKS vs. EMR?

### EMR downside
* Portability:After running for a while on AWS EMR, you can find yourself tightly coupled to AWS specific features. It can be something simple, like logging and monitoring and it can be more complicated like an auto-scaling mechanism, custom master/worker AMIs, AWS security features, etc
* Cost overhead: the Amazon EMR price is in addition to the Amazon EC2 price.

### EKS benefits
* Better pricing through the use of EC2 Spot Fleet when provisioning the cluster.
* Don't have to pay the per-instance EMR pricing surcharge. Just the EKS cluster flat-fee.
* Faster startup overhead, since you're deploying containers, not provisioning VMs.
* Easier and faster to pre-install needed software inside the containers, rather than bootstrap with EMR.
* More powerful autoscaling in EKS.


## Design Trade-off 2: Spark Submit vs. Spark Operator


![Spark operator]
(https://github.com/GoogleCloudPlatform/spark-on-k8s-operator/blob/master/docs/architecture-diagram.png)
