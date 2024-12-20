
# Materials-Lecture-and-Loadmap

### Experience Before Full Stack  
- Conda  
- Docker  
- Python for deep learning and data analysis  
- Torch (modeling and training with DDP)  
- Blogs with Minimal Mistakes and Hugo  
- Flask app hosting on GCP  
- Basic familiarity with Linux  
- Git and Github  



### How I Study  
1. I follow lectures step-by-step.  
2. I ensure I understand concepts so I can replicate them without needing the lecture again.  
3. With internet access or LLMs, I can independently research and implement the functions I want to create.  
4. Currently, I can write over 80% of my code independently in an offline setting (without external help).  
5. A project is the best way to review what you have studied. Below are some projects for reference or as checkpoints.  




### Recommendations  
- Don’t rely too much on lectures.  
- Use GPT effectively as a tool.  
- Don’t try to memorize all the code—no one does. Search for new functions as needed.  
- For styling, find good references or explore beautiful CSS resources.  
- Note everything (like this page) to review later instead of memorizing.  
- Keep notes focused on concepts, not detailed descriptions, for quick reference. For example, write "properties can send data between components."  
- Work on as many projects as possible to strengthen your skills.  



# 0. Concepts  
- **Frontend** (client): Runs on your local machine.  
- **Backend**: Runs on a remote server.(Bridge between local PC and DB)  
- Interaction between the two forms the foundation of any app.  



# 1. Frontend  

## 1.1 HTML, CSS  
### [HTML & CSS Full Course - Beginner to Pro](https://youtu.be/G3e-cpL7ofc?si=6khpQeP_MXAW5nkh)  
This lecture covers the basics of HTML and CSS. With it, you can build static websites.  

After this, I recommend watching videos on **Flexbox** and **Grid** for better layout management.  


<h2 style="color:red;"> Project 1. </h2>
<p style="color: red;">Create your own static web page as demonstrated in the lecture.</p>  



## 1.2 JavaScript  
### [JavaScript Tutorial Full Course - Beginner to Pro (2024)](https://www.youtube.com/watch?v=EerdGm-ehJQ)  
This lecture teaches how to make websites more interactive using the DOM.  
It also introduces generating HTML with JavaScript, a fundamental concept in React.js.  

### [ColorCode - 20 Things JavaScript Developers Should Know](https://www.youtube.com/playlist?list=PL1PqvM2UQiMoGNTaxFMSK2cih633lpFKP)  
Covers advanced JavaScript topics, especially async functions and API calls (Lectures 11–14).  

### [Build a JavaScript WEATHER APP in 30+ minutes!](https://www.youtube.com/watch?v=VaDUGPMjzOM)  
A hands-on lecture on building an app using public API calls.  


<h2 style="color:red;"> Project 2. </h2>
<p style="color: red;">Create your own static web page as demonstrated in the lecture. Generate your HTML code dynamically using JavaScript. And use DOM.</p>



## 1.3 React.js  

### [2022 코딩애플 리액트 강의](https://www.youtube.com/watch?v=00yJy7W0DQE&list=PLfLgtT94nNq0qTRunX9OEmUzQv4lI4pnP)  
Great for understanding the basics of React, including state and components.  

### [React Full Course for Free ⚛️ (2024)](https://www.youtube.com/watch?v=CgkZ7MvWUAA)  
While not fully comprehensive, this course explains how to transition HTML, CSS, and JS skills into React.  

Topics covered:  
- **Component**: Functions that create reusable blocks of HTML.  
- **Properties**: Pass data (e.g., objects) into components.  
- **style.module.css**: Use `{styles.className}` in JSX for styling components.  
- **useState**: Updates state and triggers re-rendering of only affected components and children. If references don't change (e.g., for lists or objects), rendering won't happen unless you create a new copy.  
- **onClick/onChange**: Simplifies event handling directly in JSX. For DOM manipulation, use `useEffect` to prevent Virtual DOM conflicts.  
- **useRef**: Similar to `useState`, but doesn’t trigger re-rendering when updated.  
- **useEffect**: Runs after the component renders, ideal for DOM manipulation or setting up event listeners.  
- **createContext**: Helps pass data between distant components. Use `.Provider` to pass values and `useContext` in children to consume them.  

### [Learn React Router v6 In 45 Minutes](https://www.youtube.com/watch?v=Ul3y1LXxzdU&list=PLE00K2dj1di6OW5VFsz0rXZeDVhLp8_6L&index=4)  
A concise lecture on using routers in React for creating multiple pages.  

Key topics:  
- **BrowserRouter**: Wraps the `App` component in `index.jsx`.  
- **Routes**: Define multiple components inside `Routes` in `App.js`. Content outside `Routes` (e.g., navigation) persists across route changes.  
- **Route**: Maps `path` (URL) to `element` (component). Example: `<Route path="/login" element={<Login />} />`.  
- **Wildcard Route**: Handles nested routes or undefined paths. Example: `<Route path="*" element={<NotFound />} />` to catch invalid URLs.  


<h2 style="color:red;"> Project 3. </h2>
<p style="color: red;">Create your own web with React. And use Routes for multiple pages.</p>



