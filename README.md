# aws-health-slack
Holds code for AWS Health Events to Slack Lambda

# Pre-Requisites:
* Generate a Slack Webhook Token and Store in SSM as `/versent/health/hook`
* This functions required feedparser module and is using layer functionality to use it. You can bundle it with your function as needed. Refer https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html#configuration-layers-path
Only dependency captured in the layet is feedparser.
`
mkdir python
pip install feedparser -t python
zip -r aws-health.zip python
`
Create a layer using UI or CLI as needed.

# Operation
It scraps the http://status.aws.amazon.com/rss/
Updated the DynamoDB Table with Service Name and Message.
If its new message or new Service, an update is sent to Slack.
If its same service and same message, nothing happens.

