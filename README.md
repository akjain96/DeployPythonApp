# DeployPythonApp

This repository is used to successfully deploy python application to VM using docker containers via Jenkins Pipeline.

## Prerequisites :
To run Jenkins CI/CD pipeline we require:
1) Jenkins Setup (either on local PC, or on VM)
2) Ansible Setup 

In this scenario we are deploying Ansible and Jenkins on Local PC  and are connecting it with AWS EC2 Instance.  

## Installations

#### 1) | Installing Jenkins |

To install Jenkins, please follow below link according to OS type. 

Windows : [Installing Jenkins on Windows](https://www.blazemeter.com/blog/how-to-install-jenkins-on-windows) 

Ubuntu 18.04 : 
[Installing Jenkins on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-18-04) 

Ubuntu 20.04 : 
[Installing Jenkins on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-20-04) 

| Setting up Jenkins for first time |

After installation of jenkins, we need to access it via :
localhost (in case of local PC installation)

```bash
http://localhost:8080
```
In case, we have installed jenkins on VM, we need to access it like :

Please make sure that VM security groups allow port 8080 (check instance inbound rule) in order to access jenkins from local PC. 

```bash
https://<instancepublicIPaddress>:8080
```

------------------------------------------------------------------------

#### 2) | Installing Ansible |

To install and configure Ansible, please follow below link according to OS type. 

Windows : [Installing Ansible on Windows](https://phoenixnap.com/kb/install-ansible-on-windows) 

Ubuntu 18.04 : 
[Installing Ansible on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-18-04) 

Ubuntu 20.04 : 
[Installing Ansible on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-20-04) 

----------------------------------------------------------------------

## Using Jenkins File in order to execute Jenkins CI / CD pipeline through JenkinsFile 

For executing Jenkins pipeline through JenkinsFile we need to follow below steps :

##### Step 1 :
```bash
Click on "New item" in Jenkins Dashboard
```
##### Step 2 :
```bash
Enter Pipeline/Item name and choose type as "Pipeline"
```
##### Step 3 :
```bash
Now in the "Pipeline" section click on definition and choose "Pipeline Script from SCM".
```
##### Step 4 :
```bash
Choose SCM type as "GIT".
```
##### Step 5 :
```bash
Add repository URL and credentials accordingly.
```
##### Step 6 :
```bash
Now in "Branches to build" section : type */development
```
##### Final Step :
```bash
After executing all above steps, click on "BuildNow" and execute jenkins pipeline
```
## Usage
Usage of file "dev.ini" :

IMPORTANT POINTS (according to ubuntu setup) : 

1) Please make sure to change IP address in dev.ini (Ansible Inventory) file according to what IP you are getting while creating instance. 

    For Example, I have used IP address, 3.109.53.224 as I got same while creating AWS EC2 instance. 

2) Please make sure to save .pem key under default created user "jenkins". 

#### You can switch user to jenkins by running below command :
```bash
sudo su 'jenkins'
```
Then go to folder : /var/lib/jenkins/ as this is home directory of jenkins and save .pem file here that you have got from Instance.

3) Make sure to add the below line under group "ssh connection"  in ansible.cfg file , Path to file : /etc/ansible/ansible.cfg 

```bash
[ssh connection]
retries = <number>
```
Provide specified number accordingly so that Jenkins pipeline will not fail while running. More number of retries lead to much successful connection. 

## License
[Deqode Solutions](https://deqode.com/)

## Author
Akhil Jain <akjain@deqode.com>
