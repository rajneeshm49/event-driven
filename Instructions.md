# Simple Event-Driven App

1. Create the DynamoDB Table:

- Name: ProductVisits
- Partition key: ProductVisitKey

2. Create the SQS Queue:

- Name: ProductVisitsDataQueue
- Type: Standard

**_Note the Queue URL_**

3. Create the Lambda function

- Name: Simple-App-Function
- Runtime: Python 3.9
- Role: create new role from templates
- Role name: simple-app-role
- Add policy templates: `Simple microservice permissions` and `Amazon SQS poller permissions`
- Code: Copy / paste the code from the `simple-app-function.py` file

4. Go to the SQS queue to configure the trigger
5. Select "Lambda triggers" and configure a trigger for the Lambda function
6. Open AWS CloudShell for testing the app
7. Upload the `message-body.zip` file to CloudShell and unzip it
8. Use `ls` and make sure you can see the `message-body-x.json` files
9. Run the following AWS CLI Command for each command, making sure yo modify the queue URL and message body file names

```bash
aws sqs send-message --queue-url https://sqs.us-east-1.amazonaws.com/682755029646/ProductVisitsDataQueue --message-body file://message-body-1.json
```

10. In DynamoDB use the "Explore items" menu item and select the table. You should be able to see the product orders in the table

1) Run the cloudformation
2) Go to cloudshell and send the messages to sqs using above command
3) Now SQS should trigger lambda function and lambda function will process and insert the SQS message details in Dynamo
