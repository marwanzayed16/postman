# postman
a script in postman to add a csrf token automatic to all requset

## token route

```php
Route::get('/token', function () {
    return ['token' => csrf_token()];
});
```

## A pre-requset script
```
pm.sendRequest("http://localhost:8000/token", function (err, response) {
    var data = response.json();

    pm.request.headers.add({
        key: 'X-CSRF-TOKEN',
        value: data.token
    });

    pm.request.headers.add({
        key: 'accept',
        value: "application/json"
    });

    pm.environment.set("csrf", data.token);
});
```
