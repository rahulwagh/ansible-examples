## Run playbook

```bash
ansible-playbook --inventory inventory/ansible-deployment-strategy/hosts ansible-deployment-strategy.yml
```


## SSH to EC2 instance

```
ssh -i /Users/rahulwagh/.ssh/aws_ec2_terraform ubuntu@ec2-3-76-33-80.eu-central-1.compute.amazonaws.com
```

## Limit on sub-set of server

```bash
ansible-playbook --inventory inventory/ansible-deployment-strategy/hosts ansible-deployment-strategy.yml --limit blue 
```

## Deploy on Sub
