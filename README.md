# aws-health-slack
Holds code for AWS Health Events to Slack Lambda

# What it does
This parses the health feed and uses DynamoDB as checkpoint before sending a message to Slack channel.

# Pre-Requisites:
* Generate a Slack Webhook Token and Store in SSM as `/versent/health/hook`
* This functions required feedparser module and is using layer functionality to use it. You can bundle it with your function as needed. Refer https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html#configuration-layers-path
Only dependency captured in the layet is feedparser.
```
mkdir python
pip install feedparser -t python
zip -r aws-health.zip python
```
Create a Lambda layer using UI or CLI as needed and reference it in the CF Template.

# Operation
* It scraps the http://status.aws.amazon.com/rss/
* It checks the service and the message in the DynamoDB table.
* If its a different Key Value Pair combo, a message is sent to Slack.
* It then updates the DynamoDB Table with Service Name and current Message.
* If its same Key Value combination (service-message), nothing happens.

# Result

![Profit](/sample.png)

