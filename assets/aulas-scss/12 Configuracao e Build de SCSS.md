## Aula 12: Configuração e Build de SCSS

### 1. Introdução aos Pré-Processadores SCSS

SCSS (Sassy CSS) é uma sintaxe de pré-processador para CSS que permite usar variáveis, aninhamento, mixins, herança e outras funcionalidades que facilitam a escrita e a manutenção do CSS. Para utilizar SCSS, precisamos configurar um pré-processador que converte o código SCSS em CSS.

### 2. Configuração de Pré-Processadores SCSS

Existem várias ferramentas que podemos usar para compilar SCSS em CSS. Vamos focar em duas das mais populares: Node-sass e Dart-sass.

#### Node-sass

**Instalação:**

Node-sass é uma biblioteca que permite compilar SCSS para CSS usando Node.js. Para instalar, você precisa ter o Node.js e o npm (Node Package Manager) instalados.

1. Inicialize um novo projeto Node:
   
   ```bash
   npm init -y
   ```

2. Instale o Node-sass:
   
   ```bash
   npm install node-sass --save-dev
   ```

3. Adicione um script no `package.json` para compilar SCSS:
   
   ```json
   "scripts": {
       "build-css": "node-sass --output-style compressed -o css/ scss/"
   }
   ```

#### Dart-sass

**Instalação:**

Dart-sass é a implementação de referência do Sass, recomendada pela equipe do Sass.

1. Inicialize um novo projeto Node:
   
   ```bash
   npm init -y
   ```

2. Instale o Dart-sass:
   
   ```bash
   npm install sass --save-dev
   ```

3. Adicione um script no `package.json` para compilar SCSS:
   
   ```json
   "scripts": {
       "build-css": "sass --style=compressed scss/:css/"
   }
   ```

### 3. Ferramentas de Build

Ferramentas de build ajudam a automatizar tarefas repetitivas, como compilação de SCSS, minificação de arquivos, etc. Vamos explorar duas ferramentas populares: Gulp e Webpack.

#### Gulp

Gulp é um task runner que usa streams Node.js para automatizar tarefas.

**Configuração:**

1. Instale o Gulp globalmente:
   
   ```bash
   npm install --global gulp-cli
   ```

2. Instale o Gulp localmente no projeto:
   
   ```bash
   npm install gulp --save-dev
   ```

3. Crie um arquivo `gulpfile.js` na raiz do projeto:
   
   ```javascript
   const gulp = require('gulp');
   const sass = require('gulp-sass')(require('sass'));
   
   gulp.task('sass', function() {
       return gulp.src('scss/**/*.scss')
           .pipe(sass({ outputStyle: 'compressed' }).on('error', sass.logError))
           .pipe(gulp.dest('css'));
   });
   
   gulp.task('watch', function() {
       gulp.watch('scss/**/*.scss', gulp.series('sass'));
   });
   
   gulp.task('default', gulp.series('sass', 'watch'));
   ```

4. Execute o Gulp:
   
   ```bash
   gulp
   ```

#### Webpack

Webpack é um módulo bundler que também pode ser usado para compilar SCSS.

**Configuração:**

1. Instale o Webpack e os loaders necessários:
   
   ```bash
   npm install webpack webpack-cli style-loader css-loader sass-loader sass --save-dev
   ```

2. Crie um arquivo `webpack.config.js` na raiz do projeto:
   
   ```javascript
   const path = require('path');
   
   module.exports = {
       entry: './src/index.js',
       output: {
           filename: 'bundle.js',
           path: path.resolve(__dirname, 'dist')
       },
       module: {
           rules: [
               {
                   test: /\.scss$/,
                   use: [
                       'style-loader',
                       'css-loader',
                       'sass-loader'
                   ]
               }
           ]
       },
       mode: 'development'
   };
   ```

3. Crie a estrutura de arquivos:
   
   ```
   project/
   ├── dist/
   ├── src/
   │   └── index.js
   ├── scss/
   │   └── style.scss
   ├── package.json
   └── webpack.config.js
   ```

4. No arquivo `src/index.js`, importe o arquivo SCSS:
   
   ```javascript
   import '../scss/style.scss';
   ```

5. Adicione um script no `package.json` para executar o Webpack:
   
   ```json
   "scripts": {
       "build": "webpack"
   }
   ```

6. Execute o Webpack:
   
   ```bash
   npm run build
   ```

### 4. Integração com Task Runners

Ambos Gulp e Webpack podem ser integrados em fluxos de trabalho maiores para gerenciar tarefas adicionais como otimização de imagens, minificação de JavaScript, etc.

#### Exemplo de Fluxo com Gulp

No `gulpfile.js`, podemos adicionar tarefas para otimizar imagens e minificar JavaScript:

```javascript
const gulp = require('gulp');
const sass = require('gulp-sass')(require('sass'));
const uglify = require('gulp-uglify');
const imagemin = require('gulp-imagemin');

gulp.task('sass', function() {
    return gulp.src('scss/**/*.scss')
        .pipe(sass({ outputStyle: 'compressed' }).on('error', sass.logError))
        .pipe(gulp.dest('css'));
});

gulp.task('scripts', function() {
    return gulp.src('js/**/*.js')
        .pipe(uglify())
        .pipe(gulp.dest('dist/js'));
});

gulp.task('images', function() {
    return gulp.src('images/*')
        .pipe(imagemin())
        .pipe(gulp.dest('dist/images'));
});

gulp.task('watch', function() {
    gulp.watch('scss/**/*.scss', gulp.series('sass'));
    gulp.watch('js/**/*.js', gulp.series('scripts'));
    gulp.watch('images/*', gulp.series('images'));
});

gulp.task('default', gulp.series('sass', 'scripts', 'images', 'watch'));
```

#### Exemplo de Fluxo com Webpack

No `webpack.config.js`, podemos adicionar loaders e plugins para outras tarefas:

```javascript
const path = require('path');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const TerserPlugin = require('terser-webpack-plugin');
const OptimizeCSSAssetsPlugin = require('optimize-css-assets-webpack-plugin');

module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
        rules: [
            {
                test: /\.scss$/,
                use: [
                    MiniCssExtractPlugin.loader,
                    'css-loader',
                    'sass-loader'
                ]
            },
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env']
                    }
                }
            }
        ]
    },
    optimization: {
        minimizer: [new TerserPlugin(), new OptimizeCSSAssetsPlugin({})],
    },
    plugins: [
        new MiniCssExtractPlugin({
            filename: '[name].css',
            chunkFilename: '[id].css'
        })
    ],
    mode: 'production'
};
```

### Conclusão

Configuramos SCSS usando Node-sass e Dart-sass, e integramos a compilação de SCSS em fluxos de trabalho com Gulp e Webpack. Essas ferramentas ajudam a automatizar a compilação e outras tarefas de build, tornando o desenvolvimento mais eficiente.

Se tiver alguma dúvida ou precisar de mais detalhes sobre qualquer parte, sinta-se à vontade para perguntar!
