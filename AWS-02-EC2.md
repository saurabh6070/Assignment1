Amazon EC2 Features
The AWS Nitro System underpins the latest generation of EC2 instances. Traditionally, hypervisors manage physical hardware and BIOS, virtualize the CPU, storage, and networking, and provide extensive management capabilities. The Nitro System offloads these functions to dedicated hardware and software, reducing instance costs. As a result, the Nitro Hypervisor delivers performance comparable to bare metal and outperforms its predecessor, the Xen Hypervisor.

1. Instances: Virtual server environments.

2. Amazon Machine Images (AMIs): Reusable templates that package the operating system and additional software installations.

3. Instance Types: Various configurations of CPU, memory, storage, and networking capacity for your instances, including:
    General Purpose: t-type and m-type
    Compute Optimized: c-type
    Memory Optimized: r-type, x-type, and z-type
    Storage Optimized: d-type, h-type, and i-type
    Accelerated Computing: f-type, g-type, and p-type

4. Secure Login: Use key pairs to securely log in to your instances.

5. Instance Store Volumes: Temporary storage volumes that are deleted when you stop or terminate your instance. Note that you can stop an EBS-backed instance but not an Instance Store-backed instance; you can only start or terminate the latter.

6. Elastic Block Store (EBS) Volumes: Persistent storage volumes for your data.

7. Regions and Availability Zones: Multiple physical locations for deploying your resources, such as instances and EBS volumes.

8. Security Groups: Firewalls that allow you to specify protocols, ports, and source IP ranges that can access your instances.

9. Elastic IP Addresses: Static IPv4 addresses for dynamic cloud computing.

10. Tags: Metadata that you can create and assign to your EC2 resources.

11. Virtual Private Clouds (VPCs): Virtual networks that are logically isolated from the rest of the AWS cloud and can optionally connect to your own network.

12. User Data: Scripts that run on instance boot.

13. Host Recovery: Automatically restarts your instances on a new host in case of unexpected hardware failure on a Dedicated Host.

14. EC2 Hibernation: Available for On-Demand and Reserved Instances running on specific instance types with Amazon Linux and Ubuntu 18.04 LTS. You can enable hibernation for your EBS-backed instances at launch and manage hibernation through the AWS Management Console, SDK, and CLI. Hibernation requires an encrypted EBS-backed instance.

15. Automatic RDS Connection: Allow automatic connection of one or more EC2 instances to an RDS database.

16. Instance States
Start: Run your instance normally. You are continuously billed while your instance is running.
Stop: Perform a normal instance shutdown. You can restart it anytime. All EBS volumes remain attached, but data in instance store volumes are deleted. You won't be charged for usage while the instance is stopped. You can attach or detach EBS volumes, create an AMI from the instance, and change the kernel, RAM disk, and instance type while in this state.
Hibernate: When an instance is hibernated, it writes the in-memory state to a file in the root EBS volume and then shuts down. The AMI used to launch the instance must be encrypted, as well as the root EBS volume. This encryption ensures proper protection for sensitive data when copied from memory to the EBS volume. While the instance is in hibernation, you pay only for the EBS volumes and Elastic IP addresses attached to it; there are no hourly charges.
Terminate: The instance performs a normal shutdown and gets deleted. You won't be able to restart an instance once you terminate it. The root device volume is deleted by default, but any attached EBS volumes are preserved by default. Data in instance store volumes are deleted.
NOTE :-
To prevent accidental termination, enable termination protection.
By enabling instance stop protection, you can prevent an instance from being accidentally stopped.

17. Root Device Volumes
The root device volume contains the image used to boot the instance. You can replace the root volume of a running EC2 instance using the initial launch state, a snapshot, or an AMI.
17.1 Instance Store-backed Instances
Data on instance store volumes is deleted when the instance is terminated or if it fails (e.g., due to underlying drive issues).
Instance store-backed instances do not support the Stop action.
Regularly back up critical data from instance store volumes to persistent storage.
17.2 Amazon EBS-backed Instances
An Amazon EBS-backed instance can be stopped and later restarted without affecting data stored in the attached volumes.
While in a stopped state, you can modify the instance's properties, change its size, update the kernel, or attach the root volume to a different running instance for debugging or other purposes.
By default, the root device volume for an AMI backed by Amazon EBS is deleted when the instance terminates.
Previously, to launch an encrypted EBS-backed EC2 instance from an unencrypted AMI, you needed to create an encrypted copy of the AMI first. Now, you can directly launch encrypted EBS-backed EC2 instances from unencrypted AMIs.

18. Amazon EC2 – AMI
18.1 An Amazon Machine Image (AMI) includes the following components:
        Template for the Root Volume: This template contains the operating system, application server, and applications for the instance.
        Launch Permissions: These permissions control which AWS accounts can use the AMI to launch instances.
        Block Device Mapping: This specifies the volumes to attach to the instance when it is launched.
18.2 AMI Types:
        Backed by Amazon EBS: The root device for an instance launched from the AMI is an Amazon EBS volume. AMIs backed by Amazon EBS snapshots can utilize EBS encryption.
        Backed by Instance Store: The root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3.

