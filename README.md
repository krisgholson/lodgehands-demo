# Build a RESTful web service using AWS Lambda, DynamoDB, and the serverless framework

Presented at Lodge Hands September 2019

Based on the example project from serverless here:
https://github.com/serverless/examples/tree/master/aws-node-rest-api-with-dynamodb-and-offline

Prerequisites:
* AWS cli and configuration with key/secret (if actually deploying to an AWS environment)
* Node.js
* serverless framework `npm install -g serverless`

Steps used to initially create this project (not necessary if you just want to check it out and run it):

Created the project from scratch using serverless cli (`serverless` or `sls`)

```bash
sls create --template aws-nodejs --path lodgehands-demo --name lodgehands-demo
cd lodgehands-demo

sls plugin install --name serverless-dynamodb-local
sls plugin install --name serverless-offline

npm install --save uuid
npm install --save-dev aws-sdk
```

Copy in configuration/resources from https://github.com/serverless/examples/tree/master/aws-node-rest-api-with-dynamodb-and-offline to enable the todos handlers and the serverless-offline to work (needs the addition of configuration that is NOT in the examples project) ..

```yaml
    stages:
      - local
```

Once you check out the source and you want to run the demo (locally), then use:

```bash
npm install
sls dynamodb install
sls offline start --stage local
sls dynamodb migrate --stage local
```

If you want to deploy to an AWS environment, then use:

```bash
sls deploy
```

## Usage

You can create, retrieve, update, or delete todos with the following commands:

### Create a Todo

```bash
curl -X POST -H "Content-Type:application/json" http://localhost:3000/todos --data '{ "text": "Learn Serverless" }'
```

Example Result:
```bash
{"text":"Learn Serverless","id":"ee6490d0-aa11e6-9ede-afdfa051af86","createdAt":1479138570824,"checked":false,"updatedAt":1479138570824}%
```

### List all Todos

```bash
curl -H "Content-Type:application/json" http://localhost:3000/todos
```

Example output:
```bash
[{"text":"Deploy my first service","id":"ac90feaa11e6-9ede-afdfa051af86","checked":true,"updatedAt":1479139961304},{"text":"Learn Serverless","id":"206793aa11e6-9ede-afdfa051af86","createdAt":1479139943241,"checked":false,"updatedAt":1479139943241}]%
```

### Get one Todo

```bash
# Replace the <id> part with a real id from your todos table
curl -H "Content-Type:application/json" http://localhost:3000/todos/<id>
```

Example Result:
```bash
{"text":"Learn Serverless","id":"ee6490d0-aa11e6-9ede-afdfa051af86","createdAt":1479138570824,"checked":false,"updatedAt":1479138570824}%
```

### Update a Todo

```bash
# Replace the <id> part with a real id from your todos table
curl -X PUT -H "Content-Type:application/json" http://localhost:3000/todos/<id> --data '{ "text": "Learn Serverless", "checked": true }'
```

Example Result:
```bash
{"text":"Learn Serverless","id":"ee6490d0-aa11e6-9ede-afdfa051af86","createdAt":1479138570824,"checked":true,"updatedAt":1479138570824}%
```

### Delete a Todo

```bash
# Replace the <id> part with a real id from your todos table
curl -X DELETE -H "Content-Type:application/json" http://localhost:3000/todos/<id>
```
