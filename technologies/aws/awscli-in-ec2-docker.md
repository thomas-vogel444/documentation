# Running aws cli on a docker container running on a EC2 instance

Scenario: 
you have a docker container running on a EC2 instance which has a role assigned with various permissions. You want to be able to run the aws cli on it.

Note:
- The EC2 instance contains metadata that can be accessed via a http call
`curl http://169.254.169.254/latest/meta-data/`
- The temporary credentials assigned to the instance in particular can be accessed via
`curl http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance`
- Calling the AWS REST API using temporary credentials require the AWS_SECURITY_TOKEN set on top of `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`
- Assuming you have `awscli`, `curl`, `jq` installed on the docker container, you can get the credentials via
```
export AWS_ACCESS_KEY_ID=`curl http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance -s | jq -r '.AccessKeyId'`
export AWS_SECRET_ACCESS_KEY=`curl http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance -s | jq -r '.SecretAccessKey'`
export AWS_SECURITY_TOKEN=`curl http://169.254.169.254/latest/meta-data/identity-credentials/ec2 security-credentials/ec2-instance -s | jq -r '.Token'`
```