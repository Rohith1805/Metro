<dependency>
		<groupId>KMIT</groupId>
			<artifactId>MultimoduleChild1</artifactId>
			<version>0.0.1-SNAPSHOT</version>
	</dependency>



pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME'
    }
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('git repo & clean') {
            steps {
                bat "git clone https://github.com/manisai28/se-lab.git"
                bat "mvn clean -f se-lab/pom.xml"
            }
        }

        stage('install') {
            steps {
                bat "mvn install -f se-lab/pom.xml"
            }
        }

        stage('test') {
            steps {
                bat "mvn test -f se-lab/pom.xml"
            }
        }

        stage('package') {
            steps {
                bat 'mvn package -f se-lab/pom.xml'
            }
        }
    }
}


Creation of Maven Java Project
 Step 1. Open Eclipse IDE
 └── 1.1. Launch Eclipse workspace
 Step 2. Install Maven Plugin (if not installed)
 └── 2.1. Go to "Help" in the top menu
 └── 2.1.1. Click "Eclipse Marketplace"
 └── 2.1.2. Search for "Maven Integration for Eclipse"
 └── 2.1.3. Install the plugin if not already installed
 Step 3. Create a New MavenProject
 └── 3.1. File-> New-> Project...
 └── 3.1.1. Expand "Maven"
└── 3.1.2. Select "Maven Project" and click "Next"
 Step 4. Set Project Configuration
 └── 4.1. Select workspace location (default or custom)
 └── 4.2. Click "Next"
 Step 5. Choose Maven Archetype
 └── 5.1. Select an archetype(e.g "org.apache.maven.archetypes-> maven-archetype-quickstart 1.4 ")
 └── 5.2. Click "Next"
 Step 6. Define Project Metadata
 └── 6.1. Group ID: (e.g., com.example)
 └── 6.2. Artifact ID: (e.g., my-maven-project)
 └── 6.3. Version: (default is usually fine)
 └── 6.4. Click "Finish"
 In Console, artifacts are grouped. When prompted with Y/N, type 'Y'.
 Step 7. Maven Project Created
 └── 7.1. Project structure is generated with a standard Maven layout
 └── 7.2. Includes:
 └── src/main/java (for Java source code)
 └── src/test/java (for test code)
 └── pom.xml (Maven configuration file)
 Step 8. Update Project Settings (if needed)
 └── 8.1. Right-click on the project-> Maven-> Update Project...
 └── 8.2. Ensure dependencies are up to date
 Step 9. Build and Run Maven Project
 └── 9.1. Right-click on App.java-> Run As-> Maven Clean
 └── 9.1.1. Right-click on App.java-> Run As-> Maven Install
└── 9.1.2. Right-click on App.java-> Run As-> Maven Test
 └── 9.1.3. Right-click on App.java-> Run As-> Maven Build
 Step 10. In the Maven Build dialog:
 └── Enter Goals: clean install test
 └── Click on Apply-> Click on Run
 Step 11. Check console for BUILD SUCCESS message.
 Step 12. Run the application:
 └── Right-click on App.java-> Run As-> Java Application
 └── Output: "Hello World" displayed.



 
 Creation of Maven web Java Project
 Step 1: Open Eclipse
 └── 1.1 Launch Eclipse IDE.
 └── 1.2 Select or create a workspace.
 Step 2: Create a New MavenProject
 └── 2.1. File-> New-> Project...
 └── 2.1.1. Expand "Maven"
 └── 2.1.2. Select "Maven Project" and click "Next"
 Step 3: Choose MavenArchetype
 └── 3.1. Select an archetype(e.g "'org.apache.maven.archetypes'-> 'maven-archetype-webapp' 1.4 ")
 └── 3.2. Click "Next"
 Step 4: Configure the Maven Project
 └── 4.1 Group Id: Enter a group ID (e.g., com.example).
 └── 4.2 Artifact Id: Enter an artifact ID (e.g., my-web-app).
 └── 4.3 Click **Finish** to create the project.
 Step 5: Add MavenDependencies
