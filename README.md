Based on the example project from serverless here:
https://github.com/serverless/examples/tree/master/aws-node-rest-api-with-dynamodb-and-offline


```bash
sls create --template aws-nodejs --path lodgehands-demo --name lodgehands-demo
cd lodgehands-demo

serverless plugin install --name serverless-dynamodb-local
serverless plugin install --name serverless-offline

npm install --save uuid
npm install --save-dev aws-sdk

# copy in configuration/resources from https://github.com/serverless/examples/tree/master/aws-node-rest-api-with-dynamodb-and-offline
# to enable the todos handlers and the serverless-offline to work

npm install
serverless dynamodb install
serverless offline start --stage local
serverless dynamodb migrate --stage local

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

## Testing
https://serverless.com/blog/unit-testing-nodejs-serverless-jest/
https://serverless.com/blog/how-test-serverless-applications/


