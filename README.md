# Mastering-AWS-Networking-VPC-VPC-Peering-Transit-Gateway
# PROBLEM STATEMENT
You will build a networking solution for a fictional FinTech company named PayWave Systems.
PayWave recently expanded its operations and separated its workloads into three functional environments:
VPC-A (Application VPC)
Runs the primary payment-processing application (APIs, microservices).
VPC-B (Analytics VPC)
Used by the data engineering team for batch jobs, fraud analytics, and reporting.
VPC-C (Shared Services VPC)
Contains centralized tools such as logging, authentication, secrets management, and monitoring dashboards.
Business requirements:
The Application VPC must communicate with Analytics for sending transaction logs.
Analytics VPC must communicate with Shared Services for authentication and reports.
The Application VPC must also communicate with Shared Services.
The company initially wants to explore VPC Peering to understand direct connectivity between environments.
Later, due to expected growth, they need a scalable, centralized architecture using Transit Gateway, since VPC Peering will create too many peering pairs to manage.

## Step 1 – Core Networking Setup
### a)  Create three VPC with diffrent CIDR Ranges as named VPC-A,VPC-B and VPC-C.
<img width="1598" height="697" alt="image" src="https://github.com/user-attachments/assets/bc17f6c0-1252-4ad7-a546-abbc3f3d23c8" />
<img width="1578" height="705" alt="image" src="https://github.com/user-attachments/assets/10767edc-7c21-469e-9d28-dbe5a8efb281" />
<img width="1590" height="693" alt="image" src="https://github.com/user-attachments/assets/2d13e465-66e5-4909-886b-89d7603b7c60" />

### b) Launch three EC2 instances wrt to each VPCs Public Subnet.
<img width="1880" height="938" alt="image" src="https://github.com/user-attachments/assets/4d76eb4d-fdca-4847-85be-861538c420ca" />
<img width="1547" height="686" alt="image" src="https://github.com/user-attachments/assets/990d9b21-3826-40fe-89be-6aa5bc8e724c" />
<img width="1557" height="662" alt="image" src="https://github.com/user-attachments/assets/3d4551fc-185a-48fe-b01c-ff8b2b8bbce5" />
<img width="1560" height="686" alt="image" src="https://github.com/user-attachments/assets/350b3f58-adec-42e9-b740-e1c694e7b994" />

## Step 2 – VPC Peering Implementation:
### 1. Search VPC in AWS and then select Peering Connection and then Create peerring Connections.
<img width="895" height="626" alt="image" src="https://github.com/user-attachments/assets/1c306645-b598-4f5e-9779-53d5db2a0329" />
<img width="1401" height="698" alt="image" src="https://github.com/user-attachments/assets/ed970d21-7d08-4ebf-9c51-c39b11f970ae" />

### 2. Create peering between VPC A & VPC B.
<img width="1392" height="741" alt="image" src="https://github.com/user-attachments/assets/6efef1c5-b653-459d-8ea2-435d574314cc" />
<img width="1647" height="688" alt="image" src="https://github.com/user-attachments/assets/2103c8f6-3481-428d-b605-7644a0b8f204" />

### 3. Now Go back to Peering connection option and check perring request and click on Action and Accept request.
<img width="1897" height="507" alt="image" src="https://github.com/user-attachments/assets/c1690bf6-452c-4799-9286-93f0811a5773" />
<img width="1652" height="592" alt="image" src="https://github.com/user-attachments/assets/bc1ea666-4150-466b-8572-5843cd98eacb" />

### 4 . Now Peering between VPC-A and VPC-B completed and in Active state.
<img width="1616" height="178" alt="image" src="https://github.com/user-attachments/assets/dd5901ef-735c-4b8c-82e0-0bffc7396a2e" />

### 5. Create rest all peering between all VPCs by Repeating above steps.
<img width="1677" height="256" alt="image" src="https://github.com/user-attachments/assets/4f5d2a98-baa3-42c3-bb0c-aa43b5a6550d" />

## Step 3 - Update Route table for both VPCs with peering connection.
### 1. Open VPC Dashboard and click on route
<img width="1042" height="650" alt="image" src="https://github.com/user-attachments/assets/1c811cc7-366d-465b-8394-3862090d466b" />

