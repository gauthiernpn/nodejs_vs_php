# Node.JS vs PHP + Express vs Laravel

#### Test machine:
- MacBook Pro (13 inch, late 2012)
- 2.9GHz Intel Core i7
- RAM 16GB 1333MHz DDR3
- HDD 1TB

- Server: nginx/1.10.0
- PHP 7.0.7
- Node 6.5.0

#### Test Conditions
- Duration: 5s
- Threads: 10
- Connections: 5000

```php
Node.js
wrk -d5s -t10 -c5000 http://localhost:3000

Laravel
wrk -d5s -t10 -c5000 http://laravel.dev
```

```php
/**
 * Test results:
 * | Subject                      | Requests/sec  | Data/sec   | Avg. Response |
 * -----------------------------------------------------------------------------
 * | Pure Node.js(Multi Thread)   | 20,873.34     | 3.09MB     | 11.40ms       |
 * | Pure Node.js(Single Thread)  | 10,375.05     | 1.53MB     | 22.70ms       |
 * | Express(JS, Multi Thread)    | 3,426.94      | 779.76KB   | 68.92ms       |
 * | Express(JS, Single Thread)   | 2,386.69      | 543.06KB   | 97.97ms       |
 * | Pure PHP(Multi Thread)       | 3,147.95      | 667.17KB   | 23.28ms       |
 * | Laravel(PHP, Multi Thread)   | 26.23         | 101.44KB   | 392.64ms      |
 * -----------------------------------------------------------------------------
 */
```

## Test Source Code

####Pure Node.js(multi- and single-thread)

```javascript
var server = http.createServer(function (request, response) {
        if (request.method == "GET") {
            response.writeHead(200, {'Content-Type': 'text/html'});
            response.write('Hello worlds');
            response.end();
        }
    });
server.listen(3000);
```

####Express(multi- and single-threaded)
```javascript
router.get('/', function (req, res, next) {
    res.send('Hello World');
});
```


#### Pure PHP
```php
echo "Hello world";
```


#### Laravel
```php
Route::get('/', function () {
    return 'Hello World';
});
```




