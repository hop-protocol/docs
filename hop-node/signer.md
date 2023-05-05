---
description: Hop Node signer documentation
---

# Signer

A Hop bonder can leverage an Ethereum key hosted in AWS Key Management Service (KMS) to enhance security and add an extra layer of validation by incorporating an AWS Lambda function between the bonder process and the KMS key. This method ensures that your Ethereum private key remains within the AWS Hardware Security Module (HSM) it was generated on. Additionally, AWS can enforce per-transaction validation to potentially halt transactions if your server is compromised, effectively binding the security of your bonder to your AWS account.

Follow these steps to configure a KMS signer with Lambda for a Hop bonder. Ensure you understand each step and have a solid grasp of AWS services and Hop Protocol concepts before implementing this feature.

## High Level Overview

After completing these steps, you will have the following setup:

* An Identity and Access Management (IAM) user on your server running the bonder process
* A Lambda function that can be invoked solely by the IAM user
* A KMS key accessible only by the Lambda function, with permissions limited to `sign` or `getPublicKey` actions

## Detailed Steps

### 1. Create a KMS key

This step generates an Ethereum key stored in AWS KMS.

1.1. On AWS, go to **Key Management Service** and create a new key. Choose the following options:

* Asymmetric
* Sign and Verify
* ECC_SECG_P256K1

1.2. Add the alias "Hop_BonderKms". Do not choose any "Administrative permissions" or "Key Usage Permissions"

### 2. Create a Lambda function

This step will create a Lambda function that can be used to interact with the KMS key.

2.1. On AWS, go to **Lambda** and create a function. Create a function and name it "Hop_BonderLambdaValidation".

2.2. On the "Code source" section of the function page, choose "Upload from..." option to upload your desired validation code. See [this repository](https://github.com/hop-protocol/lambda-bonder-transaction-validation) as a reference.

### 3. Create IAM Policies

This step entails creating one IAM policy that enables the Lambda function to interact with the KMS key and another IAM policy that permits the bonder to invoke the Lambda function.

3.1. On AWS, go to **IAM** and create a policy that will allow the Lambda function to interact with the KMS key. Choose "JSON" and insert the following:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "LambdaKMSAccess",
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

3.2. In the object above, update `YOUR_REGION` (i.e. `us-east-1`) and `YOUR_ACCOUNT_ID` (i.e. `xxxxxxxxxxxx`. You can get this from this from clicking your account dropdown on the top right of the AWS UI). Name this policy "Hop_LambdaToKmsPolicy".

3.3. Create a new policy permitting the bonder to invoke the Lambda function. Choose "JSON" and insert the following:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "UserLambdaInvoke",
            "Effect": "Allow",
            "Action": "lambda:InvokeFunction",
            "Resource": "arn:aws:lambda:<YOUR_REGION>:<YOUR_ACCOUNT_ID>:function:Hop_BonderLambdaValidation"
        }
    ]
}
```

3.4. Update `YOUR_REGION` and `YOUR_ACCOUNT_ID` in the object above. Name this policy "Hop_BonderToLambdaPolicy".

### 4. Create IAM User and Attach IAM policy

_**Notice:** If the bonder process is running on an EC2 instance, parts of this step can be simplified. The creation of the user can be bypassed and the policies can be applied directly to the EC2 instance. This guide does not provide steps showing how this._

This step will create an IAM user and attach the appropriate policies for operation.

4.1. On AWS, go to "IAM" and create a user. During the setup, choose "Attach policies directly" and search for the "Hop_BonderToLambdaPolicy". 

4.2. Once that has been completed, go back to "IAM" and choose "Policies". Search for "Hop_LambdaToKmsPolicy" and attach it to the "Hop_BonderLambdaValidation" entity. Note that the actual name of the entity will be "Hop_BonderLambdaValidation-role-xxxxxxxx".
