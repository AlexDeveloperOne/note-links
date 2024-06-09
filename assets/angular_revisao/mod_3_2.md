https://chatgpt.com/share/4091934d-2a77-4cd9-9853-b6fec8d6fc62

# Parâmetros e Guards: Navegação

May 25, 2024



Anonymous

Meu professor, peço que me ê a aula do Módulo 3: Roteamento e Navegação que é: 'Navegação' e que aborda os assuntos abaixo: - Parâmetros de rota - Guards (CanActivate, CanDeactivate)

ChatGPT

ChatGPT

### Módulo 3: Roteamento e Navegação

#### Aula: Navegação

Nesta aula, vamos explorar dois conceitos fundamentais para a navegação em aplicações web usando frameworks modernos, como Angular: parâmetros de rota e guards. Esses conceitos são cruciais para criar aplicações robustas e seguras, onde a navegação é controlada e os dados são manipulados de forma eficiente.

### Parâmetros de Rota

Os parâmetros de rota são utilizados para passar informações dinamicamente através da URL. Esses parâmetros são essenciais para criar rotas dinâmicas que podem mudar conforme os dados passados.

#### Tipos de Parâmetros de Rota

1. **Parâmetros Obrigatórios**: São aqueles que devem estar presentes na rota para que ela seja resolvida corretamente.

   Exemplo de rota com parâmetro obrigatório:

   ```typescript
   { path: 'user/:id', component: UserComponent }
   ```

   Neste caso, `:id` é um parâmetro obrigatório que deve ser fornecido na URL para acessar o `UserComponent`.

2. **Parâmetros Opcionais**: São aqueles que podem ou não estar presentes na rota. Eles são geralmente usados para fornecer informações adicionais.

   Exemplo de rota com parâmetro opcional:

   ```typescript
   { path: 'search', component: SearchComponent }
   ```

   A URL pode ser algo como `/search?query=example`.

#### Obtendo Parâmetros de Rota

Para acessar os parâmetros de rota no componente, usamos o `ActivatedRoute`:

```typescript
import { ActivatedRoute } from '@angular/router';

@Component({
  // ... outras configurações
})
export class UserComponent implements OnInit {
  userId: string;

  constructor(private route: ActivatedRoute) {}

  ngOnInit() {
    this.userId = this.route.snapshot.paramMap.get('id');
  }
}
```

#### Exemplo de Uso

Aqui está um exemplo prático onde usamos parâmetros de rota para carregar detalhes de um usuário específico:

```typescript
// app-routing.module.ts
const routes: Routes = [
  { path: 'user/:id', component: UserDetailComponent }
];

// user-detail.component.ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user-detail',
  template: `
    <div *ngIf="user">
      <h1>{{ user.name }}</h1>
      <p>{{ user.email }}</p>
    </div>
  `
})
export class UserDetailComponent implements OnInit {
  user: any;

  constructor(private route: ActivatedRoute, private userService: UserService) {}

  ngOnInit() {
    const id = this.route.snapshot.paramMap.get('id');
    this.userService.getUserById(id).subscribe(user => this.user = user);
  }
}
```

### Guards (CanActivate, CanDeactivate)

Os guards são serviços que permitem controlar o acesso às rotas com base em condições específicas. Existem vários tipos de guards, mas nesta aula vamos focar nos mais comuns: `CanActivate` e `CanDeactivate`.

#### CanActivate

O guard `CanActivate` é usado para determinar se uma rota pode ser ativada. Ele é ideal para autenticação e controle de acesso.

```typescript
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, UrlTree } from '@angular/router';
import { Observable } from 'rxjs';
import { AuthService } from './auth.service';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {

  constructor(private authService: AuthService) {}

  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
    return this.authService.isLoggedIn();
  }
}
```

Para aplicar este guard a uma rota, configuramos a rota da seguinte forma:

```typescript
const routes: Routes = [
  {
    path: 'dashboard',
    component: DashboardComponent,
    canActivate: [AuthGuard]
  }
];
```

#### CanDeactivate

O guard `CanDeactivate` é usado para impedir a navegação para fora de uma rota específica, a menos que certas condições sejam atendidas. Ele é útil, por exemplo, para confirmar que um usuário deseja sair de uma página com um formulário não salvo.

```typescript
import { Injectable } from '@angular/core';
import { CanDeactivate } from '@angular/router';
import { Observable } from 'rxjs';

export interface CanComponentDeactivate {
  canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
}

@Injectable({
  providedIn: 'root'
})
export class CanDeactivateGuard implements CanDeactivate<CanComponentDeactivate> {

  canDeactivate(
    component: CanComponentDeactivate): Observable<boolean> | Promise<boolean> | boolean {
    return component.canDeactivate ? component.canDeactivate() : true;
  }
}
```

O componente que usa este guard deve implementar a interface `CanComponentDeactivate`:

```typescript
import { Component, HostListener } from '@angular/core';
import { Observable } from 'rxjs';

@Component({
  selector: 'app-form',
  templateUrl: './form.component.html'
})
export class FormComponent implements CanComponentDeactivate {
  
  unsavedChanges = true;

  canDeactivate(): Observable<boolean> | Promise<boolean> | boolean {
    if (this.unsavedChanges) {
      return confirm('Você tem alterações não salvas. Deseja realmente sair?');
    }
    return true;
  }
}
```

Para aplicar este guard a uma rota, configuramos a rota da seguinte forma:

```typescript
const routes: Routes = [
  {
    path: 'form',
    component: FormComponent,
    canDeactivate: [CanDeactivateGuard]
  }
];
```

### Conclusão

Nesta aula, exploramos como os parâmetros de rota podem ser usados para criar rotas dinâmicas e como os guards `CanActivate` e `CanDeactivate` podem ser utilizados para controlar o acesso e a navegação dentro de uma aplicação. Esses conceitos são fundamentais para construir aplicações web modernas e seguras.

[Sign up to chat](https://chatgpt.com/)

Report content|[Terms of use](https://openai.com/policies/terms-of-use)|[Privacy policy](https://openai.com/policies/privacy-policy)|



