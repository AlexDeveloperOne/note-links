### Aula 07: Extends e Herança em SCSS

#### 1. Uso da Diretiva @extend

A diretiva `@extend` permite que um seletor herde os estilos de outro seletor. Isso ajuda a evitar a repetição de código e a manter o CSS mais limpo e fácil de manter.

**Exemplo:**

```scss
// Definindo um estilo base
.button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: blue;
  color: white;
}

// Extendendo o estilo base
.success-button {
  @extend .button;
  background-color: green;
}

.error-button {
  @extend .button;
  background-color: red;
}
```

Isso resultará em:

```css
.button, .success-button, .error-button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: blue;
  color: white;
}

.success-button {
  background-color: green;
}

.error-button {
  background-color: red;
}
```

#### 2. Diferenças entre @extend e Mixins

Embora `@extend` e mixins possam parecer semelhantes, eles têm diferenças importantes:

- **@extend**:
  
  - Cria um relacionamento de herança entre seletores.
  - O código é compartilhado entre os seletores que usam `@extend`, o que pode resultar em CSS mais compacto.
  - Todos os seletores estendidos são combinados em um bloco de regras no CSS final.

- **Mixins**:
  
  - São blocos reutilizáveis de código que podem ser incluídos onde necessário.
  - Podem aceitar argumentos para criar estilos dinâmicos.
  - Cada inclusão de um mixin adiciona código ao CSS final, o que pode aumentar o tamanho do arquivo.

**Exemplo com Mixins:**

```scss
@mixin button-style($bg-color) {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: $bg-color;
  color: white;
}

.success-button {
  @include button-style(green);
}

.error-button {
  @include button-style(red);
}
```

Isso resultará em:

```css
.success-button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: green;
  color: white;
}

.error-button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: red;
  color: white;
}
```

#### 3. Placeholders com %

Placeholders, definidos com `%`, são usados com `@extend` para criar estilos reutilizáveis sem gerar código CSS até serem estendidos. Isso é útil para definir estilos que não devem aparecer diretamente no CSS, mas que podem ser reutilizados por outros seletores.

**Exemplo:**

```scss
%button-base {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  color: white;
}

.success-button {
  @extend %button-base;
  background-color: green;
}

.error-button {
  @extend %button-base;
  background-color: red;
}
```

Isso resultará em:

```css
.success-button, .error-button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  color: white;
}

.success-button {
  background-color: green;
}

.error-button {
  background-color: red;
}
```

### Resumo

- **@extend**: Usado para herança de estilos entre seletores, resultando em CSS mais compacto.
- **Mixins**: Blocos de código reutilizáveis que podem aceitar argumentos e adicionar código CSS onde são incluídos.
- **Placeholders (%)**: Definem estilos reutilizáveis sem gerar CSS até serem estendidos, útil para manter o CSS limpo e modular.

Pronto para avançar ou há alguma dúvida sobre esses conceitos?
