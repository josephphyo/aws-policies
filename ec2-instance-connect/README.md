#### Connecting to an instance using EC2 Instance Connect ####
##### EC2 Instance Connect CLI to connect to an instance #####
 
* Please configure aws IAM access keys 
```
aws configure
```
* Generate the new private and public keys
```
ssh-keygen -t rsa -f yourpublickey
```

* Send Public Key to Server ( you need the latest version of the AWS CLI )
```
aws ec2-instance-connect send-ssh-public-key --region ap-southeast-1 --instance-id ***InstanceID*** --availability-zone ap-southeast-1a --instance-os-user ec2-user --ssh-public-key file://yourpublickey.pub
```

* The public key is made available to the instance through the instance metadata for 60 seconds. During this time, connect to the instance using the associated private key.
```
ssh -i yourpublickey.pem ec2-user@ec2-XX-XXX-XXX-XX.compute-1.amazonaws.com
```

***If for some reason you don’t connect within that 60-second window, you see the following error***
```
ssh -i yourpublickey.pem ec2-user@ec2-XX-XXX-XXX-XX.compute-1.amazonaws.com
Permission denied (publickey,gssapi-keyex,gssapi-with-mic)
```