# Konfiguration
Bevor es losgehen kann, muss man einige Bedingungen erfüllen. Unter anderem benötigt man:
* PHP >= 7.0
* Node.js
* Composer

Node.js gibt es [https://nodejs.org/en/](hier)
Composer [https://getcomposer.org/](hier)

Nachdem alles installiert wurde, kann man folgenden Befehl eingeben, um ein neues Projekt anzulegen:
```
composer create-project --prefer-dist laravel/laravel PROJECT_NAME
```

Wenn alles geklappt hat kommt man mit cd PROJECT_NAME in das neue Projektverzeichnis.
Für Laravel muss man viel mit der Kommandozeile arbeiten, falls das noch nicht klar ist.
Auch gut zu wissen, ist dass die `index.php` nicht im root sondern im public Verzeichnis liegt, zusammen mit der `.htaccess`.

### Node und Composer Packages installieren

Um nun die Packages zu installieren, die in der `package.json` und `composer.json` stehen, muss man folgende Befehle eingeben:
```
npm install && composer install
```
Danach sollte alles laufen.