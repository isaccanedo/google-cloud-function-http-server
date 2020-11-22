# :wine_glass: google cloud function http server

Chame seu código de pilha do servidor http usando um ouvinte http na memória. Não são necessários soquetes.

## index.js

```javascript
require('http').createServer((req, res) => {
  if (req.url === '/hello') return res.end('world')
})
.listen(5000)
```

## proxy.js

```javascript
exports.http = require('google-cloud-function-http-server')
require('./index.js')
```

## serverless.yml

```yaml
service: test
provider:
  name: google
  runtime: nodejs8
  project: x
  credentials: ~/.gcloud/keyfile.json

plugins:
  - serverless-google-cloudfunctions

functions:
  proxy:
    environment:
      SERVER_PORT: "5000"
    handler: http
    events:
      - http: path
```

# license

[Apache License, Version 2.0](LICENSE)
