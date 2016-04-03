# recommendationRaccoon (raccoon)

``` bash
npm install raccoon-azure-connect --save
```

+usage
``` js
raccoon.connect(6379,'<name>.redis.cache.windows.net', '<key>');
//it works
```




I changed connect function because it could not connect on azure redis.
It did not work with auth
``` js
raccoon.connect(6379,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});
//it is not work
```

in library
``` js
Raccoon.prototype.connect = function(port, url, auth){
  port = port || 6379;
  url = url || '127.0.0.1';
  auth = auth || '';

  client = redis.createClient(port, url);
  if (auth){
    client.auth(auth, function (err) {
     if (err) { throw err; }
    });
  }
};
```


i changed connect function with
``` js
Raccoon.prototype.connect = function(_port, hostName, key){
  port = _port || 6379;
  url = hostName;
  auth = {auth_pass:key, tls: {servername: hostName}};
  client = redis.createClient(port, url, auth);
};
```

finally connect like this
``` js
raccoon.connect(6379,'<name>.redis.cache.windows.net', '<key>');
//it works
```

## Links
+ origin raccoon libray url: <a href="https://github.com/guymorita/recommendationRaccoon" target="_blank">https://github.com/guymorita/recommendationRaccoon</a>
+ azure connection : <a href="https://azure.microsoft.com/en-us/documentation/articles/cache-nodejs-get-started/" target="_blank">https://azure.microsoft.com/en-us/documentation/articles/cache-nodejs-get-started/</a>
+ contact : <a href="http://altamirasoft.com" target="_blank">http://altamirasoft.com</a>