### [React 입문자들이 알아야할 Redux 쉽게설명 (8분컷)](https://www.youtube.com/watch?v=QZcYz2NrDIs)  
Explains why Redux is needed and its core concepts.  

### [React Redux](https://www.youtube.com/playlist?list=PLuHgQVnccGMDuVdsGtH1_452MtRxALb_7)  
Walks through props → Redux → React Redux, highlighting the benefits of React Redux for managing complex state and reducing unnecessary props.  

### [react-redux(2022 ver)](https://youtu.be/yjuwpf7VH74?si=RWQdZGgZM-xIsFdq)  

### [Redux toolkit](https://www.youtube.com/watch?v=9wrHxqI6zuM)  


<h2 style="color:red;"> Project 4. </h2>
<p style="color: red;">Create your own web with React. And use react-redux for global state.</p>






# 2. Backend  

## 2.0 Getting Started  
### [2시간만에 웹서버 쉽게 개발하기 (코딩애플)](https://www.youtube.com/watch?v=-zOfTS1HQTc&list=PLfLgtT94nNq1qmsvIii_CAxFlD7tvB5NE)  
A quick overview of building web servers using **Node.js**.  

Key topics:  
- HTTP requests: GET, POST, PUT, DELETE  
- Basics of **Node.js** as a JavaScript runtime environment (not a programming language).  
- **Nodemon**: Automatically restarts the server when changes are made.  



## 2.1 Node.js  
JavaScript was originally designed for browser use only. However, with the introduction of Chrome's V8 engine, Node.js emerged, enabling JavaScript to run locally. This allowed developers to use JavaScript for server-side development as well.


### [조코딩 Node.js](https://www.youtube.com/watch?v=ZeD8yNMYe-o&list=PLU9-uwewPMe2-R9-taf4oIjwrEZDgE-q2)  
Key topics from the playlist:  

- **Why Node.js?**: It allows JavaScript to run on local machines, not just browsers.  
- **npm init**: Initializes a project for managing dependencies.  
- **npm**: Unlike `pip` or `conda`, it installs packages directory-based, meaning per-project installations.  
- Modules vs. Libraries: For example, **figlet** is a module, while **React** is a library.  
- **Deploying APIs**: Learn to deploy using platforms like Cloudtype.  



## 2.2 Express.js  
### [Express Crash Course](https://www.youtube.com/watch?v=CnH3kAXSrmU&t=53s)  

Although you can build servers using just **Node.js**, starting directly with Express.js shouldn’t cause major issues.(I think)  

I’ve decided to focus on this **Express-only** lecture for now.  

It’s true that learning with vanilla Node.js first could provide a deeper understanding, but I trust my current approach. It’s similar to how I use **torch** without first creating modules from scratch with NumPy—it’s fine as long as I understand the fundamentals.  

If needed later, I can refer to this YouTuber’s Node.js lecture: [Vanilla Node.js Server Tutorial](https://www.youtube.com/watch?v=32M1al-Y6Ag).  



<h2 style="color:red;"> Project 5. - CRUD Proejct (w/o DB)</h2>  

<p style="color: red;">Create your own application using React and Express. Please refer to my repository below.</p>
<p style="color: red;">In the repository, I have utilized everything we learned so far, allowing you to review and consolidate all the concepts covered above.</p>


### [github repo](https://github.com/hyeok-jong/crud-project)  



## 2.3 MongoDB  
### [MongoDB Crash Course](https://youtu.be/ofme2o29ngU?si=sKzwqO4ShNm6yuj7)  
Nice explain of MongoDB with multiple examples.  

## 2.4 Mongoose  
### [Mongoose Crash Course - Beginner Through Advanced](https://www.youtube.com/watch?v=DZBGEVgL2eE)



<h2 style="color:red;"> Project 5. - CRUD Proejct (mini todo app)</h2>  

<p style="color: red;">Create your own application using React, Express, and MongoDB. Please refer to my repository below.</p>
<p style="color: red;">In this resposityofy 해당 앱은, DB를 사용하여 ㄹ.</p>

### [github repo](https://github.com/hyeok-jong/crud-project)  







## 2.5 Next Step

- Here, you have learned everything needed to prepare for building an application.  
- This includes creating a web page with React, a server with Express, and a database with MongoDB.  
- However, currently, all these components are running on your local PC.  
- For a real-world application, each of these should ideally run on the cloud. (Of course, it's also possible to run and deploy them from your local PC.)  
- To build a true application, you need to learn about MongoDB Atlas, Docker, and AWS services such as S3 and ECS.  



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









# 6 AWS S3 - Make Your built React on Cloud  

## 6.0 Buy your own domain  

## 6.1 AWS S3  

## 6.2 AWS CloudFront  

## 6.3 Certificate Manage  

## 6.4 Route 53  





# 7. DB Backup


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






### [User Authentication and Authorization in Express and MongoDB using JWT](https://medium.com/@it.ermias.asmare/user-authentication-and-authorization-in-express-and-mongodb-using-jwt-643503a23452)

### [Node.js + MongoDB: User Authentication & Authorization with JWT](https://www.bezkoder.com/node-js-mongodb-auth-jwt/)
