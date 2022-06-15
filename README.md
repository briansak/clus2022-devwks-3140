## DEVWKS-3140 <br /> Using SecureX orchestration for Automating Public Cloud Incident Response and Remediation

### Lab Environment: https://dcloud.cisco.com/expo/8siwn1lhagtjgyduf33tv7fpn
> **Right-click and open in a new INCOGNITO MODE/PRIVATE WINDOW**

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

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173708449-fbad4207-16f6-488c-860f-1fdceeed8fc5.png">

2) Drag AWS Service --> Generic AWS API Request to the canvas

<img width="1441" alt="image" src="https://user-images.githubusercontent.com/10421515/173708677-0a6d9e16-1661-421d-b23f-1cdc71f78044.png">

3) Name the activity **Query EC2 Instance** in the activity Display Name
4) Override the workflow target with: **AWS_Target**

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173708851-fde409ab-e0ae-43b1-b36a-f3e0054896ad.png">

5) Specify the URL near the bottom of the activity properties with:

```
https://ec2.us-east-1.amazonaws.com/?Action=DescribeInstances&Filter.1.Name=private-ip-address&Filter.1.Value={Value_Below}&Version=2016-11-15
```
Replacing "{Value_Below}" with the IP address associated with your pod in the table below and set the API Method to **GET**.

Pod 1: 172.31.31.233 <br />
Pod 2: 172.31.22.192 <br />
Pod 3: 172.31.19.34 <br />
Pod 4: 172.31.28.79 <br />
Pod 5: 172.31.27.52 <br />
Pod 6: 172.31.31.163 <br />
Pod 7: 172.31.92.122 <br />
Pod 8: 172.31.85.153 <br />
Pod 9: 172.31.91.202 <br />
Pod 10: 172.31.83.165 <br />
Pod 11: 172.31.88.102 <br />
Pod 12: 172.31.84.240 <br />

<img width="589" alt="image" src="https://user-images.githubusercontent.com/10421515/173710456-a0f3eff7-9b4a-4c71-8db8-505aeb3bb501.png">

6) Click on the "Start" element in the workflow and customize the workflow "Display Name" to **Pod # - Query EC2 Instance**

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173709384-ae518382-8d55-4652-a63e-637976a9568a.png">

7. Validate and Run this workflow near the top of the canvas.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173709797-50d88ba1-9abc-4593-831d-5b08ccc66120.png">

After running this activity, you should see the details of the instance that you queried in the output body.

<img width="568" alt="image" src="https://user-images.githubusercontent.com/10421515/172463129-832578dd-6891-49f4-8d85-201fbac1179a.png">

### Importing a workflow from Github

> **SHARED ENVIRONMENT ALERT** <br />
> Make sure you uniquely name your workflow after importing!

1) Click back to Workflows and choose the **Import** button.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173710672-bd66daf1-d85d-4586-880c-3007e300f821.png">

2) Choose, Import from **Git**, **DEVWKS-3140 Repo** for Git Repository, **sxo-aws-ir** for File Name, **Updated Keys** for Git Version, and finally **Import as a New Workflow** and click **Import**.

<img width="607" alt="image" src="https://user-images.githubusercontent.com/10421515/173711084-8e9b0220-ee98-4ed0-b482-e52b86f11489.png">

3) After importing, it will show up as **Copy(1)-AWS Incident Response**.  Open this newly created workflow.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173711264-43a14855-cc98-45f9-85c6-b1c559343c77.png">

2) Open your new workflow and make the following changes: <br />

* Name your workflow **Pod X - AWS Incident Response** replacing the pod number with yours.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173711715-1849e6ac-150d-4a34-9e1e-dbb02ea800fe.png">

* Replace the variable for 'observable_value' to match your pod above.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173711852-8d854b7a-7017-4b46-b7cd-3f9abcdd5baf.png">

Note the activites in this workflow that automate many of the steps outlined in the AWS EC2 Incident Response Guide.

> * Enables Termination Protection on the instance
> * Sets a restricted Security Group limiting access
> * Removes it from any Auto Scaling Groups
> * Removes it from any Elastic Load Balancers
> * Snapshots connected Elastic Block Storage devices
> * Tags the instance with IR details

2) Run your imported workflow.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173712097-05b9094c-e06f-422f-aadf-c88a004e4e52.png">

4) Return to your previously created workflow **Query EC2 Instance** that pulls instance details.
5) Note the differences to your instance.

### Integration with SecureX threat response

1) Click **Dashboard** at the top of the SecureX Window to exit out of the Orchestration tool.

2) Expand the **Ribbon** at the bottom of the screen to see created casebooks and incidents for this environment.
3) Find the **DEVWKS-3140 Casebook** Casebook created "By Others" by searching for 'DEVWKS' in the casebook pane.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173712877-c8889a14-392b-4454-8012-03f7b4002c5d.png">

4) Click **Investigate in Threat Response** located on the right-hand side of the Casebook drawer.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173712656-c4778e87-3b3d-4962-99b7-701186aef572.png">

This will open up a new browser window that contains the results of our investigation into one domain and the AWS internal IP addresses from our lab.

Once the enrichment of the observables is complete, you should see your IP address denoted as a 'target' in the resulting graph.

<img width="1398" alt="image" src="https://user-images.githubusercontent.com/10421515/167261531-68659cca-c8b5-4f04-b320-221f9afc36e1.png">

5) Use the drop-down to show the SecureX orchestration response actions that can be ran against this host, including the one you imported and uniquely named.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173713168-a4a55394-ef21-4d51-bb2b-b8939234ca58.png">
