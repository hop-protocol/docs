# AWS Parameter Store Setup



## Add to parameter store

1. Go to _Systems Manager_\*
2. Click on **Parameter Store** under Application Management on left sidebar
3. Click on \*_Create parameter_ button
4. Steps
   1. Name: _/Hop/Bonder/Keystore/Pass_
   2. Check **SecureString** under Type
   3. Enter keystore password in the _Value_ text field
   4. Click the **Create parameter** button

## Attach policy to role

1. Go to IAM
2. Click on **Roles** on left sidebar
   1. Filter for your EC2 Role. E.g. _HopNodeEC2Role_
   2. Click on role link
3. Click on **Attach policies button**
4. Click on **Create policy** button (this will open a new tab)
   1. Service: **Systems Manager**
   2. Check **Read**
   3. Check **GetParameter**
   4. Resources
      1. Add ARN
      2. Region: **us-east-1**
      3. Parameter name: _Hop/Bonder/\*_
   5. Click on **Next: Tags** button
   6. Click on **Next: Review** button
   7. Policy
   8. Name: _HopNodeParameterStorePolicy_
   9. Click on **Create policy** button
   10. You may now close this tab.
5. Back on main tab
6. Click refresh button
7. Filter for _HopNodeParameterStorePolicy_
8. Check box next to policy name
9. Click the **Attach policy** button

## Config

Update your config `~/.hop-node/config.json` to use the password from Paramter Store:

```json
{
  "keystore": {
    "location": "~/.hop-node/keystore.json",
    "parameterStore": "/Hop/Bonder/Keystore/Pass",
    "awsRegion": "us-east-1"
  }
}
```
