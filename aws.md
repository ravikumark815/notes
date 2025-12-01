Preset:
- Cloud Computing: On-demand delivery of IT resources over the internet with pay-as-you-go pricing.
- AWS is a cloud computing platform that offers on-demand access to a wide range of IT services over the internet, including computing power, storage, databases, networking, machine learning etc. 
- Developed by Amazon IT team in 2003 and officially launched its first service in Nov 2004.
- Has more than 200 services.
- NO pre-pay for anything

Client-Server model: A distributed structure that partitions tasks between service requestors, known as clients, and service providers, known as servers. 

Types of Cloud deployment:
- Cloud: In a cloud-based deployment model, you have the flexibility to migrate your existing resources to the cloud, design and build new applications within the cloud environment, or use a combination of both.
- On-premises: Deploying resources on premises using virtualization and resource management tools does not provide many of the benefits of cloud computing. However, it is sometimes sought for its ability to provide dedicated resources and low latency.
- Hybrid: In a hybrid deployment, cloud-based resources and on-premises infrastructure work together. This approach is ideal for situations where legacy applications must remain on premises due to maintenance preferences or regulatory requirements. Multi-cloud deployments can also be considered hybrid deployments.

6 key benefits of AWS Cloud:
- Trade fixed expense for variable expense: Businesses can transition from fixed investments to variable costs.
- Benefit from massive economies of scale: Business big or small can access advanced technologies that were previous only accessible to large enterprises.
- Stop guessing capacity: Customers can dynamically scale AWS Cloud resources up or down based on real-time demand. 
- Increase speed or agility: Businesses can rapidly deploy apps and services, accelerating time to market and facilitating quicker responses to changing needs.
- Stop spending money to run and maintain data centers: No need to invest in physical data centers. 
- Go global in minutes: Use AWS's global infrastructure to deploy apps and services across multiple areas in minutes.

High Availability: Ensuring apps and services are accessible all the time with minimal down time.
Fault tolerance: Designing a system to ensure high availability even if multiple components fail by building resilience into every layer.  

Availability Zones: Consists of one or more data centers with redundant power, networking and connectivity.
AWS Regions: Physical locations aroung the world that contain groups of data centers (AZs). Each region consists of a minimum of 3 physically separate AZs within a geographic area. 

Shared Responsibility Model:
- AWS is responsible for security of the cloud
- Customer is responsible for security in the cloud 

--- 

# Compute
- Elastice Compute Cloud (EC2): On-demand compute capacity the can be quickly launched, scaled and terminated with costs based onlu on active usage. 
    - Compute as a service (CaaS)
    - Highly Flexible
    - Cost-effective
    - Quick
    - You only pay for what you use - not stopped or terminated
- Multitenancy: Sharing underlying hardware between virtual machines. 
- Hypervisor: AWS manages the underlying host hypervisor
- EC2 configurations:
    - Windows
    - Linux
    - Internal Business apps
    - Web apps
    - Databases
    - Third-party software
- Vertical scaling: Making instances smaller or bigger, in terms of cpus, ram, storage etc as needed. 
- Networking: Customer controls the networking - what type of requests make it to the servers, publicly/privately accessible. 

How Amazon EC2 works:
- Launch an EC2 instance using by selecting an AMI that defines the OS and might include additional software. 
- Choose instance type: CPU, Memory, Network Performance
- Connect to EC2 instance using SSH or RDP or AWS Systems Manager
- Use the instance: You can begin using it to run commands, install software and perform other tasks. 

Types of Instances:
- Each EC2 instance type is grouped under an instance family which offer varying combinations of CPU, memory, storage and networking capacity
- Instace families:
    - General purpose
        - Balanced resources
        - Diverse workloads
        - Web servers
        - Code repositories
    - Compute optimized
        - Compute-intensive tasks
        - Gaming servers
        - High performance computing (HPC)
        - Scientific modeling
    - Memory optimized
        - Memory-intensive tasks
    - Accelerated computing 
        - Floating point number calculations
        - Graphics processing
        - Data pattern matching
        - Hardware accelerators
    - Storage Optimized
        - High performance for locally stored data
