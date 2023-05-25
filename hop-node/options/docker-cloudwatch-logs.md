---
description: Setting up AWS CloudWatch logging driver for Docker
---

# Docker CloudWatch Logs



{% tabs %}
{% tab title="docker-compose" %}
```yaml
bonder:
    image: hopprotocol/hop-node:mainnet
    env_file:
      - docker.env
    restart: unless-stopped
    volumes:
        - /home/ubuntu/.hop:/root/.hop
    logging:
      driver: awslogs
      options:
        awslogs-region: us-east-1
        awslogs-group: HopNode
        awslogs-create-group: 'true'
```
{% endtab %}

{% tab title="Bash" %}
```bash
docker run \
  --detach \
  --name hop-node \
  --restart=unless-stopped \
  --log-driver=awslogs \
  --log-opt awslogs-region=us-east-1 \
  --log-opt awslogs-group="HopNode" \
  --log-opt awslogs-create-group=true \
  --env-file docker.env \
  -v ~/.hop:/root/.hop \
  hopprotocol/hop-node:mainnet
```
{% endtab %}
{% endtabs %}

The region and group name can be of your choice.

## IAM CloudWatch Logs Policy Setup

These steps go over on how to setup an IAM policy for accessing specific CloudWatch logs. You do not need to do this if you're accessing the logs under the same account.

### Create EC2 role

1. Go to **IAM** service
2. Click **Roles** on sidebar
3. Click **Create role** button
4. Steps
   1. Select **AWS service** as trusted entity
   2. Select **EC2** as use case
   3. click on **Next: Permissions**
5. Steps
   1. Filter for _CloudWatchLogsFullAccess_
   2. Select **Service: CloudWatch Logs**
6. Click **Next**
7. Click **Next: Tags**
8. Click **Next: Review**
9. Steps
   1. Role Name: _HopNodeEC2Role_
   2. Click **Create role**

### Attach IAM role to ec2

1. Go to **EC2** service
2. Click on instance
3. Click on **Actions** dropdown
   1. Select **Security**
      1. Select **Modify IAM role**
   2. Select _HopNodeEC2Role_
   3. Click **Save**

### Get log group ARN

1. Go to **CloudWatch** service
2. Under **Logs** section on left sidebar, click on **Log groups**
3. Click on _HopNode_
4. Copy **ARN** on top right

### Create IAM user to view logs

1. Go to **IAM** service
2. Click on **Users** on sidebar
3. Click on **Add user**
4. Steps
   1. User name: _alice_
   2. Check **AWS Management Console access**
5. Click on **Next: Permissions**
6. Click on **Create group**
7. Click on **Create policy** (this will open a new tab)
   1. Steps
      1. Service: **CloudWatch Logs**
      2. Actions
         1. Access level
            1. Expand **List**
               1. Check **DescribeLogStreams**
            2. Check **Read**
      3. Resources
         1. Select **Specific**
         2. Under log-group
            1. **Add ARN**
               1. Paste log group ARN retrieved from CloudWatch Log Group
      4. Click on **Add additional permissions**
         1. Service: **CloudWatch Logs**
            1. Expand **List**
               1. Check **DescribeLogGroups**
               2. Under log-group
                  1. Add **Any** for log group
      5. Click on **Next: Review**
         1. Name: _CloudWatchLogsAccessPolicy_
         2. Click on **Create policy**
   2. You may close this tab
8. Back on original tab
   1. Select **Attach existing policies directly**
      1. Click **Refresh** button
      2. Filter for _CloudWatchLogsAccessPolicy_ and select
   2. Click **Next: Tags**
   3. Click **Next: Review**
   4. Right click and open in new tab **Send email** link

### View CloudWatch logs

1. Go to **CloudWatch** service
2. Under **Logs** section on left sidebar, click on **Log groups**
3. Click on _HopRunner_
4. Click on latest _Log stream_
