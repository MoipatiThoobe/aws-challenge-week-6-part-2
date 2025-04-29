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


