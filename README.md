# aws-challenge-week-6-part-2

## Conditions
To conditionally create resources, you add the optional **Conditions** section to your template. Once you define conditions and relevant criteria, you use your conditions in the **Resources** and **Outputs** template sections. CloudFormation evaluates all conditions in your template before creating any resources at stack creation or stack update. Resources that are associated with a true condition are only created during stack creation or stack update. 

In the hands on, I will be doing the following: 
* Provision resources based on Condition evalutaion
* Specify resource property values using Condition functions

1. Open the condition-resource.yaml file and add the following code to create a Parameters section in the template

<img width="437" alt="1" src="https://github.com/user-attachments/assets/80142a7b-a842-49b8-b167-d38118dee0c7" />

2. Add the following condition to evaluate if the EnvType parameter value equals to prod

<img width="143" alt="2" src="https://github.com/user-attachments/assets/61cb8679-2e29-4bfd-90a7-a69312efa291" />

3. Associate the conditions to resources that you want to conditionally provision based on the isProduction condition

<img width="359" alt="3" src="https://github.com/user-attachments/assets/f767c555-0b09-4004-b6eb-21eb7e771ec0" />

4. Create a stack on CloudFormation using the condition-resource.yaml template

<img width="959" alt="4" src="https://github.com/user-attachments/assets/aa333583-799c-43f7-b7d0-8945e34db5c2" />

5. On the **Resource** tab of the CloudFormation console, verify that the only resource provisioned is an EC2 instance

<img width="638" alt="5" src="https://github.com/user-attachments/assets/c02b600d-3220-4ee1-9560-ac0670cf2e6a" />

6. Create a new stack using the same template, this time pass the prod value for the EnvType

<img width="953" alt="6" src="https://github.com/user-attachments/assets/c07cde27-2f32-4300-9726-d83c94b9d7bc" />

7. On the **Resource** tab of the CloudFormation console, verify that the resources provisioned are EC2 instance, Volume and MountPoint

<img width="605" alt="7" src="https://github.com/user-attachments/assets/7996ea6f-2610-4a97-935b-ffe6f2833983" />

8. Open the condition-resource-property.yaml and add the following code define the *EnvType* parameter and the *isProduction* condition to create resource based on the parameter value passed

<img width="434" alt="8" src="https://github.com/user-attachments/assets/374e242c-6df0-4d18-a5d8-b5df399767f1" />

9. Add the following code to conditionally specify property values

<img width="349" alt="9" src="https://github.com/user-attachments/assets/fc82682c-5634-48f1-8cdd-7372bff206a5" />

10. Create a stack on CloudFormation using the condition-resource-property.yaml template. On the **Resource** tab of the CloudFormation console, verify that the stack created an EC2 instance.

<img width="948" alt="10" src="https://github.com/user-attachments/assets/414b04e6-feb8-4e7a-bf36-b89817cc03f8" />

11. Add the following code to conditionally create an output in the **Outputs** section of the CloudFormation template

<img width="178" alt="11" src="https://github.com/user-attachments/assets/28ad5302-7806-47dd-93cd-ad7676ea0ce9" />

12. Update the stack on Cloudformation. Open the **Outputs** tab on the CloudFormation console and verify that the *VolumeId* is present

<img width="944" alt="12" src="https://github.com/user-attachments/assets/a0154f94-fde9-45e4-8d09-d18dc5647a4e" />

13. Clean up resources by deleting the CloudFormation stacks

## Resources Dependencies
If there are no dependencies between resources you define in a template, CloudFormation iniaties the creation of all resources in parallel. There are cases where you either want to, or a required to define the order in which resources will be created: in these cases, CloudFormation creates some resources before other ones. 

In the hands on lab, I will be doing the following:
*Understand the usage of the *DependsOn* resource attribute to explicitly define resource creation order
*Use *Ref* and *Fn::GetAtt* intrinsic functions to create dependencies between resources

