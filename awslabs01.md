
## Lab A1: Create an EC2 Instance

In this lab we create a EC2 instance that will give you a Linux server in the cloud with full internet access and a web server running.


### Create EC2 with httpd already provisioned

High level steps are:

* Go the the EC2 service
* make sure region Frankfurt is selected
* Click on Launch instance
* Select Amazon Linux
* Leave t2.micro instance
* Click "Configure Instance Details"
* Goto Advanced and add the following user data:

```
sudo yum update 
sudo yum install httpd  
sudo service httpd start   
sudo chkconfig httpd on 
```

* Select create key pair (if you create your first EC2 instance only, later you can reuse it.

Wait until the instance is running, then

* Under running instances get the public IP address of your running EC2 instance.
* Try to access the newly provisioned EC2 instance with the already running web server from your local browser. It will not work, because we have to open the port first that is used by the web server.
* In the AWS console, under the security groups and add access for TCP and Port 80
* Try to access the newly provisioned EC2 instance with the already running web server from your local browser.


### Connect to the EC2 instance


Select the instance under EC2 / running instances and connect to the instance.

From a UNIX shell you can connect as follows:

```
chmod 400 mykey.pem
ssh -i "mykey.pem" ec2-user@PUBLIC_IP
```


Details are described for [Windows and UNIX](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html?icmpid=docs_ec2_console). 




## Lab A2: Use S3 for a Web Server

In this lab we use the blob storage S3 to create our own web server.

High level steps are:

* Goto S3 service
* Create a new bucket (make sure the name is unique)
* Make it publicly available
* Upload an index.html (you can use [this index.html](https://s3.eu-central-1.amazonaws.com/fmtestweb/index.html) (just click on view source and save it locally) and this [pic](https://s3.eu-central-1.amazonaws.com/fmtestweb/ocean_beach2.jpg).
* Make sure both files are publicly available.
* Write down the URL
* Check if you can access your web site.

