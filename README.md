# AWS ES Connection

AWS ES connection for the new opensearch client (@opensearch-project/opensearch)

## Usage
 Javascript:
```js
const { Client } = require('@opensearch-project/opensearch')
const { createAWSConnection, awsGetCredentials } = require('@acuris/aws-es-connection')

const awsCredentials = await awsGetCredentials()
const AWSConnection = createAWSConnection(awsCredentials)
const client = new Client({
  ...AWSConnection,
  node: 'https://node-name.eu-west-1.es.amazonaws.com'
})

// inside async func
await client.cat.help()
```

 Typescript:
```ts
import { createAWSConnection, awsGetCredentials } from '@acuris/aws-es-connection'
import AWS from 'aws-sdk'
import { Client } from '@opensearch-project/opensearch'

const awsCredentials = await awsGetCredentials()
const AWSConnection = createAWSConnection(awsCredentials)
const client = new Client({
  ...AWSConnection,
  node: 'https://node-name.eu-west-1.es.amazonaws.com'
})

// inside async func
await client.cat.help()
```

## How does it work?
This package creates a Connection class that signs the requests to AWS opensearch and a Transport class that checks that the AWS credentials haven't expired before every call, and refreshes them when needed.

## Developer notes

### Running the tests.
Make sure that your AWS credentials are available to your env, for example you could set them in your ENV.

You need a running AWS ES instance for the tests to run against. Set the endpoint URL as the env `AWS_ES_ENDPOINT`.

```
AWS_ES_ENDPOINT=https://xxxx.es.amazonaws.com npm test
```
### Tested versions
This package has been tested on versions of the official opensearch client up to 7.13.0. 