1. Open the resource-dependencies-without-dependson.yaml template and add the following code to create an S3 bucket and an SNS topic

<img width="284" alt="13" src="https://github.com/user-attachments/assets/bea7e7b7-0442-4f88-bf6d-50ff8c38aba9" />

2. Create a stack on CloudFormation using the template created in the previous step

<img width="959" alt="14" src="https://github.com/user-attachments/assets/e8df7f7d-3f55-46ae-b657-7609a09a0b13" />

3. Open the **Events** tab on the CloudFormation console, since there are dependencies between the two resources, the creation of the SNSTopic and S3Bucket resources were initiated at the same time

<img width="545" alt="14,1" src="https://github.com/user-attachments/assets/f3b60d8e-1bce-4d1c-92c1-06cfe687974e" />

4. Open the resource-dependencies-with-dependson.yaml template and add the following code that uses the *DependsOn* attribute to explicitly define a dependency between the SNSTopic and the S3 bucket

<img width="289" alt="15" src="https://github.com/user-attachments/assets/322712d5-590b-4f9f-86cf-1551e4d14ca3" />

5. Create a stack on CloudFormation using the template created in the previous step

<img width="947" alt="16" src="https://github.com/user-attachments/assets/44e29c47-98e6-4cd5-b8dc-c580effba387" />

6. Open the **Events** tab on the CloudFormation console, because of the *DependsOn* attribute CloudFormation created the S3 bucket first and the SNSTopic afterwards

<img width="544" alt="16 1" src="https://github.com/user-attachments/assets/cb4b4257-cd28-4486-867d-7a752fb69f75" />

7. Open the resource-dependencies-with-intrinsic-functions.yaml template and add the following code to create an SNS topic, an SNS topic subscription, EC2 Security Group and SecurityGroupIngress

<img width="299" alt="17" src="https://github.com/user-attachments/assets/84c06dff-b84d-4c9c-8be9-13a795ea078a" />

8. Create a stack on CloudFormation using the template created in the previous step

<img width="935" alt="18" src="https://github.com/user-attachments/assets/5b9c8a72-9b2b-44e7-a28c-427ec2a0df38" />

9. SNS topic subscription email confirmation

<img width="686" alt="18 1" src="https://github.com/user-attachments/assets/6b134715-694d-4d34-9ad9-c729d1224b69" />

10. Open the resource-dependencies-challenge.yaml template and modify the EC2 instance resource definition with the following

<img width="259" alt="19" src="https://github.com/user-attachments/assets/bbdf8087-5ff7-4a34-830a-af18d532b6b0" />

11. Add the *DependsOn* attribute for the Amazon S3 bucket

<img width="277" alt="20" src="https://github.com/user-attachments/assets/3e572d8a-3901-4bd7-918d-ba528e293d29" />

12. Create the stack on CloudFormation using the template that was created in the previous step

<img width="950" alt="21" src="https://github.com/user-attachments/assets/1448bcbe-3d9d-49ca-9828-b6192a0bf4fe" />

13. Clean up resources by deleting the CloudFormation stacks

## Dyanamic References
Dynamic references are used in the CloudFormation template to reference external values stored in AWS services. When you use a dynamic reference, CloudFormation retrives the value of the specified reference when necessary during a stack and change set operations. However, CloudFormation never stores the actual reference value. 

In the hands on lab, I will be doing the following: 
* Compose a dynamic reference string to access an external value in the CloudFormation template
* Retrieve the latest version of a Parameter store parameter
* Retrieve a specific version of a secrets manager secret
* Extract a value for a specific key, from a secret that uses a JSON format

1. Create a parameter using the AWS Command Line Interface (CLI)

<img width="227" alt="22" src="https://github.com/user-attachments/assets/a8061a11-aaa8-4867-98b3-c263edd3c608" />

2. Open ec2-instance.yaml and add the following code in the Properties section, the ImageId property and a dynamic reference to the parameter