└── 5.1 Openthe **pom.xml** file in the Maven project.
 └── 5.2 Add the necessary dependencies for your web project (e.g., Servlet, JSP):
 Gotobrowser-> Open mvnrepository.com
 Search for 'Java Servlet API'-> Select the latest version
  Copy the dependency code-> Paste it in MavenWeb’s pom.xml under the target folder
 └── Example:
 ```xml
 <dependency>
 <groupId>javax.servlet</groupId>
 <artifactId>javax.servlet-api</artifactId>
 <version>4.0.1</version>
 <scope>provided</scope>
 </dependency>
 ```
 Step 6:-. Configure server:
 └── Window->ShowView->Servers
 └── Add server-> Select Tomcat v9.0 server-> Click Next
 └── Configure server options (e.g., ports, server location).
 Step 7:-. Modify 'tomcat-users.xml':
 └── Add role and user details under <tomcat-users> tag.
 Step 8:. Build the project:
 └── Right-click on index.jsp-> Run As-> Maven Clean
 └── Right-click on index.jsp-> Run As-> Maven Install
 └── Right-click on index.jsp-> Run As-> Maven Test
 └── Right-click on index.jsp-> Run As-> Maven Build
Step 9. In the Maven Build dialog:
 └── Enter Goals: clean install test
 └── Click on Apply-> Click on Run
 Step 10. Check console for BUILD SUCCESS message.
 Step 11. Run the application:
 └── Right-click on index.jsp-> Run As-> Run on Server
 └── Select the Tomcat server-> Click on Finish
 Step 12. Output: "Hello World" webpage displayed.
 Note:-Now push yours Maven java project and Maven Web Project into your github
 ⭐ PART 8 — Multi-Module Maven Project (Parent + Child Projects)

Pages 125–134 show the complete steps. ✔

se_lab_manual

🔶 Step-by-Step Multi-module Project Creation
📌 Step 1 — Create Parent Project

File → New → Other → Maven → Maven Project
Select:

✔ Create Simple Project (skip archetype)

Enter:

GroupId: KMIT
ArtifactId: MultiModule
Packaging: pom


Click Finish

(Shown in page 126–127) ✔

se_lab_manual

📌 Step 2 — Create Child 1 (JAR module)

Right-click Parent → New → Maven Module
✔ Check "Create Simple Project"
ArtifactId = MultiModuleChild1
Finish

📌 Step 3 — Create Child 2 (Web module)

Right-click Parent → New → Maven Module
ArtifactId = MultiModuleChild2
Search → choose:

👉 maven-archetype-webapp

Finish
Type Y when console asks (page 130) ✔

se_lab_manual

📌 Step 4 — Add module dependency (Child2 depends on Child1)

In child2’s pom.xml add:

<dependency>
    <groupId>KMIT</groupId>
    <artifactId>MultimoduleChild1</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>


(Page 132) 

se_lab_manual

📌 Step 5 — Build in correct order

Build sequence:

1️⃣ Right-click Parent → Run As → Maven Install
2️⃣ Right-click Child1 → Run As → Maven Install
3️⃣ Right-click Child2 → Run As → Maven Install

