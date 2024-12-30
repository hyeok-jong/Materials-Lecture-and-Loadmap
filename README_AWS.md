


# 3. Application Abstract.(Use Cloud)  
- As mentioned earlier, the application will be deployed to the cloud.  
- First, upload MongoDB to ensure the database runs smoothly in the cloud.  
- Next, learn Docker to prepare for deploying the backend (API).  
- Deploy the backend to ECS and verify that the React project runs properly on the local environment.  
- Finally, build the React project and upload it to S3. Once this is done, the process is complete.  
- For each step, try one by one.  
1. Use only mongoDB Altas : frontend and backend run on local PC and DB runs on Cloud.  
2. Upload API to AWS ECS : only frontend runs on local PC.  
3. Upload built react to AWS S3 : Everything runs on Cloud. Now this is application.  




# 4 MongoDB Atlas - Database to Cloud.  
To make database runs on cloud.    
1. Go to [MongoDB](https://www.mongodb.com)  
2. Create new project -> cluster.  
3. Free tier with region.  
4. Make databse account.  
5. Network Access -> And your local IP to IP Whitelist.  
```
ifconfig -l | xargs -n1 ipconfig getifaddr
```
6. Cluster section -> Connect -> copy your connection string.  
```
mongodb+srv://<username>:<password>@<cluster-name>.mongodb.net/<dbname>?retryWrites=true&w=majority
```  
7. Link your MongoDB cloud to your express.  
```JavaScript
import mongoose from 'mongoose';
import dotenv from 'dotenv';
dotenv.config();
const MONGO_URI = process.env.MONGO_URI;

const connectDB = async () => {
  try {
    await mongoose.connect(MONGO_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    console.log('MongoDB Connected!'.green.bold); 
  } catch (err) {
    console.error('MongoDB Failed:'.red.bold, err.message); 
    process.exit(1); 
  }
};
export default connectDB;
```
8. Go to [MongoDB Compass](https://www.mongodb.com/try/download/compass) and install.  
THis is GUI so easy to control.  
9. Connect your DB by the URL above again.  

Now your database is located on mongoDB Atlas which is remote cloud.  

Also, in MongoDB Altas you can easily backup DB and security options.  




# 5 AWS ECS - Make Your Backend Express (API) Run on Cloud  
This step involves deploying your Express backend to AWS ECS. Below are the steps, their purposes, and key features:  

## 5.1 Abstract.  

1. **Docker - Build Image for AWS ECR**  
   - **Purpose**: Containerize your backend application for deployment.
   - **Key Task**: Create a Dockerfile, build the image, and push it to AWS Elastic Container Registry (ECR).  

2. **IAM**  
   - **Purpose**: Manage permissions for accessing AWS services securely.
   - **Key Task**: Create an IAM role for ECS with permissions to pull images from ECR and access other AWS resources.

3. **AWS CLI**  
   - **Purpose**: Automate interactions with AWS resources.
   - **Key Task**: Use the CLI to configure AWS, authenticate, and execute deployment commands.

4. **VPC (Virtual Private Cloud)**  
   - **Purpose**: Isolate your network and resources for security and scalability.
   - **Key Task**: Create a VPC for hosting your ECS cluster.

5. **VPC - Subnets**  
   - **Purpose**: Divide your VPC into public and private sections for organizing resources.
   - **Key Task**: Create subnets for deploying resources like ECS tasks and load balancers.

6. **VPC - Internet Gateway**  
   - **Purpose**: Enable internet access for your resources.
   - **Key Task**: Attach an Internet Gateway to the VPC for public-facing resources.

7. **Route Table**  
   - **Purpose**: Define traffic routing rules within your VPC.
   - **Key Task**: Associate the Internet Gateway with a route table to enable external access.

8. **NAT Gateway**  
   - **Purpose**: Provide internet access for private subnets (e.g., ECS tasks).
   - **Key Task**: Create a NAT gateway and associate it with a private subnet.

9. **Elastic IP**  
   - **Purpose**: Assign a fixed IP address for external communication.
   - **Key Task**: Add the Elastic IP to your MongoDB Atlas whitelist to enable database access.

10. **ECS Cluster**  
    - **Purpose**: Manage your containerized applications.
    - **Key Task**: Create an ECS cluster to host your tasks and services.

11. **ECS Task Definition**  
    - **Purpose**: Define the specifications for running your container.
    - **Key Task**: Configure the container image, CPU, memory, and environment variables.

12. **ECS Service**  
    - **Purpose**: Ensure your task runs continuously and handles scaling.
    - **Key Task**: Create a service to run your task in the cluster.

13. **ALB (Application Load Balancer)**  
    - **Purpose**: Distribute incoming traffic across multiple ECS tasks.
    - **Key Task**: Create an ALB and get a URL to connect your frontend with the API.

14. **Security Groups**  
    - **Purpose**: Control access to your resources.
    - **Key Task**: Configure rules to allow specific IPs or ports for secure communication.

15. **Target Group**  
    - **Purpose**: Connect the ALB to your ECS tasks.
    - **Key Task**: Define the backend instances that will handle the traffic from the ALB.  

16. **ECR**  
    - **Purpose**: Repository for Docker Image.
    - **Key Task**: Save Docker Image and run the container on ECS.  





## 5.2 Docker  
See my [repo](https://github.com/hyeok-jong/Dockerfiles) for more details about Docker.  
Here, I use `docker-compose` to build the image, create the container, and start it all at once.

### Dockerfile

```Dockerfile
# Use the official Node.js image with version 22.11.0
FROM node:22.11.0

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install Node.js dependencies
RUN npm install

# Copy all remaining source code into the container
COPY . .

# Accept a custom start command as a build argument
ARG START_COMMAND

# Set the environment variable for the start command
ENV START_COMMAND=${START_COMMAND}

# Execute the provided start command when the container starts
CMD ["sh", "-c", "${START_COMMAND}"]
```

### docker-compose.yml

```yaml
version: '3.8'

services:
  backend:
    container_name: backend-container
    build:
      context: .   # Use the current directory for the build context
      dockerfile: Dockerfile  # Specify the Dockerfile to use
      args:
        START_COMMAND: "${START_COMMAND}"  # Pass the start command as a build argument
    image: devaws  # Specify the name of the image to build
    ports:
      - "${PORT}:${PORT}"  # Map the host and container ports using the environment variable
    env_file:
      - .env  # Load environment variables from a .env file
    volumes:
      - .:/app  # Mount the current directory into the container
      - /app/node_modules  # Bind the node_modules directory to avoid conflicts
    command: ["sh", "-c", "${START_COMMAND}"]  # Execute the start command
```

### How to Use  
Run the following command to build the Docker image, create the container, and start it:  
```bash
docker-compose up --build
```

This process:  
1. Builds a Docker image locally.  
2. Creates and starts the container in a single step.  

By testing locally first, you can ensure everything works as expected. Once verified, you can upload the built Docker image to AWS for deployment.  

The uploaded Docker image contains all the necessary code and dependencies for running your backend.  





## **5.3 AWS IAM**

### **5.3.1. Creating a User and Assigning Policies**  
1. Navigate to **AWS Management Console** → **IAM** → **Users** → Click **Create user**.  
2. Under **Attach policies directly**, add:  
   - `AmazonEC2ContainerRegistryFullAccess`  
   - `AmazonECS_FullAccess`  
   - `AmazonEC2ContainerRegistryReadOnly` (**Added as the previously missing policy**)  
3. After creating the user, go to user to generate an **Access Key** from the **Security Credentials(CLI)** section.



### **5.3.2 Logging into AWS CLI**  
1. After installing the CLI, log in using the generated **Access Key**:  
   ```bash
   aws configure
   ```  
2. Verify successful login with the following command:  
   ```bash
   aws sts get-caller-identity
   ```  



### **5.3.3 Setting Up ECS Task Execution Role**  

To enable ECS tasks to pull images from ECR, configure the `ecsTaskExecutionRole`.  

1. Navigate to **AWS Management Console** → **IAM** → **Roles** → Click **Create role**.  
2. Select **Trusted entity type**: AWS service → Use case: **ECS**.  
3. Attach the following policies:  
   - `AmazonECSTaskExecutionRolePolicy`  
   - `AmazonEC2ContainerRegistryReadOnly`  
4. Name the role as `ecsTaskExecutionRole`.  
5. Specify this role as the **Task execution role** when creating the ECS Task Definition.  
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "ecs-tasks.amazonaws.com"
            },
            "Action": "sts:AssumeRole"
        }
    ]
}

