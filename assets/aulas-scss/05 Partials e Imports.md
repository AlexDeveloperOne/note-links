### Aula 05 de SCSS: Partials e Imports

#### 1. Criação de Arquivos Parciais

No SCSS, arquivos parciais são usados para dividir o código em partes menores e mais gerenciáveis. Um arquivo parcial é apenas um arquivo SCSS normal, mas seu nome começa com um sublinhado (`_`). Por exemplo:

```scss
// _variables.scss
$primary-color: #3498db;
$font-stack: 'Helvetica, sans-serif';
```

#### 2. Uso da Diretiva `@import`

Para utilizar os arquivos parciais no seu arquivo SCSS principal, você usa a diretiva `@import`. Isso permite que você modularize seu código e importe apenas os arquivos que precisa. 

Exemplo:

```scss
// main.scss
@import 'variables';

body {
  font-family: $font-stack;
  color: $primary-color;
}
```

Note que ao usar `@import`, você não precisa incluir o sublinhado `_` nem a extensão `.scss`.

#### 3. Modularização do Código SCSS

A modularização ajuda a manter o código organizado e fácil de manter. Aqui está um exemplo de como você pode estruturar seu projeto SCSS usando partials e `@import`:

1. **Estrutura de Pastas:**
   
   ```
   styles/
   ├── _variables.scss
   ├── _mixins.scss
   ├── _base.scss
   ├── _layout.scss
   ├── _components.scss
   └── main.scss
   ```

2. **Conteúdo dos Arquivos:**
   
   ```scss
   // _variables.scss
   $primary-color: #3498db;
   $secondary-color: #2ecc71;
   $font-stack: 'Helvetica, sans-serif';
   ```
   
   ```scss
   // _mixins.scss
   @mixin border-radius($radius) {
     -webkit-border-radius: $radius;
        -moz-border-radius: $radius;
         -ms-border-radius: $radius;
             border-radius: $radius;
   }
   ```
   
   ```scss
   // _base.scss
   body {
     font-family: $font-stack;
     color: $primary-color;
   }
   ```
   
   ```scss
   // _layout.scss
   .container {
     width: 80%;
     margin: 0 auto;
   }
   ```
   
   ```scss
   // _components.scss
   .button {
     background-color: $secondary-color;
     @include border-radius(5px);
   }
   ```
   
   ```scss
   // main.scss
   @import 'variables';
   @import 'mixins';
   @import 'base';
   @import 'layout';
   @import 'components';
   ```

Ao fazer isso, você mantém cada parte do seu código SCSS em arquivos separados, o que torna mais fácil localizar e atualizar estilos específicos sem mexer em um único arquivo gigantesco.

### Conclusão

O uso de partials e `@import` no SCSS é fundamental para manter seu código organizado, modular e fácil de manter. Com essas práticas, você pode facilmente dividir seu código em partes reutilizáveis e gerenciáveis.