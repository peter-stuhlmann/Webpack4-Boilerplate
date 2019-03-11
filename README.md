# Webpack 4 Boilerplate

[![MIT License](https://img.shields.io/github/license/peter-stuhlmann/Webpack4-Boilerplate.svg)](LICENSE) ![Code size](https://img.shields.io/github/languages/code-size/peter-stuhlmann/Webpack4-Boilerplate.svg) ![downloads](https://img.shields.io/github/downloads/peter-stuhlmann/Webpack4-Boilerplate/total.svg) [![open issues](https://img.shields.io/github/issues/peter-stuhlmann/Webpack4-Boilerplate.svg)](https://github.com/peter-stuhlmann/Webpack4-Boilerplate/issues) [![closed issues](https://img.shields.io/github/issues-closed/peter-stuhlmann/Webpack4-Boilerplate.svg)](https://github.com/peter-stuhlmann/Webpack4-Boilerplate/issues?q=is%3Aissue+is%3Aclosed)

Wenn Du dieses Repository klonst, musst Du folgenden Command im Terminal eingeben, um *node_modules* zu erstellen und die Konfiguration funktionsfähig zu machen:

```
$ npm i
```

---

**Alternative: So kannst Du webpack selbst einrichten**

## Schritt für Schritt: webpack 4 selbst einrichten

Führe als erstes die folgenden Schritte im Terminal durch:
```
$ npm init -y
$ npm i --save-dev webpack webpack-cli
$ npm i --save-dev @babel/core
$ npm i --save-dev babel-loader
$ npm i --save-dev @babel/preset-env
```
_(Anstelle von ```--save-dev``` kannst Du auch die Kurzform ```-D``` schreiben.)_

Ergänze in der _package.json_ den Punkt 'scripts':
```
"dev": "webpack --mode development --watch",
"build": "webpack --mode production"
```

```"dev"``` und ```"build"``` können individuell benannt werden.


Erstelle und öffne eine Datei mit dem Name _webpack.config.js_.

Schreibe in die _webpack.config.js_:
```
var path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'dist/assets/js/'),
        filename: 'script.js'
    },
    module {
        rules:[
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: "babel-loader",
                    options: {
                        presets: ["@babel/preset-env"]
                    }
                }
            }
        ]
    }
}
```

Erstelle im Hauptverzeichnis zwei Ordner, _src_ und _dist_.   
**_src:_** In diesen Ordner kommen alle Dateien, die Du mit babel-webpack kompilieren willst, z.B. Javascript-Dateien   
**_dist:_** In diesen Ordner können Dateien gepackt werden, die nicht kompiliert werden müssen, z.B. images. Außerdem beinhaltet dieser Ordner später alles was Du auf Deiner Website veröffentlichen möchtest. Deine bearbeiteten Dateien aus dem Ordner _src_ werden automatisch im Ordner _dist_ sichtbar.

---

Nun kannst Du webpack-babel nutzen.
So könntest Du jetzt starten:

Erstelle eine _index.html_ im Ordner _dist_ und eine _index.js_ im Ordner _src_.  
Verlinke in der _index.html_ eine Javascript-Datei mit dem Namen _script.js_ mit dem Pfad _assets/js/_. Möchtest Du den Pfad oder den Dateinamen ändern musst Du auch 'path' und 'filename' in der _webpack.config.js_ entsprechend anpassen.  
Für dieses Beispiel gilt: Um Deinen Javascript-Code zu bearbeiten nutze bitte die _index.js_ im Ordner _src_. Deinen HTML-Code änderst Du in der _index.html_ im Ordner _dist_.

---

Wenn Du die kompilierte Version speichern möchtest, z.B. um das Projekt zu veröffentlichen, schreibe
```
$ npm run build
```

Und um die Entwickler-Version bzw. den nicht minimierten Code zu sehen, schreibe
```
$ npm run dev
```

---

[&copy; Peter R. Stuhlmann Webentwicklung](https://peter-stuhlmann-webentwicklung.de)