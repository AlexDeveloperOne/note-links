## Módulo 6: Async/Await

Olá alunos,

Hoje vamos mergulhar em um conceito incrível e poderoso do ECMAScript 2017: Async/Await. Este recurso foi introduzido para tornar o trabalho com código assíncrono mais limpo, legível e fácil de entender. Vamos explorar o que é Async/Await e como podemos usá-lo para melhorar nosso código.

#### a. O que é Async/Await?

Async/Await é uma sintaxe no JavaScript que facilita a escrita e o entendimento do código assíncrono. Antes do Async/Await, trabalhar com operações assíncronas geralmente envolvia o uso de callbacks ou Promises encadeadas, o que às vezes podia levar a um código complicado e difícil de acompanhar. Com Async/Await, podemos escrever código assíncrono de forma mais sequencial e parecida com código síncrono, tornando-o mais compreensível.

#### b. Definindo funções assíncronas

Para começar a usar o Async/Await, primeiro precisamos entender como definir funções assíncronas. Uma função assíncrona é uma função que opera de forma assíncrona, o que significa que ela pode realizar tarefas enquanto aguarda o resultado de operações assíncronas, como a obtenção de dados de um servidor.

Para definir uma função assíncrona, utilizamos a palavra-chave async antes da palavra-chave function, como mostrado no exemplo abaixo:

```javascript
async function minhaFuncaoAssincrona() {
    // Código assíncrono aqui
}
```

Isso indica que `minhaFuncaoAssincrona` é uma função assíncrona que pode conter código assíncrono.

#### c. Utilizando a palavra-chave await

Agora que sabemos como definir funções assíncronas, podemos usar a palavra-chave await dentro delas para aguardar o resultado de operações assíncronas, como a resolução de Promises. O await pausa a execução da função assíncrona até que a Promise seja resolvida e retorna o resultado dessa Promise.

Veja um exemplo de como usar await dentro de uma função assíncrona:

```javascript
Copy code
async function minhaFuncaoAssincrona() {
    // Aguarda a Promise ser resolvida e atribui o resultado a uma variável
    let resultado = await minhaPromise;
    
    // Código para continuar após a Promise ser resolvida
}
```

Dessa forma, podemos escrever código assíncrono de forma mais clara e fácil de entender.

Espero que esta introdução ao Async/Await tenha sido útil para vocês. Pratiquem e experimentem com este recurso para tornar seu código mais eficiente e legível. Se tiverem alguma dúvida, não hesitem em perguntar!



## Outro exemplo de Async/Await:

Vamos ver um exemplo mais robusto que demonstra como o Async/Await pode ser útil em situações do mundo real.

Suponha que estamos desenvolvendo um aplicativo de previsão do tempo, e precisamos fazer uma chamada assíncrona para uma API de previsão do tempo para obter os dados mais recentes. Vamos criar uma função assíncrona que faz essa chamada e exibe os dados da previsão.

```javascript
// Função para buscar dados da previsão do tempo de uma API assíncrona
async function buscarPrevisaoTempo(cidade) {
    try {
        // Fazemos uma chamada assíncrona para a API de previsão do tempo
        let resposta = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${cidade}&appid=SEU_APP_ID`);
        
        // Aguardamos a resposta da API e convertemos para JSON
        let dados = await resposta.json();

        // Exibimos os dados da previsão do tempo
        console.log(`Previsão do tempo para ${cidade}:`);
        console.log(`- Temperatura: ${dados.main.temp}°C`);
        console.log(`- Tempo: ${dados.weather[0].description}`);
    } catch (erro) {
        // Em caso de erro, exibimos uma mensagem de erro
        console.error('Erro ao buscar previsão do tempo:', erro);
    }
}

// Chamamos a função para buscar a previsão do tempo para uma cidade específica
buscarPrevisaoTempo('São Paulo');
```
Neste exemplo:

- Definimos uma função assíncrona `buscarPrevisaoTempo`, que recebe o nome de uma cidade como parâmetro.
- Dentro da função assíncrona, fazemos uma chamada assíncrona para a API de previsão do tempo usando `fetch`.
- Usamos `await` para aguardar a resposta da API e depois converter os dados para JSON.
- Exibimos os dados da previsão do tempo na console.
- Se ocorrer algum erro durante o processo, tratamos o erro e exibimos uma mensagem de erro.

Este exemplo demonstra como o Async/Await pode simplificar o código ao lidar com operações assíncronas, tornando-o mais legível e fácil de entender, mesmo em situações do mundo real, como fazer chamadas assíncronas para APIs externas.

