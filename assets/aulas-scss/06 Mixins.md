### Aula 06 de SCSS: Mixins

#### Definição e Uso de Mixins

Um **mixin** em SCSS é uma forma de agrupar conjuntos de declarações CSS que podem ser reutilizados em todo o código. Eles permitem que você evite a repetição de código, mantenha seu CSS organizado e facilite a manutenção.

**Sintaxe básica:**

```scss
@mixin nome-do-mixin {
  // declarações CSS
}
```

**Exemplo:**

```scss
@mixin rounded-corners {
  border-radius: 10px;
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
}

.box {
  @include rounded-corners;
}
```

#### Passagem de Argumentos para Mixins

Mixins podem aceitar argumentos, permitindo que você os torne ainda mais flexíveis e reutilizáveis.

**Sintaxe:**

```scss
@mixin nome-do-mixin($parametro1, $parametro2) {
  // uso dos parâmetros nas declarações CSS
}
```

**Exemplo:**

```scss
@mixin rounded-corners($radius) {
  border-radius: $radius;
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
}

.box {
  @include rounded-corners(15px);
}
```

#### Mixins com Parâmetros Padrão

Você pode definir valores padrão para os parâmetros de um mixin. Isso é útil quando você quer que o mixin tenha um comportamento padrão, mas ainda permita a flexibilidade de substituí-lo conforme necessário.

**Sintaxe:**

```scss
@mixin nome-do-mixin($parametro1: valor-padrao, $parametro2: valor-padrao) {
  // uso dos parâmetros nas declarações CSS
}
```

**Exemplo:**

```scss
@mixin rounded-corners($radius: 10px) {
  border-radius: $radius;
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
}

.box {
  @include rounded-corners; // usa o valor padrão de 10px
}

.card {
  @include rounded-corners(20px); // substitui o valor padrão para 20px
}
```

### Resumo

1. **Definição e Uso de Mixins**: Mixins agrupam declarações CSS para reutilização.
2. **Passagem de Argumentos**: Mixins podem aceitar argumentos para tornar o código mais flexível.
3. **Parâmetros Padrão**: Valores padrão podem ser definidos para os parâmetros dos mixins, proporcionando comportamento padrão com a possibilidade de substituição.

#### Prática

Para fixar o conteúdo, experimente criar um mixin que defina uma sombra de caixa (`box-shadow`) e permita ajustar a cor e o desfoque da sombra como parâmetros, com valores padrão definidos.
