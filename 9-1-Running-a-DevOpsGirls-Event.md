# The following is a list of instructions on how to run a DevOpsRepresent Event

## Resources

### Comms templates

You will need to contact the attendees three times: 

1.) The invite, covering the scope, the location, and the date of the program

 - When is it happening?
 - Where is it happening?
 - What's being covered?
 - Any dietary requirements?
 - What your operating system of choice is
 - Current AWS experience

2.) A confirmation email + details of Slack Teams, Github Repos, and Login dates.

 - A link to the Slack Team Signup
 - A link to the Github Repo
 - Confirmation link
 - A link to the AWS Console login
 - Wifi access details (if necessary)

Comms templates are as follows:

```
[To be added]
```

3.) A post-event email, containing well wishes, and new links:

 - A survey containing questions for how the program was received
 - Links to meetups, conferences
 - Links to free educational material
 - Details on how to signup for AWS Free Tier



## 1.) Establish roles:

### Organizers:

#### Things to organize on the way:

 - Establish timeline. When is the event happening?
 - Pick invitation mechanism: Eventbrite, Meetup
 - Coaches and presenters. Which companies/people can help you on the day?
 - Communication plan. You'll want to contact attendees regarding the event. 

#### Things to organize for the day:

 - Organize catering, and coffee
 - Social channels, communication plan
 - Organize swag

#### Miscellaneous needs

 - A Slack team to invite all other attendees in
 - An AWS account you'll need to setup
 - IAM users for every single attendee

#### Materials / Facilities

 - Emergency contact detail, so they can get in the premises
 - Printout "My Name Is" sheets
 - Printouts of one-time-login IAM passwords
 - Microphones, speakers
 - Power outlets

# AWS Account Requirements

There are a few things you need to do to prepare an AWS account for this training.

## Create RDS Instance

You'll need to create an RDS instance in advance, with the following details:

Database Name: devopsrepdb
Database User: devopsrep
Database Password: devopsreprds!

*The instance should have "Publically acessible" set to disabled.*

## Security Group Setup 

Go to the RDS instance, then go to *Instance Actions*. Select *See Instance Details*. 

In the next window, you should be able to see the security group that the RDS instance is running on. Make sure it allows access from your VPC subnet - default is `172.31.0.0/16`. Parameters as follows:

```
Protocol: TCP
Port: 3306
Source: 172.31.0.0/16
```

## Create Internal DNS Hosted Zone (Route 53)

You'll need to create a Private Hosted Zone for Route 53. Go to *Services > Route 53*, then click on *Create Hosted Zone*. You'll want to set the following:

```
Domain Name: devopsrep.internal
VPC: [Your Default VPC]
```

## Create a *devopsrep-training* S3 Bucket

You're going to want to create an S3 bucket as well. Go to *Services > S3*, then create a new bucket called `devopsrep-training`. In the bucket, select *Properties*, then go to *Permissions*. Select *Add Bucket Policy* and put the following in:

```
{
	"Version": "2008-10-17",
	"Id": "1",
	"Statement": [
		{
			"Sid": "VPC Only access",
			"Effect": "Allow",
			"Principal": {
				"AWS": "*"
			},
			"Action": [
				"s3:GetObject",
				"s3:PutObject"
			],
			"Resource": [
				"arn:aws:s3:::devopsrep-training",
				"arn:aws:s3:::devopsrep-training/*"
			],
			"Condition": {
				"StringEquals": {
					"aws:sourceVpc": "vpc-cad8d0a8"
				}
			}
		}
	]
}
```

## Create an S3 VPC Endpoint

You're going to want to make the S3 endpoint internal only. Do the following:

1.) Go to Services > VPC > Endpoints

2.) Select *Create Endpoint*

3.) In the Endpoint configuration, set the following:

```
VPC: [your default VPC]
Service: com.amazonaws.ap-southeast-2.s3
Policy:

{
    "Statement": [
        {
            "Action": "*",
            "Effect": "Allow",
            "Resource": "*",
            "Principal": "*"
        }
    ]
}

```

4.) In the route table selection, select all the Route Tables displayed.

After this, the environment should be ready.


## On the day 

### Registration

Have two (2) volunteers take down the names of the people attending off a list. There will be two lists: a.) unconfirmed, and b.) confirmed. For the unconfirmed attendees, make sure to add them to the following:

 - as an IAM user in AWS
 - as a Slack user