```





## **5.4 VPC and Network Configuration**

### **5.4.1 Creating a VPC**  
1. Navigate to **AWS Management Console** → **VPC** → Click **Create VPC**.  
2. Configure the VPC:  
   - **Name**: `mongoDB-VPC`  
   - **IPv4 CIDR block**: `10.0.0.0/16`  
   - **IPv6 CIDR block**: None  
   - **Tenancy**: Default  
3. Click **Create VPC**.



### **5.4.2 Creating Subnets**  
Use the VPC created earlier to configure subnets.

#### **Public Subnet**  
1. **Name tag**: `mongoDB-public-1`  
2. **IPv4 CIDR block**: `10.0.1.0/24`  
3. **Availability Zone**: e.g., `ap-northeast-2a`

#### **Additional Public Subnet**  
1. **Name tag**: `mongoDB-public-2`  
2. **IPv4 CIDR block**: `10.0.2.0/24`  
3. **Availability Zone**: e.g., `ap-northeast-2b`

#### **Private Subnet**  
1. **Name tag**: `mongoDB-private-1`  
2. **IPv4 CIDR block**: `10.0.3.0/24`  
3. **Availability Zone**: e.g., `ap-northeast-2a`

#### **Additional Private Subnet**  
1. **Name tag**: `mongoDB-private-2`  
2. **IPv4 CIDR block**: `10.0.4.0/24`  
3. **Availability Zone**: e.g., `ap-northeast-2b`



### **5.4.3 Creating and Attaching an Internet Gateway**  
1. **Name tag**: `mongoDB-igw`  
2. Attach the gateway to the VPC:  
   - Navigate to **created igw → Actions → Attach to VPC** → Select `mongoDB-VPC`.



### **5.4.4 Configuring Route Tables**

Each route table connects to two subnets.

#### **5.4.4.1 Public Route Table**  
1. **Name tag**: `public-route-table`  
2. Add a route(Edit routes):  
   - Destination: `0.0.0.0/0`  
   - Target: Internet Gateway (`mongoDB-igw`)  
3. Associate the table with public subnets:  
   - Subnet associations → Explicit Subnet associations → Select `mongoDB-public-1` and `mongoDB-public-2`.

#### **5.4.4.2 Private Route Table**  
1. **Name tag**: `private-route-table`  
2. Complete configuration after creating the NAT Gateway.



### **5.4.5 Setting Up NAT Gateway and Elastic IP**

#### **5.4.5.1 Creating an Elastic IP**  
1. Navigate to **VPC → Elastic IPs → Allocate Elastic IP address**.

#### **5.4.5.2 Creating a NAT Gateway**  
1. **Name tag**: `mongoDB-nat`.  
2. **Subnet**: Choose one of the public subnets (`mongoDB-public-1` or `mongoDB-public-2`).  
3. **Elastic IP**: Select the allocated Elastic IP.

#### **5.4.5.3 Associating the Private Route Table**  
1. Add a route to the private route table:  
   - Destination: `0.0.0.0/0`  
   - Target: NAT Gateway (`mongoDB-nat`).  
2. Associate the private route table with private subnets:  
   - Subnet associations → Explicit Subnet associations → Select `mongoDB-private-1` and `mongoDB-private-2`.




## **5.5 Docker to ECR**


#### **5.5.1 Build Docker Image**
1. **Build using Docker Compose**:
   ```bash
   docker-compose up --build
   docker image inspect image-name:latest --format '{{.Architecture}}'
   ```
   - `docker-compose up --build`: Builds and starts the container using Docker Compose.
   - `docker image inspect`: Checks detailed information about the specified image, such as its architecture (`Architecture`).

#### **5.5.2 Create an ECR Repository**
1. In the AWS Management Console, go to **Elastic Container Registry → Create Repository**.  
2. **Repository Name**: `express-backend`

#### **5.5.3 Upload Docker Image to ECR**
1. Log in to ECR:
   ```bash
   aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.<region>.amazonaws.com
   ```
   - Replace `<region>` with your AWS region (e.g., `us-east-1`).
   - Replace `<AWS_ACCOUNT_ID>` with your AWS account ID.

2. Tag the image and upload it to ECR:
   ```bash
   docker tag express-backend:latest <AWS_ACCOUNT_ID>.dkr.ecr.<region>.amazonaws.com/express-backend:latest
   docker push <AWS_ACCOUNT_ID>.dkr.ecr.<region>.amazonaws.com/express-backend:latest
   ```
   - `docker tag`: Assigns the specified ECR repository name to the local image.
   - `docker push`: Pushes the tagged image to the ECR repository.




## **5.6 ECS Cluster and Service Configuration**

### **5.6.1 Create an ECS Cluster**
1. Navigate to **AWS Management Console → ECS → Create Cluster**.  
2. **Cluster Name**: `mongoDB-ecs-cluster`  
3. **Infrastructure**: Select `AWS Fargate` (serverless container hosting).  



### **5.6.2 Create a Task Definition**
1. Go to **ECS → Task Definitions → Create new Task Definition**.  
2. **Launch Type**: Choose `Fargate`, Linux/ARM64.    
3. **Task Execution Role**: Select the previously created `ecsTaskExecutionRole` (this is crucial).  

4. **Container Configuration**:
   - **Name**: `mongo-app`  
   - **Image URI**: Enter the URI of the Docker image uploaded to ECR (e.g., `<AWS_ACCOUNT_ID>.dkr.ecr.<region>.amazonaws.com/express-backend:latest`).  
   - **Environment Variables**:
     ```plaintext
     MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/dbname
     ```
     - Replace `username`, `password`, `cluster.mongodb.net`, and `dbname` with actual MongoDB connection details.

5. **Network Mode**: Select `awsvpc` (ensures each task has its own network interface).  
6. **Task Size**:
   - **CPU**: Select `0.5 vCPU`.  
   - **Memory**: Choose `1 GB`.  
   - **Container Port Mapping**:  
     - **Port**: `3000`  
     - **Protocol**: `TCP` (for HTTP traffic).  

7. Click **Create Task Definition**.



#### **Additional Notes**:
- Ensure the **Task Execution Role** (`ecsTaskExecutionRole`) includes the `AmazonEC2ContainerRegistryReadOnly` policy. Without this permission, the ECS task will not be able to pull images from ECR.
- Double-check that the **Image URI** in the task definition matches the one uploaded to ECR.





## **5.7 ALB and Target Group Setup (Before ECS Service)**

To route traffic for ECS services, you must configure an **Application Load Balancer (ALB)** and a **Target Group** in advance. Setting up the ALB should be the first step.



### **5.7.1 Create an ALB**
1. Go to **AWS Management Console → EC2 → Load Balancers → Create Load Balancer**.  
2. **Configuration**:  
   - **Type**: Application Load Balancer (ALB).  
   - **Name**: `mongo-alb`.  
   - **Scheme**: `internet-facing` (accessible from the internet).  
   - **Listeners**:
     - **Protocol**: HTTP.  
     - **Port**: 80.  
   - **VPC**: Select the `mongoDB-VPC`.  
   - **Subnets**: Choose two public subnets (e.g., `mongoDB-public` and `mongoDB-public-2`).  

3. **Security Group** (this should ideally be created beforehand):  
   - **Name**: `ALB-SG`.  
     - **Inbound Rules**:
       - **Protocol**: HTTP.  
       - **Port**: 80.  
       - **Source**: `0.0.0.0/0` (allows access from anywhere).  
     - **Outbound Rules**:
       - **All traffic**: `0.0.0.0/0` (default setting).  
4. Listeners and routing 
HTTP : 80
Target Group



#### **Preparation Before ALB Setup**

Before setting up the ALB, ensure the following:
- **VPC** is already created and properly configured.  
- You are logged into the AWS Management Console.  
- **AWS Region** is set to match the region where your VPC and ECS cluster are deployed.  



## **5.8 Steps to Create Security Groups (Before ALB Setup)**


### **5.8.1 Navigate to the EC2 Service Page**  
- In the AWS Management Console, type `EC2` in the top search bar and select the EC2 service.  

### **5.8.2 Open the Security Groups Menu**  
- In the left sidebar, under the **Network & Security** section, click **Security Groups**.



### **5.8.3 Create Security Group for ALB (`ALB-SG`)**

1. Click the **Create security group** button at the top.  
2. **Security group name**: `ALB-SG`.  
3. **Description**: `SG for ALB`.  
4. **VPC**: Select the VPC where your application operates (e.g., `mongoDB-VPC`).  
5. **Inbound rules**:  
   - Click **Add rule**.  
   - **Type**: `HTTP`.  
   - **Port**: `80`.  
   - **Source**: `0.0.0.0/0`.  
     (This allows HTTP traffic from anywhere in the world.)  
6. Leave **Outbound rules** as the default (`All traffic allowed`).  
7. Click **Create security group**.  

   → The Security Group for the ALB (`ALB-SG`) is now ready to use.



### **5.8.4 Create Security Group for ECS Tasks (`ECS-TASK-SG`)**

1. Click the **Create security group** button again.  
2. **Security group name**: `ECS-TASK-SG`.  
3. **Description**: `SG for ECS Tasks`.  
4. **VPC**: Select the same VPC as used for the ALB (`mongoDB-VPC`).  
5. **Inbound rules**:  
   - Click **Add rule**.  
   - **Type**: `Custom TCP`.  
   - **Port Range**: Enter the port your container uses (e.g., `3000`).  
   - **Source**: Select the previously created `ALB-SG`.  
     (This ensures that only traffic from the ALB can access the ECS tasks.)  
6. Leave **Outbound rules** as the default (`All traffic allowed`).  
7. Click **Create security group**.  

   → The Security Group for ECS Tasks (`ECS-TASK-SG`) is now ready.



### **How to Use These Security Groups**

1. **When Creating the ALB**:  
   - Assign the `ALB-SG` security group to the ALB.  

2. **When Configuring ECS Service or Task Definition**:  
   - Assign the `ECS-TASK-SG` security group to the ECS tasks.  
   - Use private subnets for the ECS tasks and disable Public IP assignment for enhanced security.






## **5.9 Create Target Group (Before Security Group Setup)**

1. Navigate to **EC2 → Target Groups → Create Target Group -> IP addresses**.  
2. **Configuration**:  
   - **Name**: `mongo-target-group`.  
   - **Target Type**: `IP` (for tasks that use `awsvpc` network mode).  
   - **Protocol**: HTTP.  
   - **Port**: `3000` (ECS container port).  
   - **VPC**: Select `mongoDB-VPC`.  

3. **Register Targets**:  
   - Do not register any targets manually. ECS tasks will automatically register their IPs with the target group when running.  
   - Simply proceed with creating the Target Group.



## **5.10 Create ECS Cluster**

1. Go to **AWS Management Console → ECS → Clusters → Create Cluster**.  
2. **Cluster Template**: Select **Networking only**.  
3. **Cluster Name**: Enter `mongoDB-ecs-cluster`.  
4. Click **Create Cluster** to complete the process.  

## **5.11 ECS Service Creation**
### **5.11.1 Create the Service**

1. Navigate to **ECS → Services → Create**.  
2. **Configuration**:  
   - **Cluster**: Select `mongoDB-ecs-cluster`.  
   - **Launch Type**: `Fargate`.  
   - **Task Definition**: Choose the previously created task definition (`mongo-app-task`).  
   - **Service Name**: Enter `mongo-app-service`.  
   - **Number of Tasks**: Set to `1` (minimum number of running tasks).  



### **5.11.2 Network Configuration**  

1. **VPC**: Select `mongoDB-VPC`.  
2. **Subnets**: Choose both `mongoDB-private` subnets.  
3. **Security Group**:  
   - Assign the **ECS-TASK-SG** security group created earlier:  
     - **Inbound Rules**:  
       - **Type**: Custom TCP  
       - **Port**: `3000` (application port)  
       - **Source**: `ALB-SG` (ensures traffic comes only from the ALB).  
     - **Outbound Rules**:  
       - **Type**: All Traffic  
       - **Destination**: `0.0.0.0/0`.  
4. **Public IP**: Set to `Disabled` (as the service runs in private subnets).  



### **5.11.3 Load Balancer Configuration**  

1. **Load Balancer Type**: Select `Application Load Balancer`.  
2. **Load Balancer Name**: Choose `mongo-alb`.  
3. **Container to Load Balance**:  
   - **Container Name**: `mongo-app` (name used in the task definition).  
   - **Container Port**: `3000` (port exposed by the ECS container).  
4. **Target Group**: Choose the previously created target group (`mongo-target-group`).  



#### **Additional Notes**:  
- Ensure **ECS-TASK-SG** and **ALB-SG** have proper cross-references in their inbound and outbound rules for seamless traffic flow.  
- Verify that the **VPC Network ACLs (NACL)** do not block inbound or outbound traffic (default settings allow all).  




## **5.12 MongoDB Atlas Setup**

1. Retrieve the **Elastic IP** associated with the NAT Gateway in your VPC:  
   - Go to **AWS Management Console → VPC → Elastic IPs**.  
   - Find the Elastic IP assigned to your NAT Gateway and copy it.

2. Add the Elastic IP to **MongoDB Atlas IP Whitelist**:  
   - Log in to **MongoDB Atlas**.  
   - Navigate to **Network Access → IP Whitelist**.  
   - Click **Add IP Address**.  
   - Paste the Elastic IP of the NAT Gateway.  
   - Save the changes.  

This ensures your ECS tasks can securely connect to MongoDB Atlas from the private subnets.



### **(Optional) Consider ECR VPC Endpoints**

If you want to access Amazon ECR without using a NAT Gateway, consider adding the following VPC endpoints to your VPC:  

- `com.amazonaws.<region>.ecr.api`  
- `com.amazonaws.<region>.ecr.dkr`  

Steps to add VPC endpoints:  
1. Go to **AWS Management Console → VPC → Endpoints → Create Endpoint**.  
2. Select the appropriate endpoint service (ECR API or DKR).  
3. Attach it to the VPC and subnets where your ECS tasks are running.  
4. Update the security groups for the VPC endpoint to allow traffic from ECS tasks.

This allows ECS to pull images from ECR in a private network without needing a NAT Gateway.


### **Final Verification**

1. Test the API using the **ALB DNS Name**:
   ```http
   http://<ALB-DNS-Name>:80
   ```
   Replace `<ALB-DNS-Name>` with the DNS name of your ALB.  

2. Monitor the **ECS Service Logs**:  
   - Go to **AWS Management Console → ECS → Tasks → Logs**.  
   - Verify that the ECS tasks are running and connecting to MongoDB Atlas successfully.  

3. Check **MongoDB Atlas Monitoring**:  
   - Go to the **Atlas Dashboard → Database Deployments → Monitoring**.  
   - Ensure the application is connecting and querying as expected.

4. Troubleshoot any issues:  
   - Recheck the following configurations:  
     - NAT Gateway setup.  
     - Task Execution Role permissions.  
     - Security group and NACL rules.  
     - Route table settings.  




# **6. API - HTTP -> HTTPS Redirection**

---

## **6.1 Custom Domain**
In the previous setup, using the ALB's DNS name allowed the API to work correctly.  
However, for HTTPS, a custom domain is required.  
I used **Dynadot** for my domain management.

**Dynadot DNS Configuration:**
- **Subdomain:** `api`
- **Record Type:** `CNAME`
- **IP Address or Target Host:** ALB's DNS name (e.g., `albname-idnumber.ap-northeast-2.elb.amazonaws.com`).

Test the setup by accessing:
- **URL:** `http://api.customdomain.com`
- You should see `SUCCESS`.