- Choose right Instance Size.

- How to provision AWS resources:: APIs(Application programming interfaces) behind the scenes
    - AWS Management Console :: Setup test environments, testing, monitor billing etc.
    - AWS CLI :: Make API calls using the terminal on your machine
    - AWS SDK :: Interact with AWS resources through various programming examples.

- When you deploy an EC2 instance, you are responsible for configuring security, managing the guest operating system (OS), applying updates, and setting up firewalls (security groups).

EC2 billing options:
- On-Demand: Pay only for the compute capacity you consume with no upfront payments or long-term commitments required.
- Savings Plans: Save up to 72 percent across a variety of instance types and services by committing to a consistent usage level for 1 or 3 years.
- Reserved instances: Get a savings of up to 75 percent by committing to a 1-year or 3-year term for predictable workloads using specific instance families and AWS Regions.
- Spot instances: Bid on spare compute capacity at up to 90 percent off the On-Demand price, with the flexibility to be interrupted when AWS reclaims the instance.
- Dedicated hosts: Reserve an entire physical server for your exclusive use. This option offers full control and is ideal for workloads with strict security or licensing needs.
- Deedicated instances: Pay for instances running on hardware dedicated solely to your account. This option provides isolation from other AWS customers.

## Scalability and Elasticity:
- Scalability is about a system’s potential to grow over time, whereas elasticity is about the dynamic, on-demand adjustment of resources.
- Scalability refers to the ability of a system to handle an increased load by adding resources. You can scale up by adding more power to existing machines, or you can scale out by adding more machines. Scalability focuses on long-term capacity planning to make sure that the system can grow and accommodate more users or workloads as needed.
    - Vertical Scaling | Scaling up: Increase machine size
    - Horizontal Scaling | Scaling out: More machines
- Elasticity: Elasticity is the ability to automatically scale resources up or down in response to real-time demand. A system can then rapidly adjust its resources, scaling out during periods of high demand and scaling in when the demand decreases. Elasticity provides cost efficiency and optimal resource usage at any given moment.

- Amazon EC2 Auto Scaling: automatically adjusts the number of EC2 instances based on changes in application demand, providing better availability. It offers two approaches: 
    - Dynamic scaling adjusts in real time to fluctuations in demand. 
    - Predictive scaling preemptively schedules the right number of instances based on anticipated demand.

An Auto Scaling group is configured with the following three key settings.
- Minimum capacity: The minimum capacity defines the least number of EC2 instances required to keep the application running. This makes sure that the system never scales below this threshold. It's the number of EC2 instances that launch immediately after you have created the Auto Scaling group. 
- Desired Capacity: The desired capacity is the ideal number of instances needed to handle the current workload, which Auto Scaling aims to maintain. If you do not specify the desired number of EC2 instances in an Auto Scaling group, the desired capacity defaults to your minimum capacity.
- Maximum Capacity: The maximum capacity sets an upper limit on the number of instances that can be launched, preventing over-scaling and controlling costs.


Amazon cloudwatch service: Used to monitor metrics such as CPU, latency etc. to decide the scaling decision for Amazon EC2 scaling

Directing Traffic with Elastic Load Balancing:
- Elastic Load Balancing: Elastic Load Balancing (ELB) automatically distributes incoming application traffic across multiple resources, such as EC2 instances, to optimize performance and reliability. A load balancer serves as the single point of contact for all incoming web traffic to an Auto Scaling group. As the number of EC2 instances fluctuates in response to traffic demands, incoming requests are first directed to the load balancer. From there, the traffic is distributed evenly across the available instances.
- ELB distribute internal or external traffic to instances based on different routing strategies. 
- Benefits:
    - Efficient Traffic Distribution: ELB evenly distributes traffic across EC2 instances, preventing overload on any single instance and optimizing resource utilization.
    - Automatic scaling: ELB scales with traffic and automatically adjusts to changes in demand for a seamless operation as backend instances are added or removed.
    - Simplified Management: ELB decouples front-end and backend tiers and reduces manual synchronization. It also handles maintenance, updates, and failover to ease operational overhead.

