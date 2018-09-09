# Container implementation

This project uses Docker and Kubernetes to run and manage the application. The traditional way of implementing kubernetes ends in managing configuration and infrastructure with less emphasis on application and networking. It used to be time-consuming and ends up in troubleshooting many networking and implementation issues. 

### Installation:

The installation of EKS has been done following AWS blogs and best practices. Refer below for detailed steps.
[EKS installation](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html)

## Why Amazon EKS?

Amazon EKS makes it easy to deploy, manage and scale containerized applications using Kubernetes in AWS. There are many benefits of using EKS-

* EKS runs across multiple availability zones and automatically detect and replaces the unhealthy      nodes. Provides patching and upgrades on demand. You create worker node and connect to the cluster.

* Applications managed by EKS are compatible with applications managed by standard Kubernetes.

* The channel between worker nodes and managed control plane are secured by default.

* The worker nodes are under autoscaling group which ensure minimum nodes are there at any given       time.

* There are many companies who have adopted this and are scaling and saving cost on their      infrastructure.

* EKS run in the VPC using your own security groups and NACL which provides high level of isolation.


 Kubernetes for this project is implemented in us-east region as EKS is not available for Australia.

 ![kubernetes](https://user-images.githubusercontent.com/42830023/45264776-29383680-b485-11e8-9cbb-5deaa66a5a66.JPG)


 # References:

 * [AWS best practices.](https://aws.amazon.com/whitepapers/architecting-for-the-aws-cloud-best-practices/)
 * [ AWS EKS](https://aws.amazon.com/eks/)
