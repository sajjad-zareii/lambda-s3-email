# lambda-s3-email
# AWS Lambda: S3 Event to SES Email Notification.

This project demonstrates how to use an AWS Lambda function to send an email via Amazon SES (Simple Email Service). The email content includes event data, making it useful for alerting or notifying based on triggers such as S3 bucket events.

## Features
- Sends an HTML email using Amazon SES.
- Reads sender and recipient email addresses from environment variables.
- Logs the SES response for tracking email delivery.

## Prerequisites
1. **AWS SES Setup**:
   - Verify the sender and recipient email addresses in SES.
   - Ensure your SES account is out of the sandbox or the recipient email is verified.
2. **IAM Role**:
   - Attach a policy to the Lambda execution role with permissions for SES (`ses:SendEmail`).
3. **Environment Variables**:
   - `from_email`: Verified SES email address as the sender.
   - `to_email`: Verified SES email address as the recipient.

## Deployment
1. Create a Lambda function in the AWS Management Console.
2. Copy the contents of `processS3andSendEmail.py` into the Lambda editor or upload it as a ZIP file.
3. Set the following environment variables in the Lambda configuration:
   - `from_email`
   - `to_email`
4. Test the function using a sample event to ensure the email is sent successfully.

## Example Usage
The Lambda function can be triggered by events such as an S3 file upload. The event payload is included in the email body for contextual information. 

### Example Email
```html
<html>
<body>
<h2>Email from AWS SES!</h2>
<br/>
{ "Records": [ { "eventName": "ObjectCreated:Put", "bucket": "example-bucket", "key": "example-key" } ] }
</body>
</html>
```

## Code Explanation
The function:
1. Reads the sender and recipient email addresses from environment variables.
2. Constructs an HTML email body containing the event data.
3. Sends the email using the SES `send_email` API.
4. Logs the response, including the SES message ID.

## Logging
Check the Lambda function logs in Amazon CloudWatch for SES response IDs and debug information.
