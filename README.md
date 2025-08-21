# 🎓 Student Application Deployment using Jenkins, Maven & Tomcat on AWS EC2

This project demonstrates how to deploy a **Java Student Web Application** packaged as a WAR file using **Maven**, **Jenkins CI/CD Pipeline**, and hosted on **Tomcat** running on an AWS EC2 instance.  

It covers the full flow: **Source Code → Build → Deployment → Running on Cloud**.  

---

## 📌 Project Overview

The objective of this project is to automate deployment of a Java-based Student Management application.  
Here’s the flow:

- The application source code is pushed to **GitHub**.
- Jenkins is configured to:
  1. **Checkout** the code from GitHub.
  2. **Build & package** the project into a `.war` file using Maven.
  3. **Deploy** the `.war` file to an EC2 server where Tomcat is running.
- Finally, the deployed app is accessible through a browser at:  
  👉 `http://<EC2-PUBLIC-IP>:8080/`

This ensures every new commit or change can be deployed quickly with automation.

---

## 🛠️ Tech Stack

- **Java 17** → Programming language used to build the application.  
- **Maven** → Dependency management and build tool to create the WAR file.  
- **Tomcat 10** → Application server used to host Java web applications.  
- **Jenkins** → Automation server that runs the CI/CD pipeline.  
- **AWS EC2** → Virtual server in the cloud to host the deployed app.  

---

## 📂 POM.xml

The `pom.xml` defines:
- Project details (`groupId`, `artifactId`, `version`).  
- **Compiler plugin** to ensure Java 17 compatibility.  
- **WAR plugin** so Maven packages the app into a `.war` file.  
- Dependency on **Servlet API**, required for web applications.  

This ensures that when we run `mvn package`, a deployable `studentapp.war` is generated.

---

## 📂 Jenkins Pipeline (Jenkinsfile)

This **Jenkinsfile** defines an automated pipeline with three key stages:

1. **Checkout** → Pulls the latest source code from GitHub.  
2. **Build WAR** → Runs `mvn clean package` to compile and generate the WAR file inside `target/`.  
3. **Deploy to Tomcat** →  
   - Copies the WAR file to the EC2 instance using **scp**.  
   - Replaces the old deployment with the new one.  
   - Renames it as `ROOT.war` so the app runs at the Tomcat root context (`/`).  
   - Restarts the Tomcat service.  

At the end, Jenkins prints a success message with the application URL.

---

## ⚡ How the Pipeline Works (Step by Step)

1. **Code Checkout** → Jenkins fetches the source code from GitHub (main branch).  
2. **Build & Package** → Maven compiles the Java code, runs tests (if any), and generates a `WAR` file.  
3. **File Transfer** → Jenkins copies the WAR file to the AWS EC2 server securely via SSH.  
4. **Deployment** → The existing `ROOT.war` is removed and replaced with the new WAR.  
5. **Restart Tomcat** → Tomcat service is restarted to load the new application.  
6. **Access App** → The application becomes live on:  
   `http://<EC2-PUBLIC-IP>:8080/`

This makes the process **repeatable, automated, and reliable**.

---

## 📸 Screenshots

Below are screenshots that explain the setup and deployment:

### 1. Jenkins Setup
Shows the Jenkins job configuration for the pipeline.  
![Jenkins Setup](images/jenkins%20setup.png)

### 2. Tomcat
Tomcat server running on AWS EC2, ready to host the application.  
![Tomcat](images/tomcat.png)

### 3. AWS EC2 Security Groups
Security groups configured to allow HTTP (8080) and SSH access.  
![Security Groups](images/security%20groups.png)

### 4. AWS EC2 Servers
The EC2 instances used for Jenkins and Tomcat deployment.  
![Servers](images/servers.png)

### 5. Student Application Output
Final application running successfully in the browser.  
![Output](images/output.png)

---

## 🌐 Accessing the Application

Once deployed, the app can be accessed from a browser:  

```

[http://3.80.109.99:8080/](http://3.80.109.99:8080/)

```
