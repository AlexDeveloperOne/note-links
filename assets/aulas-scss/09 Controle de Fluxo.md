### Aula 09 de SCSS: Controle de Fluxo

Nesta aula, vamos explorar o controle de fluxo no SCSS, que nos permite adicionar lógica ao nosso código. Vamos cobrir condicionais e laços de repetição.

#### Condicionais (@if, @else, @else if)

As condicionais em SCSS permitem que você adicione lógica ao seu código, fazendo com que diferentes blocos de CSS sejam aplicados com base em certas condições.

##### @if

A diretiva `@if` permite que você execute um bloco de código CSS apenas se uma condição for verdadeira.

```scss
$color: red;

button {
  @if $color == red {
    background-color: red;
  }
}
```

##### @else if

A diretiva `@else if` permite que você especifique uma nova condição a ser testada se a condição anterior falhar.

```scss
$color: green;

button {
  @if $color == red {
    background-color: red;
  } @else if $color == green {
    background-color: green;
  }
}
```

##### @else

A diretiva `@else` permite que você defina um bloco de código CSS a ser executado se todas as condições anteriores falharem.

```scss
$color: blue;

button {
  @if $color == red {
    background-color: red;
  } @else if $color == green {
    background-color: green;
  } @else {
    background-color: blue;
  }
}
```

#### Laços de Repetição

Os laços de repetição permitem que você repita um bloco de código várias vezes, o que pode ser útil para gerar CSS dinâmico e reduzir a redundância.

##### @for

A diretiva `@for` permite que você crie um laço que se repete um número específico de vezes.

```scss
@for $i from 1 through 5 {
  .item-#{$i} {
    width: 2em * $i;
  }
}
```

##### @each

A diretiva `@each` permite que você itere sobre cada item em uma lista ou mapa.

```scss
$colors: red, green, blue;

@each $color in $colors {
  .#{$color}-text {
    color: $color;
  }
}
```

##### @while

A diretiva `@while` permite que você crie um laço que se repete enquanto uma condição for verdadeira.

```scss
$i: 1;

@while $i < 6 {
  .item-#{$i} {
    width: 2em * $i;
  }
  $i: $i + 1;
}
```

### Prática

Vamos aplicar o que aprendemos em um exemplo prático.

#### Exemplo

Vamos criar um conjunto de botões com cores e tamanhos diferentes usando condicionais e laços de repetição.

```scss
$colors: red, green, blue;
$sizes: 1em, 2em, 3em;

@each $color in $colors {
  @each $size in $sizes {
    .btn-#{$color}-#{$size} {
      background-color: $color;
      font-size: $size;
    }
  }
}

$color: blue;

.button {
  @if $color == red {
    background-color: red;
  } @else if $color == green {
    background-color: green;
  } @else {
    background-color: blue;
  }
}
```

Neste exemplo, usamos `@each` para iterar sobre as listas de cores e tamanhos e criar classes de botões correspondentes. Além disso, usamos `@if`, `@else if` e `@else` para definir a cor de um botão específico com base no valor da variável `$color`.

Isso conclui nossa aula sobre controle de fluxo no SCSS. Pratique esses conceitos e veja como eles podem tornar seu código SCSS mais dinâmico e eficiente!