<img width="349" alt="23" src="https://github.com/user-attachments/assets/b9fd32c6-1dd8-45c0-9610-320e74d5bc7f" />

3. Create a stack on CloudFormation using the ec2-instance.yaml template

<img width="947" alt="24" src="https://github.com/user-attachments/assets/78440922-eb61-4a4c-baff-dae8cfd87fc1" />

4. In the CLI verify that the ID of the image used for the EC2 instance matches the image ID stored in the Parameter store paramter

<img width="244" alt="25" src="https://github.com/user-attachments/assets/cdd3a978-6905-4bee-9c09-cbd6dd46bf58" />

5. Create a stack on CloudFormation using database.yaml template. This stack will create an Amazon RDS database.

<img width="941" alt="27" src="https://github.com/user-attachments/assets/6c1a86ea-f4b0-4ab4-bb7d-c9de7088e1ec" />

6. Open lambda-function.yaml and update the template by appending the *Properties* section with the *Environment* property, with variables using dynamic references to the AWS Secrets manager

<img width="511" alt="28" src="https://github.com/user-attachments/assets/efe9f6fd-3962-48bc-bc76-52acf1c2b13c" />

7. Create a stack on CloudFormation using the lambda-function.yaml template. In the template that was just deployed, database connection parameters are retrieved during stack runtime using a dynamic string.

<img width="956" alt="29" src="https://github.com/user-attachments/assets/bd4ce95e-9ed7-4ebf-a59f-c6d0722e42ea" />

8. In the CLI invoke the example Lambda function that was created and save the output inside of a JSOn file

<img width="422" alt="30" src="https://github.com/user-attachments/assets/aaefae8d-c205-4cf7-b9eb-099a9f34b6e3" />

9. Print the content of the JSON file

<img width="617" alt="31" src="https://github.com/user-attachments/assets/6246225e-e7a4-4cd5-b66a-04df8e1ea80a" />

10. Create a Parameter store parameter specifying the required memory configuration

<img width="734" alt="32" src="https://github.com/user-attachments/assets/deae0dd9-41a1-4e54-a325-43d206368b09" />

11. Open lambda-memory-size.yaml template and add the following code which includes the *MemorySize* property using a dynamic reference to the parameter

<img width="322" alt="33" src="https://github.com/user-attachments/assets/e86f7012-2f5d-4d23-bf44-273a402ee818" />

12. Create a stack on CloudFormation using the lambda-memory-size.yaml template

<img width="948" alt="34" src="https://github.com/user-attachments/assets/ad4315c6-8c34-4c98-8ef5-fd8ee7aab74d" />

13. In the CLI, verify that the Lambda function was created using the SSM Parameter value for MemorySize

<img width="695" alt="35" src="https://github.com/user-attachments/assets/e24a4a1f-609a-4693-a048-eab82b6a8c56" />

14. Clean up recources by deleting the Lambda functions, Parameter store parameters and the CloudFormation stacks


## Nested stacks
You can mix and match different templates but use nested stacks to create a single, unified stack. 

In the hands on lab, I will be doing the following:
* Build a root stack that contains all other stacks
* Build a VPC stack which the EC2 instance will be placed into
* Build a IAM instance role stack
* Build the EC2 instance stack

1. Create an S3 bucket by creating a stack on CloudFormation using the template-and-stack.yaml template

<img width="943" alt="1" src="https://github.com/user-attachments/assets/86d069fb-3c61-4491-a018-5be436050546" />

2. Open main.yaml and add the following code to add parameters so that they can be passed to the nested stack

<img width="598" alt="2" src="https://github.com/user-attachments/assets/eca615fd-a91c-434f-93f1-8e28f12a2d83" />

3. Add the following code to create a VPC resource

<img width="410" alt="3" src="https://github.com/user-attachments/assets/40217ea5-0db9-4828-98aa-642e7090dd08" />

4. Upload vpc.yaml template file to the S3 bucket

