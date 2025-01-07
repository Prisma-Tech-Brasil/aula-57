# Criando um Projeto React Manualmente

Este guia explica como configurar um projeto React do zero, sem utilizar ferramentas como `create-react-app`. Vamos configurar o Babel e o Webpack para gerenciar o desenvolvimento.

## Passo a Passo

### 1. Inicializando o Projeto

1. Crie uma nova pasta para o projeto e execute:
   ```bash
   npm init -y
   ```
   Isso cria um arquivo `package.json` básico.

2. Instale as dependências do Babel:
   ```bash
   npm i @babel/core @babel/preset-env @babel/cli -D
   ```

3. Configure o Babel criando um arquivo `.babelrc` na raiz do projeto:
   ```json
   {
     "presets": ["@babel/preset-env"]
   }
   ```

### 2. Transpilando Código com Babel

1. Crie a estrutura de diretórios:
   ```bash
   mkdir src
   echo "const user = {}; console.log(user?.address?.street);" > src/index.js
   ```

2. Execute o Babel para transpilar o código:
   ```bash
   npx babel src -d build
   ```

O código transpilado será salvo na pasta `build`.

### 3. Configurando o Babel para React

1. Instale os pacotes adicionais:
   ```bash
   npm i @babel/preset-react react react-dom
   ```

2. Atualize o arquivo `.babelrc`:
   ```json
   {
     "presets": ["@babel/preset-env", "@babel/preset-react"]
   }
   ```

3. Crie um arquivo `index.html` na pasta `public`:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <title>React App</title>
   </head>
   <body>
     <div id="root"></div>
   </body>
   </html>
   ```

4. Adicione o código React no `src/index.js`:
   ```javascript
   import React from "react";
   import ReactDOM from "react-dom";

   ReactDOM.render(<h1>Olá, mundo!</h1>, document.getElementById("root"));
   ```

### 4. Configurando o Webpack

1. Instale as dependências do Webpack:
   ```bash
   npm i webpack webpack-cli html-webpack-plugin clean-webpack-plugin -D
   ```

2. Crie o arquivo `webpack.config.js`:
   ```javascript
   const path = require("path");
   const HtmlWebpackPlugin = require("html-webpack-plugin");
   const { CleanWebpackPlugin } = require("clean-webpack-plugin");

   module.exports = {
     entry: path.resolve(__dirname, "src", "index.js"),
     output: {
       path: path.resolve(__dirname, "build"),
       filename: "bundle.[hash].js",
     },
     plugins: [
       new HtmlWebpackPlugin({
         template: path.resolve(__dirname, "public", "index.html"),
       }),
       new CleanWebpackPlugin(),
     ],
     module: {
       rules: [
         {
           test: /\.js$/,
           exclude: /node_modules/,
           use: {
             loader: "babel-loader",
           },
         },
       ],
     },
   };
   ```

3. Atualize o `package.json` para adicionar um script de build:
   ```json
   {
     "scripts": {
       "build": "webpack"
     }
   }
   ```

### 5. Executando o Projeto

1. Execute o script de build:
   ```bash
   npm run build
   ```

2. Abra o arquivo gerado em `build/index.html` no navegador para ver a aplicação React em funcionamento.

---

Agora você tem um projeto React configurado manualmente, com suporte a Babel e Webpack!