19. Amazon EC2 – AMI Management
19.1 Copying AMIs: You can copy AMIs to different regions to facilitate global deployment.
19.2 Recycle Bin: Restore deleted AMIs using the recycle bin feature.
19.3 Lock Retention Rules: Set rules to protect AMIs from modifications and deletions.
19.4 LastLaunchedTime Timestamp: Check this timestamp to see when your AMI was last used to launch an instance.
19.5 Public AMI Deprecation: By default, a public AMI is deprecated after two years from its creation date.
19.6 Verified Providers: In the EC2 console, public AMIs owned by Amazon or verified Amazon partners are marked as verified providers.
19.6 EventBridge Integration: When an AMI changes state, an event is automatically generated. Use Amazon EventBridge to detect and respond to these events.
19.7 Instance Metadata Service Version 2 (IMDSv2): Configure an AMI to use IMDSv2 when requesting instance metadata.
19.8 There is a data transfer charge when copying AMI from one region to another

20. Amazon EC2 Image Builder
20.1 A fully managed AWS service that automates the creation, management, and deployment of your Amazon Machine Images (AMIs)
20.2 The AWS Management Console, AWS Command Line Interface, or AWS APIs can be used to create custom images in your AWS account.
20.3 The customized images that Image Builder creates in your account are owned by you, and you can configure pipelines to automate updates as well as system patching for the images in your AWS account.
Amazon EC2 Image Builder also provides a stand-alone command to create an AMI with the configuration resources that you have defined.

21. Amazon EC2 Pricing
21.1 AWS imposes a small hourly charge if an Elastic IP address is not associated with a running instance, or if it is associated with a stopped instance or an unattached network interface.
21.2 You are charged for any additional Elastic IP addresses associated with an instance.
21.3 If data is transferred between these two instances, it is charged at “Data Transfer Out from EC2 to Another AWS Region” for the first instance and at “Data Transfer In from Another AWS Region” for the second instance.

22. Amazon Elastic Compute Cloud Security
22.1 Use IAM to control access to your instances (see AWS Security and Identity Service).
*    IAM policies
*    IAM roles
22.2 Restrict access by only allowing trusted hosts or networks to access ports on your instance.
22.3 A security group acts as a virtual firewall that controls the traffic for one or more instances.
*    Create different security groups to deal with instances that have different security requirements.
*    You can add rules to each security group that allows traffic to or from its associated instances.
*    You can modify the rules for a security group at any time.
*    New rules are automatically applied to all instances that are associated with the security group.
*    Evaluates all the rules from all the security groups that are associated with an instance to decide whether to allow traffic or not.
*    By default, security groups allow all outbound traffic.
*    Security group rules are always permissive; you can’t create rules that deny access.
*    Security groups are stateful
22.4 If you don’t specify a security group when you launch an instance, the instance is automatically associated with the default security group for the VPC, which has the following rules:
*    Allows all inbound traffic from other instances associated with the default security group
*    Allows all outbound traffic from the instance.
22.5 Disable password-based logins for instances launched from your AMI, since passwords can be cracked or found.
22.6 You can replicate the network traffic from an EC2 instance within your Amazon VPC and forward that traffic to security and monitoring appliances for content inspection, threat monitoring, and troubleshooting.
22.7 When creating a new key pair, you can specify the key format (.pem & .ppk).
22.8 Querying of the public key and creation date of an EC2 key pair is supported.
22.9 For EC2 Instance Connect and EC2 Serial Console, ED25519 keys are now supported.

23. Amazon EC2 Networking
*    An Elastic IP address is a static IPv4 address designed for dynamic cloud computing. With it, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.
*    If you have not enabled auto-assign public IP address for your instance, you need to associate an Elastic IP address with your instance to enable communication with the internet.
*    An Elastic IP address is for use in a specific region only.
*    By default, all AWS accounts are limited to five (5) Elastic IP addresses per region, because public (IPv4) internet addresses are a scarce public resource.
*    You can transfer Elastic IP addresses from one AWS account to another.
*    By default EC2 instances come only with a private IP when created in a private subnet, and public and private IP when created in a public subnet.
*    An elastic network interface is a logical networking component in a VPC that represents a virtual network card, which directs traffic to your instance
*    Every instance in a VPC has a default network interface, called the primary network interface (eth0). You cannot detach a primary network interface from an instance.
*    You can create and attach additional network interfaces. The maximum number of network interfaces that you can use varies by instance type.
*    You can attach a network interface to an instance in a different subnet as long as its within the same AZ
*    Default interfaces are terminated with instance termination.
*    Scale with EC2 Scaling Groups and distribute traffic among instances using Elastic Load Balancer.
*    You can configure EC2 instances as bastion hosts (aka jump boxes) in order to access your VPC instances for management, using SSH or RDP protocols
*    Enhanced Networking – It provides higher bandwidth, higher packet per second (PPS) performance, and consistent lower inter-instance latencies, which are being used in Placement Groups. It uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities. SR-IOV is a method of device virtualization that provides higher I/O performance and lower CPU utilization when compared to traditional virtualized network interfaces.
*    Elastic Fabric Adapter (EFA) – This is a network device that you can attach to your EC2 instance to significantly accelerate machine learning applications and High Performance Computing (HPC). It empowers your computing resources to achieve the application performance of an on-premises HPC cluster, with the elasticity and scalability provided by AWS. Compared with a TCP transport that is traditionally used in cloud-based HPC systems, EFA provides lower and more consistent latency and higher throughput as it enhances the performance of inter-instance communication.

