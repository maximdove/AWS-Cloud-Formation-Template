## Installation of an app (Without Domain Implementation)

### Pre-Requisites:
1. **AWS Account**: Ensure you have an AWS account with necessary permissions to create resources via CloudFormation.
2. **AWS CLI or AWS Management Console**: Have AWS CLI installed and configured on your machine or use AWS Management Console for deploying the CloudFormation template.
3. **S3 Bucket**: Ensure that you have an S3 bucket where your PHP application code is uploaded. Update the `my-project-code-bucket` in your CloudFormation template with your actual S3 bucket name.

### Steps:

#### 1. Deploy the CloudFormation Template:
   - **Via AWS Management Console**:
     1. Log in to the AWS Management Console.
     2. Navigate to `Services > CloudFormation`.
     3. Click on `Create stack`.
     4. In the `Specify template` section, upload your CloudFormation template.
     5. Follow the wizard, specify the stack name and any required parameters, then create the stack.
     6. AWS CloudFormation will now provision the resources defined in the template.

#### 2. Upload the Application Code to S3:
   1. Zip your application code.
   2. Upload the zipped code to the S3 bucket you specified in the CloudFormation template.

#### 3. Database Initialization:

   1. **Access RDS Instance**:
      - After the CloudFormation stack has been successfully created, navigate to the RDS Dashboard in the AWS Management Console.
      - Locate and click on the RDS instance that was created by the CloudFormation stack.

   2. **Retrieve Database Endpoint**:
      - In the RDS instance details page, find the endpoint under the Connectivity & security tab. 

   3. **Connect to Database**:
      - Use a MySQL client to connect to the database using the endpoint, port, and credentials specified in the CloudFormation template.

   4. **Run Initialization Script**:
      - Once connected to the database, execute the script provided in `script.sql` to create the database, tables, and any other necessary structures. You can do this by copying and pasting the script into your MySQL client, or by loading the script file and executing it.

   5. **Verify Initialization**:
      - Verify that the database, tables, and other structures have been created successfully by running some test queries or checking the schema in your MySQL client.

   6. **Update Application Configuration**:
      - Ensure that the application configuration (`db.php`) has the correct values to connect to the new database. If you followed the CloudFormation template, these values should be retrieved from environment variables and no action is needed.

#### 4. Access the Application:
   1. Once the database is initialized and verified, go to the `Outputs` tab in the AWS CloudFormation console and find the value for `LoadBalancerDNS`.
   2. Open a web browser and type in the DNS name of the Load Balancer followed by the file name of your application's entry point, for example, `http://<LoadBalancerDNS>/index.php`.

#### 5. Restrict Access (Optional):
   1. If you want to restrict access to your application from certain IP addresses, navigate to the Security Groups section in the EC2 Dashboard of the AWS Management Console.
   2. Locate and select the security group associated with your Load Balancer and/or EC2 instances.
   3. Edit the inbound rules to specify the allowed IP addresses and deny all others.

#### 6. Connect to EC2 Instances (Optional):
   1. Navigate to the AWS Systems Manager Dashboard in the AWS Management Console.
   2. In the left navigation pane, click on Session Manager.
   3. Click on "Start Session" and select the EC2 instance(s) within your Auto Scaling Group (ASG) you wish to connect to.
   4. Click on "Start Session" again to initiate a session with the selected EC2 instance.

By following these steps, you will have successfully deployed and configured your PHP application on AWS infrastructure without domain implementation, and with options for restricting access and connecting to EC2 instances for further management.