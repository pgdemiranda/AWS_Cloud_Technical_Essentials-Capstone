# AWS Cloud Technical Essentials

The architecture presented is a capstone project for the AWS Cloud Technical Essentials course, where a solution was required for a scenario involving web application requests and database queries.

## Scenario: 
You have a web application that accepts requests from the internet. Clients can send requests to query for data. When a request comes in, the web application queries a MySQL database and returns the data to the client.

## Instructions: 
- Design a three-tier architecture that follows AWS best practices by using services such as Amazon Virtual Private Cloud (Amazon VPC), Amazon Elastic Compute Cloud (Amazon EC2), Amazon Relational Database Service (Amazon RDS) with high availability, and Elastic Load Balancing (ELB). 
- Create an architecture diagram that lays out your design, including the networking layer, compute layer, database layer, and anything else that’s needed to accurately depict the architecture.
- Write a few paragraphs that explain why you chose the AWS services that you used and how they would support the solution for the given scenario. Your explanation must describe how traffic flows through the different AWS components—from the client to the backend database, and back to the client.

## Services used in this project:
- **IAM** - Identity and Access Management;
- **VPC** - Virtual Private Cloud;
- **EC2** - Elastic Compute Cloud;
- **RDS** - Relational Database Service;
- **ELB** - Elastic Load Balancing;
- CloudWatch. 

## Solution:

### 01. **Networking** Layer:
A Virtual Private Cloud (VPC) was created to establish a secure and isolated infrastructure for the web application. The VPC allows for the configuration of subnets and routing tables to manage network settings effectively.

### 02. **Compute** Layer:
To ensure high availability and fault tolerance, two EC2 instances were deployed across different availability zones. These instances host the web application, handle incoming requests, and execute database queries. Elastic Load Balancing (ELB) evenly distributes traffic across instances and performs health checks. Auto Scaling Groups automatically adjust the number of instances based on demand to optimize scalability and cost efficiency.

### 03. **Database** Layer:
Amazon RDS was chosen to host the MySQL database. With Multi-AZ deployment, automatic failover to a standby replica is provided, ensuring high availability. It simplifies maintenance tasks and enhances database resilience.

<center><img src="AWS SOLUTION.png"></center>
<center>Diagram of solution architected with different AWS services</center>


1. First of all, with the assistance of IAM, an IAM Role will allow EC2 to access the database, then the VPC will be set.
2. The client sends a request to the web application via the internet. The request enters the Amazon VPC after passing through the client's network and internet gateway.
3. The Elastic Load Balancer (ELB) receives the request and directs it to an available EC2 instance in the compute layer.
4. Auto Scaling Groups dynamically will adjust the number of EC2 instances based on demand. The ELB distributes requests among the instances, scaling up or down as needed to handle traffic fluctuations.
5. The selected EC2 instance forwards the request to the application running on it. The application processes the request and interacts with the MySQL database.
6. Now, the application sends a query to the MySQL database hosted on Amazon RDS. The database processes the query and retrieves the requested data.
7. Data will be sent back from the MySQL database to the EC2 instance, which forwards it to the web application.
8. Then, the web application returns the requested data as a response, which flows back through the EC2 instance, Elastic Load Balancer, and internet gateway to reach the client.
9. Finally, the assistance of CloudWatch, the performance of our compute resources and the database will be monitored in order to identify areas for optimization. Additionally, logs will also be collected to detect errors and resolve them in real-time.

## Conclusion
For future steps, additional layers can be added. In the case of a cardio disease detection project, we propose adding an Amazon SageMaker layer and an Amazon API Gateway layer. This setup, combined with a supervised machine learning Classification model, would enable us to provide responses to clients. By inputting weight, height, age, blood pressure, and family history of heart disease, the system would return the probability of developing a cardio disease.