- Routing methods: 
    - Round Robin: Distributes traffic evenly across all available servers in a cyclic manner.
    - Least Connections: Routes traffic to the server with the fewest active connections, maintaining a balanced load.
    - IP Hash: Uses the client’s IP address to consistently route traffic to the same server.
    - Least Response Time: Directs traffic to the server with the fastest response time, minimizing latency.

## Messaging and Queuing:
- Tightly Coupled Architecture: If a single component fails or changes, it causes issues for other componenets or even the whole system
- Monolithic Applications: Applications consist of multiple components that work together to transmit data, fulfill requests, and keep the application running smoothly. In a traditional approach to application architecture, the components—such as database logic, web application servers, user interfaces, and business logic—are tightly coupled.
- Microservices architecture: To improve application availability and resilience, you can adopt a microservices architecture. In this approach, application components are loosely coupled, meaning that if one component fails, the others continue to function normally. The communication between components remains intact, and the failure of a single component does not impact the entire system. This design promotes greater flexibility and reliability in the application.

- Amazon Event Bridge: EventBridge is a serverless service that helps connect different parts of an application using events, helping to build scalable, event-driven systems. With EventBridge, you route events from sources like custom apps, AWS services, and third-party software to other applications. EventBridge simplifies the process of receiving, filtering, transforming, and delivering events, so you can quickly build reliable applications.
- Amazon Simple Queue Service (SQS): Amazon SQS is a message queuing service that facilitates reliable communication between software components. It can send, store, and receive messages at any scale, making sure messages are not lost and that other services don't need to be available for processing. In Amazon SQS, an application places messages into a queue, and a user or service retrieves the message, processes it, and then removes it from the queue.
    - Send messages
    - Store messages
    - Receive messages
- Payload: Data within a message
- Amazon Simple Notification Service (SNS): A channel for messages to be delivered. They need a immediate response. Can also be used to send out notifications to user via push, sms, email and so on. Amazon SNS is a publish-subscribe service that publishers use to send messages to subscribers through SNS topics. In Amazon SNS, subscribers can include web servers, email addresses, Lambda functions, and various other endpoints.

# Compute Services
- Unmanaged Services: AWS takes care of the underlying physical infrastructure, but you're responsible for setting up, securing, and maintaining the operating system, network configurations, and applications on your instances. Ex. EC2
- Managed Services: While AWS handles much of the operational overhead, you might still need to perform some provisioning or configuration depending on the service. Ex: ELB, SNS, SQS
- Serverless: Eliminating the need to provision or manage any servers at all. The underlying infrastructure is fully managed by AWS, so you can focus entirely on writing and deploying code. Ex. Lambda

## AWS Lambda
- Lambda is a serverless compute service that runs code in response to events without the need to provision or manage servers. It automatically manages the underlying infrastructure, scaling resources based on the volume of requests. 
- You are charged only for the compute time consumed, down to the millisecond. 
- Lambda handles execution, scaling, and resource allocation. You can optimize performance by configuring the appropriate memory size for your function.
- Function as a Service
Important topics:
    - Triggers
    - Runtimes
