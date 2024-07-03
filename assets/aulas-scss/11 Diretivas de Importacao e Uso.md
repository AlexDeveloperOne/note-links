### Aula 11 de SCSS: Diretivas de Importação e Uso

#### 1. @import e @use

Em SCSS, as diretivas `@import` e `@use` são usadas para incluir arquivos externos em seu projeto. No entanto, cada uma tem suas peculiaridades e é importante entender suas diferenças e como utilizá-las corretamente.

##### @import

A diretiva `@import` permite que você importe arquivos SCSS ou CSS diretamente em seu arquivo principal. Por exemplo:

```scss
@import 'variables';
@import 'mixins';
@import 'reset';
```

No entanto, `@import` tem algumas limitações, como a possibilidade de criar problemas de desempenho ao compilar, pois pode importar os mesmos arquivos várias vezes. 

##### @use

A diretiva `@use` é uma maneira mais moderna e eficiente de importar arquivos SCSS. Ela carrega o arquivo apenas uma vez e permite um melhor gerenciamento de namespaces. Por exemplo:

```scss
@use 'variables';
@use 'mixins';
@use 'reset';
```

Ao usar `@use`, você precisa prefixar as variáveis e mixins com o nome do módulo. Isso ajuda a evitar conflitos de nomes:

```scss
@use 'variables' as vars;

body {
  color: vars.$primary-color;
}
```

#### 2. Diferenças entre @import e @use

- **Reimportação**: `@import` pode importar o mesmo arquivo várias vezes, enquanto `@use` carrega o arquivo apenas uma vez.
- **Namespaces**: `@use` utiliza namespaces, evitando conflitos de nomes, enquanto `@import` insere o conteúdo diretamente no escopo global.
- **Performance**: `@use` melhora a performance ao evitar reimportações desnecessárias.
- **Estrutura e Manutenção**: `@use` ajuda a criar um código mais modular e organizado, facilitando a manutenção.

#### 3. Namespaces e como usá-los

Namespaces em SCSS são utilizados para evitar conflitos de nomes, especialmente em projetos grandes. Com `@use`, cada módulo importado tem seu próprio namespace.

##### Exemplo de uso de namespaces:

**Arquivo `_variables.scss`**

```scss
$primary-color: #333;
$secondary-color: #666;
```

**Arquivo `_mixins.scss`**

```scss
@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

**Arquivo `styles.scss`**

```scss
@use 'variables' as vars;
@use 'mixins' as mix;

body {
  color: vars.$primary-color;
}

.container {
  @include mix.center;
}
```

#### Vantagens de Usar Namespaces:

- **Evita Conflitos**: Cada módulo tem seu próprio namespace, evitando conflitos de nomes.
- **Clareza**: Facilita a leitura e manutenção do código, pois fica claro de onde cada variável ou mixin está vindo.
- **Modularidade**: Permite um desenvolvimento mais modular, onde cada parte do código pode ser trabalhada separadamente.

### Exercício Prático

Para fixar o aprendizado, crie um pequeno projeto SCSS seguindo os passos abaixo:

1. Crie três arquivos SCSS: `_variables.scss`, `_mixins.scss` e `styles.scss`.
2. No arquivo `_variables.scss`, defina algumas variáveis de cores.
3. No arquivo `_mixins.scss`, defina alguns mixins úteis.
4. No arquivo `styles.scss`, importe os arquivos utilizando `@use` e aplique as variáveis e mixins em alguns estilos básicos.

Com isso, você terá uma compreensão prática de como utilizar as diretivas `@import` e `@use` no SCSS, além de entender as vantagens dos namespaces.

Se tiver alguma dúvida ou precisar de mais exemplos, estou aqui para ajudar!
