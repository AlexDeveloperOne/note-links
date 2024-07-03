### Aula 10: Interpolação em SCSS

A interpolação em SCSS é uma funcionalidade poderosa que permite inserir dinamicamente valores de variáveis, cálculos ou outras expressões em seletores e propriedades CSS. Isso é feito usando a sintaxe `#{}`. Vamos explorar como usar a interpolação para criar seletores e propriedades dinâmicas.

#### 1. Interpolação em Seletores

Você pode usar interpolação para criar seletores dinâmicos baseados em variáveis ou outras expressões. Isso é especialmente útil quando você precisa gerar vários seletores semelhantes.

**Exemplo:**

```scss
$base: 'col';

@for $i from 1 through 4 {
  .#{$base}-#{$i} {
    width: 100% / $i;
  }
}
```

Neste exemplo, estamos criando classes `.col-1`, `.col-2`, `.col-3`, e `.col-4`, cada uma com uma largura proporcional.

#### 2. Interpolação em Propriedades

A interpolação também pode ser usada em nomes de propriedades. Isso é útil quando você quer definir dinamicamente várias propriedades semelhantes.

**Exemplo:**

```scss
$prop: 'margin';

.container {
  #{$prop}-top: 10px;
  #{$prop}-right: 15px;
  #{$prop}-bottom: 10px;
  #{$prop}-left: 15px;
}
```

Neste exemplo, estamos criando as propriedades `margin-top`, `margin-right`, `margin-bottom`, e `margin-left` usando a interpolação da variável `$prop`.

#### 3. Interpolação em Valores de Propriedades

Você pode interpolar variáveis ou expressões diretamente nos valores das propriedades.

**Exemplo:**

```scss
$base-color: blue;
$darken-percentage: 20%;

.button {
  background-color: #{$base-color};
  color: darken(#{$base-color}, $darken-percentage);
}
```

Aqui, estamos definindo a cor de fundo como `blue` e a cor do texto como uma versão escurecida de `blue`.

#### 4. Interpolação em Strings

A interpolação permite combinar strings e variáveis para formar novos valores.

**Exemplo:**

```scss
$font-stack: 'Helvetica, Arial, sans-serif';
$primary-font: 'Helvetica';

body {
  font-family: #{$font-stack};
}

.primary-text {
  font-family: $primary-font;
}
```

Neste exemplo, usamos a interpolação para definir a propriedade `font-family` dinamicamente.

### Exercícios Práticos

1. **Crie Seletores Dinâmicos:**
   
   - Use uma variável para definir um prefixo de classe e gere várias classes com diferentes valores de propriedade.
   
   - **Exemplo:**
     
     ```scss
     $prefix: 'item';
     
     @for $i from 1 through 3 {
       .#{$prefix}-#{$i} {
         font-size: 10px * $i;
       }
     }
     ```

2. **Defina Propriedades Dinâmicas:**
   
   - Use a interpolação para criar várias propriedades com base em uma variável.
   
   - **Exemplo:**
     
     ```scss
     $spacing: 'padding';
     
     .box {
       #{$spacing}-top: 10px;
       #{$spacing}-bottom: 15px;
       #{$spacing}-left: 5px;
       #{$spacing}-right: 5px;
     }
     ```

3. **Combine Strings e Variáveis:**
   
   - Crie uma variável com uma parte de uma string e use a interpolação para completar a string em diferentes propriedades.
   
   - **Exemplo:**
     
     ```scss
     $theme-color: 'red';
     
     .header {
       background-color: #{$theme-color};
       border-color: darken(#{$theme-color}, 20%);
     }
     ```

### Conclusão

A interpolação em SCSS oferece flexibilidade e dinamismo na escrita de CSS, permitindo que você crie seletores e propriedades de maneira eficiente e reutilizável. Pratique os exemplos fornecidos e experimente diferentes combinações para ver como a interpolação pode simplificar seu trabalho com SCSS.
