# Blade
Mit Blade ist es einfach seine views zu generieren. Alle Blade Dateien befinden sich im `resources/views` Ordner. mit der Funktion `view($file, $data)` sprechen wir also eine Datei in diesem Verzeichnis an. Wenn wir eine Datei in einem Unterverzeichnis davon auswählen wollen, so müssen wir die Wegschritte mit einem `.` abtrennen. Dabei können wir die Endung `.blade.php` weglassen, z.B. `view('pages.home', $data)`.
### Beispiel
Wie kann jetzt so eine Blade Datei aussehen?
```php
@extends('layouts.app')

@section('page_title', '')
@section('page_description', '')

@section('main')
<div class="container">
    <div class="row">
      <div class="col-xs-12 col-md-6">
        @each('components.post-overview', $posts, 'post')
      </div>
    </div>
</div>
@endsection
```
Gehen wir das ganze mal durch. Was auffällt sind die Directives, die mit einem "@" beginnen. Ganz oben steht `@extend`, was Blade sagt, dass die angegebene Blade Datei "extended" wird. Die Datei `layouts/app.blade.php` kann z.B. so aussehen:
```php
<!DOCTYPE html>
<html lang="{{ app()->getLocale() }}">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- CSRF Token -->
    <meta name="csrf-token" content="{{ csrf_token() }}">

    <title>@yield('page_title')</title>
    <meta name="description" content="@yield('page_description')">

    <!-- Styles -->
    <link href="{{ asset('css/app.css') }}" rel="stylesheet">
</head>
<body>
    <div id="app">
        @include('components.navigation')

        <main>
            @yield('main')
        </main>

        @include('components.footer')
    </div>
    <!-- Scripts -->
    <script src="{{ asset('js/app.js') }}"></script>
</body>
</html>
```

Hier einmal eine Liste von allen Directives:
### {{ $var }}
Die Hauptdirective, ist nichts anderes als ein `<?php echo $var; ?>`
### {!! $var !!}
Quasi das gleiche wie {{ }} nur das hiermit reines HTML ausgegeben wird.
### @include($path)
Wird genutzt um Subviews zu inkludieren.
### @yield($section_name)
Yield ist ein Platzhalter. Mit @yield('main) definieren wir eine Section, die später befüllt wird.
### @section($section_name) | @endsection
Diese Directive kann als Block oder Inline benutzt werden. Im ersten Beispiel benutzen wir sie Inline um die Meta Tags mit Daten zu füttern und als Block um den Main Content Bereich zu definieren. Ein Block muss dann allerdings mit @endsection geschlossen werden.
### @if(boolean) | @elseif(boolean) | @else | @endif
Sollte selbsterklärend sein. Ergibt der Teil in den Klammern == true, dann wird der Block gerendert.
### @foreach($array as $item) | @endforeach
Ebenfalls selbsterklärend. Sehr praktisch, um durch Eloquent Collections zu loopen.
### @each($component_name, $array, 'item_name')
@each ist ein inline foreach. Zuerst geben wir den Pfad zur Komponente an die gerendert werden soll, dann das Array durch das geloopt wird und als letzten Parameter ein String mit dem Variablen Namen, welchen Das aktuelle Item in der Komponente haben soll.
### @isset($var) | @endisset
Kurzfrom von @if(isset($var))
### @empty($var) | @endempty
Kurzfrom von @if(empty($var))
### @php | @endphp
Falls man dochmal reines PHP in die View schreiben möchte, kann man das zwischen diesen Tags machen, sollte man aber vermeiden.

## Custom Directives
Es gibt auch die Möglichkeit Custom Direcitves zu definieren, das geht im AppServiceProvider, im boot() Block, z.B. so:
```php
public function boot()
{
    Blade::directive('lang', function ($expression) {
        return "<?php if ($language == $expression) { ?>";
    });
}
```
Damit könnten wir z.B. folgendes machen:
```php
@lang('de')
# Something
@endlang
```
was zu folgendem wird:
```php
<?php if ($language == 'de') { ?>
# Something
<?php } ?>
```
