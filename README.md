# Webpack 4 Boilerplate

[![MIT License](https://img.shields.io/github/license/peter-stuhlmann/Webpack4-Boilerplate.svg)](LICENSE) ![Code size](https://img.shields.io/github/languages/code-size/peter-stuhlmann/Webpack4-Boilerplate.svg) ![downloads](https://img.shields.io/github/downloads/peter-stuhlmann/Webpack4-Boilerplate/total.svg) [![open issues](https://img.shields.io/github/issues/peter-stuhlmann/Webpack4-Boilerplate.svg)](https://github.com/peter-stuhlmann/Webpack4-Boilerplate/issues) [![closed issues](https://img.shields.io/github/issues-closed/peter-stuhlmann/Webpack4-Boilerplate.svg)](https://github.com/peter-stuhlmann/Webpack4-Boilerplate/issues?q=is%3Aissue+is%3Aclosed)

Wenn Du dieses Repository klonst, musst Du folgenden Command im Terminal eingeben, um *node_modules* zu erstellen bzw. die notwenigen Plugins zu installieren und die Konfiguration somit funktionsfähig zu machen:

```
$ npm i
```

---

**Alternative: So kannst Du webpack selbst einrichten**

## Schritt für Schritt: webpack 4 selbst einrichten

**(1) Initialisiere npm**
```
$ npm init -y
```

**(2) Plugins installieren**  
In Deinem Hauptverzeichnis wurde nun eine _package.json_-Datei erstellt. Installiere nun ein paar notwendige Plugins.

Dazu gibt es zwei Möglichkeiten:

(2a) Installiere die Plugins manuell über das Terminal. So hast Du i. d. R. die aktuellste Version. 
```
$ npm i @babel/core --save-dev
$ npm i @babel/preset-env --save-dev
$ npm i babel-loader --save-dev
$ npm i css-loader --save-dev
$ npm i file-loader --save-dev
$ npm i html-webpack-plugin --save-dev
$ npm i mini-css-extract-plugin --save-dev
$ npm i node-sass --save-dev
$ npm i optimize-css-assets-webpack-plugin --save-dev
$ npm i postcss-loader --save-dev
$ npm i postcss-preset-env --save-dev
$ npm i sass-loader --save-dev
$ npm i style-loader --save-dev
$ npm i uglifyjs-webpack-plugin --save-dev
$ npm i webpack --save-dev
$ npm i webpack-cli --save-dev
```
_(```--save-dev``` gibt an, dass Du die Plugins als devDependencies installieren möchtest. Anstelle von ```--save-dev``` kannst Du auch die Kurzform ```-D``` schreiben.)_

(2b) Oder kopiere Code 2b.1 in Deine _package.json_-Datei und installiere die Plugins hinterher mit dem Befehl 2b.2.

(2b.1)
```
"devDependencies": {
    "@babel/core": "^7.3.4",
    "@babel/preset-env": "^7.3.4",
    "babel-loader": "^8.0.5",
    "css-loader": "^2.1.1",
    "file-loader": "^3.0.1",
    "html-webpack-plugin": "^3.2.0",
    "mini-css-extract-plugin": "^0.5.0",
    "node-sass": "^4.11.0",
    "optimize-css-assets-webpack-plugin": "^5.0.1",
    "postcss-loader": "^3.0.0",
    "postcss-preset-env": "^6.6.0",
    "sass-loader": "^7.1.0",
    "style-loader": "^0.23.1",
    "uglifyjs-webpack-plugin": "^2.1.2",
    "webpack": "^4.29.6",
    "webpack-cli": "^3.2.3"
  }
```

(2b.2.)
```
$ npm i
```

**(3) Scripts**  
Ergänze in der _package.json_ den Punkt 'scripts' um folgende Zeilen:
```
"dev": "webpack --mode development --watch",
"build": "webpack --mode production"
```

```"dev"``` und ```"build"``` können individuell benannt werden.


**(4) webpack.config.js**  
Erstelle und öffne eine Datei mit dem Namen _webpack.config.js_. Schreibe in diese Datei:
```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const UglifyJsPlugin = require('uglifyjs-webpack-plugin');
const OptimizeCSSAssetsPlugin = require('optimize-css-assets-webpack-plugin');

module.exports = {
    entry: './src/assets/js/main.js',
    output: {
        path: path.resolve(__dirname, 'dist/'),
        filename: 'assets/js/main.js'
    },
    optimization: {
        minimizer: [new UglifyJsPlugin(), new OptimizeCSSAssetsPlugin()]
    },
    devtool: "source-map",
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: "babel-loader",
                    options: {
                        presets: ["@babel/preset-env"]
                    }
                }
            },
            {
                test: /\.css$/,
                use: ['style-loader', 'css-loader']
            },
            {
                test: [/.css$|.scss$/],
                use: [
                    MiniCssExtractPlugin.loader,
                    {
                        loader: 'css-loader',
                        options: {
                            sourceMap: true
                        }
                    },
                    {
                        loader: 'postcss-loader',
                        options: {
                            ident: 'postcss',
                            sourceMap: true,
                            plugins: [
                                require('autoprefixer')({
                                    browsers: ['> 1%', 'last 2 versions']
                                })
                            ]
                        }
                    },
                    {
                        loader: 'sass-loader',
                        options: {
                            sourceMap: true
                        }
                    }
                ]
            },
            {
                test: /\.(png|jpg|gif)$/,
                use: [
                    {
                        loader: 'file-loader',
                        options: {
                            name: '[name].[ext]',
                            outputPath: 'assets/img/'
                        }
                    }
                ]
            }
        ]
    },
    plugins: [
        new MiniCssExtractPlugin({
            filename: 'assets/css/style.css'
        }),
        new HtmlWebpackPlugin({
            title: 'Setting up webpack 4',
            template: 'src/index.html',
            inject: true,
            minify: {
                removeComments: true,
                collapseWhitespace: true
            }
        })
    ]
}
```

**(5) Projektstruktur im Ordner _src_**  
Erstelle im Hauptverzeichnis einen Ordner _src_. In diesen Ordner kommen Deine HTML-, Javascript-, SCSS- und Bilddateien. Folgende Ordnerstruktur gilt für dieses Beispiel, kann aber natürlich verändert werden. In dem Fall musst Du aber auch die Pfade in der _webpack.config.js_ entsprechend anpassen.

```
src
│
└───index.html
│
└───assets
    │
    └───js
    │   └───main.js
    │
    └───scss
    │   └───style.scss
    │
    └───img
        └───logo.png
```

---

_index.html_ Du musst Dein Stylesheet und Deine Javascript-Datei nicht einbinden. Das geschieht bei der Kompilierung automatisch.
"Sicher ist sicher?" Nein! Wenn Du diese Dateien trotzdem einbindest werden sie doppelt verlinkt.

_main.js_ Importiere Deine SCSS- und Bild-Dateien. Ungewöhnlich, muss aber bei webpack so sein.
```
import "../scss/style.scss"
import "../img/logo.png"
```

---

Wenn Du Dein Projekt kompilieren/minimieren möchtest, gib folgenden Befehl ein. Es wird ein Ordner _dist_ erstellt, in dem Du all Deine Dateien minimiert finden wirst. Diese kannst Du dann z.B. auf Deine Website hochladen.
```
$ npm run build
```

Und um die Entwickler-Version bzw. den nicht minimierten Code im _dist_-Ordner zu speichern, schreibe
```
$ npm run dev
```

**Achtung!** Bearbeite Deine Dateien nur im Ordner _src_. Der _dist_-Ordner ist nur für die Ausgabe gedacht.

---

[&copy; Peter R. Stuhlmann Webentwicklung](https://peter-stuhlmann-webentwicklung.de)