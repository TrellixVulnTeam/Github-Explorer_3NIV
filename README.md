# GitHub-Explorer

- [x] Configurando ambiente ⚙️
- [ ] Conceitos Importantes 📘
- [ ] Chamadas HTTP 🗣
- [ ] Usando Typescript 📘
- [ ] Finalizando aplicação 🚚

## Preparing environment
```cmd
$ yarn init -y
```
#### Node Modules
* Normais
 ```cmd
$ yarn add react
$ yarn add react-dom //Render the react elements
```
* Desenvolvimento (Não vai para a produção):
```cmd
$ yarn add @babel/cli @babel/core @babel/preset-env @babel/preset-react -D
```

 ### Babel
 Converte o código para que o navegador entenda
 #### Configuração
 ```javascript
 //babel.config.js
 module.exports = {
    presets: [
        '@babel/preset-env',
        ['@babel/preset-react', {
            runtime: 'automatic'
        }]
    ]
 }
 ```
 ### Executar
 ```cmd
 yarn babel src/index.js --out-file dist/bundle.js
 ```
 
### Webpack
Estipula uma série de 'loaders' para converter os arquivos a fim de deixar legíveis ao browser
#### Installing
 ```cmd
 yarn add webpack webpack-cli webpack-dev-server -D
 yarn add html-webpack-plugin -D // Add the bundle.js to index.html
 yarn add cross-env -D //Permiti a inserção de variáveis de ambiente em qualquer sistema operacional
 ```
* Loaders:
```cmd
 yarn add css-loader sass-loader style-loader node-sass -D //instala pré processador de css para inserir novas funcionalidades .scss
 yarn add babel-loader -D
```
#### Configure webpack.config.js
```javascript
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const isDevelopment = process.env.NODE_ENV != 'production';
module.exports = {
    mode: isDevelopment ? 'development' : 'production',
    devtool: 'eval-source-map', //source map facilita a depuração do código
    entry: path.resolve(__dirname, 'src', 'index.jsx'),
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },
    resolve: {
        extensions: ['.js', '.jsx'],
    },
    devServer: {
        contentBase: path.resolve(__dirname, 'public'),
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: path.resolve(__dirname, 'public', 'index.html'),
        })
    ],
    module: {
        rules: [
            {
                test: /\.jsx$/,
                exclude: /node_modules/,
                use: 'babel-loader'
            },
            {
                test: /\.scss$/,
                exclude: /node_modules/,
                use: ['style-loader', 'css-loader', 'sass-loader']
            }
        ],
    }
};
```
### Executar
 * Cria um atalho no package json
 ```json
 {
  "name": "github-explorer",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "dev": "webpack serve",
    "build": "cross-env NODE_ENV=production webpack"
  },
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
  }
}
```
 ```cmd
 $ yarn dev 
 $ yarn build
 ```
  
