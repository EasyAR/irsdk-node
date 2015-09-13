### Samples

#### Add search target
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

#### Search target
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
