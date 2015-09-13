### Classes

#### Farmer
CRUD for targets

* `function farmerClient(host, appKey, appSecret)`
  * `function ping()`
  * `function getTargets()`
  * `function createTarget(target)`
  * `function getTarget(targetId)`
  * `function updateTarget(targetId, data)`
  * `function deleteTarget(targetId)`

#### Gateway
Searching of targets

* `function gatewayClient(host, appKey, appSecret)`
  * `function ping()`
  * `function search(image)`
  * `function createTunnel()`
  * `function searchViaTunnel(tunnel, image)`

### Sample usage

#### Add a target represented by an image
```javascript
var farmer = sdk.farmer('http://localhost:8888', 'test_app_key', 'test_app_secret');

farmer.createTarget({
    'egg': 'spam',
    'image': fs.readFileSync('test.jpg').toString('base64')
})
.then(function(resp) {
    console.log(resp.result.targetId);
})
.fail(function(err) {
    console.log(err);
});
```

#### Search a target by an image
```javascript
var gateway = sdk.gateway('http://localhost:8080', 'test_app_key', 'test_app_secret');

gateway.createTunnel()
.then(function(resp) {
    var tunnel = resp.result.tunnel;
    var image = {
        'foo': 'bar',
        'image': fs.readFileSync('test.jpg')
    };
    return gateway.searchViaTunnel(tunnel, image);
})
.then(function(resp) {
    console.log(resp.result.target.targetId);
})
.fail(function(err) {
    console.log(err);
});
```
