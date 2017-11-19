# Eloquent
Models represäntieren die Daten unserer App. Mit folgendem Befehl können wir ein ein neues Model erstellen:
```
php artisan make:model Model
```
Fügen wir in dem Befehl das `-m` flag am Ende hinzu, wird gleichzeitig auch eine Datenbank Migration erstellt. Dazu aber später mehr.
### Ein Model erstellen
Um ein neues Model zu erstellen gibt es mehrere Möglichkeiten, hier ein Beispiel: Wir haben ein Model namens "Post", in dem der Titel, der Body-Text und der name des Authors eines Blogposts gespeichert wird. 
In unserer `Route::post('post/new', PostController@create)` Route wird der Controller aufgerufen. Hier brauchen wir erst einmal ganz oben die Zeile `use App\Post;`, damit wir das Model in dem Controller benutzen können. Die Funktion an sich könnte so aussehen:
```php
public function create(Request $request)
{   
    // Zuerst erstellen wir ein neues Model dieser Art.
    $post = new Post;

    // Dann füttern wir es mit Daten aus dem POST Request.
    $post->title = $request->title;
    $post->body = $request->body;
    $post->author = $request->author;

    // Jetzt schreiben wir die neue Zeile in die Datenbank.
    $post->save();

    // Oder so:
    $post = Post::create([
        'title' => $request->title,
        'body' => $request->body,
        'author' => $request->author
    ]);
}
```
Wenn wir mit User-generierten Daten arbeiten, sollten wir den Input vorher validieren, das ist ein Thema für sich, mit laravel jedoch auch super einfach.
### Model Daten bekommen
Um nun ein Model, welches in der Datenbank steht zu bekommen, steht uns ebenfalls die Eloquent API zur Verfügung.
```php
public function get()
{
    $posts = Post::where('author', 'Peter Lustig')->orderBy('created_at', 'DESC)->limit(10)->get();
}
```
Eloquent macht es sehr einfach komplexe Datenbankqueries zu erstellen und mit unserer App zu interagieren. Jetzt wo wir unsere Posts haben, könnte das Blade Template unfegähr so aussehen:
```php
@foreach($posts as $post)
<div class="post">
    <h3>{{ $post->title }}</h3>
    <small>von {{ $post->author }}</small>
    <p>{{ $post->body }}</p>
</div>
@endforeach
```
### Eloquent API
Hier einmal eine nette Liste von nützlichen Funktionen.
#### Model::find($integer)
Mit find() geben wir eine ID an und bekommen einen einzigen Eintrag aus der Datenbank.
#### Model::all()
Mit all() bekommen wir alle Einträge.
#### Model::get()
Mit get() bekommen wir alle Einträge aus der aktuellen Query.
#### Model::count()
Damit bekommen wir die Anzahl der Zeilen aus der aktuellen Query
#### Model::where($column, $operator, $value)
Damit können wir Models filtern, der $operator ist optional und per default ein "=".
#### Model::orWhere()
Siehe where(), nur mit "OR" in der Query.
#### Model::orderBy($column, $ascOrDesc)
Mit orderBy() sortieren wir unsere Models.
#### Model::update([$column => $value])
Wenn wir ein Model geholt haben, können wir es manipulieren und mit update() updaten.
```php
$post = Post::find(1);
$post->title = "Ein neuer Titel";
$post->update();

// Oder

$post->update([
    'title' => "Ein neuer Titel"
]);
```
#### Model::delete()
Funktioniert ähnlich wie update().
