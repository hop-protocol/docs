---
description: Hop Node signer documentation
---

# Signer

A Hop bonder can use an Ethereum key hosted in AWS KMS. An additional layer of validation can be added by using a Lambda function between the bonder process and the KMS key. By using this method, your Ethereum private key never leaves the AWS HSM that it is generated on. Additionally, you can place per-transaction validation on AWS in order to potentially stop transactions if your server has been compromised. With this method, the security of your bonder is now tied more closely to the security of your AWS account (as opposed to strictly your server security if using an encrypted keystore that lives on the server).

These steps show how to set up a KMS signer with Lambda for a Hop bonder. Please make sure you understand every step before using this feature.


## High Level Overview

After completing these steps, you will have the following setup:

* An IAM user that lives on your server running the bonder process
* A Lambda function that can only be invoked by the IAM user
* A KMS key that can only be used by the Lambda function. This key can only `sign` or call `getPublicKey`.

## Detailed Steps

### Create a KMS key

This step will generate an Ethereum key that lives in AWS KMS.

On AWS, go to "Key Management Service" and create a new key. Choose the following options:

* Asymmetric
* Sign and Verify
* ECC_SECG_P256K1

Add the alias "Hop_BonderKms". Do not choose any "Administrative permissions" or "Key Usage Permissions"

### Create a Lambda function

This step will create a Lambda function that can be used to interact with the KMS key.

On AWS, go to "Lambda" and create a function. Create a function and name it "Hop_BonderLambdaValidation".

On the "Code source" section of the function page, choose "Upload from..." option to upload your desired validation. See [this repo](https://github.com/hop-protocol/lambda-bonder-transaction-validation) as a reference.

### Create IAM Policies

This step will create one IAM policy to allow the Lambda function to interact with the KMS key and another IAM policy to allow the bonder to invoke the Lambda function.

On AWS, go to "IAM" and create a policy that will allow the Lambda function to interact with the KMS key. Choose "JSON" and insert the following:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "kms:GetPublicKey",
                "kms:Sign"
            ],
            "Resource": "arn:aws:kms:<YOUR_REGION>:<YOUR_ACCOUNT_ID>:key/Hop_BonderKms"
        }
    ]
}
```

In the object above, update `YOUR_REGION` (i.e. `us-east-1`) and `YOUR_ACCOUNT_ID` (i.e. `xxxxxxxxxxxx`. You can get this from this from clicking your account dropdown on the top right of the AWS UI). Name this policy "Hop_LambdaToKmsPolicy".

Create a new policy that will allow the bonder to invoke the Lambda function. Choose "JSON" and insert the following:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "lambda:InvokeFunction",
            "Resource": "arn:aws:lambda:<YOUR_REGION>:<YOUR_ACCOUNT_ID>:function:Hop_BonderLambdaValidation"
        }
    ]
}
```

Update `YOUR_REGION` and `YOUR_ACCOUNT_ID` in the object above. Name this policy "Hop_BonderToLambdaPolicy".

### Create IAM User and Attach IAM policy

_**Notice:** If the bonder process is running on an EC2 instance, parts of this step can be simplified. The creation of the user can be bypassed and the policies can be applied directly to the EC2 instance. This guide does not provide steps showing how this._

This step will create an IAM user and attach the appropriate policies for operation.

On AWS, go to "IAM" and create a user. During the setup, choose "Attach policies directly" and search for the "Hop_BonderToLambdaPolicy". 

Once that has been completed, go back to "IAM" and choose "Policies". Search for "Hop_LambdaToKmsPolicy" and attach it to the "Hop_BonderLambdaValidation" entity. Note that the actual name of the entity will be "Hop_BonderLambdaValidation-role-xxxxxxxx".
