
# DevOps-project-implementing-DevOps-lifecycle

Implementing DevOps lifecycle on Website using Ansible,Docker,Jenkins

#### Project Description

- **Project Name**: DevOps Lifecycle Implementation for XYZ Software

#### Objective:
- To implement a complete DevOps lifecycle for XYZ Software, ensuring automated build, test, and deployment processes for their product available on GitHub. The goal is to streamline and enhance the efficiency of the software development and deployment pipeline.

# Key Features:

**1.Automated Software Installation:**

- Using Ansible to install Jenkins, Docker, and other necessary software on target machines.

**2.Git Workflow Implementation:**

- Establishing a Git branching strategy with ` master ` and ` develop ` branches.

**3.Continuous Integration and Continuous Deployment (CI/CD):**

- Setting up Jenkins to automate builds, tests, and deployments based on branch commits.

**4.Containerization:**

- Using Docker to containerize the application, ensuring consistency across environments.

**5.Jenkins Pipeline:** 

- Defining Jenkins jobs for building, testing, and deploying the application using a Docker container.

#### Benefits:

- **Efficiency:**  Automating the build, test, and deployment processes reduces manual intervention and speeds up the development lifecycle.
- **Consistency**: Containerization ensures that the application runs consistently across different environments.
- **Reliability**: Automated testing and deployment reduce the risk of human error and increase the reliability of releases.
- **Scalability**: The infrastructure and processes are scalable, allowing the company to grow without significant changes to the pipeline.

#### Step1: Launch instances & install necessary softwares

- Launch ec2 instances i.e master,slave1,slave2 and install necessary softwares like ansible with the commands are in the file ansible-installation.sh

- Check the ansible version using command ` ansible --version `
-  Create the keys to “Master” instance & Paste to “Slave1” & “Slave2”
-  Run this command: ` ssh-keygen ` to create the “public” & “private” key.
-  Run this command to land inside the .ssh directory: ` cd .ssh/ `
-  Run this command: ` cat id_rsa.pub ` to copy the content.
-  Go to “Slave1” & run this command ` cd .ssh/ ` to land inside the .ssh directory.
-  Run this command to open the “authorized_keys” file: ` vi authorized_keys `
-  Paste the public key content in the ` authorized_keys ` file. Press “ESC” & type :wq! To quit & save the file.
-  Do same for slave2
-  Put the “Slave IPs” into the “Ansible Host File”.Go to “Master Machine” & type this command:
```
sudo nano /etc/ansible/hosts
```

- Paste these commands in the host file:
```
slave1 ansible_host=168.31.29.124
slave2 ansible_host=168.31.29.96

```
-  Run this ansible command to ping the machines:

```
ansible -m ping all.

```

#### Create an Ansible playbook to install Jenkins, Docker, and other dependencies:

-  Run this command to create an ansible-playbook.yaml file to execute the “master.sh” & “slave.sh” through “Ansible”  with the command

```
sudo nano ansible-playbook.yaml

```

-  Create a “master.sh” file & paste the below commands here to install the tools such as “Jenkins”, “Docker”, & “Java”. Use this command:
```
sudo nano master.sh
```
- same for the slave.sh with command
```
sudo nano slave.sh
```

- The script for the "master.sh, slave.sh" are available in this files
-  Type this command to execute the “master.sh” & “slave.sh” using ` Ansible-installation.sh ` file.
-   Go to “Master”, and type these commands to check whether Jenkins, Docker & Java has been successfully installed or not.
```
docker --version
jenkins --version
java --version
```

#### Step3. Set up Jenkins (CI/CD)

- Put the URL: http://(ip):8080/. Press “enter” from the keyboard. Jenkins Dashboard will be opened.
- Paste the command ` sudo cat /var/lib/jenkins/secrets/initialAdminPassword ` to “Jenkins Master”. Press “enter” from the keyboard & a token will be provided.
- Paste the token in “Dashboard” & click on “Continue”.
- Install suggested plugins
- Create the necesarry credentials in jenkins dashboard like username,password,email....
- Jenkins dashboard will be ready
- Add “Slave1” in “Jenkins”, Go to “Jenkins Master” & click on “New Node” and create node.
- Give requried configurations like remote root directories and launch methods (via ssh) add credentialS,Provide host IP of slave1 then  “Slave1 Node” has been successfully launched
- Same process for slave 2

#### Step4.:  Implement Git Workflow

- Create and configure Git branches:
- ` master ` branch: Stable production code.
- ` develop ` branch: Active development, features, and integration.
- clone the git repository to get ` index.html ` file and image that are in [pradeep251285](https://github.com/pradeep251285/DevOps-Lifecycle-Implementation.git)
- After implementing git workflow push the commits with the command
```
git push — all
```
- Create a Webhook for Trigger the Jobs

#### Step.4:  The code should be containerized with the help of a Dockerfile.

- Create a Dockerfile & Push it into the “Master” Branch
- Run the command to create Dockerfile
```
sudo nano Dockerfile
```
- Dockerfile configurations are in this file "Dockerfile"
- After run the dockerfile

#### jenkins pipeline setup

-  The above tasks should be defined in a Jenkins Pipeline with the following jobs:
-  Job2: Test
-  Job3: Prod
-  Create a “Test” Job by clicking new Item and select freestyle project
-  Go to the “GitHub” account & click on Code. Go to the “HTTPS” section & copy the link.
-  In “Source Code Management”, choose “Git”. Put “Repo URL” in the “Repository URL” section.
-  Choose “Branch” as “develop” in “Branch Specifier”.
-  Choose “GitHub hook trigger for GITScm polling” in “Build Triggers”.
-  Click on “Apply”. After clicking on “Apply”, choose “Save”. our test job is succesfully created
-  Same for Create a “Prod” Job and modify some configs Remain other settings as it is. Choose “Branch Specifier (blank for ‘any’) as “*/master”.then our prod is success
-  Click on “Configure” in “Prod”,Click on “Build Steps”,Add build step,Click on “Execute Shell”.Put these commands to build a container on port 80:
```
sudo  docker build . -t finalrelease
sudo docker run -itd -p 80:80 finalrelease
```
- Then go to github ad choose index.html file we can modify the code as per our needs
- Go to prod job and click build now it will be succesfully build
- We can see our console output
- Go to “Slave2” & Paste the “Public IP Address” in the “Browser Address Bar”
- We can get output of the project as the image given below

  

- We can create new files in git and commit the files it will automatically triggerd through the git webhook and build will be happen


![github3](https://github.com/user-attachments/assets/ce085332-0aa6-44ad-8bfd-62a148ae2dab)
