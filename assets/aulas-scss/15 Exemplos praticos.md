
Claro! Vamos explorar a aula 15 de SCSS com exemplos práticos, projetos reais e exercícios para praticar.

## Aula 15: SCSS - Exemplos Práticos

### Introdução ao SCSS

SCSS é uma sintaxe do Sass (Syntactically Awesome Stylesheets) que adiciona recursos avançados ao CSS, como variáveis, aninhamento, mixins, herança, entre outros.

### Conteúdo da Aula

1. **Variáveis**
2. **Aninhamento**
3. **Mixin**
4. **Extends**
5. **Funções**
6. **Exemplos Práticos**
7. **Projetos Reais Utilizando SCSS**
8. **Exercícios para Praticar**

### 1. Variáveis

As variáveis permitem armazenar valores que podem ser reutilizados em todo o código.

```scss
$primary-color: #3498db;
$font-stack: Helvetica, sans-serif;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

### 2. Aninhamento

O aninhamento facilita a leitura e manutenção do código, especialmente para seletores complexos.

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    text-decoration: none;
    &:hover {
      text-decoration: underline;
    }
  }
}
```

### 3. Mixins

Os mixins são blocos de código que podem ser reutilizados em várias partes do CSS.

```scss
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
  border-radius: $radius;
}

.box { @include border-radius(10px); }
```

### 4. Extends

O `@extend` permite compartilhar um conjunto de regras CSS entre seletores.

```scss
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.message { @extend %message-shared; }
.success { @extend %message-shared; background-color: #e0ffe0; }
.error { @extend %message-shared; background-color: #ffe0e0; }
```

### 5. Funções

O SCSS permite criar funções que retornam valores.

```scss
@function px-to-rem($px, $base-font-size: 16) {
  @return #{$px / $base-font-size}rem;
}

body { font-size: px-to-rem(18); }
```

### 6. Exemplos Práticos

#### Estilizando um Card

```scss
$card-bg: #fff;
$card-shadow: 0 2px 4px rgba(0,0,0,0.1);
$card-padding: 20px;

.card {
  background: $card-bg;
  box-shadow: $card-shadow;
  padding: $card-padding;
  border-radius: 5px;

  .card-header {
    font-size: 1.5em;
    margin-bottom: 10px;
  }

  .card-body {
    font-size: 1em;
    color: #666;
  }
}
```

### 7. Projetos Reais Utilizando SCSS

#### Projeto 1: Landing Page

- **Estrutura de Pastas:**
  
  - `styles/`
    - `_variables.scss`
    - `_mixins.scss`
    - `_base.scss`
    - `main.scss`

- **main.scss:**

```scss
@import 'variables';
@import 'mixins';
@import 'base';

body {
  font-family: Arial, sans-serif;
  color: $primary-color;
  background: #f5f5f5;
}

.header {
  @include border-radius(5px);
  background: $secondary-color;
  padding: 20px;
  text-align: center;
}
```

### 8. Exercícios para Praticar

#### Exercício 1: Variáveis e Mixins

Crie um arquivo SCSS que utilize variáveis para definir cores e fontes, e um mixin para borda arredondada. Utilize esses elementos em uma estrutura básica de página.

#### Exercício 2: Aninhamento e Extends

Estilize uma lista de navegação utilizando aninhamento e extends. Crie classes para itens de navegação ativos e inativos.

#### Exercício 3: Projeto Completo

Crie um mini projeto de página inicial de um site fictício, utilizando todos os recursos abordados: variáveis, mixins, aninhamento, extends e funções. Estruture seu SCSS em múltiplos arquivos importados em um arquivo principal.

### Conclusão

O SCSS é uma ferramenta poderosa que melhora a manutenção e reutilização do código CSS. Com a prática, você conseguirá criar estilos de maneira mais eficiente e organizada.



## Um exemplo mostrando a estrutura de pastas



Claro! Vamos criar um exemplo de projeto utilizando a estrutura mencionada:

### Estrutura de Pastas

