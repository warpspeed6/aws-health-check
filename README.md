# aws-health-slack
Holds code and Cloudformation Teamplate for AWS Health Events to Slack Lambda Function. 

# What it does
This parses the health feed and uses DynamoDB as checkpoint before sending a message to Slack channel.

# Pre-Requisites 
* Generate a Slack Webhook Token and Store in SSM as `/company/health/hook` or a parameter of your choice. Check this link for generating Slack Webhook https://api.slack.com/incoming-webhooks
* This functions required feedparser module to scrape the RSS feed and is using layer functionality to reduce the bundled size.
* You can bundle it with your function as needed. Refer https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html#configuration-layers-path
* Only dependency captured in the layer is feedparser.

# What you should know
* You could use sam or any other choice of tooling. I really wanted to learn about lambda layers and took this work as a challenge but feel free to submit a PR and polish it.
* I understand I can handle exceptions better. :smile:

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

