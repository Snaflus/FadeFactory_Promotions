# Introduction

This repository is 1 of 5 microservices for the "FadeFactory" exam project in the subject "Development of Large Systems" (DLS)

# Continous deployment

GitHub workflow automatically builds and deploys when main branch is changed

TODO:

Expand unit tests

Terraform infrastructure as code

# Usage and integration

The web app watches for messages in the supplied message queue. Message are expected to be JSON in the following format:
```json
{
    "data": {
        "promotionId": 1,
        "promotionSubject": "HUGE Sale",
        "promotionDescription": "50% off on your next haircut (fades only)",
        "promotionReceivers": [
            {
                "name": "name1",
                "email": "name1@host.com"
            },
            {
                "name": "name2",
                "email": "name2@host.com"
            }
        ]
    }
}
```
If an invalid message is submitted to the message queue the web app will move it to the dead letter queue with the accompanying error code attached.

# Hosting

A Linux Web App is running at: https://fadefactorypromotions.azurewebsites.net/

It connects to a Queue in an Azure Service Bus

As the Web App is running on a cheap (FREE) F1 SKU it needs to be pinged on the address above to be running and consuming the message queue

# Passwords and secrets

Secrets are stored in a oneline Base64 encoded file stored in GitHub secrets.

# Local development

The project is very straight forward to run in a local environment

First set up a local .env file following the format of env_template, then run:

```bash
$ npm install
$ npm run <package.json script>
```