---

## **6.2 AWS ACM - SSL Certificate**
1. Navigate to **AWS Certificate Manager (ACM)** → **Request** → **Request a public certificate**.
2. **Domain Name:** `api.customdomain.com`.
3. Select **DNS validation (recommended)**.
4. Obtain the **CNAME** and **VALUE** for DNS validation.

---

## **6.3 Custom Domain Validation**
1. In **Dynadot DNS Settings**:
   - **Subdomain:** Remove the domain part (e.g., `_random-string.api` instead of `_random-string.api.customdomain.com`).
   - **Record Type:** `CNAME`.
   - **Value:** Use the CNAME value provided by ACM (`random-value.acm-validations.aws`).
2. Return to **AWS ACM** and confirm the certificate status becomes **Issued** (takes ~5 minutes).

---

## **6.4 ALB - Add HTTPS Listener**
1. Navigate to **AWS EC2 → Load Balancers → Select your ALB**.
2. Go to the **Listeners and Rules** tab → **Add Listener**.
3. Configure:
   - **Protocol:** HTTPS.
   - **Port:** 443.
   - **Target Group:** Use the existing Target Group with HTTP.
   - **Certificate (from ACM):** Select the issued certificate for `api.customdomain.com`.

---

## **6.5 ALB - HTTP -> HTTPS Redirection**
1. Navigate back to the same ALB → Select the **HTTP Listener (Port 80)**.
2. Modify the **Default Action**:
   - **Action:** Redirect to.
   - **Redirect to:** HTTPS.
   - **Port:** 443.
   - **Response Code:** 301 (Moved Permanently).

