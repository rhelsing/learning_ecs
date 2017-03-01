#Docker cluster tutorial w/ ecs

This assumes you have aws set up, configured a sub user, have aws cli access.

1. Install CLI

```bash
sudo curl -o /usr/local/bin/ecs-cli https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-darwin-amd64-latest

sudo chmod +x /usr/local/bin/ecs-cli

ecs-cli --version
```


2. edit ~/.ecs/config

Set the name of the cluster

```
[ecs]
cluster                     = testing
aws_profile                 = default
region                      = us-east-1
aws_access_key_id           = XXXXX
aws_secret_access_key       = XXXXX
compose-project-name-prefix = ecscompose-
compose-service-name-prefix = ecscompose-service-
cfn-stack-name-prefix       = amazon-ecs-cli-setup-
```

3. Tutorial (used docker-compose.yml by default)

###spawn cluster (will take a good bit)
```bash
ecs-cli up --keypair aws --capability-iam --size 2 --instance-type t2.medium
```

###test as a task
```bash
ecs-cli compose up

ecs-cli compose down
```


###run as a service (production)
```bash
ecs-cli compose service up

ecs-cli ps #ip address

ecs-cli compose scale 2
```

####clean up
```bash
ecs-cli compose service rm

ecs-cli down --force
```
