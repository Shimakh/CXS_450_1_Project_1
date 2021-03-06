# CXS_450_1_Project_1

**Configuring the Jupyter Data Science Notebook Servere on AWS**
----
**Configuring the AWS account**

* First we need to sign up for AWS (Amazon web services) at: http://aws.amazon.com

* Log in to AWS console

* Choose a region (It is recommended to choose a region that is grographicly closer to us) 

**Prepration to luanch a new Instance (EC2)**

* Set up our key pair 

   A.First we need to creat our ssh key pair locally using these set of commands at Gitbash:


Then hit Enter twise to accept the defult location. 

`ls ~/.ssh` 

will give us the location of our ssh key, then type:

`cat ~/.ssh/id_rsa.pub`

This last command will give us the content of our generated key pair.

Now we just need to copy this contenet, and go back to our AWS console.

   B.Import key pair

Click on the key pair section tab, then choose Import key pair.

Choose a name for the key pair and copy the content to the Public Key Content part and hit Import.


* Configuring our security group
 
Hit the Create security Group tab
 
We need to choose Add Rule to choose our own ports. 

The ports that we need are: 22 , 8888 , 2376, 27016  

22 is ssh and 8888 is http

It is important to choose Anywhere as our source
 
Then hit Create.

Now we have everything to launch our instance.

**Launching the new EC2**

1. Choose Ubuntu Server (as our AMI) 
2. After that we choose our Instance type (Free Tier T2.micre) the second row
3. Skip the third step configure Instance Detailes
4. On this step we change the storage size to 30G
5. We skip the 5th step, and move over to the 6th step
6. Inthis Step we just choose the security groups thet we already created
7. Now we just review the changes thet we've done, choose the existing the key pair, and hit Launch

**Docker Installation**

We copy the public Ip of our new instance, and we go over to bash and copy it in this command:
`ssh ubuntu@PUBLICIPADDRESS`


in order to connect to the system we type: y

$now we are connected.

Then we install docker using:

`curl -sSL https://get.docker.com | sh`

Now we just need to copy past this part

`Sudo usermod -aG docker ubuntu`

we should log out now using:

`exit`

And log back in.

We can make sure that everything works by this command:

`docker -v`

**Runing Jupyter**

To download jupyter we type this command:

`docker pull jupyter/datascience-notebook`

To verify we type this command:



`docker images`

To shorten the name of the image we run:

`docker tag IMAGEID dsnb`

`docker images`

Now we want to use this image, so we type:

`docker run -v /home/ubuntu:/home/jovyan -p 8888:8888 -d jupyter/datascience-notebook`

To use it we open a new browser, and at the address bar we put the IP address of our AWS instance.

Now we need a token as our password to accessing jupyter. 

To get that we run:

`docker exec CONTAINERID jupyter notebook list`

We can copy the token and paste it to the password spot.

Finally our Jupyter Notebook is ready to use.

![aws](https://user-images.githubusercontent.com/35311746/34923678-d215484a-f952-11e7-8bf5-f627e8b2e8c5.jpg)



# Budget for using 3 EC2 for 3 months 


The charge for 3 EC2 instances at the same time for a month with Windows as the operating system and T2.micro as Instance type
comes to 25.83$.
And the total for 3 months will be 77.49