If you build Child2 before Parent, you will get a BUILD FAILURE (page 133)
✅ WEEK 8 — Jenkins Freestyle Jobs (VERY BEGINNER VERSION)
Goal: Learn how to run Java & Web projects automatically using Jenkins.
________________________________________
⭐ PART 1 — Install & Open Jenkins
1.	Open your browser.
2.	Type:http://localhost:8080
You will see the Jenkins dashboard.
________________________________________
⭐ PART 2 — Create Maven Java Build Job (MavenJava_Build)
1️⃣ Click “New Item”
•	Left side → first option.
2️⃣ Give a name
Example:
MavenJava_Build
Select:
Freestyle Project
Click OK.
________________________________________
3️⃣ Fill Project Details
Inside Configuration page:
Description:
Java Build demo
________________________________________
4️⃣ Add GitHub Code
Scroll to:
✔Source Code Management → Choose Git
You will see a box:
Repository URL
Paste your Maven Java GitHub link here (example):
https://github.com/someone/maven-java-demo.git
________________________________________
5️⃣ Build Steps (Very Important)
Scroll to Build section → click:
▶Add Build Step → Invoke top-level Maven targets
You will now add 2 steps:
STEP A
•	Maven version: select your configured Maven (example: MAVEN_HOME)
•	Goals:clean
STEP B (again click “Add Build Step”)
•	Goals:install
________________________________________
6️⃣ Post-Build Actions
Scroll down → Click:
▶Add post-build action → Archive the artifacts
Files to archive:**/*
Then again:
▶Add post-build action → Build other projects
Enter:MavenJava_Test
Choose:
•	Trigger only if build is stable
7️⃣ Save the job
Click Save at bottom.
________________________________________
⭐ PART 3 — Create MavenJava_Test Job
1️⃣ Click “New Item”
Name:MavenJava_Test
Select Freestyle → OK.
________________________________________
2️⃣ Description
Test demo
________________________________________
3️⃣ Build Environment
Scroll → tick:
✔ Delete workspace before build starts
Why?
It removes old files so test always runs fresh.
________________________________________
4️⃣ Copy the build output from previous job
Build Steps → Add Build Step → Copy artifacts from another project.
Fill:
•	Project name → MavenJava_Build
•	Build → Stable build only
•	Artifacts to copy:**/*
________________________________________
5️⃣ Add Test Step
Add Build Step → Invoke top-level Maven targets
•	Goals:test
________________________________________
6️⃣ Archive test results
Add Post Build Action → Archive artifacts
Files:**/*
Click Save
________________________________________
⭐ PART 4 — Create Pipeline View
Steps:
1.	On Jenkins dashboard, click “+” beside “All”
2.	Name:MavenJava_Pipeline
3.	Select: Build Pipeline View
4.	Pipeline flow:
o	Initial job → MavenJava_Build
5.	Save.
________________________________________
⭐ PART 5 — Run
1.	Open pipeline view
2.	Click “Run”
3.	Green = success
4.	Click boxes → open console
________________________________________
✨Maven Java part DONE!
________________________________________
⭐ PART 6 — Repeat SAME for Maven Web Project
You will create 3 jobs:
1.	MavenWeb_Build
2.	MavenWeb_Test
3.	MavenWeb_Deploy
And pipeline.
The steps are exactly same as Java — except the deploy job:
In MavenWeb_Deploy:
•	Copy artifacts from test job
•	Add Post-build Action → Deploy WAR/EAR to container
•	WAR file:**/*.war
•	Add Tomcat 9 remote server
o	username: admin
o	password: 1234
o	URL: http://localhost:8085/
Done.
________________________________________
✅ WEEK 9 — Scripted Pipeline (BEGINNER VERSION)
Goal: Create ONE Jenkins job using Pipeline script.
________________________________________
1️⃣ Click “New Item”
Name:ScriptedPipeline
Choose:Pipeline
Click OK.
________________________________________
2️⃣ Scroll down to Pipeline section
Under Definition, select:
Pipeline script
________________________________________
3️⃣ Paste the script

pipeline {
agent any
   tools{
        maven 'MAVEN-HOME'
    }
    stages {
        stage('git repo & clean') {
            steps {
                bat "git clone <provide your github link>"
                bat "mvn clean -f mavenjava"
            }
        }
        stage('install') {
            steps {
                bat "mvn install -f mavenjava"
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f mavenjava"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f mavenjava"
            }
        }
    }
}

