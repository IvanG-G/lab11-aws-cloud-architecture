# lab11-aws-cloud-architecture


## **Part 1: Designing Cloud Infrastructure**
  * Task:
    * Design a cloud infrastructure for a scalable web application.
    * Include components like compute instances, storage, and network configurations.
    * Use AWS EC2, S3, and VPC to build the basic architecture.

<img width="600" alt="image" src="https://github.com/IvanG-G/lab11-aws-cloud-architecture/assets/138608967/c731c339-814f-4875-b477-daa67a5af8b1">


## **Part 2: IAM Configuration**
 * Task:
   * Define IAM roles and policies for different components of the architecture, such as developers, admins, and application servers.
   * Ensure that each role adheres to the principle of least privilege.


**Roles:**
 * **Role** DevOps Admin: Permissions to administrate, create and assign IAM roles, Manage completely any AWS resource, access to costs, metrics, full access to the entire infrastructure.
 * **Role** Devops: Manage completely any AWS resource.
 * **Role** Developer: Access to applications on EC2, logs and information related to.
 * **Role** DB admin: Access to databases in AWS, editing in low environments but only for query in high environments


## **Part 3: Resource Management Strategy**
 * Task:
   * Develop a strategy for managing resources that includes auto-scaling, load balancing, and cost optimization using AWS Auto Scaling, ELB, and AWS Budgets.

For the strategy we can use the next components:
 * Auto-Scaling: Creates several copies of one EC2 this scaling can be vertical, or horizontal.
 * Load Balancing: Use the pods that were created by Auto Scaling and get to work depending on their workload
 * Cost optimization: Implement Cloud Financial Managment, and constanly study the costs, depending on that, we could use different type of tiering of every service on AWS, this is achieving measuring costs, usage, traffic and DB/Storage usage.


## **Part 4 & 5: Theoretical Implementation**
Using the AWS services identified, outline the architecture for the web application. Describe how each component interacts with others, focusing on the flow of data and control between services. This description should detail the role of each service in the architecture, ensuring a clear understanding of their interactions and dependencies.

This is the description of every component and their interactions:
 * DNS: transforms the domain name service to an IP address.
 * Cloud Front: Stores all the front application this connects to a firewall and at the same time we will connect to the first load balancer.
 * Firewall: between CloudFront and DNS, to prevent unnecesary network traffic.
 * AWS cloud, is by itself defending against ddos attack
 * AWS VPC: this ensures security and isoletion on every deep layer on our application.
 * ECS Web servers: This are the services that will process all the http request gathered from the front. This two (Or more) will be connected to the next layer of ECS
 * ECS App servers: In charge of processing the bussiness rules, querying to database, process information and return them to Web servers.
 * DynamoDB: works as a fast querying database, this data will be in dynamo only for 6 months, after that, lambda will migrate old information to an instance of S3. In case that the data is not in our DynamoDB, we will ask to lambda to look after the information on S3.
 * S3: Gathers all the informations that is not used in at least, 6 months, it will keep the security and we will havve the information, but not in our principal database.


* **Discuss how the designed IAM policies contribute to overall security.**
  The roles that I design ensures the security because only the personal of DevOps can create delete or administrate the infraestructure of the system. And only one person, that is the admin, can give and retrieve this roles.
  The developers can only see the ec2 instances, to see their application, logs, information about executions, and just that, and db admins can modify the databases but only in lower environments, the higher environments are only for querying.
  

