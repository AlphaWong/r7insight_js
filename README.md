le.js
=====

Client-side JavaScript logging library for [InsightOps](https://www.rapid7.com/solutions/it-operations/).

[![Build Status](https://travis-ci.org/rapid7/r7insight_js.png?branch=master)](https://travis-ci.org/rapid7/r7insight_js)

# how to use
```html
<script src="https://raw.githubusercontent.com/rapid7/r7insight_js/0b3a79fca9dc402767bb6be2ca34b1f16cc05051/product/le.js"></script>
<script>
  LE.init({token:'Log token key',region:'us'});
</script>
```

# simple code
```js
import axios from 'axios';

const LOG_TOKEN = process.env.REACT_APP_INSIGHTOPS_API_KEY;
const BASE_URI = 'https://us.js.logs.insight.rapid7.com';
const POST_PATH = '/v1/logs/';

const LOG_LEVEL = {
  LOG: 'LOG',
  WARN: 'WARN',
  ERROR: 'ERROR',
  INFO: 'INFO',
};

const Logger = ({ level, message, data }) => {
  return axios.post(`${BASE_URI}${POST_PATH}${LOG_TOKEN}`, {
    level,
    event: { message, data: JSON.stringify(data) },
  });
};

const log = ({ message, data }) => {
  return Logger({ level: LOG_LEVEL.LOG, message, data });
};

const warm = ({ message, data }) => {
  return Logger({ level: LOG_LEVEL.WARN, message, data });
};

const error = ({ message, data }) => {
  return Logger({ level: LOG_LEVEL.ERROR, message, data });
};

const info = ({ message, data }) => {
  return Logger({ level: LOG_LEVEL.INFO, message, data });
};

export { Logger, LOG_LEVEL, log, warm, error, info };

```

# curl
```console
curl -X POST \
  https://us.js.logs.insight.rapid7.com/v1/logs/xxx-xxx-xxx-xxx-xxx-xxx \
  -H 'Accept: */*' \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Cache-Control: no-cache' \
  -H 'Connection: keep-alive' \
  -H 'Content-Length: 56' \
  -H 'Content-Type: application/json' \
  -H 'Host: us.js.logs.insight.rapid7.com' \
  -H 'User-Agent: PostmanRuntime/7.19.0' \
  -H 'X-Requested-With: XMLHttpRequest' \
  -H 'cache-control: no-cache' \
  -d '{"event":{"message":"123", "data":"321"},"level":"INFO"}'
  
```
