# SSH Agent Forwarding

Allows you to use SSH to connect without having to use the `-i <keyfile>` option when you connect or uploading the private key to a bastion instance.

SSH Agent will try 5 keys sequentially. Since instance terminate the connection after 5 tries, ensure that you have 5 or fewer keys added to the agent.

## Adding private keys to ssh agent

Add the private key to the SSH agent
```
ssh-add -K <private-key>
```

View the private keys in the agent
```
ssh-add -L
```

ssh unto the bastion
```
ssh -A <user>@<bastion-ip>
```

From the bastion ssh unto the instance in the private subnet
```
ssh <user>@<private-instance-ip>
```