<img width="946" alt="4" src="https://github.com/user-attachments/assets/a13d336f-11d1-4f66-aee5-cc6bd20e0ae0" />

5. Create a stack on CloudFormation using the main.yaml template file

<img width="956" alt="5" src="https://github.com/user-attachments/assets/ec8ee179-0894-4777-b8aa-250107f58f96" />

6. Open iam.yaml and sdd the following code to create an IAM role with permissions to allow Session Manager to access the EC2 instance

<img width="360" alt="6" src="https://github.com/user-attachments/assets/e5f81ec1-28c4-44e7-b5c0-c3eb3772b9a8" />

7. Open main.yaml and add the following code to create the IAM resource

<img width="416" alt="7" src="https://github.com/user-attachments/assets/86ff0e5e-5d8b-45ce-bd21-425adb92cb00" />

8. Upload the iam.yaml to the S3 bucket

<img width="944" alt="8" src="https://github.com/user-attachments/assets/91dea5fe-9423-4fb1-85b9-dce1384b4dc2" />

9. Update the previously created nested stack with the updated main.yaml template

<img width="952" alt="9" src="https://github.com/user-attachments/assets/414ea34b-f978-41d0-b433-86d1613cb715" />

10. Open ec2.yaml and add the following code to the *Parameters* section

<img width="359" alt="10" src="https://github.com/user-attachments/assets/67c742fb-d67b-428d-aa4d-64f59ed04ffb" />

11. Open main.yaml and add the following code to create the EC2 resource

<img width="436" alt="11" src="https://github.com/user-attachments/assets/8908defd-32c4-4f5a-a693-7245a068750f" />

12. Add the following code to the Parameters section of the EC2 stack in main.yaml

<img width="242" alt="12" src="https://github.com/user-attachments/assets/97a3574b-ebc4-4325-9c32-d8cb709eb494" />

13. Open ec2.yaml and add the following code to create 2 parameters

<img width="196" alt="13" src="https://github.com/user-attachments/assets/8bf4cee8-9b99-4f5c-a823-6b1d07cac3c5" />

14. Add the following code to reference the *VpcId* parameter in the *WebServerSecurityGroup* resource

<img width="120" alt="14" src="https://github.com/user-attachments/assets/cd00a3ce-70f2-4bef-b19d-d53196287c97" />

15. Add the following code to vpc.yaml

<img width="217" alt="15" src="https://github.com/user-attachments/assets/bb3176b5-6284-4d46-a1aa-b26926c9bdb7" />

16. Add the following code to main.yaml to add VpcId and SubnetId to the EC2Stack stack

<img width="293" alt="16" src="https://github.com/user-attachments/assets/fd6e94fa-778a-441a-a932-f8fa8a1e3833" />

17. Open iam.yaml and add the following code

<img width="247" alt="17" src="https://github.com/user-attachments/assets/8e44a802-2dcc-43c0-bbf8-ee964900d0fc" />

18. Open ec2.yaml and add the following code to create a parameter

<img width="261" alt="18" src="https://github.com/user-attachments/assets/68d7afe1-6564-4b56-86b5-a60340e8f91a" />

19. Open main.yaml and add the following code to add the *WebServerInstanceProfile* parameter to the EC2 stack

<img width="493" alt="19" src="https://github.com/user-attachments/assets/757407f3-87b4-409a-99e2-a865fc102bd3" />

20. Add the following code to main.yaml to add the *WebsiteURL* to the *Outputs* section

<img width="280" alt="20" src="https://github.com/user-attachments/assets/aa2fecc7-431c-40ce-9481-acc659b1b0f9" />

21. Upload the updated vpc.yaml, ec2.yaml and iam.yaml to the S3 bucket

<img width="947" alt="21" src="https://github.com/user-attachments/assets/4273ca27-f85e-450d-80dd-4a8e9003fbea" />

<img width="953" alt="23" src="https://github.com/user-attachments/assets/feacecb7-fad3-496a-be9a-09b075c1a7b5" />