### 2. Select VPC for which want to update route table,Goto route tab and click on edit route.
<img width="1641" height="697" alt="image" src="https://github.com/user-attachments/assets/0ff6bde2-dc43-401f-a638-dfae970551ab" />

### 3. Click on Add route and enter destination CIDR range.
### 4. Choose peering connection and select Perering ID and save changes.
<img width="1757" height="602" alt="image" src="https://github.com/user-attachments/assets/13960eb3-fd43-4da1-87f9-3ab2dc81cdde" />

### 5. Update route table for all VPCs
<img width="1638" height="420" alt="image" src="https://github.com/user-attachments/assets/364b9afd-6390-4af1-a261-ce11964c6744" />
<img width="1632" height="553" alt="image" src="https://github.com/user-attachments/assets/9e8e869e-53f2-4c93-a87c-4390ba6d74c2" />
<img width="1662" height="632" alt="image" src="https://github.com/user-attachments/assets/f5ea0cc4-d098-4935-ac54-b8fc5d7f521e" />

## Step 4 - Now time to test VPC peering between all three VPCs.

### 1. Check security group for all three active EC2 instances must be enabled **All ICMP - IPv4** on all three instances.
<img width="1622" height="542" alt="image" src="https://github.com/user-attachments/assets/6e818e53-877f-4f10-8ab2-3c1c6db11922" />
<img width="1617" height="555" alt="image" src="https://github.com/user-attachments/assets/d87fe5a6-1da0-48bb-880f-8f936ae7b235" />
<img width="1697" height="547" alt="image" src="https://github.com/user-attachments/assets/98085c7a-1327-46b1-9d6e-a81bbbf48476" />

### 2. Login to EC2 instance with associated with VPC- A and ping pulic ip for VPC-B & VPC-C EC2 instance.
<img width="1638" height="350" alt="image" src="https://github.com/user-attachments/assets/c291ba28-763f-4618-90de-5f85d29d2569" />
<img width="1622" height="331" alt="image" src="https://github.com/user-attachments/assets/572c1e9d-e8fc-458a-9c79-7dccd6f73d80" />
<img width="1621" height="308" alt="image" src="https://github.com/user-attachments/assets/4f9d685c-802e-479d-af00-a8758f004d93" />

  #### A. Here we are getting response from EC2 instance instance associated with VPC-B.
  <img width="667" height="203" alt="image" src="https://github.com/user-attachments/assets/b5b8a2ad-d526-4ec9-ae03-b4b734f6ad5c" />
  
  #### B. Here we are tryed to ping EC2 instance instance associated with VPC-C.
  <img width="661" height="287" alt="image" src="https://github.com/user-attachments/assets/3098b29c-985e-4a4c-8a0b-89ce733f2557" />

### 3. We will try one more time to ping VPC-A & VPC-B EC2 instances public IP from VPC-C EC2 instance.
  #### A. Here we tried to ping with VPC-B from VPC-C and Getting proper response.
  <img width="675" height="255" alt="image" src="https://github.com/user-attachments/assets/e10d23cd-bfc1-43aa-81d5-db4b9716ee14" />
  
  #### B. While trying to ping with VPC-A from VPC-C , we are not getting response, Because we didn't updated route table for VPC-C with VPC-A CIDR and didn't allowed ping to VPC-A from others.
  
  <img width="1602" height="523" alt="image" src="https://github.com/user-attachments/assets/fc4c7b4f-5dde-4659-be92-940035bf67aa" />
  <img width="1657" height="527" alt="image" src="https://github.com/user-attachments/assets/d346c3d3-38d1-4dda-ab5e-822a42e97532" />
  <img width="636" height="215" alt="image" src="https://github.com/user-attachments/assets/5b78a401-5215-4889-b113-24219a819cb1" />

  #### C. After making correction of security group and Route table we started getting Response with VPC- A also.
  <img width="1636" height="518" alt="image" src="https://github.com/user-attachments/assets/ada6ef3d-7459-4340-9c10-6d2fbc4a201a" />
  <img width="787" height="186" alt="image" src="https://github.com/user-attachments/assets/77fadcf2-6493-4306-92b4-1b58075f2624" />
  <img width="1636" height="542" alt="image" src="https://github.com/user-attachments/assets/ae1d07eb-dc01-4e04-9846-80fbc7a77275" />



  

  






 












