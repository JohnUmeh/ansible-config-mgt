# ansible-config-mgt

In this project, we will be auntomating a number of activities on several servers uing Ansible configuration management. This implies that we can automate many of our activities and processes on our webservers and tool setups without going to the individual servers using Ansible client as a jump server(Bostian Host).

The new architecture of the setup

![Screenshot from 2023-03-29 17-39-45](https://user-images.githubusercontent.com/77943759/228608623-38dc6d1c-814c-4951-83b2-783979534af9.png)

Task
Install and configure Ansible client to act as a Jump Server/Bastion Host
Create a simple Ansible playbook to automate servers configuration


## **INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE**

Update Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.

![jenkins-ansible](https://user-images.githubusercontent.com/77943759/228610659-db4a5ad7-0c23-42f0-8b45-2248f1d881e5.png)


In GitHub account create a new repository and name it ansible-config-mgt.

Install Ansible

```
sudo apt update

sudo apt install ansible
```
![ansibleinstall](https://user-images.githubusercontent.com/77943759/228625714-354afc3f-bcfb-4c29-a5e3-3915fe66c10f.png)



Check your Ansible version by running 

`ansible --version`

![ansibleversion](https://user-images.githubusercontent.com/77943759/228625837-ea66cb5e-2041-4f3c-bd84-3b089f2c02f4.png)


**Configure Jenkins build job to save your repository content every time you change it** 

1. Create Elastic ip and attach it to Jenkins-Ansible server. This is because we dont want the public Ip changing every time we power the Instance off and on. Learn how to create elastic ip [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html). Learn how to associate your elastic instance to your webserver [here](https://medium.com/progress-on-ios-development/connecting-an-ec2-instance-with-a-godaddy-domain-e74ff190c233).


2.Create a new Freestyle project ansible in Jenkins and point it to your ‘ansible-config-mgt’ repository.

![ansiblejob](https://user-images.githubusercontent.com/77943759/228625943-e5310d57-9ee8-4c3b-8999-c96699d5993b.png)


3. Configure Webhook in GitHub and set webhook to trigger ansible build

![webhook](https://user-images.githubusercontent.com/77943759/228629316-4c30870c-9d3d-4f3c-a9c4-8c75757cdc50.png)


4. Configure a Post-build job to save all (**) files

5. Test your setup by making some change in README.MD file in master branch and make sure that builds starts automatically and Jenkins saves the files (build artifacts) in following folder

`ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/`

