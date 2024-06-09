https://chatgpt.com/share/f2f2ccb7-abc8-4df6-9e87-17b8db988ed4



# Gerenciar Estado com NgRx

May 26, 2024

Meu professor, poço que me ê a aula do Módulo 7: Gerenciamento de Estado que é: NgRx que aborda os assuntos abaixo:  Actions, Reducers, Effects e Selectors

ChatGPT

Claro, posso ajudá-lo com uma explicação sobre o NgRx e seus principais componentes: Actions, Reducers, Effects e Selectors.

### Módulo 7: Gerenciamento de Estado com NgRx

#### Introdução ao NgRx

NgRx é uma biblioteca para Angular inspirada no padrão Redux, que facilita o gerenciamento do estado da aplicação de forma preditiva e escalável. Ele utiliza o conceito de unidirecionalidade do fluxo de dados, o que significa que o estado da aplicação flui em uma única direção, tornando o comportamento da aplicação mais previsível.

#### 1. Actions

**Ações** são objetos simples que representam uma intenção de mudar o estado. Cada ação tem um tipo (`type`) e, opcionalmente, um payload (dados adicionais que a ação pode carregar). As ações são despachadas (dispatched) para iniciar uma mudança de estado.

**Exemplo de uma ação:**

```typescript
import { createAction, props } from '@ngrx/store';

export const loadItems = createAction('[Item List] Load Items');
export const loadItemsSuccess = createAction('[Item List] Load Items Success', props<{ items: Item[] }>());
export const loadItemsFailure = createAction('[Item List] Load Items Failure', props<{ error: any }>());
```

#### 2. Reducers

**Reducers** são funções puras que especificam como o estado da aplicação deve mudar em resposta a uma ação. Eles recebem o estado atual e a ação como parâmetros e retornam um novo estado.

**Exemplo de um reducer:**

```typescript
import { createReducer, on } from '@ngrx/store';
import { loadItems, loadItemsSuccess, loadItemsFailure } from './item.actions';
import { Item } from './item.model';

export interface ItemState {
  items: Item[];
  loading: boolean;
  error: any;
}

export const initialState: ItemState = {
  items: [],
  loading: false,
  error: null
};

export const itemReducer = createReducer(
  initialState,
  on(loadItems, state => ({ ...state, loading: true })),
  on(loadItemsSuccess, (state, { items }) => ({ ...state, loading: false, items })),
  on(loadItemsFailure, (state, { error }) => ({ ...state, loading: false, error }))
);
```

#### 3. Effects

**Effects** são utilizados para lidar com operações assíncronas e interações com serviços externos. Eles escutam ações despachadas e, com base nelas, podem despachar outras ações, realizar chamadas a serviços, etc.

**Exemplo de um effect:**

```typescript
import { Injectable } from '@angular/core';
import { Actions, createEffect, ofType } from '@ngrx/effects';
import { ItemService } from './item.service';
import { loadItems, loadItemsSuccess, loadItemsFailure } from './item.actions';
import { catchError, map, mergeMap } from 'rxjs/operators';
import { of } from 'rxjs';

@Injectable()
export class ItemEffects {

  loadItems$ = createEffect(() => this.actions$.pipe(
    ofType(loadItems),
    mergeMap(() => this.itemService.getItems().pipe(
      map(items => loadItemsSuccess({ items })),
      catchError(error => of(loadItemsFailure({ error })))
    ))
  ));

  constructor(
    private actions$: Actions,
    private itemService: ItemService
  ) {}
}
```

#### 4. Selectors

**Selectors** são funções puras que permitem extrair pedaços de estado da store. Eles são usados para selecionar partes específicas do estado e fornecer esses dados aos componentes.

**Exemplo de um selector:**

```typescript
import { createSelector, createFeatureSelector } from '@ngrx/store';
import { ItemState } from './item.reducer';

export const selectItemState = createFeatureSelector<ItemState>('items');

export const selectAllItems = createSelector(
  selectItemState,
  (state: ItemState) => state.items
);

export const selectLoading = createSelector(
  selectItemState,
  (state: ItemState) => state.loading
);

export const selectError = createSelector(
  selectItemState,
  (state: ItemState) => state.error
);
```

#### Resumo

- **Actions:** Definem a intenção de mudar o estado.
- **Reducers:** Descrevem como o estado muda em resposta às ações.
- **Effects:** Lidam com operações assíncronas e lógica complexa fora dos reducers.
- **Selectors:** Permitem extrair e selecionar partes do estado da store para uso nos componentes.

Espero que isso ajude a entender os conceitos básicos do gerenciamento de estado com NgRx! Se precisar de mais detalhes ou exemplos, sinta-se à vontade para perguntar.

[Get started with ChatGPT](https://chatgpt.com/)

Report content|[Terms of use](https://openai.com/policies/terms-of-use)|[Privacy policy](https://openai.com/policies/privacy-policy)|

?