---

## **6.6 ECS -> Security Group**
Ensure the security group attached to your ALB is correctly configured.

1. Select the **security group** attached to the ALB.
2. Edit **Inbound Rules**:
   - **HTTP (Port 80):** Keep open for redirection purposes.
   - **HTTPS (Port 443):** Allow traffic.
     - **Type:** HTTPS.
     - **Port Range:** 443.
     - **Source:** `0.0.0.0/0` (allow all IPs).

---

## **6.7 Testing**
1. Test the following configurations in your API client or browser:
   - **Old URL (HTTP):** This should redirect to HTTPS or fail.
   - Update your base URL:
     ```javascript
     // export const baseURL = 'http://albname-idnumber.ap-northeast-2.elb.amazonaws.com';
     export const baseURL = 'https://api.customdomain.com';
     // export const baseURL = 'http://api.customdomain.com';
     ```
2. Confirm that all requests now work over HTTPS.

---

This completes the **HTTP to HTTPS redirection** setup for your API using a custom domain! If you encounter any issues, let me know for further assistance. 😊




---

# 7 AWS S3 - Deploying Your Built React App on the Cloud  
This guide helps you deploy a React app to AWS S3 with a custom domain.

## 7.1 Build Your React App  
Run the following command to build the production version of your React app:  
```bash
npm run build
```  
This generates a `build/` folder containing all static files for deployment.

