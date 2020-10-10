

 # AUTOMATED DEPLOYMENT USING AWS AND TERRAFORM


Although Deploying a website is an easy task, but it is a little time consuming. Usually developers repeat the same process of deployment of their sites and other cloud resources again and again, which pretty much consumes their time and energy.

But there is an easy way to automate all these time consuming steps and deploy the site in a go. This can be done easily on a AWS Cloud using Terraform , with the website code stored in GitHub.


**OUTLINES**


Have to create/launch Application using Terraform

1. Create the key and security group which allow the port 80.

2. Launch EC2 instance.

3. In this Ec2 instance use the key and security group which we have created in step 1.

4. Launch one Volume (EBS) and mount that volume into /var/www/html

5. Developer have uploaded the code into github repo also the repo has some images.

6. Copy the github repo code into /var/www/html

7. Create S3 bucket, and copy/deploy the images from github repo into the s3 bucket and change the permission to public readable.

8 Create a Cloudfront using s3 bucket(which contains images) and use the Cloudfront URL to update in code in /var/www/html


**REQUIREMENTS**


> AWS Account

> AWS CLI Installed

> Terraform Installed

> Create a file with .tf extension in a particular folder where all the code for Terraform Configuration can be written.


**CONFIGURING TERRAFORM AND AWS**


![Screenshot (1233)](https://user-images.githubusercontent.com/64742449/95665117-cf762f00-0b6a-11eb-994a-a813fcd63ea3.png)


**CREATING A KEY**

For going inside the instance and doing something a key is required and it can be created by the following code


![Screenshot (1234)](https://user-images.githubusercontent.com/64742449/95665199-b15cfe80-0b6b-11eb-8f49-c1a9d8a892d6.png)



**CREATING A SECURITY GROUP WHICH ALLOWS PORT 80**

A security group is also needed to be attached to the instance for the security of the OS, so that anyone cannot enter , only some specific ports are allowed.


![Screenshot (1235)](https://user-images.githubusercontent.com/64742449/95665179-7eb30600-0b6b-11eb-8a9a-2243976c5a41.png)



**LAUNCHING AN EC2 INSTANCE WHICH USES THE KEY AND THE SECURITY GROUP CREATED IN THE PREVIOUS STEPS**

An EC2 Instance is launched by using the key and the security group which have been created in the previous steps.


![Screenshot (1236)](https://user-images.githubusercontent.com/64742449/95665205-be79ed80-0b6b-11eb-865d-705fdaf309ac.png)



**LAUNCHING AN EBS VOLUME**

An EBS Volume is a type of a Pen Drive that can be attached to the EC2 Instance anytime needed and can be used to copy data from or to the instance.


![Screenshot (1237)](https://user-images.githubusercontent.com/64742449/95665213-dd787f80-0b6b-11eb-8d98-fe3858ec6a5e.png)


**ATTACHING THE EBS VOLUME TO THE INSTANCE AND MOUNTING THAT VOLUME TO THE /var/www/html FOLDER***

After the volume has been created it has to be mounted on the Instance. Here the EBS volume is being mounted on the /var/www/html folder of the created instance.


![Screenshot (1238)](https://user-images.githubusercontent.com/64742449/95665230-013bc580-0b6c-11eb-9fac-24a9b55a01b7.png)


**DOWNLOADING THE GITHUB REPO IN WHICH THE DEVELOPER HAS PUT SOME CODE AND IMAGES TO THE LOCAL SYSTEM**

The Developer uploads some kind of code to the GitHub repo from where it has to be taken and the images present in the repo have to be uploaded to the s3 bucket.


![Screenshot (1239)](https://user-images.githubusercontent.com/64742449/95665244-31836400-0b6c-11eb-86a8-430c975f97a6.png)


**CREATING A S3 BUCKET AND MAKING IT PUBLIC READABLE**

s3 Bucket is used to store data. It is just like our Google Drive. A s3 bucket is created to store the images uploaded by the Developer in the GitHub repo.


![Screenshot (1240)](https://user-images.githubusercontent.com/64742449/95665247-347e5480-0b6c-11eb-88d9-92060c7ed24f.png)


**UPOADING THE DATA DOWNLOADED(IMAGES) FROM THE GITHUB REPO TO THE S3 BUCKET**

To store the data in the s3 bucket , the data(images) uploaded by the Developer have to be uploaded in the s3 bucket. This is done by using the following code.


![Screenshot (1241)](https://user-images.githubusercontent.com/64742449/95665250-38aa7200-0b6c-11eb-9ed3-9f29493d93d4.png)



**CREATING A CLOUDFRONT DISTRIBUTION**

Cloud Front is a service provided by AWS for a faster content delivery of files, since we don't frequently change our 'static' content we can use a CloudFront for a better experience of clients visiting our site. A CloudFront can be created as


![Screenshot (1242)](https://user-images.githubusercontent.com/64742449/95665269-6e4f5b00-0b6c-11eb-8de0-34f54c38cf72.png)

![Screenshot (1243)](https://user-images.githubusercontent.com/64742449/95665271-714a4b80-0b6c-11eb-9fa4-3e9f0d40667e.png)



The code is now ready with all the steps written in the configuration file.

**CREATING THE INFRASTRUCTURE**

You need to go inside the folder where the .tf file has been made and run the command as


![Screenshot (1245)](https://user-images.githubusercontent.com/64742449/95665276-7e673a80-0b6c-11eb-80dd-af20661fc668.png)

to download all the plugins required to run the code.

Run the following command to check if there is some mistake in the code.

![Screenshot (1244)](https://user-images.githubusercontent.com/64742449/95665275-7a3b1d00-0b6c-11eb-816e-a2ef6191751d.png)


If the output of the above command is "Success" then deploy the infrastructure by using the command as

![Screenshot (1247)](https://user-images.githubusercontent.com/64742449/95665295-b8384100-0b6c-11eb-813e-fef8dd6078ca.png)


**AFTER SUCCESSFUL RUNNING OF THE CODE**

After the code has been successfully run the following architecture has been deployed and the various components created are


![Screenshot (1248)](https://user-images.githubusercontent.com/64742449/95665298-bbcbc800-0b6c-11eb-8009-7592e8405588.png)

![Screenshot (1220)](https://user-images.githubusercontent.com/64742449/95665407-8ecbe500-0b6d-11eb-86c0-978869a1f4f4.png)

![Screenshot (1251)](https://user-images.githubusercontent.com/64742449/95665311-e453c200-0b6c-11eb-8a65-0cd01445cb8c.png)

![Screenshot (1222)](https://user-images.githubusercontent.com/64742449/95665363-2250e600-0b6d-11eb-9fa0-a27ae3aea7b4.png)

![Screenshot (1223)](https://user-images.githubusercontent.com/64742449/95665334-f59cce80-0b6c-11eb-8ab4-bff7030cdc75.png)

![Screenshot (1218)](https://user-images.githubusercontent.com/64742449/95665330-efa6ed80-0b6c-11eb-9b41-6c2d76dd51e6.png)


The website that has been deployed be seen by using the instance ip 


![Screenshot (1250)](https://user-images.githubusercontent.com/64742449/95665391-55937500-0b6d-11eb-91fc-986ae1c6f6a2.png)



Thanks for Reading !!!
