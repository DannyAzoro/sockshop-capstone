# Sock shop (Seployment of a Microservice-based Application)
The sock shop application shown is the part where users see. This is an online shop that sells socks. The intention of this deployment is to aid the display and testing of microservices and cloud technologies. 

# Objective
The goal is to use a more novel approach to deploy the sock shop to ensure automation and efficiency. This novel approach involves using Infrastructure as a code (Iaac) to ensure a secure deployment on kubernetes to produce a quick, reproducible, efficient deployment process.
# Resources
The sock shop Microservices Demo is gotten from a GitHub repository at https://github.com/microservices-demo/microservices-
# Requirements and Tools used for the Project
This project is configured in a Linux environment. A shell script - installer.sh contains the necessary commands to install and initialize all dependencies required for a successful execution of the project. This script includes terraform, unzip, kubectl, aws cli, helm and Jenkins. 
The unzip command extracts an archived file in Linux. Terraform run our Terraform configurations. Kubectl run Kubernetes commands. The aws cli sets up the AWS environment. Helm manages Kubernetes applications and Jenkins - the Continuous Integration Continuous Deployment (CI/CD) tool used in this project, is the open source automation server used to reliably build, test and deploy the software.

# The Repository
sockshop-capstone is the name of the repository, and it is available in the master branch of the GitHub repository https://github.com/DannyAzoro/sockshop-capstone. It contains three major folders namely eks, kubernetes, and capstone-images, and four files namely installer.sh, cluster-Jenkinsfile, Jenkinsfile, and README.md.

# The Folders
### The eks Folder

The eks folder contains Terraform configuration files for the creation of an Elastic Kubernetes cluster in AWS (Amazon Web Services). An EKS (Elastic Kubernetes Service) cluster, a VPC (virtual private cloud), a node group for the cluster and an IAM (Identity and Access Management) roles for the cluster and the node groups were all created.

### The Kubernetes Folder
This folder houses four sub-folders namely micro-service, prometheus-helm, ingress-rule, and nginx-controller. There are various sections of the sock shop application, and with the micro-service folder which contains Terraform configuration files, each of the various sections, alonside the associated services and databases were deployed. The prometheus-helm folder contains Terraform configuration files for the creation of helm_release resource. The major function of Helm is to manage Kubernetes applications. The helm chart helps us define, install, and upgrade even very complex Kubernetes applications. A chart is a helm package which contains all the resource definitions necessary to run an application inside a Kubernetes cluster. A release is an instance of a chart running inside a Kubernetes cluster. The nginx-controller folder contains Terraform configuration files that defines the parameters for Ingress-nginx and also Route53 hosted zone. The Ingress-nginx is an Ingress controller for Kubernetes which uses Nginx webserver as avreverse proxy and a load balancer. A domain name, "azorod.com.ng" was obtained from qservers domain. This was hosted using Amazon Route 53, with the configurations provided. The ingress-rule folder contains Terraform configuration files that Ingress rules for the sock shop application and also prometheus-grafana into the hosted zone. The sock shop application is hosted as a subdomain under the domain name at "sock-shop.azorod.com.ng".

### Deployment Platform

Jenkins, an automation tool to build, test and deploy software is the Continuous Integration Continous Delivery (CI/CD) platform used.  Two Jenkins files were used in this project - the "cluster-Jenkinsfile", used to deploy the creation of our Kubernetes cluster. This cluster-Jenkinsfile also sets our environments by configuring our AWS credentials to enable Jenkins communicate with AWS. Parameters were also set to be able to create and destroy the cluster with just a click when you select to build with parameters. The second Jenkinsfile - "Jenkinsfile" also sets the environment by configuring the AWS credentials. It has four "create" stages to automate the deployment of the four sub-folders under the "kubernetes" folder. Four stages of "destroy" have also been set to enable the infrastructure to be easily destroyed with just a click.


# Visualizing the project - Steps from start to finish with pictures
1. Create an ec2 instance on AWS with a VPC having an inbound (Ingress) rule allowing All traffic, Port 22, Port 443 and Port 80 while also having an Outbound (Egress) rule allowing All traffic on ipv4 and ipv6.

2. Clone the repository from github basically to run the istaller.sh with its dependencies using the following command (./installer.sh)
![clone the repo](/capstone-images/capstone%201.png)

![run./installer.sh](/capstone-images/capstone%202.png)

3. Optional test on eks directory to find out if there is any error with the files by changing directory (cd) to the eks directory and running the following commands
```
$cd eks
$terraform init
$terraform apply --auto-approve
$terraform destroy --auto-approve
```
![](/capstone-images/capstone%203.png)
![](/capstone-images/capstone%204.png)
![](/capstone-images/capstone%206.png)

4. Copy the IP address of the ec2 instance on aws to the (xxx.xxx.xx.xx:8080) this will open the jenkins default page then click on 'install suggested pluggins' to get started.
![](/capstone-images/jenkins%202.png)
![](/capstone-images/jenkins%203.png)

5. Setup the environment and link jenkins with github and set the file path to both the jenkinsfile and cluster-jenkinsfile.
![](/capstone-images/jenkins%204.png)
![](/capstone-images/jenkins%20pipeline%20setup.png)

6. Pipeline failure then success after a commit
![](/capstone-images/jenkins%20pipeline%20failure%20then%20success%20after%20a%20commit%20was%20made.png)

7. This is the automated deployment of sockshop using the jenkinsfile and the deployment of the eks cluster using cluster-jenkinsfile.
![](/capstone-images/jenkins%20pipeline%20running.png)

8. Asides the resources created on AWS (mentioned above), Sockshop applications and grafana would be created on route53 and also nameservers that would be copied and pointed to a domain name. In this case, my domain name - azorod.com.ng, as shown below

![](/capstone-images/nameservers%20update.png)

9. A secure certificate was created on AWS certificate manager. After it is issued, the sock-shop and grafana URL pointing to your domain name can be inputed in the browser. this will open the sock-shop page. Copying the grafana URL will also open the grafana dashboard which visually monitors the microservice-base applications. In as much as a secured certificate on AWS was issued both the sock-shop application and grafana dashboard were not secured on the browser.

![](/capstone-images/aws%20cert%20ready.png)

10. Sock sock reflecting my domain name (azorod.com.ng)

![](/capstone-images/sock-shop.png)

11. Grafana reflecting my domain name (azorod.com.ng)

![](/capstone-images/grafana%201.png)
![](/updated-sock-shop/capstone-images/grafana%202.png)