- Max limit of 15 mins
- Supports most languages
- `

## Containers and Orchestration:
- Containers: 
    - Solve the portability by providing a consistent environment that can be replicated anywhere
    - They package everything: code, runtime, dependencies and configuration into a single portable unit
    - Faster start time and improved efficiency
- Orchestration:
    - Monitoring the health of the containers
    - Manage the lifecycle: Starting and stopping them when needed
    - Updating them
    - Managing the networking for them
    - Scaling
    - Recovery from failure
    - Two orchestration services in AWS: 
        - Elastic Container Service (ECS):
            - Streamlined and integrated
            - Define some parameters such as container images, EC2 instance type and load balancers
            - Fully managed services
        - Elastic Kubernetes Service (EKS):
            - Kubernetes is an open source platform that automates containerized application deployment, scaling and management
            - More complex, control and flexibility
    - Elastic Container Registry (ECR):
        - Full managed docker registry
        - Stores container images
    - Two services on where to run the containers:
        - Elastic Cloud Compute (EC2):
            - You manage the VM instances 
            - You have full control
        - Amazon Fargate:
            - Serverless, efficient and convenience. 
- Putting it together:
    - Start with uploading a container image to ECR
    - Choose an orchestration service based on your needs: ECS or EKS
    - Select which compute platform to run the container: EC2 or Fargate

## Elastic Beanstalk
    - Elastic Beanstalk is a fully managed service that streamlines the deployment, management, and scaling of web applications. Developers can upload their code, and Elastic Beanstalk automatically handles the provisioning of infrastructure, scaling, load balancing, and application health monitoring.

## AWS Batch
    - AWS Batch is a fully managed service that you can use to run batch computing workloads on AWS. It automatically schedules, manages, and scales compute resources for batch jobs, optimizing resource allocation based on job requirements.
## AWS Lightsail
    - Amazon Lightsail is a cloud service offering virtual private servers (VPSs), storage, databases, and networking at a predictable monthly price. It’s ideal for small businesses, basic workloads, and developers seeking a straightforward AWS experience without the complexity of the full AWS Management Console. 
## AWS Outposts: 
    - AWS Outposts is a fully managed hybrid cloud solution that extends AWS infrastructure and services to on-premises data centers. It provides a consistent experience between on premises and the AWS Cloud, offering compute, storage, and networking components.
---
# Going Global
- Regions: Geographical areas around the world that are made up of multiple data centers.
- Availability Zones: Distinct locations within a Region, each designed as an independent zone with its own power, networking, and connectivity.
- Edge locations: They offer localized delivery of the most frequently accessed content by caching data like images, videos and other resources allowing users to get content with lower latency. 
- AWS Cloud Formation: 
    - A content delivery network (CDN) and caching system designed to serve content as close as possible to the end-users.
    - To automate the deployment of cloud resources for consistency across different regions
    - Infrastructure as Code (IaC)
- Factors when selecting Regions
    - Each region is isolated
    - Compliance: Some governments don't allow you to transfer data out of the region. 
    - Proximity: Closer to customers, lower the latency
    - Feature availability: Some AWS services may not be able to other regions. 
    - Pricing: Some locations are more cost effective to operate.
- Advantages of deploying multi-region and multi-AZ resources:
    - High Availability: Capability of a system to operate continuously without failing.
    - Agility: Refers to the ability to quickly adapt to changing requirements or market conditions.
    - Elasticity: Refers to the ability of a system to scale resources up or down automatically in response to changes in demand.
- AWS Accelarator
- Route 53: It is a DNS that routes end users to internet applications. Essentially converts human-readable URLs to machine readable IPs.
- AWS Outposts: Essentially to run AWS services on premise

---
# Networking
- Virtual Private Cloud (VPC): Lets you provision a logically isolated section of the AWS Clous where you can launch AWS resources in a virtual network that you define
- Subnet: A subnet is a section of a VPC in which you can group resources based on security or operational needs.
    - Public subnets contain resources that need to be accessible by the public, such as an online store’s website.
    - Private subnets contain resources that should be accessible only through your private network. 
- Internet Gateway: To allow public traffic from the internet to access your VPC, you attach an internet gateway to the VPC. An internet gateway is a connection between a VPC and the internet. 
- Route table: Consists of rules that are used to determine where network traffic is directed. Each subnet must be associated to a route table
- Virtual Private Network: VPN creates a connection that is more like a secure tunnel through the internet. Using encryption, it hides and protects everything you send and receive from outside eyes. 
- Virtual Private Gateways: With a virtual private gateway, you can establish a VPN connection between your VPC and a private network, such as an on-premises data center or internal corporate network. A virtual private gateway allows traffic into the VPC only if it is coming from an approved network.
- AWS Client VPN
    - Used to connect your remote workers and on-premises networks to the cloud.
    - It is a fully managed, elastic VPN service that automatically scales up or down based on user demand. 
    - Because it is a cloud VPN solution, you don’t need to install and manage hardware or try to estimate how many remote users to support at one time.
    - AWS Client VPN provides advanced authentication, remote access.
- AWS Site-to-Site VPN
    - Site-to-Site VPN creates a secure connection between your data center or branch offices and your AWS Cloud resources.
    - It can be used for application migration and secure communication between remote locations.
- AWS PrivateLink (Normal connection to other clouds with best bandwidth and low latency)
    - Used for connecting your clients in your VPC to resources, other VPCs, and endpoints across internet including other cloud providers
    - AWS PrivateLink is a highly available, scalable technology that you can use to privately connect your VPC to services and resources as if they were in your VPC. 
- AWS Direct Connect (Normal connection to on prem with best bandwidth and low latency)
    - Direct Connect is a service that makes it possible for you to establish a dedicated private connection between your network and VPC in the AWS Cloud.
    - AWS Direct Connect reduces network costs and increases amount of bandwidth.
- AWS Transit Gateway: Used to connect your Amazon VPCs and on-premises networks through a central hub. As your cloud infrastructure expands globally, inter-Region peering connects transit gateways together using the AWS Global Infrastructure.
- NAT Gateway: You can use a NAT gateway so that instances in a private subnet can connect to services outside your VPC but external services can't initiate a connection with those instances. 
- API Gateway: AWS service for creating, publishing, maintaining, monitoring, and securing APIs at any scale.
- Network Access Contol Lists (ACLs): 
    - A virtual firewall that controls inbound and outbound traffic at the subnet level. 
    - Each account includes a default network ACL that allows all inbound and outbound traffic. 
    - Stateless packet filtering: Network ACLs perform stateless packet filtering. They remember nothing and check packets that cross the subnet border each way: inbound and outbound. 
    - Scope: Subnet level (associated with subnets)
- Security Groups: 
    - A security group is the VPC component that checks packet permissions for an Amazon EC2 instance. It is a virtual firewall that controls inbound and outbound traffic for specific AWS resources, like Amazon EC2 instances.
    - By default, a security group denies all inbound traffic and allows all outbound traffic. 
    - Stateful packet filtering: Security groups perform stateful packet filtering. They remember previous decisions made for incoming packets.
    - Scope: Instance level (attached to EC2 instances)

## VPN vs Direct Connect:
VPN:
    - Secure
    - Flexible
    - Remote access
    - Small-scale
    - Dedicated connection isn't necessary
Direct Connect:
    - High Bandwidth
    - Low Latency
    - Consistent Performance
    - Large Data Transfers
    - Critical Applications
    - Dedicated connections
    - Physical hard wire connections
- In certain cases, VPN is also used as failover to direct connect
- Multiple direct connects are combined for bigger bandwidth in certain cases. 

## Global Networking:
- Edge networking services: Edge networking is the process of bringing information storage and computing abilities closer to the devices that produce that information and the users who consume it.
- Amazon route 53: Route 53 is a DNS that provides a reliable and cost-effective way to route end users to internet applications. Route 53 directs end users to your resources with globally dispersed DNS servers and automatic scaling. It gives developers and businesses a reliable way to route end users to internet applications hosted in AWS.
- Amazon Cloud Front: CloudFront is a content delivery network (CDN) service that delivers your content with faster loading times, cost savings, and reliability.
- Amazon Global Accelerator: Global Accelerator is a service that uses the AWS global network to improve application availability, performance, and security. It uses intelligent traffic routing and fast failover if something goes wrong in one of your application locations.