# Emojibot

Learning AWS Lambda on Node.js.

## Getting started

* [Create an AWS account](https://aws.amazon.com/free/) if haven't got one already
* [Install Serverless](https://serverless.com/framework/docs/providers/aws/guide/installation/) and [configure your AWS credentials](https://serverless.com/framework/docs/providers/aws/guide/credentials/)
* [Create your Slack app](https://api.slack.com/slack-apps#create-app) and configure its credentials by creating a `local.yml` file:

	```
	# Local variables -- DO NOT COMMIT!
	
	dev:
	  slack:
	    clientId: "<Your Dev Slack App Client ID>"
	    clientSecret: <Your Dev Slack App Client Secret>
	
	production:
	  slack:
	    clientId: "<Your Production Slack App Client ID>"
	    clientSecret: <Your Production Slack App Client Secret>
	```

  Note that the client id must be quoted otherwise it is interpreted as a number. Do not commit this file. It is already Git ignored.
* Deploy the server to AWS Lambda:

	```
	npm install
	serverless deploy
	```

  Make a note of the endpoints output once it has deployed, e.g.:
  
	```
	endpoints:
	  GET - https://ab12cd34ef.execute-api.eu-west-1.amazonaws.com/dev/install
	  GET - https://ab12cd34ef.execute-api.eu-west-1.amazonaws.com/dev/authorized
	  POST - https://ab12cd34ef.execute-api.eu-west-1.amazonaws.com/dev/event
	```
	
* Go to your [Slack app](https://api.slack.com/apps) settings and update them to point to your server:
  * Select 'OAuth & Permissions' and under 'Redirect URLs' add the `authorized` endpoint
  * Select 'Event Subscriptions' and:
    * Turn on 'Enable Events'
    * In the 'Request URL' box paste the `event` endpoint
    * Under 'Subscribe to Bot Events' add bot user events for:
      * `message.channels`
      * `message.groups`
      * `message.im`
      * `message.mpim`
  * Select 'Bot Users' and add a bot user

* Finally, install your Slack app by visiting your `install` endpoint and clicking the 'Add to Slack' button

## See also

* Blog: [Building a serverless chatbot on AWS Lambda](https://www.blackpepper.co.uk/blog/creating-a-serverless-slack-bot-on-aws-lambda)
