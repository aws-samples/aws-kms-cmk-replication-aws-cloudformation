## AWS KMS CMK Key Replication for AWS CloudFormation

Using AWS CloudFormation templates to deploy resources is a primary focus in using infrastructure as code (IaC) within AWS.  However, some aspects of services are not supported by CloudFormation and must be done manually or with other solutions—KMS CMK key replication being one.  While CloudFormation supports creating KMS CMKs natively, replicating any key created must be done out of band of the stack creating an extra process step.  This solution aims to allow this functionality via a CloudFormation custom resource that will reference a Lambda function deployed by the product and is aimed for use with complex architectural stacks that are creating or making use of KMS CMKs where key replication is a desired functionality as part of said stack.

## Usage

1. Clone the repository and identify the solution template “kms_key_replication.baseline.template.yml” in the “templates/” directory.  This template may be uploaded to S3 for use in the next step but it is not necessary.

2. Use the identified solution template to launch an AWS CloudFormation stack.  Since the functional code of the solution implements threading, identify if the number of Python max workers should be adjusted and enter that value as a parameter to the template.  
For the next step, take note in the output section of the solution CloudFormation stack of the ARN for the KMS CMK key replication Lambda function.

3. Identify the example file “custom_resource.example.yml” in the “templates/” directory of the cloned repository.  This file explains—through an example implementation—how to utilize the deployed solution as a custom resource in separate CloudFormation templates.  Ensure that any **KMS CMKs to be replicated are multi-region keys**.  
Once the CloudFormation custom resource has been implemented and deployed, identify the replicated KMS CMKs through the KMS Console in the regions originally specified as a parameter to the custom resource.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

