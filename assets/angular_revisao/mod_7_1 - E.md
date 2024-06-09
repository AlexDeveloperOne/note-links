https://chatgpt.com/share/62f310b3-be01-4b02-98f9-85d9e453ac2a


# Ger. Estado c/ NgRx

May 26, 2024

Meu professor, poço que me ê a aula do Módulo 7: Gerenciamento de Estado que é: NgRx que aborda os assuntos abaixo:  Introdução ao Redux e NgRx

ChatGPT

Claro, aqui está um resumo abrangente da aula sobre o Módulo 7: Gerenciamento de Estado com NgRx, incluindo uma introdução ao Redux e NgRx.

### Módulo 7: Gerenciamento de Estado com NgRx

#### Introdução ao Redux

Redux é uma biblioteca para gerenciamento de estado previsível em aplicações JavaScript, geralmente usada com React, mas também aplicável a outras bibliotecas e frameworks, como Angular (com NgRx). Redux se baseia em três princípios fundamentais:

1. **Store Única**: Toda a aplicação tem uma única store, que contém o estado global. Isso facilita a manutenção e o debug da aplicação.
2. **Estado Imutável**: O estado é imutável e só pode ser alterado enviando actions. Isso significa que o estado nunca é modificado diretamente, mas sim substituído por uma nova versão modificada.
3. **Pure Functions (Reducers)**: As alterações no estado são feitas por funções puras chamadas reducers, que recebem o estado atual e uma action, e retornam um novo estado.

Esses princípios ajudam a criar aplicações mais previsíveis e fáceis de testar.

#### Fluxo de Trabalho do Redux

1. **Dispatch**: Uma action é disparada.
2. **Reducers**: A action é processada por reducers que produzem um novo estado.
3. **Store**: O novo estado é armazenado na store.
4. **View**: A interface do usuário (UI) é atualizada para refletir o novo estado.

#### Introdução ao NgRx

NgRx é uma implementação do Redux para Angular. Ele proporciona um conjunto de bibliotecas para gerenciar o estado de aplicações Angular, seguindo os mesmos princípios do Redux. NgRx é composto por vários pacotes, cada um com uma função específica:

1. **@ngrx/store**: Para gerenciar o estado e fazer a comunicação entre componentes através da store.
2. **@ngrx/effects**: Para gerenciar efeitos colaterais (side effects) como chamadas HTTP.
3. **@ngrx/entity**: Para gerenciar coleções de entidades de forma mais fácil.
4. **@ngrx/router-store**: Para sincronizar o estado do roteador com a store.
5. **@ngrx/store-devtools**: Para integrar com ferramentas de desenvolvimento, como o Redux DevTools.

#### Fluxo de Trabalho do NgRx

1. **Action**: Define um evento que descreve algo que aconteceu na aplicação. Pode conter payloads com dados necessários.
2. **Reducer**: Função pura que toma o estado atual e uma action, e retorna um novo estado.
3. **Selector**: Funções para selecionar partes do estado da store.
4. **Effect**: Gerencia operações assíncronas, como chamadas a APIs, que despacham novas actions conforme necessário.

#### Exemplo Prático com NgRx

1. **Definindo Actions**:

```typescript
import { createAction, props } from '@ngrx/store';

export const loadItems = createAction('[Item List] Load Items');
export const loadItemsSuccess = createAction('[Item List] Load Items Success', props<{ items: Item[] }>());
export const loadItemsFailure = createAction('[Item List] Load Items Failure', props<{ error: any }>());
```

1. **Criando Reducers**:

```typescript
import { createReducer, on } from '@ngrx/store';
import { loadItems, loadItemsSuccess, loadItemsFailure } from './item.actions';

export const initialState = {
  items: [],
  loading: false,
  error: null
};

const _itemReducer = createReducer(
  initialState,
  on(loadItems, state => ({ ...state, loading: true })),
  on(loadItemsSuccess, (state, { items }) => ({ ...state, loading: false, items })),
  on(loadItemsFailure, (state, { error }) => ({ ...state, loading: false, error }))
);

export function itemReducer(state, action) {
  return _itemReducer(state, action);
}
```

1. **Criando Effects**:

```typescript
import { Injectable } from '@angular/core';
import { Actions, createEffect, ofType } from '@ngrx/effects';
import { of } from 'rxjs';
import { catchError, map, mergeMap } from 'rxjs/operators';
import { ItemService } from './item.service';
import { loadItems, loadItemsSuccess, loadItemsFailure } from './item.actions';

@Injectable()
export class ItemEffects {
  loadItems$ = createEffect(() => this.actions$.pipe(
    ofType(loadItems),
    mergeMap(() => this.itemService.getAll()
      .pipe(
        map(items => loadItemsSuccess({ items })),
        catchError(error => of(loadItemsFailure({ error })))
      ))
    )
  );

  constructor(
    private actions$: Actions,
    private itemService: ItemService
  ) {}
}
```

1. **Configurando a Store no Angular Module**:

```typescript
import { NgModule } from '@angular/core';
import { StoreModule } from '@ngrx/store';
import { EffectsModule } from '@ngrx/effects';
import { itemReducer } from './item.reducer';
import { ItemEffects } from './item.effects';

@NgModule({
  imports: [
    StoreModule.forRoot({ items: itemReducer }),
    EffectsModule.forRoot([ItemEffects])
  ],
  declarations: [/* seus componentes */],
  providers: [ItemService]
})
export class AppModule {}
```

#### Conclusão

NgRx fornece uma maneira estruturada e previsível de gerenciar o estado da aplicação, tornando-a mais fácil de entender, testar e manter. Com a combinação de actions, reducers, selectors e effects, você pode gerenciar o estado de forma eficiente, especialmente em aplicações complexas.

Se você tiver dúvidas específicas ou precisar de mais detalhes sobre algum tópico, sinta-se à vontade para perguntar!

[Get started with ChatGPT](https://chatgpt.com/)

Report content|[Terms of use](https://openai.com/policies/terms-of-use)|[Privacy policy](https://openai.com/policies/privacy-policy)|

?

