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

1) https://ec2.us-east-1.amazonaws.com/?Action=DescribeInstances&Filter.1.Name=instance-id&Filter.1.Value={Value Below}&Version=2016-11-15

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
	* 
