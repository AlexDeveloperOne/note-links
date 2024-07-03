### Aula 03 de SCSS: Variáveis

#### 1. Definição e Uso de Variáveis

As variáveis em SCSS permitem armazenar valores que podem ser reutilizados em vários lugares do código. Isso facilita a manutenção e a consistência do estilo.

**Sintaxe:**

```scss
$nome-da-variável: valor;
```

**Exemplo:**

```scss
$primary-color: #3498db;
$font-size: 16px;

body {
  color: $primary-color;
  font-size: $font-size;
}
```

#### 2. Tipos de Variáveis

Em SCSS, você pode usar variáveis para armazenar diferentes tipos de valores. Vamos explorar alguns tipos comuns:

##### a. Cores

Você pode armazenar valores de cores em variáveis.

**Exemplo:**

```scss
$red: #ff0000;
$blue: #0000ff;

button {
  background-color: $red;
  color: $blue;
}
```

##### b. Números

Números podem incluir unidades como `px`, `%`, `em`, etc.

**Exemplo:**

```scss
$padding: 20px;
$margin: 10%;

.container {
  padding: $padding;
  margin: $margin;
}
```

##### c. Strings

Strings podem ser usadas para valores como fontes ou caminhos de arquivos.

**Exemplo:**

```scss
$font-family: 'Arial, sans-serif';
$background-image: 'url(image.png)';

body {
  font-family: $font-family;
  background: $background-image;
}
```

##### d. Listas

Listas podem armazenar múltiplos valores, separados por espaços ou vírgulas.

**Exemplo:**

```scss
$font-sizes: 12px, 14px, 16px, 18px;

h1 {
  font-size: nth($font-sizes, 4); // 18px
}
```

##### e. Mapas

Mapas são pares chave-valor, semelhantes aos objetos em JavaScript.

**Exemplo:**

```scss
$theme-colors: (
  primary: #3498db,
  secondary: #2ecc71,
  danger: #e74c3c
);

.alert {
  color: map-get($theme-colors, danger);
}
```

#### 3. Variáveis Globais e Locais

##### Variáveis Globais

Por padrão, todas as variáveis definidas no SCSS são globais e podem ser acessadas de qualquer lugar no código.

**Exemplo:**

```scss
$global-color: #ff6347;

div {
  color: $global-color;
}

p {
  background-color: $global-color;
}
```

##### Variáveis Locais

As variáveis locais são definidas dentro de um bloco de código e só podem ser acessadas dentro desse bloco. 

**Exemplo:**

```scss
.container {
  $local-color: #8e44ad;
  color: $local-color;
}

.other-container {
  // $local-color não está disponível aqui
  color: $global-color;
}
```

Para tornar uma variável local global dentro de um bloco de código, você pode usar a palavra-chave `!global`.

**Exemplo:**

```scss
.container {
  $local-color: #8e44ad !global;
}

p {
  color: $local-color; // Agora $local-color é acessível globalmente
}
```

### Exercício Prático

Tente criar um arquivo SCSS onde você define variáveis para cores, tamanhos de fonte e espaçamentos, e depois use essas variáveis para estilizar diferentes elementos de uma página HTML.

```scss
// Definindo variáveis
$primary-color: #3498db;
$secondary-color: #2ecc71;
$base-font-size: 16px;
$padding: 20px;
$margin: 10%;

// Usando variáveis
body {
  font-size: $base-font-size;
  color: $primary-color;
}

header {
  background-color: $secondary-color;
  padding: $padding;
}

footer {
  margin: $margin;
}
```

Com a prática, você verá como as variáveis em SCSS podem simplificar e melhorar seu fluxo de trabalho de CSS.