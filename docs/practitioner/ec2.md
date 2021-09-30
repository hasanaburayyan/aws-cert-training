# EC2 Elastic Compute Cloud

Oldest services
Virtual server or servers in cloud.
Web service that provides resizable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minutes
allowing you to quickly scale capacity both up and down as your needs change

## EC2 Pricing Models

1. On Demand (allows you to pay a fixed rate by the hour (or second) with no commitment)
2. Reserved  (Provides you with a capacity reservation and offers a significant discount on the hourly charge for an instance. Contract terms are 1 or 3 years)
3. Spot      ( Enables you to bid a price you want to pay for instance capacity)
		NOTE: if amazon EC2 terminates spot instance because of pricing change during your hour of use you will NOT be charged however if you terminate the instance early 
			you are charged for any hour which the instance ran.
4. Dedicated Hosts (Physical EC2 server dedicated for your use.)

### EC2 Pricing

- Clock Hours of Server Time
- Instance Type
- Pricing Model
- Number of Instances
- Load Balancing
- Detailed Monitoring
- Auto Scaling
- Elastic IP Addresses
- Operating Systems and Software Packages
- Pricing Models
- On Demand
- Reserved
- Spot
- Dedicated Hosts
- Lambda Pricing
- Request Pricing
- Free Tier: 1 million requests per month
- $0.20 per 1 mil
- AWS Budgets:
- Gives ability to set custom budgets that alert you when your costs or usage exceed (or are forecasted to exceed your budgeted amount) 
- Used to budget costs before they are incurred


### Silly Acronym To Remember EC2 Types : FIGHT DR MCPXZ

F - For FPGA
I - FOR IOPS
G - Graphics
H - High Disk Throughput
T - Cheap general purpose
D - For Density
R - For RAM
M - Main choice for general purpose apps
C - For Compute
P - Graphics
X - Extreme Memory
Z - Extreme memory and CPU
