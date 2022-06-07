## DEVWKS-3140 <br /> Using SecureX orchestration for Automating Public Cloud Incident Response and Remediation

### Lab Environment: https://dcloud.cisco.com/expo/8siwn1lhagtjgyduf33tv7fpn
<img width="472" alt="image" src="https://user-images.githubusercontent.com/10421515/167255166-77d523d5-737d-4bce-a6ba-8e09d39750c6.png">

_**IaaS API Documentation**_ <br />
AWS: https://docs.aws.amazon.com <br />
GCP: https://cloud.google.com/compute/docs/reference/rest/v1 <br />
Azure: https://docs.microsoft.com/en-us/rest/api/azure <br />

### Creating Your First AWS Activity

> **SHARED ENVIRONMENT ALERT** <br />
> Make sure you uniquely name your workflow when creating!

API Reference: https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInstances.html

Create a new activity that will provide the details of an EC2 instance, following the example presented.

1) Create a **New Workflow**
2) Drag AWS Service --> Generic AWS API Request to the canvas

<img width="458" alt="image" src="https://user-images.githubusercontent.com/10421515/172461098-a35c7d45-981b-4d25-a4fb-b30778a09e2b.png">

3) Name the activity **Query EC2 Instance** in the activity Display Name

<img width="156" alt="image" src="https://user-images.githubusercontent.com/10421515/172461171-c7ca628e-90ad-4cd2-9570-fc21309eb703.png">

4) Override the workflow target with: **AWS_Target**

<img width="170" alt="image" src="https://user-images.githubusercontent.com/10421515/172462522-b3bd48ac-1bff-40b2-9048-4daae961d370.png">

5) Specify the URL near the bottom of the activity properties with:
> https://ec2.us-east-1.amazonaws.com/?Action=DescribeInstances&Filter.1.Name=instance-id&Filter.1.Value={Value_Below}&Version=2016-11-15 <br /> <br />
Replacing "{Value_Below}" with the IP address associated with your pod in the table below.

Pod 1: 172.31.31.233 <br />
Pod 2: 172.31.22.192 <br />
Pod 3: 172.31.19.34 <br />
Pod 4: 172.31.28.79 <br />
Pod 5: 172.31.27.52 <br />
Pod 6: 172.31.31.163 <br />
Pod 7: <br />
Pod 8: <br />
Pod 9: <br />
Pod 10: <br />
Pod 11: <br />
Pod 12: <br />

<img width="574" alt="image" src="https://user-images.githubusercontent.com/10421515/172463557-1f4a9652-d0b0-49d8-b7df-9feaad200395.png">

6) Click on the "Start" element in the workflow and customize the workflow "Display Name" to **Query EC2 Instance -- [your name]**

<img width="519" alt="image" src="https://user-images.githubusercontent.com/10421515/172464069-004d0fca-b2e1-4395-88cf-0a371b8ddeb8.png">

After running this activity, you should see the details of the instance that you queried in the output body.

<img width="568" alt="image" src="https://user-images.githubusercontent.com/10421515/172463129-832578dd-6891-49f4-8d85-201fbac1179a.png">

### Importing a workflow from Github

> **SHARED ENVIRONMENT ALERT** <br />
> Make sure you uniquely name your workflow after importing!

1) Open your new workflow and make the following changes: <br />
	* Replace the variable for 'observable_value' to match your pod above.
	* Verify the target is set to 'AWS_Target' at the workflow level
	* Verify the workflow is defined as a Response workflow

<img width="571" alt="image" src="https://user-images.githubusercontent.com/10421515/167260694-43250513-e132-48bf-bbb8-740c023a13cb.png">

Note the activites in this workflow that automate many of the steps outlined in the AWS EC2 Incident Response Guide.

> * Enables Termination Protection on the instance
> * Sets a restricted Security Group limiting access
> * Removes it from any Auto Scaling Groups
> * Removes it from any Elastic Load Balancers
> * Snapshots connected Elastic Block Storage devices
> * Tags the instance with IR details

2) Run your imported workflow.
3) Return to your previously created workflow **Query EC2 Instance** that pulls instance details.
4) Note the differences to your instance.

### Integration with SecureX threat response

1) Click **Dashboard** at the top of the SecureX Window to exit out of the Orchestration tool.
2) Expand the **Ribbon** at the bottom of the screen to see created casebooks and incidents for this environment.
3) Find the **DEVWKS-3140** Casebook created "By Others" by searching for '3140' in the casebook pane.

<img width="705" alt="image" src="https://user-images.githubusercontent.com/10421515/172470194-b99a5776-7c1d-43f3-8b55-434f2b7ee5f7.png">

4) Click **Investigate in Threat Response** located on the right-hand side of the Casebook drawer.

<img width="481" alt="image" src="https://user-images.githubusercontent.com/10421515/172470596-621aea40-313a-4f1b-8d4b-529e0bf7c6c9.png">

This will open up a new browser window that contains the results of our investigation into one domain and the AWS internal IP addresses from our lab.

Once the enrichment of the observables is complete, you should see your IP address denoted as a 'target' in the resulting graph.

<img width="1398" alt="image" src="https://user-images.githubusercontent.com/10421515/167261531-68659cca-c8b5-4f04-b320-221f9afc36e1.png">

5) Use the drop-down to show the SecureX orchestration response actions that can be ran against this host, including the one you imported and uniquely named.

<img width="484" alt="image" src="https://user-images.githubusercontent.com/10421515/167261584-3b5fca36-71c0-44c3-bee5-423067f8c7f5.png">


