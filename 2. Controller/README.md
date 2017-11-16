# Controller
In den Controllern schreiben wir die ganze Logik der Applikation, wo wir dann die Daten in die View übergeben.
Wir haben also diese Route:
```php
Route::get('product/{id}', 'ProductDetailController@index');
```
Wir rufen also den `ProductDetailController` auf und führen die Funktion `index` aus.
Einen neuen Controller kann man mit der Konsole erstellen, indem man folgendes eingibt:
```
php artisan make:controller ProductDetailController
```  
Dieser Befehl erstellt im `app/Http/Controllers` die Datei `PostDetailController.php`. Die sieht dann so aus.
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class ProductDetailController extends Controller
{
    //
}

```

Hier kann man dann die Funktion `index` schreiben.
```php
public function index($id) {
    return $id;
}
```
Wie man sieht, kann man dem Controller auch diese parameter übergeben.
Wenn man nun eine View returnen möchte, kann man das so machen.
```php
public function index($id) {
    $data = [
        'title' => 'Produktdetailseite'
        'id' => $id
    ];

    return view('pages.product_detail', $data);
}
```
Es wird also die Blade View 'product_detail' aufgerufen, welche sich im resources/views/pages/ Verzeichnis befindet. Dieser View kann man dann als zweiten Parameter in der Funktion ein Array übermitteln, mit Daten, die im Controller generiert wurden.