---

## 7.2 Buy a Custom Domain  
You can purchase a domain from any domain registrar. For this example, Dynadot is used.

---

## 7.3 Create an S3 Bucket  

1. **Create a new S3 bucket**:  
   - Name it the same as your custom domain (e.g., `customdomain.com`).
   - Uncheck **Block all public access** (you'll see a warning, which is normal).  

2. **Enable Static Website Hosting**:  
   - Go to the bucket's **Properties** tab.  
   - Enable **Static Website Hosting**.  
   - Set the following:  
     - **Index Document**: `index.html`  
     - **Error Document**: `index.html` (necessary for React Router).  

3. **Upload Your Build Files**:  
   - Upload all files from the `build/` folder to the root of your S3 bucket.  

4. Permissions  
Block all public access -> On.  


---

## 7.4 Configure Bucket Policy  

To make the contents of your bucket publicly accessible:  
1. Go to the **Permissions** tab of your bucket.  
2. Add the following JSON to the **Bucket Policy** section:  
OAC 사용할꺼임.  
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudfront.amazonaws.com"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::your_domain.com/*",
            "Condition": {
                "StringEquals": {
                    "AWS:SourceArn": "arn:aws:cloudfront::<YOUR_ACCOUNT_ID>:distribution/<CLOUDFRONT_ID>"
                }
            }
        }
    ]
}
```
CLOUDFRONT_ID : CloudFront -> Distribution ID  

Step 1: Origin 설정  
Origin Domain:  
https://<bucket-name>.s3.<region>.amazonaws.com (REST API URL 사용).  
Origin Access Control (OAC) 활성화:  
CloudFront 콘솔에서 Origin Access Control 설정을 추가.  
생성된 OAC를 S3 버킷 정책에 반영.  
Step 2: Behaviors 설정  
Default Root Object:  
index.html로 설정하여 기본 파일을 제공.  
Viewer Protocol Policy:  
Redirect HTTP to HTTPS로 설정하여 HTTP 요청을 HTTPS로 리다이렉트.  




This policy allows public access to the files in your bucket. Replace `yourdomain.com` with your actual bucket name (domain).



## 7.5 ACM SSL  

1. **Go to the ACM Console**  
   - In the AWS Management Console, change the region to **US East (N. Virginia)** (`us-east-1`) from the top-right corner.

2. **Request a Certificate**  
   - Navigate to **Certificate Manager (ACM)** → Click **Request a Certificate**.  
   - Choose **Request a Public Certificate**.  

3. **Enter Domain Names**  
   - Add your domain names (e.g., `yourdomain.com` and `www.yourdomain.com`).  

4. **Choose Validation Method**  
   - Select **DNS Validation** → Click **Next**.  

5. **Verify the CNAME Record Provided by ACM**  
   - Example CNAME record provided by ACM:  
     - **Name**: `_randomstring.yourdomain.com`  
     - **Value**: `_anotherstring.acm-validations.aws`  

6. **Add the CNAME Record to Your DNS Management Service**  
   - If using Route 53 (or another domain management service), add the provided CNAME record to your DNS settings.  

7. **Check Certificate Status**  
   - Return to ACM and wait for the status to change to **Issued**.  
   - This process may take 5–30 minutes.


## 7.6 Dynadot: Completing ACM Certificate Validation  

1. **CNAME Record Example from ACM**  
   - **Name**: `_randomstring.yourdomain.com`  
   - **Value**: `_anotherstring.acm-validations.aws`  

2. **Add the CNAME Record in Dynadot**  
   - Navigate to Dynadot's DNS management settings.  
   - Add the CNAME record as follows:  
     - **Subdomain**: `_randomstring` (only the part before `.yourdomain.com`)  
     - **Record Type**: CNAME  
     - **Target Host**: `_anotherstring.acm-validations.aws`  

3. **Save Changes**  
   - Save the settings in Dynadot.  

4. **Verify Certificate Status in ACM**  
   - Return to the AWS ACM console and check if the certificate status changes to **Issued**.  
   - This may take 5–30 minutes.  

5. **Region Reminder**  
   - Ensure that you remain in the **US East (N. Virginia)** (`us-east-1`) region throughout this process.  




## 7.7 AWS CloudFront  

### 1. Create Distribution  

#### Origin Settings  

- **Origin Domain Name**:  
  - Select the website endpoint of your S3 bucket.  
  - Example: `yourdomain.com.s3-website-ap-northeast-2.amazonaws.com`.  
  - **Important**: Ensure you select "Use website endpoint."  
    - Reason: S3's static website hosting only supports HTTP. Using the website endpoint ensures CloudFront works correctly.  

- **Origin Access**:  
  - **Port**: 80  
  - **Origin Shield**: No  
    - Reason: Only enable Origin Shield if large-scale traffic is expected. Otherwise, it is unnecessary for typical use cases.  

---

#### Default Settings  

- **Compress Objects Automatically**: Yes  
- **Viewer Protocol Policy**: Redirect HTTP to HTTPS  
- **Allowed HTTP Methods**: All  
- **WAF**: Optional (Use if you need Web Application Firewall protection).  

---

### 2. Distribution Settings  

- **Price Class**: Use all edge locations (best performance)  
  - Reason: Ensures optimal performance by using all global edge locations.  

- **Alternate Domain Name (CNAME)**: `yourdomain.com`, `www.yourdomain.com`  
  - Reason: Connects your custom domain to CloudFront.  

- **Custom SSL Certificate**: Select the certificate issued by ACM (`yourdomain.com`)  
  - Reason: Required to enable HTTPS support. Ensure the certificate status is **Issued**.  

- **Supported HTTP Versions**: HTTP/2, HTTP/3  
  - Reason: Supports the latest protocols for better performance.  

- **Default Root Object**: `index.html`  
  - Reason: Ensures the root URL ("/") loads the default page of your React app.  

- **IPv6**: On  
  - Reason: Supports modern network protocols for improved compatibility.  

- **Logging**: Off (enable only if needed)  
  - Reason: Logging incurs additional costs, so use it only when required.  

---

### 3. Verify the CloudFront Distribution  

- Select the newly created CloudFront distribution.  
- Go to the **General** tab and note the **Domain Name**:  
  - Example: `d1234abcd.cloudfront.net`.  

---

### 4. Dynadot DNS Configuration  

#### (1) Primary Domain (`yourdomain.com`)  
- **Record Type**: CNAME  
- **Target Host**: `d1234abcd.cloudfront.net` (CloudFront distribution domain).  
- **Subdomain**: Leave blank.  

#### (2) Subdomain (`www.yourdomain.com`)  
- **Record Type**: CNAME  
- **Target Host**: `d1234abcd.cloudfront.net` (CloudFront distribution domain).  
- **Subdomain**: `www`.  

#### (3) Existing API and ACM Settings  
- Keep the following settings unchanged:  
  - **Subdomain**: `api` → Connected to ALB (Application Load Balancer).  
  - **Subdomain**: `_9dddc9e71bd89...` → Used for ACM certificate validation.  





## 7.8 Route 53  

You **do not need Route 53**. Since you're already using Dynadot DNS, and it is working perfectly, Route 53 is unnecessary for this setup.

### Why You Don't Need Route 53  

#### **1. DNS Management**  
- DNS settings are already configured in Dynadot, so there's no need to add Route 53.  
- Route 53 is AWS's DNS service and should only be used if required.  

#### **2. Current Situation**  
- Dynadot is successfully managing both CloudFront and API connections.  
- ACM certificate validation has also been completed through Dynadot's CNAME records.  
- For hosting your React app and API, Dynadot alone is sufficient.  

#### **3. Additional Costs**  
- Using Route 53 incurs costs for hosted zones and per-query charges.  
- Dynadot includes DNS management features in its domain cost, making it more cost-efficient.  

#### **Conclusion**  
- Dynadot DNS can handle everything you need.  
- Route 53 is unnecessary unless you want to manage the domain entirely within AWS or require seamless AWS service integration.  

Let me know if you have any additional questions! 😊  

---

## 7.9 Updating React App Files in S3 and CloudFront  

Below is a simple guide to reflect changes when the build files of your React app are updated.

---

### **1. Create a New Build**  

After making changes to your React app, generate a new build:  
```bash
npm run build
```  
- This will create a `build/` directory with the latest static files.

---

### **2. Update Files in the S3 Bucket**  

#### **Option 1: Using AWS CLI (Recommended)**  
1. Ensure AWS CLI is installed and configured.  
2. Sync the new build files to your S3 bucket:  
   ```bash
   aws s3 sync ./build s3://your-bucket-name --delete
   ```  
   - `--delete` removes unnecessary files from the S3 bucket.  
   - Replace **your-bucket-name** with your actual S3 bucket name.  

#### **Option 2: Using AWS Management Console**  
1. Navigate to the **S3 Console** and select your bucket.  
2. (Optional) Delete existing files:  
   - Click **Select All** → **Delete**.  
3. Upload new files:  
   - Click the **Upload** button and upload all files from the `build/` directory.

---

### **3. Invalidate CloudFront Cache**  

Since CloudFront uses caching, updated files might not immediately reflect. Perform a **cache invalidation** to ensure changes are applied.

#### **Option 1: Using AWS CLI**  
1. Run the following command to invalidate the cache:  
   ```bash
   aws cloudfront create-invalidation --distribution-id YOUR_DISTRIBUTION_ID --paths "/*"
   ```  
   - Replace **YOUR_DISTRIBUTION_ID** with your CloudFront distribution ID (found in the CloudFront console).  
   - `/*` invalidates all file paths.  

#### **Option 2: Using AWS Management Console**  
1. Go to the **CloudFront Console** and select your distribution.  
2. Navigate to the **Invalidations** tab → Click **Create Invalidation**.  
3. Enter `/*` in the **Paths** field → Click **Invalidate**.

---

### **4. Final Verification**  

1. Visit `https://leehyeokjong.com` or `https://www.leehyeokjong.com` to ensure the changes are reflected.  
2. Cache invalidation may take a few minutes to complete.  

---

### **Automation Tip (CI/CD)**  

To automate the update process, use CI/CD tools like **GitHub Actions** or **AWS CodePipeline**:  
1. Automatically trigger a build when code is updated.  
2. Upload the build files to S3.  
3. Invalidate CloudFront cache.  
















# Next Steps After Completing Web, Server, and Database on AWS  

Once you’ve set up the web app, server, and database and verified everything is working correctly on AWS, here’s how you can manage updates or additional development:

---

## **Development Workflow**  

### **1. Updating Only the React App**  
- **Local Testing**:  
  - Run the updated React app locally while using the existing AWS API.  
  - Configure the local React app to make API requests to the AWS API endpoint (`api.yourdomain.com`).  
  - Example in `.env.local`:  
    ```env
    REACT_APP_API_URL=https://api.yourdomain.com
    ```  

- **Deploy to AWS**:  
  - Once the React app changes are tested locally, build the app:  
    ```bash
    npm run build
    ```  
  - Upload the new build files to the S3 bucket and invalidate the CloudFront cache (as described in **6.9**).

---

### **2. Updating the API**  
- **Local Testing**:  
  - Run both the React app and the API locally to test the changes together.  
  - Update the React app’s `.env.local` to point to the local API:  
    ```env
    REACT_APP_API_URL=http://localhost:5000
    ```  
  - Test all interactions between the frontend and backend to ensure compatibility.

- **Deploy to AWS**:  
  - Push the updated API code to the AWS server and restart the backend service.  
  - Ensure the React app on S3 is configured to use the AWS-hosted API.

---

### **3. Updating Both React and API**  
- **Local Testing**:  
  - Run both services locally and test the complete system together.  
  - Example local setup:  
    - React app running on `http://localhost:3000`.  
    - API running on `http://localhost:5000`.  

- **Deploy to AWS**:  
  - Deploy the updated React app to S3 and invalidate the CloudFront cache.  
  - Deploy the updated API to AWS and restart the backend service.  

---

## **Best Practices for Development and Updates**  

1. **Separate Environments**:  
   - Maintain separate environments for development, staging, and production.  
   - Use environment variables to switch between local and AWS endpoints.  

2. **Version Control**:  
   - Use Git to track changes for both frontend and backend code.  
   - Commit frequently and use meaningful commit messages.  

3. **Testing**:  
   - Test locally before deploying.  
   - Consider setting up automated tests for both React and API components.  

4. **Automation**:  
   - Use CI/CD tools (e.g., GitHub Actions) to automate the deployment process for React and the API.  

---



# 8. DB Backup










# YouTube Teacher Recommendations  
- [SuperSimpleDev](https://www.youtube.com/@SuperSimpleDev/videos)  
- [ColorCode](https://www.youtube.com/@ColorCode-io)  
- [Traversy Media](https://www.youtube.com/@TraversyMedia)  








## 2.5 JWT, Express, and MongoDB(Local PC).  

1. Send Login Data: Browser sends username and password to the server.  
2. Create JWT: Server verifies the credentials and generates a JWT using a secret key.  
3. Return JWT: Server sends the generated JWT back to the browser.  
4. Store JWT: Browser stores the JWT (e.g., in localStorage or cookies).  
5. Send Authenticated Request: Browser includes the JWT in the Authorization header for subsequent requests.  
6. Validate JWT: Server validates the JWT to ensure the request is authenticated.  
7. Return Response: Server processes the request and sends the response back to the browser.  



# TBD  
web socket for chat app  
React APP  
Cloudflare






### [User Authentication and Authorization in Express and MongoDB using JWT](https://medium.com/@it.ermias.asmare/user-authentication-and-authorization-in-express-and-mongodb-using-jwt-643503a23452)

### [Node.js + MongoDB: User Authentication & Authorization with JWT](https://www.bezkoder.com/node-js-mongodb-auth-jwt/)
