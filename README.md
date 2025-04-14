
# ☁️ Deploying an Application Load Balancer on AWS (Step-by-Step)

As part of building scalable infrastructure on AWS, I configured an Application Load Balancer (ALB) to distribute traffic across multiple targets (EC2 instances, IPs, or Lambda functions). Here’s a breakdown of the setup process:

## Step 1: Creating a Target Group

To begin, I configured a target group, which serves as the destination for the load balancer’s traffic. I used the AWS EC2 console to:

- Select target type: EC2 instances by ID or specific IP addresses.

- Define group settings: custom name, protocol/port, IP type (IPv4/IPv6), VPC, and protocol version.

- Customize health checks to monitor target availability using configurable thresholds.

- Optionally, I added tags for better resource tracking and management.


## Step 2: Registering Targets

Once the target group was created, I registered the backend resources:

- For EC2 Instances: selected instances and specified ports.

- For IP Addresses: manually added private IPs within the selected VPC.

- For Lambda functions: linked by name or ARN.

After registration, these targets began receiving traffic once verified as healthy.

## Step 3: Configuring the Load Balancer

Using the EC2 console, I spun up an Application Load Balancer with the following configurations:

- **Basic setup:** unique name, scheme (Internet-facing or Internal), and IP address type (IPv4, Dualstack).

- **Network mapping:** associated the load balancer with a VPC, enabled subnets across Availability Zones, and set up security groups.

- **For Lambda functions:** linked by name or ARN.

- **Listeners:** added HTTP/HTTPS listeners and attached the previously created target group as the default action.

- **HTTPS setup (optional):** used certificates from AWS Certificate Manager (ACM) or IAM, and enabled mutual TLS for added security if needed.

- **Integrations:** optionally connected with services like AWS WAF and Global Accelerator for enhanced protection and global traffic optimization.

## Step 4: Testing the Load Balancer

To verify functionality:

- I monitored the target group's health status to ensure instances passed health checks.

- Retrieved the DNS name of the load balancer and tested it via a browser (depending on internal/external setup).

- When healthy, the ALB routed requests successfully to the target instances, confirming proper configuration.
