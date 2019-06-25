# Receive Message From Twilio

This example shows how easy it is,  to receive Incoming SMS visa Twilio using webMethods.io and send it as email to other interested parties. This functionality can be used for receiving alerts, status via SMS and updating other IT systems. It can be used for Lead generation, creating tickets in ServiceNow etc.

## Prerequisite

Twilio account with at least one phone numver to receive and send SMS.


## Setup

1. Go ahead and get started creating a blank workflow. If you need a refresher on how to get to this point, this [guide](https://docs.webmethods.io/workflow-building-blocks/creating-first-workflow) can be a great introduction. Your starting point should resemble ![this](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/Creating_First_Workflow.png)

2. The Webhook is created by modifying the start icon, which is is the entrypoint to the new flow. Please select the gear on top of the start icon to access settings. Once settings is selected in the start icon, a 'trigger' dialog will appear that allows Webhook to be selected.![trigger](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/trigger.png) 

3. Leave Webhook Authentication unchecked. Check/Enable Webhook Payload, add the structure of the input payload into the "Body" text area and click next. Note the webhook url and save this for later. As a best practice, Authentication should be added immedately after flow ("Call AWS Lambda Directly") is working ![webhook](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/webhook.png)  ![webhookpayload](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/webhook_payload.png) 

4. Select done once presented with the final dialog. You should now see the start arrow dialog replaced with a webhook icon. ![webhookconfigured](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/webhookconfigured.png)


5. Now the flow is ready to process, once the webhook receives the request. In the search dialog lookup "Amazon" service and select "Amazon Web Services" service, drag and drop it into the flow canvas. ![awsservice](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/aws_service.png) Connect the arrows from start to the email icon and then to the end icon. This inserts the 'Amazon web services' step in the flow. 

6. Connect the start step to 'Amazon web services' step. Also connect from 'Amazon webservices' to the stop step. ![invokeawsservice](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/invoke_aws_service.png)

7. Configure the "Amazon webservices" step by clicking the gear icon in the step. Select action as "Lambda Invoke function". Give it a name (ie the step name) as "Lambda Invoke Function". Optional, Please take a look at all the actions supported by the service, which includes calling "Execute Lambda Function via API Gateway". Click + icon next to "Connect to Amazon Webservices" drop down and configure the account credentials to connect to AWS instance. ![awsconnectionconfig](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/aws_connection_config.png). Note - if you had already configured the AWS credentials, just reuse it by selecting from "Connect to Amazon Webservices" drop down.

8. Configure the AWS credentials. You will use AWS access key ID and access key to connect to AWS instance in this screen. ![awsserviceaccountinfo](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/aws_service_account_info.png) Click Add to close the window and go back to  configure "Amazon websservices "Lambda Invoke function" window. Click "Next" 

9. In the Mapping screen, add the AWS Region for the function, provide exact name of the Lambda function you would like to call in AWS and  input data to functions arguments. ![awsservicemapping](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/aws_service_mapping.png) Click Next and complete the form. The resulting flow will look like as below. ![finalflow](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/final_flow.png)The flow is now ready for testng in the webMethods.io UI

10. To make this a flow a useful Rest API, you need to return a response. This can be performed by adding a "Return Data on Sync Webhook" service step. In order to do this, in the search dialog lookup "Return" service and select  "Return Data on Sync Webhook" service, drag and drop into the flow canvas. ![returnresponse](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/return_webhook.png) The resulting flow will look like as below ![returnresponselinked](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/return_webhook_linked.png) 

11.Configure the "Return Data on Sync Webhook" service by clicking on the gear icon on the service step, give it a name and click next

12. In this page map the response status code from Lambda function to Response data of the "Return Data on Sync Webhook" service. ![returnwebhookmapped](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/return_webhook_mapped.png)

13. The flow is now ready to test as a Rest API from an external tool like Postman. Please make sure to grab the exposed Rest URL from the Webhook URL field in the first flow step(webhook) and use it as the Rest API URL. ![restcall](https://github.com/flyondeals/webmethodsio-examples/blob/master/aws-lamda/rest.png)
