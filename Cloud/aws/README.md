
### AWS
http://aws.amazon.com/

##### AWS_ACCESS_KEY_ID   and   AWS_SECRET_ACCESS_KEY
```
Go to: http://aws.amazon.com/
Go to your AWS account overview
Account menu in the upper-right (has your name on it)
sub-menu: Security Credentials
```

##### [AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/reference/index.html)
* [Installing the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)

##### [aws configure](http://docs.aws.amazon.com/cli/latest/reference/configure/index.html)
```bash
$ aws configure

AWS Access Key ID [None]: XXXXXXXXXXXXXXXXXXXX
AWS Secret Access Key [None]: xxxxxxxxxxxxxxxx+yyyyyyyyyyyyyyyy+zzzzzz
Default region name [None]: us-east-2
Default output format [None]: json
```
```
$ aws --version
```


### EC@

##### [Instance Lifecycle](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html)

```bash
aws ec2 describe-instances
-- aws ec2 terminate-instances --instance-ids i-0b281c344f312f0bx
aws ec2 start-instances --instance-ids i-0b281c344f312f0bx
aws ec2 stop-instances  --instance-ids i-0b281c344f312f0bx
```

##### SSH fingerprint verification for Amazon AWS EC2
* [Amazon EC2 Key Pairs](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
* [Connecting to Your Linux Instance Using SSH](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)

```
chmod 400 ~/.ssh/my-pk-ami.pem

# connect 
ssh -vvv -i ~/.ssh/my-pk-ami.pem ec2-user@xx.xx.xx.ip
```

#### EC2 Instance Lifecycle change
```
aws ec2 describe-instances
--aws ec2 terminate-instances --instance-ids i-0b281c344f312f0bx
aws ec2 start-instances --instance-ids i-0b281c344f312f0bx
aws ec2 stop-instances  --instance-ids i-0b281c344f312f0bx
```


