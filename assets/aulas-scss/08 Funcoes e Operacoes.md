### Aula 08: Funções e Operações no SCSS

#### Funções Embutidas no SCSS

O SCSS oferece uma variedade de funções embutidas que facilitam operações comuns. Estas funções são categorizadas em diferentes tipos, como funções de cores, funções matemáticas e funções de strings.

##### Funções de Cores

As funções de cores permitem manipular e ajustar cores. Aqui estão algumas das mais comuns:

- `lighten($color, $amount)`: Clareia uma cor.
- `darken($color, $amount)`: Escurece uma cor.
- `saturate($color, $amount)`: Aumenta a saturação de uma cor.
- `desaturate($color, $amount)`: Diminui a saturação de uma cor.
- `mix($color1, $color2, [$weight])`: Mistura duas cores.

Exemplo:

```scss
$primary-color: #3498db;

.button {
  background-color: $primary-color;
  border-color: darken($primary-color, 10%);
  color: lighten($primary-color, 40%);
}
```

##### Funções Matemáticas

As funções matemáticas são úteis para realizar cálculos diretamente no SCSS:

- `percentage($value)`: Converte um número em uma porcentagem.
- `round($value)`: Arredonda um número.
- `ceil($value)`: Arredonda um número para cima.
- `floor($value)`: Arredonda um número para baixo.

Exemplo:

```scss
$base-padding: 16px;

.container {
  padding: $base-padding;
  margin: ceil($base-padding / 3);
}
```

##### Funções de Strings

As funções de strings ajudam a manipular strings:

- `quote($string)`: Adiciona aspas a uma string.
- `unquote($string)`: Remove aspas de uma string.
- `str-length($string)`: Retorna o comprimento de uma string.
- `to-upper-case($string)`: Converte uma string para maiúsculas.
- `to-lower-case($string)`: Converte uma string para minúsculas.

Exemplo:

```scss
$font-family: unquote("Helvetica, Arial, sans-serif");

body {
  font-family: $font-family;
}
```

#### Criando Funções Personalizadas

Além das funções embutidas, você também pode criar suas próprias funções no SCSS usando a diretiva `@function`.

##### Sintaxe Básica

```scss
@function nome-da-funcao($parametro1, $parametro2) {
  // lógica da função
  @return resultado;
}
```

##### Exemplo: Função para Converter Pixels em REM

```scss
@function px-to-rem($px, $base-font-size: 16px) {
  @return $px / $base-font-size * 1rem;
}

body {
  font-size: px-to-rem(18px);
  padding: px-to-rem(24px, 18px);
}
```

##### Exemplo: Função para Calcular a Área de um Retângulo

```scss
@function area($width, $height) {
  @return $width * $height;
}

.box {
  width: 100px;
  height: 200px;
  content: "Área: #{area(100px, 200px)}";
}
```

### Resumo

Nesta aula, você aprendeu sobre:

1. **Funções Embutidas no SCSS**
   - Funções de cores: `lighten`, `darken`, `saturate`, `desaturate`, `mix`.
   - Funções matemáticas: `percentage`, `round`, `ceil`, `floor`.
   - Funções de strings: `quote`, `unquote`, `str-length`, `to-upper-case`, `to-lower-case`.
2. **Criando Funções Personalizadas**
   - Como definir uma função personalizada usando `@function`.
   - Exemplos de funções personalizadas para converter pixels em REM e calcular a área de um retângulo.

Agora você pode utilizar funções embutidas e criar suas próprias funções para manipular e calcular valores em seus estilos SCSS!