22. Update the previously created nested stack with the updated template

<img width="958" alt="24" src="https://github.com/user-attachments/assets/d52c6844-f707-4ae7-b088-584e3ceb76ff" />

23. Verify that the application was successfully deployed by opening a new browser tab and pasting the *WebsiteURL*. The *WebsiteURL* can be found in the **Outputs** tab on the CloudFormation console

<img width="950" alt="25" src="https://github.com/user-attachments/assets/6bcf48b2-620c-4efb-9101-3e34e126b229" />

24. Clean up resources by deleting the root stack and S3 bucket stack

## Cross stack references
The concept of **Cross stack** is to use intrinsic functions to import previously exported values using Paramaters.

In the hands on lab, I will be building:
* VPC stack
* IAM instance role stack
* EC2 instance stack

1. Open vpc.yaml and add the following code

<img width="370" alt="1" src="https://github.com/user-attachments/assets/61d1680e-c384-46c0-a9ae-821d000f888d" />

2. Create the VPC stack on CloudFormation using the vpc.yaml template

<img width="956" alt="2" src="https://github.com/user-attachments/assets/228166fc-2fd7-4205-a35c-eb35aa11a87d" />

3. Open iam.yaml and add the following code to the *Outputs* section

<img width="379" alt="3" src="https://github.com/user-attachments/assets/dfe53fa7-c19a-4654-bf29-47417301836f" />

4. Create the IAM stack on CloudFormation using the iam.yaml template

<img width="950" alt="4" src="https://github.com/user-attachments/assets/55673610-8ce5-463b-8a22-9c0b376c90a9" />

5. Open ec2.yaml and add the following code to update the paramaters section

<img width="440" alt="5" src="https://github.com/user-attachments/assets/da74cc0e-cd65-4b1f-92ac-4a729541aa2a" />

6. Add the following code to update the WebServerInstance resource in the Resources section

<img width="551" alt="6" src="https://github.com/user-attachments/assets/8758eb5a-d44b-4d10-a970-c0de080ca4f4" />

7. Add the following code to update the security group resource

<img width="560" alt="7" src="https://github.com/user-attachments/assets/10b30709-b1a9-4f60-8f3b-f73c579a64b0" />

8. Create the EC2 stack on CloudFormation using the ec2.yaml template

<img width="953" alt="8" src="https://github.com/user-attachments/assets/7c61f3c8-f5ed-4452-9fe7-ebef40f19b75" />

9. Verify that the application was deployed successfully by entering the WebsiteURL in a new tab. The WebsiteURL can be found on the **Outputs** tab of the CloudFormation console.

<img width="958" alt="9" src="https://github.com/user-attachments/assets/81d14b26-866e-4645-a8f2-47f96c9c115e" />

10. Verify that you log into the instance using Session Manager

<img width="950" alt="10" src="https://github.com/user-attachments/assets/01c6b2ec-13d2-49f7-be9d-09f65f56cd62" />

11. Clean up resources by deleting the EC2 stack first, then the IAM and VPC stacks

## Langauge extensions

A language extension is a transform, which is macro hosted by CloudFormation.

In the hands on lab, I will be doing the following:
* Understanding how to incorporate the AWS::LanguageExtensions transform in the CloudFormation template
* Use language extensions in my CloudFormation template

1. Open language-exntensions.yaml and add the following code

<img width="578" alt="1" src="https://github.com/user-attachments/assets/383bb212-c24e-44f9-8e62-f15d6f0a969e" />

2. Add a parameter to the Parameters section

<img width="197" alt="2" src="https://github.com/user-attachments/assets/8bccec35-ccf6-47a1-8d33-16470e471796" />

3. In the Resources section, add a Deletion policy to the EC2 instance resource

<img width="300" alt="3" src="https://github.com/user-attachments/assets/fb2e46d0-2cc3-4327-b2d7-13f95cd97948" />

