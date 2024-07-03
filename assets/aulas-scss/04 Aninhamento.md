### Aula 04 de SCSS: Aninhamento (Nesting)

Nesta aula, vamos explorar o conceito de aninhamento (nesting) em SCSS, que permite escrever CSS de uma forma mais organizada e hierárquica. Vamos cobrir:

1. Aninhamento de seletores
2. Operador de concatenar `&`
3. Diretriz `@at-root`

#### 1. Aninhamento de Seletores

O aninhamento em SCSS permite que você escreva seletores dentro de outros seletores, refletindo a hierarquia HTML de forma mais clara. Por exemplo, em vez de escrever CSS de forma plana, você pode aninhar seletores para mostrar a relação entre eles.

##### Exemplo sem aninhamento:

```css
.navbar {
  background-color: #333;
}

.navbar .nav-item {
  color: white;
}

.navbar .nav-item .nav-link {
  text-decoration: none;
}
```

##### Exemplo com aninhamento:

```scss
.navbar {
  background-color: #333;

  .nav-item {
    color: white;

    .nav-link {
      text-decoration: none;
    }
  }
}
```

No exemplo acima, o código SCSS aninhado reflete a estrutura do HTML, facilitando a leitura e a manutenção.

#### 2. Operador de Concatenar `&`

O operador `&` é usado em SCSS para fazer referência ao seletor pai dentro de um bloco de regras aninhado. Ele pode ser útil para criar seletores mais complexos, como pseudo-classes e modificadores de classe.

##### Exemplo básico:

```scss
.button {
  color: blue;

  &:hover {
    color: red;
  }
}
```

##### Exemplo com modificadores de classe:

```scss
.button {
  color: blue;

  &--large {
    font-size: 20px;
  }

  &--small {
    font-size: 10px;
  }
}
```

#### 3. Diretriz `@at-root`

A diretriz `@at-root` permite que você "saia" do contexto de aninhamento atual e defina estilos no nível raiz. Isso é útil quando você quer aplicar estilos fora do contexto aninhado.

##### Exemplo básico:

```scss
.container {
  color: black;

  @at-root {
    .global-style {
      background-color: yellow;
    }
  }
}
```

##### Exemplo com interpolação:

```scss
.nav {
  ul {
    margin: 0;

    @at-root {
      #{&}__item {
        list-style: none;
      }
    }
  }
}
```

No exemplo acima, o seletor `.nav ul` será aninhado normalmente, mas o `.nav__item` será gerado no nível raiz.

### Prática

Para consolidar o aprendizado, pratique reescrevendo seus estilos CSS usando aninhamento em SCSS. Experimente utilizar o operador `&` para criar pseudo-classes e modificadores de classe, e utilize `@at-root` quando precisar definir estilos fora do contexto aninhado.

Se tiver alguma dúvida ou quiser mais exemplos, estarei aqui para ajudar!