https://chatgpt.com/share/4bd1c0b2-a4c5-4a6b-a34d-ceb91ba65635

# Interceptores HTTP em Angular.

May 26, 2024

Meu professor, poço que me ê a aula do Módulo 6: Comunicação com APIs que é: HTTPClient que aborda os assuntos abaixo:  Interceptores de HTTP

ChatGPT

Claro! Vou te dar uma visão geral sobre interceptores de HTTP no contexto do HTTPClient.

### Interceptores de HTTP

Interceptores de HTTP são uma funcionalidade poderosa disponível em muitas bibliotecas de cliente HTTP, como o Angular HttpClient, Axios, e outras. Eles permitem interceptar e modificar solicitações HTTP ou respostas antes que elas sejam processadas pela aplicação.

#### O que são Interceptores de HTTP?

Interceptores de HTTP são componentes que podem ser inseridos na cadeia de solicitações/respostas HTTP. Eles permitem executar lógica personalizada em diferentes estágios do ciclo de vida de uma solicitação HTTP:

1. **Antes de enviar a solicitação**: Permite modificar a solicitação, adicionar cabeçalhos de autenticação, registrar ou modificar os parâmetros da solicitação.
2. **Depois de receber a resposta**: Permite manipular a resposta recebida, lidar com erros de forma centralizada, ou modificar os dados da resposta antes que eles cheguem ao serviço ou componente que fez a solicitação.

#### Como Funcionam os Interceptores?

Os interceptores são geralmente registrados em uma cadeia (pipeline) onde cada um pode modificar a solicitação ou resposta e passar para o próximo interceptor na cadeia.

Aqui está um exemplo genérico em TypeScript usando o Angular HttpClient:

```typescript
import { Injectable } from '@angular/core';
import { HttpEvent, HttpInterceptor, HttpHandler, HttpRequest, HttpResponse } from '@angular/common/http';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class MyHttpInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    // Manipula a solicitação antes de enviar
    const clonedRequest = req.clone({
      headers: req.headers.set('Authorization', 'Bearer my-token')
    });

    console.log('Request:', clonedRequest);

    return next.handle(clonedRequest).pipe(
      tap(event => {
        if (event instanceof HttpResponse) {
          // Manipula a resposta recebida
          console.log('Response:', event);
        }
      })
    );
  }
}
```

Neste exemplo, `MyHttpInterceptor` intercepta todas as solicitações HTTP, adiciona um cabeçalho de autorização e loga a solicitação e resposta.

#### Benefícios dos Interceptores

1. **Reutilização de Código**: Código comum, como autenticação e tratamento de erros, pode ser centralizado.
2. **Centralização da Lógica de Negócio**: Pode lidar com lógica complexa, como retry policies ou cache, em um único lugar.
3. **Facilidade de Manutenção**: Alterações podem ser feitas em um ponto central sem necessidade de modificar cada chamada de serviço.

#### Registro de Interceptores

Em Angular, por exemplo, registramos os interceptores no módulo principal da aplicação:

```typescript
import { HTTP_INTERCEPTORS } from '@angular/common/http';
import { MyHttpInterceptor } from './my-http-interceptor';

@NgModule({
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: MyHttpInterceptor, multi: true }
  ]
})
export class AppModule {}
```

O `multi: true` indica que podem haver múltiplos interceptores.

#### Interceptores em Outras Bibliotecas

Em outras bibliotecas como Axios, a configuração de um interceptor é similar:

```javascript
import axios from 'axios';

// Intercepta a solicitação
axios.interceptors.request.use(request => {
  request.headers['Authorization'] = 'Bearer my-token';
  console.log('Request:', request);
  return request;
});

// Intercepta a resposta
axios.interceptors.response.use(response => {
  console.log('Response:', response);
  return response;
}, error => {
  console.error('Error:', error);
  return Promise.reject(error);
});
```

#### Considerações Finais

Os interceptores são uma ferramenta poderosa para manipular solicitações e respostas HTTP de maneira centralizada e reutilizável. Eles melhoram a manutenção e a clareza do código ao mover lógica repetitiva para um único lugar.

Espero que isso ajude a entender melhor os interceptores de HTTP! Se tiver alguma dúvida específica ou precisar de mais exemplos, sinta-se à vontade para perguntar.

[Get started with ChatGPT](https://chatgpt.com/)

Report content|[Terms of use](https://openai.com/policies/terms-of-use)|[Privacy policy](https://openai.com/policies/privacy-policy)|