4. Create a stack on CloudFormation using the language-extensions.yaml template

<img width="955" alt="4" src="https://github.com/user-attachments/assets/9626a936-74d3-40aa-9fe1-948102617541" />

5. Open language-extensions.yaml and add the following code to add a CloudWatch dashboard with CPU utilization data of the EC2 instance

<img width="478" alt="5" src="https://github.com/user-attachments/assets/be32d04c-0bab-492c-84d7-b4fd9c49fbb6" />

6. Update the stack on CloudFormation with the updated template

<img width="950" alt="6" src="https://github.com/user-attachments/assets/9072d766-6fd0-47f1-8f80-43ee143c58d0" />

7. Navigate to CloudWatch to see the Dashboard that was created

<img width="953" alt="7" src="https://github.com/user-attachments/assets/9d739ba5-626e-410d-a470-1def12652e06" />

8. The JSON for the dahboard that matches the YAML in the template

<img width="873" alt="8" src="https://github.com/user-attachments/assets/97173e6d-d3e3-4ec8-aa63-93f858ca3164" />

9. Add the following code to language-extensions-challenge.yaml

<img width="232" alt="10" src="https://github.com/user-attachments/assets/25a681d7-a723-4cbb-9565-7f420b1151fe" />

10. Add the DeletionPolicyParameter to the S3 Resource

<img width="291" alt="11" src="https://github.com/user-attachments/assets/376b05f4-bb53-444e-b8a1-adb45affac45" />

11. Add the following code to add a CloudWatch dashboard

<img width="248" alt="12" src="https://github.com/user-attachments/assets/59450e2b-1056-4331-8b5f-d75264abc93c" />

12. Create a stack on CloudFormation using the language-extensions-challenge.yaml template

<img width="938" alt="13" src="https://github.com/user-attachments/assets/d56f3b25-e9c9-43bd-8c8d-6c3983d99c5c" />

13. Navigate to S3 to see the bucket that was created using the stack

<img width="941" alt="14" src="https://github.com/user-attachments/assets/2df9d012-09ec-45c4-9684-d5ab848920c3" />

14. Navigate to CloudWatch to see the Dashboard that was created

<img width="950" alt="15" src="https://github.com/user-attachments/assets/4dc34a31-f409-48b0-9263-f04089ee7c38" />

15. Clean up resources by deleting both of the stacks


## Looping over collections with Fn::ForEach
The Fn::ForEach intrinsic function allows you to describe resources that share the same/similar configuration, with dynamic iterations that you use to map resource configurations to loop-like structures

1.Open s3-buckets.yaml and add the following code to **Resources** section

<img width="310" alt="1" src="https://github.com/user-attachments/assets/69084f48-fdbb-4760-af95-8e53df19aea9" />

2. Create a stack on CloudFormation using the s3-buckets.yaml template

<img width="959" alt="2" src="https://github.com/user-attachments/assets/09d9a00d-4fcc-406d-8d39-a7e4cd74cda7" />

3. Open vpc.yaml and add the following code to create two public subnets and two private subnets

<img width="310" alt="3" src="https://github.com/user-attachments/assets/5212d556-8348-42c4-8b1d-14520f54829b" />

4. Add the following code to the existing inner loop to create four route tables and associate them to the relevant subnets

<img width="341" alt="4" src="https://github.com/user-attachments/assets/8d627004-573f-4c29-98d5-7f1ee9a458c4" />

5. Add the following code to create 2 AWS::EC2::Route resources for public subnets

<img width="308" alt="5" src="https://github.com/user-attachments/assets/a77a041c-25b4-4d5b-9f22-3e7273da7b65" />

6. Add the following code to create 2 Nat gateways and 2 routes that each Nat gateway will use as a target

<img width="305" alt="6" src="https://github.com/user-attachments/assets/e5081ada-f05b-4e45-aba8-15be1b1f756b" />

7. Create a stack on CloudFormation using the vpc.yaml template

