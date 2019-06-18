# Adding S3 notifications

In order for Soda to get notified of new data arriving on S3 and 
automatically trigger test & metric execution, you can register 
S3 notifications with the procedure below.

There are potential 2 different AWS accounts involved.  
The `BucketAccount` is the account where the S3 bucket is located.
The `SodaAccount` is the account where Soda is installed. 

The architecture for notifications looks like this

S3 (`BucketAccount`) -> SNS topic (`BucketAccount`) -> SQS queue (`SodaAccount`) -> Soda app server SQS queue (`SodaAccount`)

You typically will have to perform the next procedures: 

### Requirements before you start

Before you start, ask Soda the `SQS ARN endpoint` for S3 notifications. 

### Procedure to create SNS topic and register S3 notifications 

In the AWS Management Console, go to the service SNS
* click on topics
* click create topic
* click on access policy
* Enter the following policy
```
{
  "Version": "2008-10-17",
  "Id": "__default_policy_ID",
  "Statement": [
    {
      "Sid": "__default_statement_ID",
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": [
        "SNS:GetTopicAttributes",
        "SNS:SetTopicAttributes",
        "SNS:AddPermission",
        "SNS:RemovePermission",
        "SNS:DeleteTopic",
        "SNS:Subscribe",
        "SNS:ListSubscriptionsByTopic",
        "SNS:Publish",
        "SNS:Receive"
      ],
      "Resource": "arn:aws:sns:AWS_REGION:AWS_ACCOUNT_ID:SNS_TOPIC_NAME",
      "Condition": {
        "StringEquals": {
          "AWS:SourceOwner": "AWS_ACCOUNT_ID"
        }
      }
    }
  ]
}
```

### Procedure to link S3 notifications to SNS

* Go to the service S3
* Click on a bucket you want notifications for
* Go to properties
* Click on events
* Click on add notification
* Check “All object create events”
* In the Send-to checkbox, choose SNS topic
* Choose your newly created sns topic

### Procedure to connect SNS to SQS

• Go SNS
• Click Subscriptions
• enter your topic ARN in the “Topic ARN” textbox
• Select SQS for protocol
• Enter the SQS ARN endpoint that soda will provide you

