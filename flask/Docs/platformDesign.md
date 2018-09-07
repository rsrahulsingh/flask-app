# Network design


This document contains the information about network and it's various component. The network is designed for test purposes only and should not be used for production.

Assumptions:


* The network is designed in single region- AWS Sydney and uses most resources from AWS Sydney DC.
* The load balancer serves HTTP traffic as of writing this.
* Application is standalone with inbuilt webserver and no databases.



# VPC


VPC is most important component of cloud based infrastructure and it is important to get it right from the first. VPC design has far-reaching implications for scaling, fault-tolerance and security. It is responsible for infrastructure flexibility and will save your important time to free up address space. It is important to lay out VPC in correct way then the careless way. VPC for this project is set up in AWS Sydney region.

## Subnet


 Subnet layout is the key to a well-functioning VPC. Subnets determine routing, Availability Zone distribution and Network Access Control Lists. VPC is not a data center, data center network or switches. A VPC is a software defined network optimized for moving massive amount of packets into, out of and across AWS region.

 Below are few reason of creating different subnets:
* You need different hosts to route in different ways- Internal only, pulbic-facing.
* You need to distribute workloads across different multiple AZ to achieve fault-tolerance.
* Security requirements for NACL and route table to serve specific ports and subnets.

In this project 4 subnets are created to server traffic and with one being spare for future use.


## Routing


It is important to apply the principle of proper and secure routing when you are exposing your servers to internet. Route tables helps to route traffic from Internet to the VPC.
The project uses 2 route tables - Public and Private. Public route table is associated with Public subnet and private route table is associated with Private subnet. 

## Fault-Tolerance


AWS provides geographic distribution out of the box in the form of Availability Zones (AZs). Every region has at least two.

Subnets cannot span multiple AZs. So to achieve fault tolerance, you need to divide your address space among the AZs evenly and create subnets in each. The more AZs, the better. if you have three AZs available, split your address space into four parts and keep the fourth segment as spare capacity.
The reason you need to divide your address space evenly is so the layout of each AZ is the same as others. This will help resources like autoscaling groups to be evenly distributed. If you create disjointed address blocks, it will require lot of maintenance.

In this project we have divided our subnet into similar block . The division is based on block not on number of IPs.


## Security


The first layer of defense in a VPC is the routing layer.

Above the routing layer are two levels of complementary controls: Security Groups and NACLs. Security Groups are dynamic, stateful and capable of spanning the entire VPC. NACLs are stateless (meaning you need to define inbound and outbound ports), static and subnet-specific.

Generally, you only need both if you want to distribute change control authority over multiple groups of admins. For instance, you might want your sys admin team to control the security groups and your networking team to control the NACL’s. That way, no one party can single-handedly defeat your network restrictions.

In practice, NACLs should be used sparingly and, once created, left alone. Given that they’re subnet-specific and punched down by IP addresses, the complexity of trying to manage traffic at this layer increases geometrically with each additional rule.

Security Groups are where the majority of work gets done. Unless you have a specific use-case like the ones described earlier, you’ll be better served by keeping your security as simple and straightforward as possible. That’s what Security Groups do best.

The VPC for this project is  subdivided into different blocks as below -

```
10.0.0.0/16:
    10.0.0.0/18 — AZ A
        10.0.0.0/19 — Private
        10.0.32.0/19
               10.0.32.0/20 — Public
               10.0.48.0/20
                   10.0.48.0/21 — Protected
                   10.0.56.0/21 — Spare
    10.0.64.0/18 — AZ B
        10.0.64.0/19 — Private
        10.0.96.0/19
                10.0.96.0/20 — Public
                10.0.112.0/20
                    10.0.112.0/21 — Protected
                    10.0.120.0/21 — Spare
    10.0.128.0/18 — AZ C
        10.0.128.0/19 — Private
        10.0.160.0/19
                10.0.160.0/20 — Public
                10.0.176.0/20
                    10.0.176.0/21 — Protected
                    10.0.184.0/21 — Spare
    10.0.192.0/18 — Spare

```


The platform is setup as per below architecture.

![network diagram](https://user-images.githubusercontent.com/42830023/45151239-1ae1e480-b211-11e8-82f7-2b3ef6b15a9f.PNG)


# References

* [AWS whitepapers.](https://aws.amazon.com/whitepapers/)
* [AWS best practices.](https://aws.amazon.com/whitepapers/architecting-for-the-aws-cloud-best-practices/)
* AWS and git blogs.