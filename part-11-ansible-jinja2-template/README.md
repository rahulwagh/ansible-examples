## Run playbook

```bash
ansible-playbook --inventory inventory/ansible-jinja2-template-playbook/hosts ansible-jinja2-template-playbook.yml
```


## How to find apache is installed or not 

```
type -a apache2 
```


## SSH to EC2 instance

```
ssh -i /Users/rahulwagh/.ssh/aws_ec2_terraform ubuntu@ec2-18-196-119-203.eu-central-1.compute.amazonaws.com
```