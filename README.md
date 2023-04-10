# Data flow using Airbyte

## Connect to Avanti's Airbyte

<b>1. Connect to EC2 instance:</b>

```
SSH_KEY=**********.pem // file path of the key downloaded to connect to Avanti's EC2 instance.
INSTANCE_IP=REPLACE_WITH_AVANTI_INSTANCE_IP
chmod 400 $SSH_KEY //allow key to have permissions.
ssh -i $SSH_KEY -L 8000:localhost:8000 ubuntu@$INSTANCE_IP
```

Visit http://localhost:8000 to verify the deployment.

<b>2. Enter Avanti's username and password.</b>

## Set up own instance on EC2

<b>1. Connect to EC2 instance:</b>

```
SSH_KEY=**********.pem // file path of the key downloaded to connect to your EC2 instance.
INSTANCE_IP=REPLACE_WITH_YOUR_INSTANCE_IP
chmod 400 $SSH_KEY //allow key to have permissions.
ssh -i $SSH_KEY -L 8000:localhost:8000 ubuntu@$INSTANCE_IP
```

<b>2. To install Docker, run the following command in your SSH session on the instance terminal:</b>

```
sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker $USER
```

<b>3. To install docker-compose, run the following command in your ssh session on the instance terminal:</b>

```
sudo yum install -y docker-compose-plugin
docker compose version
```

<b>4. Install Airbyte:</b>

```
mkdir airbyte && cd airbyte
wget https://raw.githubusercontent.com/airbytehq/airbyte/master/{.env,docker-compose.yaml}
docker compose up -d # run the Docker container
```

<b>5. Create an SSH tunnel for port 8000:</b>

```
ssh -i $SSH_KEY -L 8000:localhost:8000 -N -f ec2-user@$INSTANCE_IP
```

Visit http://localhost:8000 to verify the deployment.

<b>6. You will be asked for a username and password. By default, that's username `airbyte` and password `password`. Once you deploy airbyte to your servers, be sure to change these in your environment's `.env` file:<b/>

```

    # Set to empty values, e.g. "" to disable basic auth
    BASIC_AUTH_USERNAME=your_new_username_here
    BASIC_AUTH_PASSWORD=your_new_password_here
```