```
styles/
  ├── _variables.scss
  ├── _mixins.scss
  ├── _base.scss
  └── main.scss
```

### Conteúdo dos Arquivos

#### `_variables.scss`

Aqui, definimos todas as variáveis que utilizaremos no projeto.

```scss
// _variables.scss

$primary-color: #3498db;
$secondary-color: #2ecc71;
$text-color: #333;
$background-color: #f5f5f5;
$font-stack: 'Helvetica, Arial, sans-serif';
$border-radius: 5px;
```

#### `_mixins.scss`

Neste arquivo, criamos mixins reutilizáveis.

```scss
// _mixins.scss

@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
  border-radius: $radius;
}

@mixin box-shadow($shadow) {
  -webkit-box-shadow: $shadow;
  -moz-box-shadow: $shadow;
  box-shadow: $shadow;
}

@mixin transition($property, $duration) {
  -webkit-transition: $property $duration;
  -moz-transition: $property $duration;
  -o-transition: $property $duration;
  transition: $property $duration;
}
```

#### `_base.scss`

Aqui definimos estilos globais e elementos básicos.

```scss
// _base.scss

body {
  font-family: $font-stack;
  color: $text-color;
  background: $background-color;
  margin: 0;
  padding: 0;
}

h1, h2, h3, h4, h5, h6 {
  color: $primary-color;
}

a {
  color: $secondary-color;
  text-decoration: none;
  @include transition(color, 0.3s);

  &:hover {
    color: darken($secondary-color, 10%);
  }
}

button {
  background: $primary-color;
  color: #fff;
  padding: 10px 20px;
  border: none;
  @include border-radius($border-radius);
  @include transition(background-color, 0.3s);

  &:hover {
    background: darken($primary-color, 10%);
  }
}
```

#### `main.scss`

Este é o arquivo principal onde importamos os outros arquivos SCSS e adicionamos estilos específicos da página.

```scss
// main.scss

@import 'variables';
@import 'mixins';
@import 'base';

.header {
  background: $primary-color;
  color: #fff;
  padding: 20px;
  text-align: center;
  @include border-radius($border-radius);
  @include box-shadow(0 2px 4px rgba(0, 0, 0, 0.1));
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;

  .card {
    background: #fff;
    padding: 20px;
    margin-bottom: 20px;
    @include border-radius($border-radius);
    @include box-shadow(0 2px 4px rgba(0, 0, 0, 0.1));

    .card-header {
      font-size: 1.5em;
      margin-bottom: 10px;
    }

    .card-body {
      font-size: 1em;
      color: $text-color;
    }
  }
}

.footer {
  background: $secondary-color;
  color: #fff;
  text-align: center;
  padding: 10px 0;
  @include border-radius($border-radius);

  a {
    color: #fff;
    &:hover {
      color: darken(#fff, 10%);
    }
  }
}
```

### Utilizando os Arquivos SCSS

No seu projeto, certifique-se de compilar os arquivos SCSS para CSS utilizando uma ferramenta como `sass` ou outro pré-processador de sua preferência. 

Exemplo de compilação usando `sass` no terminal:

```sh
sass styles/main.scss styles/main.css
```

### Estrutura de HTML para Visualizar os Estilos

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="styles/main.css">
  <title>Projeto SCSS</title>
</head>
<body>
  <header class="header">
    <h1>Bem-vindo ao Meu Projeto SCSS</h1>
  </header>

  <div class="container">
    <div class="card">
      <div class="card-header">Card Header</div>
      <div class="card-body">Este é o corpo do card.</div>
    </div>
    <div class="card">
      <div class="card-header">Outro Card</div>
      <div class="card-body">Mais conteúdo de exemplo.</div>
    </div>
  </div>

  <footer class="footer">
    <p>© 2024 Meu Projeto SCSS. Todos os direitos reservados.</p>
    <a href="#">Link para algo</a>
  </footer>
</body>
</html>
```

Com esta estrutura, você tem um projeto organizado e reutilizável utilizando SCSS. Sinta-se à vontade para expandir e modificar conforme necessário.
