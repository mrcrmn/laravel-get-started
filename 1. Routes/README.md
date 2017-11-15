# Routes
Jetzt geht's los. In der `routes/web.php` Datei geht es quasi los. Hier können wir die Routen eintragen auf die Laravel reagieren soll. Das ganze sieht so z.B. so aus.
```php
Route::get('product/{id}', function($id) {
    return view('product_detail', $id);
});
```

Wenn wir num im Browser `localhost/product/1` eingeben, wird diese Route aufgerufen und die Funktion ausgeführt.
Wie man sieht, kann man auch mit '{}' einen Parameter mitgeben.
Folgende Methoden stehen zur Verfügung: 
```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```
Besser wäre aber folgendes:
```php
Route::get('product/{id}', 'ProductDetailController@index');
```
Dazu aber mehr im nächsten Kapitel ;)
