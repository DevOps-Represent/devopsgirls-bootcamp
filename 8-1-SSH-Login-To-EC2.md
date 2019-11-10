## SSH Login to your EC2 instance

### 1) Find your EC2 instance's Public IP
In AWS Click on EC2

Go to the Running Instances

Find  and select your EC2 instance

Copy your EC2 instance's IPv4 Public IP

### 2) Change your .pem key's mode to 'read-only'
Open your terminal

Go to your downloaded .pem key file and change the file’s mode to read-only

Run command in bash (assuming you’ve saved it in downloads):

`$chmod 400 ~/Downloads/keyname.pem`

Example
$chmod 400 ~/Downloads/leorentanyag.pem 
 
### 3) SSH into your instance using your pem key

`ssh -i ~/Downloads/<keyname.pem> ec2-user@<IPv4 Public IP adress>`

Example:
ssh -i ~/Downloads/leorentanyag.pem ec2-user@13.55.214.58
