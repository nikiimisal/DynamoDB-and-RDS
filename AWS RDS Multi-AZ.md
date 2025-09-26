# Create Amazon RDS Database

## Used AWS services:
1. Relational database service.
2. EC2 service.
3. AWS system manager service.

## Project Objectives:
* Use the AWS Management Console to create RDS subnet groups
* Create RDS database clusters
* Manage access to RDS clusters using security group rules
* Connect to your RDS cluster and edit tables

## Step 1: Logging In to the Amazon Web Services Console
login to the Amazon Web Services Console using your credentials.

## Step 2: Creating an RDS Subnet Group
When creating a DB instance in a VPC, you must select a DB subnet group. Amazon RDS uses that DB subnet group and your preferred Availability Zone to select a subnet and an IP address within that subnet to associate with your DB instance. 

1. In the AWS Management Console search bar, enter RDS, and click the RDS result under Services.

2. From the RDS dashboard, click Subnet Groups from the left-hand menu.

3. Click Create DB Subnet Group to open the creation wizard.

4. Fill out the form using the following data.
    * Name: Demoproject
    * Description: rds-project
    * VPC ID: select the available one
5. Select all the AZs and the subnets available from the dropdown menu and then click Create.

In this step, we used the AWS Management Console to create a DB Subnet Group.

## Step 3: Setting up Security Group Rules for Connecting to the RDS Instance

You will use an EC2 instance to run queries against the RDS database in upcoming Lab Steps. In order to allow incoming traffic from EC2 instances to the RDS instance inside the same VPC, we must configure the appropriate security group rules.

1. In the AWS Management Console search bar, enter VPC, and click the VPC result under Services.

2. In the navigation pane to the left, click Security Groups.

3. Click on Create security group.

4. Fill the creation form as described below:
    * Security group name: rds-demo-sg
    * Description: security group for RDS
    * Inbound rules: click on Add rule
        * Type: MySQL/Aurora
        * Protocol: TCP
        * Port: 3306
        * Source: (Custom) - 172.31.0.0/16 (Ip address of the VPC)
5. Click Create security group, and you will be ready to connect to your RDS instance inside the VPC.

## Step 4: Creating a Database Using RDS
1. In the AWS Management Console search bar, enter RDS, and click the RDS result under Services.

2. Click Databases on the left menu followed by Create database.

3. Under Choose a database creation method ensure that Standard Create is selected.

4. Choose the MySQL database engine and leave the version as the default selected.

5. Select Free tier as the creation template.

6. In the Settings section, set the following options:
    * DB instance identifier: rds-project
    * Master username: admin
    * Master password: myStrongRDSpwd!

7. In the Instance configuration section, set the following option:
    * DB Instance Class: Select Burstable classes and select db.t2.micro from the drop-down
8. In the Storage section, set the following option:
    * Allocated Storage: 20 GiB
    * Click the Storage autoscaling drop-down
    * Enable Storage Autoscaling: Unchecked
9. In the Connectivity section, provide additional information that RDS needs to launch the MySQL DB instance:
    * VPC Security Group(s): Select the rds-demo-sg
    * Make sure to delete the default VPC SG and only have the rds-launch-wizard attached
10. In the Monitoring section, set the following values:
    * Enable Enhanced monitoring: Unchecked
11. In the Additional configuration section, click the drop-down, and set the following values.

    * Database options Initial database name: rdsdemodb
    * Enable automatic backups: Unchecked
11. Make sure to uncheck the Deletion protection checkbox.

12. Click Create database.

In this step, we used the AWS Management Console to create an RDS Database.

## Step 5: Starting an AWS Systems Manager Session Manager Browser Shell Session
Session Manager is part of AWS Systems Manager suite of tools for gaining operational insights and taking action on AWS resources.Session manager provides secure access to instances without the need to distribute passwords or SSH keys. Session Manager also allows you to connect to instances without having to open any inbound ports. 

1. Navigate to AWS Systems Manager > Session Manager and click Start session to create a browser-based Linux shell session.

we already create an ec2 instance of name web.

2. Select the web instance as the Target instance and click Start Session.

In this step, we created a session to open a browser-based shell on an EC2 instance using AWS Systems Manager Session Manager.

## Step 6: Connecting to RDS and Creating a Database Table
Your RDS instance is ready and accessible from any EC2 instance created within the same VPC, so you can use your Session Manager session to connect to the database. In this step, we will connect to your RDS instance and create a database table.

1. In your Session Manager shell session, enter the following command to change to the default Amazon Linux user (ec2-user) running in a bash shell:
```
sudo -i -u ec2-user
```
2. Install the mysql client by entering:
```
sudo yum -y install mysql
```
3. Navigate to the RDS database view.

4. Click the DB identifier of the RDS instance you created and in the Connectivity & Security section that appears take note of the Endpoint.

5. In your session, run the following command replacing your.endpoint.aws.com with the endpoint you noted earlier:
```
mysql -h <your.endpoint> -u admin -p rdsdemodb
```
This command connects you to the database using the username specified by -u flag and the database name using -p flag.

6. When prompted, insert the Master RDS Password: myStrongRDSpwd!

7. Create a new table by executing this command:
```
CREATE TABLE laboratory ( id INT, name VARCHAR(100) );
```

8. Verify that your table was created by executing this command:
```
DESC laboratory;
```
9. Close your database connection by executing this command:
```
quit;
```
In this step, we logged into an RDS instance and create a database table.

## Step 7: Deleting an RDS Database
1. From the RDS Console, click Databases in the left menu.

2. Click on your RDS Database instance

3. Click on Actions > Delete:

4. Uncheck the Create final snaphot? checkbox, check the acknowledgment checkbox, and enter delete me in the confirmation text box before clicking Delete.

Your RDS instance is now in the Deleting status and will take a few minutes to complete.

In this step, we deleted the RDS database using the AWS Management Console.


