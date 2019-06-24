# Adding S3 notifications

We use S3 notifications as one of the options to automatically trigger test execution when new data arrives. By doing this, you for example don't have to trigger test execution from e.g. Airflow, or schedule test execution via cron. You can register 
S3 notifications via the procedure below.

Soda can connect from the account it's installed in, to any number of S3 buckets on other accounts (bucket accounts) that you have. In summary:
* The `BucketAccount` is the account where the S3 bucket that you want to monitor is located.
* The `SodaAccount` is the account where Soda (and its metric store) is installed. 

The S3 notification architecture for Soda looks like this:

S3 (`BucketAccount`) -> SNS topic (`BucketAccount`) -> SQS queue (`SodaAccount`) -> Soda app server SQS queue (`SodaAccount`)

Follow the following procedures to set-up Soda S3 notifications:

### Requirements before you start

Before you start, ask Soda the `SQS ARN endpoint` for S3 notifications by contacting support.

### Procedure 1/3: Create SNS topic and register S3 notifications 

In the AWS Management Console, go to the service SNS:
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

### Procedure 2/3: Link S3 notifications to SNS

* Go to the service S3
* Click on a bucket you want notifications for
* Go to properties
* Click on events
* Click on add notification
* Check “All object create events”
* In the Send-to checkbox, choose SNS topic
* Choose your newly created sns topic

### Procedure 3/3: Connect SNS to SQS

• Go SNS
• Click Subscriptions
• enter your topic ARN in the “Topic ARN” textbox
• Select SQS for protocol
• Enter the SQS ARN endpoint (see requirements before you start).