<img width="956" alt="7" src="https://github.com/user-attachments/assets/e3f53078-a3f9-4f7b-b6d1-b5b858893490" />

8. Add the following code to the **Output** section of vpc.yaml

<img width="466" alt="8" src="https://github.com/user-attachments/assets/ad1a949e-5072-4410-bfc8-aa573099c4cd" />

9. Update the stack on CloudFormation using the updated vpc.yaml template

<img width="957" alt="9" src="https://github.com/user-attachments/assets/84c89933-26d8-4929-8208-b055d6ed5ec1" />

10. Clean up resources by deleting the CloudFormation stacks

## Update behaviours of stack resources
CloudFormation updates resources by comparing changes between the updated template you provide, and resource configurations you describedin the previous version of your template. Resource configurations that haven't changed remain unaffected during the update process; otherwise CloudFormation uses one of the following *update behaviours*: **Update with No Interruption, Updates with Some Interruption, and Replacement**, depending on which new property you add, or on which property value you modify, for a given resource type  you describe in your template.

1. Open update-behaviors-of-stack-resources.yaml and add the following code to the *Parameters* section

<img width="449" alt="1" src="https://github.com/user-attachments/assets/50d3e1a6-8e26-4b8a-b6c0-dd998998a795" />

2. Add the following code to create an EC2 instance resource

<img width="230" alt="2" src="https://github.com/user-attachments/assets/38cd9d0a-0a00-4898-9f68-5c0897adb8f2" />

3. Create a stack on CloudFormation using the update-behaviors-of-stack-resources.yaml template

<img width="953" alt="3" src="https://github.com/user-attachments/assets/0b47f21c-08ee-4dc2-8844-1fc26b8b7413" />

4. Update the stack, on the **Parameters** page change the value of the LatestAmiId parameter

<img width="947" alt="5" src="https://github.com/user-attachments/assets/b508b777-f1c4-4ada-8d1d-396506c4da1b" />

5. Navigate to the Amazon EC2 console, on the Instances page a new instance has been launched and the instance created earlier was terminated. This ia happening because when the stack was updated, CloudFormation created a new instance first and deleted the previous one. This is an example of replacement behaviour.

<img width="766" alt="7" src="https://github.com/user-attachments/assets/d4d24f67-a14f-4d33-8eaa-2091fe1f4151" />

6. Update the stack, on the **Parameters** page change the value of the instance size parameter. Navigate to the EC2 console while the stack is updating, the instance will be stopped and once the instance type has been updated it will run again

<img width="760" alt="8" src="https://github.com/user-attachments/assets/ad5d861a-5868-4888-8201-79ebda51d2b8" />

<img width="741" alt="10" src="https://github.com/user-attachments/assets/35261f6b-e16f-4662-bf9d-4a6fa54a70ea" />

7. Add the following code to update-behaviors-of-stack-resources.yaml to specify the Monitoring property definition for the EC2 Instance

<img width="229" alt="9" src="https://github.com/user-attachments/assets/72992ba7-d9d5-4b3f-8ac9-31d8fc8a1e2b" />

8. Update the stack on CloudFormation using the updated template

<img width="950" alt="11" src="https://github.com/user-attachments/assets/8deac807-4d8c-47a8-bd38-830bf369da78" />

9. Update the Value of the Name tag key in update-behaviors-of-stack-resources.yaml

<img width="260" alt="12" src="https://github.com/user-attachments/assets/553a377c-84eb-4575-bf82-13cf717a68f4" />

10. Update the stack on CloudFormation with the updated template

<img width="944" alt="13" src="https://github.com/user-attachments/assets/5c29a8cf-8670-4b70-9b77-f2a88fcff1ab" />

11. The updated Value of the Name Tag

<img width="824" alt="14" src="https://github.com/user-attachments/assets/92c3cbe1-fb5f-4855-8c50-e9e936305531" />

12. Clean up resources by delating the stack