Change:
git clone <paste your GitHub URL>
And change “mavenjava” to your folder name if needed.
________________________________________
4️⃣ Save
________________________________________
5️⃣ Run
Click Build now.
Take screenshots of:
•	Build stages
•	Console output
Done.
________________________________________
✅ WEEK 10 — Minikube, Kubernetes, Nagios, AWS (BEGINNER VERSION)
________________________________________
⭐ PART 1 — Minikube
1️⃣ Start Minikube
Open CMD or PowerShell:
minikube start
2️⃣ Create an nginx server
kubectl create deployment mynginx --image=nginx
Check:
kubectl get pods
3️⃣ Expose the deployment
kubectl expose deployment mynginx --type=NodePort --port=80 --target-port=80
4️⃣ Scale to 4 pods
kubectl scale deployment mynginx --replicas=4
->Port forwarding: kubectl port-forward svc/mynginx 8081:80
8081 can be replaced by any
->Kubernets dashboard 
Minikube dashboard
->Stopping
kubectl delete deployment mynginx
kubectl delete service mynginx
minikube stop
________________________________________
⭐ PART 2 — Nagios in Docker
1️⃣ Pull image
docker pull jasonrivers/nagios:latest
2️⃣ Run Nagios
docker run --name nagiosdemo -p 8888:80 jasonrivers/nagios:latest
3️⃣ Open browser
Go to:
http://localhost:8888
Login:
•	username: nagiosadmin
•	password: nagios
stopping: docker stop nagiosdemo
________________________________________
✅ WEEK 11 — GitHub Webhook + Jenkins Email (SUPER SIMPLE)
________________________________________
⭐ PART 1 — Install ngrok
Run in CMD:
ngrok http 8080
You will see:
https://abc123.ngrok.io (just for example)
Copy this.
________________________________________
⭐ PART 2 — Add Webhook in GitHub
1.	Open your GitHub repo → Settings → Webhooks
2.	Click Add Webhook
3.	Payload URL:
https://abc123.ngrok.io/github-webhook/ (make sure to add /github-webhook/ at the end of your ngrokurl)
4.	Content type:application/json
5.	Events:✔ Just the push event
6.	Add webhook
________________________________________
⭐ PART 3 — Configure Jenkins job
Open your job → Configure → Build Triggers
✔ Tick:GitHub hook trigger for GITScm polling
Save.
________________________________________
⭐ PART 4 — Test webhook
1.	Make any change to your GitHub project
2.	Push the code
3.	Jenkins WILL automatically start building
DONE.
________________________________________
⭐ PART 5 — Email Notification Setup (Beginner version)
Step 1 — Setup Gmail App Password
1.	Open Google Account → Security
2.	Turn on 2-step verification
3.	Create App Password → choose “Other”
4.	Copy the 16-character password
________________________________________
Step 2 — Jenkins Email settings
In Jenkins:
•	Manage Jenkins → Configure System
•	Scroll to “E-mail Notification”
•	Fill:
SMTP Server → smtp.gmail.com
Use SMTP Auth → ✔
Username → your Gmail
Password → (your app password) (16-character password that you got)
Use SSL →✔
Port → 465
Click Send test email
If received → success.
________________________________________
⭐ PART 6 — Add email to Job
Open your job → Configure → Post-build actions:
Add:
Editable Email Notification
Add recipients → Save → Build.
DONE.
________________________________________
✅ WEEK 12 — Deploying App in AWS EC2 Using Docker
________________________________________
⭐ PART 1 — Create EC2 instance
1.	AWS → Start Lab and click on the green-dot →EC2 → Launch Instance
2.	Name: ubuntu
3.	AMI: Ubuntu Server 22.04 LTS (Free tier)
4.	Instance type: t2.micro
5.	Create new key pair → download .pem file
6.	Security group:
✔ SSH (22)
✔ HTTP (80)
7.	Launch instance.
________________________________________
⭐ PART 2 — Connect to EC2
Go to instance → Click Connect → SSH tab
Copy:
ssh -i "your-key.pem" ubuntu@<your-public-ip>
Paste into PowerShell.
You are now inside your remote Ubuntu machine.
________________________________________
⭐ PART 3 — Install 
Run:
sudo aptupdate
sudo apt-get install docker.io
sudo apt install git
sudo apt install nano
________________________________________
Create a html file and push into git or what ever is given 
⭐ PART 4 — Clone your project
git clone <your GitHub link>
cd <project folder>
________________________________________
⭐ PART 5 — Create Dockerfile
Run:
nano Dockerfile
Paste:
FROM nginx:alpine
COPY . /usr/share/nginx/html
(For maven WEB project)-> docker file code 
FROM tomcat:9-jdk11
COPY target/*.war/usr/local/tomcat/webapps
Save:
•	CTRL + O → Enter
•	CTRL + X
________________________________________
⭐ PART 6 — Build Docker image
sudo docker build -t mywebapp .
________________________________________
⭐ PART 7 — Run the container
sudo docker run -d -p 80:80 mywebapp
________________________________________
⭐ PART 8 — Open your website
Copy your EC2 public IP
Paste in browser → Your website appears 🎉
->Stopping 
sudo docker ps -> gives container id 
sudo docker stop <container id>