24. Amazon EC2 Monitoring
24.1 EC2 items to monitor
*    CPU utilization, Network utilization, Disk performance, Disk Reads/Writes using EC2 metrics
*    Memory utilization, disk swap utilization, disk space utilization, page file utilization, log collection using a monitoring agent/CloudWatch Logs
24.2 Automated monitoring tools include:
*    System Status Checks – monitor the AWS systems required to use your instance to ensure they are working properly. These checks detect problems with your instance that require AWS involvement to repair.
*    Instance Status Checks – monitor the software and network configuration of your individual instance. These checks detect problems that require your involvement to repair.
*    Amazon CloudWatch Alarms – watch a single metric over a time period you specify, and perform one or more actions based on the value of the metric relative to a given threshold over a number of time periods.
*    Amazon CloudWatch Events – automate your AWS services and respond automatically to system events.
*    Amazon CloudWatch Logs – monitor, store, and access your log files from Amazon EC2 instances, AWS CloudTrail, or other sources.
24.3 Monitor your EC2 instances with CloudWatch. By default, EC2 sends metric data to CloudWatch in 5-minute periods.
24.4 You can also enable detailed monitoring to collect data in 1-minute periods.


25. Instance Metadata and User Data
*    Instance metadata is data about your instance that you can use to configure or manage the running instance.
*    Instance metadata and user data are not protected by cryptographic methods.
*    View all categories of instance metadata from within a running instance at http://169.254.169.254/latest/meta-data/
*    You can pass two types of user data to EC2: shell scripts and cloud-init directives.
*    User data is limited to 16 KB.
*    If you stop an instance, modify its user data, and start the instance, the updated user data is not executed when you start the instance.
*    Retrieve user data from within a running instance at http://169.254.169.254/latest/user-data
*    An instance tag can be accessed from the instance metadata.
*    When using Auto Scaling groups, the instance metadata contains information about an instance’s target lifecycle state.

26. Placement Groups
*    You can launch or start instances in a placement group, which determines how instances are placed on underlying hardware.
*    Cluster – clusters instances into a low-latency group in a single Availability Zone. Recommended for applications that benefit from low network latency, high network throughput, or both, and if the majority of the network traffic is between the instances in the group.
*    Spread – spreads instances across underlying hardware. Recommended for applications that have a small number of critical instances that should be kept separate from each other. Note: A spread placement group can span multiple Availability Zones, and you can have a maximum of seven running instances per Availability Zone per group.
*    Partition placement groups is an Amazon EC2 placement strategy that helps reduce the likelihood of correlated failures for large distributed and replicated workloads such as HDFS, HBase, and Cassandra running on EC2.
*    Partition placement groups spread EC2 instances across logical partitions and ensure that instances in different partitions do not share the same underlying hardware. In addition, partition placement groups offer visibility into the partitions and allow topology aware applications to use this information to make intelligent data replication decisions, increasing data availability and durability.

27. Amazon EC2 Rules
*    The name you specify for a placement group must be unique within your AWS account for the region.
*    You can’t merge placement groups.
*    An instance can be launched in one placement group at a time; it cannot span multiple placement groups.
*    Instances with a tenancy of host cannot be launched in placement groups.

28. Spot-Instances
*    Request unused EC2 instances, which can lower your costs significantly. Spot Instances are available at up to a 90% discount compared to On-Demand prices.
*    Spot Instances with a defined duration (also known as Spot blocks) are designed not to be interrupted and will run continuously for the duration you select. This makes them ideal for jobs that take a finite time to complete, such as batch processing, encoding and rendering, modeling and analysis, and continuous integration.
*    A Spot Fleet is a collection of Spot Instances and optionally On-Demand Instances. The service attempts to launch the number of Spot Instances and On-Demand Instances to meet your specified target capacity. The request for Spot Instances is fulfilled if there is available capacity and the maximum price you specified in the request exceeds the current Spot price. The Spot Fleet also attempts to maintain its target capacity fleet if your Spot Instances are interrupted.
*    A Spot Capacity pool is a set of unused EC2 instances with the same instance type, operating system, Availability Zone, and network platform.
*    You can start and stop your Spot Instances backed by Amazon EBS at will.
*    You can modify instance types and weights for a running EC2 Fleet or Spot Fleet without having to recreate it.
*    Allocation strategy for Spot Instances
        LowestPrice – The Spot Instances come from the pool with the lowest price. This is the default strategy.
        Diversified – The Spot Instances are distributed across all pools.
        CapacityOptimized – The Spot Instances come from the pool with optimal capacity for the number of instances that are launching.
        InstancePoolsToUseCount – The Spot Instances are distributed across the number of Spot pools that you specify. This parameter is valid only when used in combination with the lowest Price.
