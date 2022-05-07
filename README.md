## DEVWKS-3140 <br /> Using SecureX orchestration for Automating Public Cloud Incident Response and Remediation

### Lab Environment: https://dcloud.cisco.com/expo/8siwn1lhagtjgyduf33tv7fpn
<img width="472" alt="image" src="https://user-images.githubusercontent.com/10421515/167255166-77d523d5-737d-4bce-a6ba-8e09d39750c6.png">

_**IaaS API Documentation**_ <br />
AWS: https://docs.aws.amazon.com <br />
GCP: https://cloud.google.com/compute/docs/reference/rest/v1 <br />
Azure: https://docs.microsoft.com/en-us/rest/api/azure <br />

_**Creating Your First AWS Activity**_

> **SHARED ENVIRONMENT ALERT** <br />
> Make sure you uniquely name your workflow when creating!

API Reference: https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInstances.html

1) https://ec2.us-east-1.amazonaws.com/?Action=DescribeInstances&Filter.1.Name=instance-id&Filter.1.Value={Value_Below}&Version=2016-11-15

Pod 1: 172.31.31.233 <br />
Pod 2: 172.31.22.192 <br />
Pod 3: 172.31.19.34 <br />
Pod 4: 172.31.28.79 <br />
Pod 5: <br />
Pod 6: <br />
Pod 7: <br />
Pod 8: <br />
Pod 9: <br />
Pod 10: <br />
Pod 11: <br />
Pod 12: <br />

_**Importing a workflow from Github**_

> **SHARED ENVIRONMENT ALERT** <br />
> Make sure you uniquely name your workflow after importing!

1) Open your new workflow and make the following changes: <br />
	* Replace the variable for 'observable_value' to match your pod above.
	* Verify the target is set to 'AWS_Target' at the workflow level
	* Verify the workflow is defined as a Response workflow

<img width="571" alt="image" src="https://user-images.githubusercontent.com/10421515/167260694-43250513-e132-48bf-bbb8-740c023a13cb.png">

Note the activites in this workflow that automate many of the steps outlined in the AWS EC2 Incident Response Guide.

1) Enables Termination Protection on the instance
2) Sets a restricted Security Group limiting access
3) Removes it from any Auto Scaling Groups
4) Removes it from any Elastic Load Balancers
5) Snapshots connected Elastic Block Storage devices
6) Tags the instance with IR details

Run your imported workflow. 

Return to your created workflow that pulls instance details.

Note the differences to your instance.

_**Integration with SecureX threat response**_

<img width="1398" alt="image" src="https://user-images.githubusercontent.com/10421515/167261531-68659cca-c8b5-4f04-b320-221f9afc36e1.png">

<img width="484" alt="image" src="https://user-images.githubusercontent.com/10421515/167261584-3b5fca36-71c0-44c3-bee5-423067f8c7f5.png">


