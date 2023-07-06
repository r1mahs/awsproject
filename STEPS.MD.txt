## Set up a VPC

- First, set up a Virtual Private Cloud (VPC).
- Use IPV4 `10.0.0.016`.
- Enable DNS host names.

## Create an Internet Gateway

- Create a new internet gateway.
- Attach the internet gateway to the VPC to enable web access.

## Set up Subnets in Availability Zones

- Create two subnets in two Availability Zones (AZ).
- Make one subnet in `us-east-1a` AZ with the CIDR block `10.0.0.024`.
- Make another subnet in `us-east-1b` AZ with the CIDR block `10.0.1.024`.

## Enable Auto-Assign IP Settings

- Enable auto-assign IP settings for the subnets.
- This ensures that any launched EC2 instance is automatically assigned an IPv4 address.

## Create a Route Table

- Create a route table for the VPC.
- Add a public route to the route table to allow traffic to the internet.

## Connect Subnets to Route Table

- Connect the two subnets to the route table.
- This provides access to the internet for the associated subnets.

## NAT Gateway Setup in AZ

- Set up a NAT gateway in each AZ.
- NAT gateway provides internet access to private route tables.
- Make sure to assign an Elastic IP and place it in the public AZ.

## Create Route Table for Private AZ

- Create a new route table for the private AZ.
- Set the destination as `0.0.0.0`, target as the NAT gateway.
- Associate the route table with the private subnets in AZ1.

## Create Security Groups

- Create security groups to control inbound and outbound traffic.
- Application Load Balancer S.G. Apply to ALB, port 80 and 443, source `0.0.0.00`.
- SSH S.G. Use for SSH access, limit source to your IP address.
- Web server S.G. Allow traffic from ALB and SSH.
- Database security group Allow traffic from web server SG.
- EFS security group Allow traffic from web server and EFS.

## Installing WordPress

- SSH into the EC2 instance using the code `ssh ec2-user@(publicip)`.
- Make sure to use the correct SSH key for authentication.

## Installing ALB

- Create EC2 instances for the web server in AZ1 and AZ2.
- Add a target group and route it to both EC2 instances.
- Create an Application Load Balancer (ALB) and select the ALB security group.
- Access the website using the ALB DNS address.
- Optionally, update the domain name in WordPress.

## Get a Domain Name with Route53

- Use Route53 to obtain a new domain name.
- Create a record set in Route53 to route the domain.

## Register an SSL Certificate

- Register for an SSL certificate in AWS Certificate Manager.
- SSL encryption secures communications.
- Create a record set in Route53 to validate the SSL certificate.

## Launch Bastion Host

- Launch a bastion host to SSH into the public EC2 and then access the private EC2.
- Download PuTTY for SSH access.

## Creating a Keypair

- Create a keypair for encryption.
- The public key is used for EC2, and the private key is used to SSH into the EC2.

## Launching EC2 Instance

- Launch an EC2 instance.

## Creating RDS Instance

- Before creating the RDS database, create a subnet group.
- Specify the subnets in which the RDS database works.
- Create the RDS database.

## Creating EFS with Mount Targets

- Create an EFS with mount targets in the private data subnets of each AZ.
- This allows pulling code from the EFS.

