### Aula 13 de SCSS: Boas Práticas

#### Organização de Arquivos SCSS

Uma boa organização de arquivos SCSS é essencial para a manutenção e escalabilidade do projeto. Aqui estão algumas práticas recomendadas:

1. **Divisão em Partials**: Quebre seu arquivo SCSS em vários arquivos menores, conhecidos como "partials". Esses arquivos menores são importados em um arquivo principal, geralmente chamado de `main.scss` ou `styles.scss`.
   
   ```scss
   // main.scss
   @import 'base/reset';
   @import 'base/typography';
   @import 'layout/grid';
   @import 'components/buttons';
   @import 'components/forms';
   ```

2. **Estrutura de Pastas**:
   
   - `base/`: Contém reset, variáveis, mixins, etc.
   
   - `layout/`: Estilos relacionados ao layout, como grids e containers.
   
   - `components/`: Estilos para componentes reutilizáveis como botões, formulários, cards, etc.
   
   - `pages/`: Estilos específicos para páginas.
   
   - `themes/`: Temas ou variações de estilos.
   
   - `utils/`: Funções, mixins e outros utilitários.
     
     Exemplo de estrutura de pastas:
     
     ```
     styles/
     ├── base/
     │   ├── _reset.scss
     │   ├── _typography.scss
     │   ├── _variables.scss
     ├── layout/
     │   ├── _grid.scss
     │   ├── _header.scss
     ├── components/
     │   ├── _buttons.scss
     │   ├── _forms.scss
     ├── pages/
     │   ├── _home.scss
     │   ├── _about.scss
     ├── themes/
     │   ├── _dark.scss
     │   ├── _light.scss
     ├── utils/
     │   ├── _mixins.scss
     │   ├── _functions.scss
     └── main.scss
     ```

#### Convenções de Nomenclatura

Seguir convenções de nomenclatura consistentes ajuda na legibilidade e na manutenção do código.

1. **BEM (Block Element Modifier)**: Um método popular de nomenclatura que melhora a estrutura e a clareza do código.
   
   ```scss
   .block {
     &__element {
       &--modifier {
         // Estilos aqui
       }
     }
   }
   ```
   
    Exemplo:
   
   ```scss
   .button {
     &__icon {
       &--large {
         // Estilos aqui
       }
     }
   }
   ```

2. **Kebeb-case para Variáveis e Mixins**: Use kebab-case para variáveis e mixins para manter consistência.
   
   ```scss
   // Variáveis
   $primary-color: #3498db;
   
   // Mixins
   @mixin center-content {
     display: flex;
     justify-content: center;
     align-items: center;
   }
   ```

3. **Prefixos para Classes Utilitárias**: Use prefixos como `u-` para classes utilitárias para diferenciá-las facilmente de outras classes.
   
   ```scss
   .u-margin-top-small {
     margin-top: 10px;
   }
   ```

#### Performance e Otimização

Para garantir que o código SCSS seja eficiente e performático, siga estas práticas:

1. **Minimização do CSS**: Use ferramentas como `cssnano` para minificar o CSS em produção.
   
   ```bash
   npm install cssnano --save-dev
   ```

2. **Remoção de Código Morto**: Utilize ferramentas como `purgecss` para remover CSS não utilizado.
   
   ```bash
   npm install @fullhuman/postcss-purgecss --save-dev
   ```

3. **Evitar aninhamento excessivo**: Aninhamento excessivo pode levar a CSS complexo e difícil de manter. Limite o aninhamento a no máximo 3 níveis.
   
   ```scss
   .navbar {
     .nav-item {
       .nav-link {
         // Não aninhe mais do que isso
       }
     }
   }
   ```

4. **Uso de Variáveis e Mixins**: Aproveite variáveis para valores repetitivos e mixins para conjuntos de propriedades repetitivas, evitando redundâncias.
   
   ```scss
   // Variáveis
   $font-stack: 'Helvetica, sans-serif';
   $primary-color: #333;
   
   // Uso de variáveis
   body {
     font: 100% $font-stack;
     color: $primary-color;
   }
   
   // Mixins
   @mixin border-radius($radius) {
     border-radius: $radius;
   }
   
   .box { 
     @include border-radius(10px); 
   }
   ```

5. **Arquivos Fonte Pequenos**: Mantenha os arquivos SCSS menores para reduzir o tempo de compilação e facilitar a manutenção. Utilize a organização em partials.

### Conclusão

Seguindo essas boas práticas de organização de arquivos, convenções de nomenclatura e otimização de performance, você poderá escrever código SCSS mais eficiente, legível e fácil de manter. Mantenha-se atualizado com novas técnicas e ferramentas para continuar aprimorando seu workflow de desenvolvimento.
