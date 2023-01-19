# Data flow using Airbyte

This repository contains code to set up Airbyte.

## 1. Connect to EC2 instance:

a. Store the file path of the key downloaded to connect to EC2 instance.

`SSH_KEY=**********.pem`

b. Store the IP address of the EC2 instance.

`INSTANCE_IP=REPLACE_WITH_YOUR_INSTANCE_IP`

c. Allow key to have permissions.

`chmod 400 $SSH_KEY`

d. Connect to EC2 instance.

`ssh -i $SSH_KEY ubuntu@$INSTANCE_IP`

## 2. Start Airbyte

```
cd airbyte
docker-compose up -d
```

Visit http://localhost:8000 to verify the deployment.
