# Terraform - jenkins-ami

### This generates an EC2 instance called jenkins_master_ami then creates an AMI from that instance called jenkins_master

Create a file in the root of this project called terraform.tfvars and populate it with the following using your own values:

    aws_key_name = "aws_key_name"
    aws_default_region = "aws_default_region"
    aws_access_key = "aws_access_key"
    aws_secret_key ="aws_secret_key"
    region = "region"

Next run the terraform script.

    terraform apply

Look up the AMI that was just created and get the ID. When you locate the ID run the AWS CLI command to create a copy like so:

    aws ec2 copy-image --source-region us-east-1 --source-image-id <value> --name jenkins_master_ami_copy

The output should look something like:

    {
    "ImageId": "ami-XXXXXXXX"
    }

Use that ImageId to update the devops-terraform project. After checking to make sure the copy finished make sure to run:

    terraform destroy

At this point all that should be left is a newly created AMI named jenkins_master_ami_copy
