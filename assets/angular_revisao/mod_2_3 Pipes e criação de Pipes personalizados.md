https://chatgpt.com/share/20a71f26-9fa3-457e-be91-61f12ef217df



# Criar Pipes Personalizados.

May 25, 2024



Anonymous

Meu professor, peço que me ê a aula do Módulo 2: Fundamentos do Angular que é: Templates que aborda os assuntos abaixo: - Pipes e criação de Pipes personalizados

ChatGPT

Claro, aqui está uma aula sobre Templates do Angular focando em Pipes e criação de Pipes personalizados.

------

### Módulo 2: Fundamentos do Angular

## Aula: Templates - Pipes e Criação de Pipes Personalizados

### Objetivos da Aula

1. Compreender o que são Pipes em Angular e sua utilidade.
2. Aprender a usar os Pipes embutidos no Angular.
3. Criar Pipes personalizados para atender necessidades específicas.

### 1. Introdução aos Pipes

Os Pipes no Angular são uma maneira de transformar dados em templates. Eles recebem um valor, processam esse valor e retornam um valor transformado para exibição.

#### Exemplo de Pipes embutidos:

- `date` - formata datas.
- `uppercase` e `lowercase` - transforma texto em maiúsculas ou minúsculas.
- `currency` - formata números como moeda.
- `percent` - formata números como porcentagem.

**Sintaxe básica:**

```html
{{ value | pipeName }}
```

**Exemplo:**

```html
<p>{{ birthday | date }}</p>
```

Isso transforma o valor de `birthday` em uma data formatada.

### 2. Utilizando Pipes Embutidos

#### Date Pipe:

```html
<p>Data: {{ today | date:'dd/MM/yyyy' }}</p>
```

Formata a data atual no formato `dia/mês/ano`.

#### Currency Pipe:

```html
<p>Preço: {{ price | currency:'BRL':'symbol' }}</p>
```

Formata o valor `price` como moeda brasileira.

#### Uppercase e Lowercase:

```html
<p>{{ message | uppercase }}</p>
```

Transforma `message` em maiúsculas.

### 3. Criação de Pipes Personalizados

Às vezes, os Pipes embutidos não atendem a todas as necessidades, então é possível criar Pipes personalizados.

#### Passo a Passo para criar um Pipe personalizado:

1. **Gerar o Pipe:** Use o Angular CLI para gerar um Pipe:

   ```bash
   ng generate pipe custom
   ```

2. **Implementação do Pipe:** A implementação básica de um Pipe personalizado envolve a criação de uma classe que implementa a interface `PipeTransform`.

   **Exemplo:**

   ```typescript
   import { Pipe, PipeTransform } from '@angular/core';
   
   @Pipe({
     name: 'custom'
   })
   export class CustomPipe implements PipeTransform {
     transform(value: string, ...args: any[]): string {
       // Lógica de transformação aqui
       return value.split('').reverse().join('');
     }
   }
   ```

3. **Usando o Pipe no Template:** Após a criação, utilize o novo Pipe no template.

   ```html
   <p>{{ 'Olá Angular' | custom }}</p>
   ```

   Isso exibirá o texto invertido: "ralugnA álO".

#### Exemplo Detalhado: Pipe para Formatar Telefone

1. **Gerar o Pipe:**

   ```bash
   ng generate pipe phoneFormat
   ```

2. **Implementar o Pipe:**

   ```typescript
   import { Pipe, PipeTransform } from '@angular/core';
   
   @Pipe({
     name: 'phoneFormat'
   })
   export class PhoneFormatPipe implements PipeTransform {
     transform(value: string): string {
       if (!value) return value;
   
       let formattedValue = value.replace(/\D/g, '');
       if (formattedValue.length === 11) {
         return formattedValue.replace(/(\d{2})(\d{5})(\d{4})/, '($1) $2-$3');
       } else if (formattedValue.length === 10) {
         return formattedValue.replace(/(\d{2})(\d{4})(\d{4})/, '($1) $2-$3');
       }
       return value;
     }
   }
   ```

3. **Utilizar no Template:**

   ```html
   <p>Telefone: {{ '11987654321' | phoneFormat }}</p>
   ```

   Isso formatará o número de telefone para o padrão: (11) 98765-4321.

### 4. Conclusão

Os Pipes são uma ferramenta poderosa no Angular para transformar dados diretamente no template, facilitando a exibição de dados formatados sem lógica extra no componente. A criação de Pipes personalizados permite maior flexibilidade e reutilização de lógica de formatação em toda a aplicação.

### Exercícios Práticos

1. **Exercício 1:** Utilizar diferentes Pipes embutidos para formatar dados em um componente Angular.
2. **Exercício 2:** Criar um Pipe personalizado que transforme textos em camelCase.
3. **Exercício 3:** Implementar e usar um Pipe que formate números de CPF.

------

Se precisar de mais exemplos ou detalhes sobre algum dos tópicos, sinta-se à vontade para perguntar!

[Sign up to chat](https://chatgpt.com/)

Report content|[Terms of use](https://openai.com/policies/terms-of-use)|[Privacy policy](https://openai.com/policies/privacy-policy)|



