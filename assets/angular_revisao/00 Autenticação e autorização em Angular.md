https://chatgpt.com/share/2b5f89ec-0e3b-4d79-95dc-6af1c4761c89

# Autenticação em Angular

May 26, 2024



Anonymous

Sou aluno e te peço meu instrutor uma aula de 'Autenticação e Autorização' em Angular com os seguintes assuntos:  Implementação de autenticação.

ChatGPT

ChatGPT

Claro, vou elaborar uma aula detalhada sobre 'Autenticação e Autorização' em Angular, abordando a implementação de autenticação. Vamos seguir uma estrutura que inclui os conceitos principais, os passos para implementar autenticação, exemplos de código, e uma breve discussão sobre autorização.

## Aula: Autenticação e Autorização em Angular

### Objetivos da Aula

1. Compreender os conceitos de autenticação e autorização.
2. Implementar um sistema de autenticação em Angular.
3. Utilizar serviços e guards para gerenciar a segurança da aplicação.

### 1. Introdução

**Autenticação** é o processo de verificar a identidade do usuário (ex: login com nome de usuário e senha).

**Autorização** é o processo de verificar se o usuário autenticado tem permissão para acessar um recurso específico.

### 2. Preparação do Ambiente

Para começar, certifique-se de ter o Angular CLI instalado. Caso ainda não tenha, você pode instalar utilizando o comando:

```
bash
Copy code
npm install -g @angular/cli
```

### 3. Criação do Projeto

Crie um novo projeto Angular:

```
bashCopy codeng new angular-auth-demo
cd angular-auth-demo
```

### 4. Implementação de Autenticação

#### 4.1. Instalação de Dependências

Para esta aula, vamos utilizar o pacote `@auth0/angular-jwt` para ajudar no gerenciamento do token JWT (JSON Web Token).

```
bash
Copy code
npm install @auth0/angular-jwt
```

#### 4.2. Configuração do JWT

Vamos configurar o interceptor do JWT. No arquivo `app.module.ts`, adicione as seguintes importações e configure o `HttpClientModule` e `JWT`:

```
typescriptCopy codeimport { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
import { JwtModule } from '@auth0/angular-jwt';

import { AppComponent } from './app.component';
import { AuthService } from './auth.service';

export function tokenGetter() {
  return localStorage.getItem('access_token');
}

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule,
    JwtModule.forRoot({
      config: {
        tokenGetter: tokenGetter,
        allowedDomains: ["localhost:4200"],
        disallowedRoutes: []
      }
    })
  ],
  providers: [
    AuthService
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

#### 4.3. Serviço de Autenticação

Crie um serviço de autenticação para lidar com as operações de login, logout e verificação do estado de autenticação. Crie um arquivo chamado `auth.service.ts` na pasta `src/app`:

```
typescriptCopy codeimport { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Router } from '@angular/router';
import { Observable, BehaviorSubject } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private loggedIn = new BehaviorSubject<boolean>(false);

  constructor(private http: HttpClient, private router: Router) {}

  login(username: string, password: string): Observable<any> {
    return this.http.post<{token: string}>('http://localhost:3000/login', {username, password})
      .pipe(tap(res => {
        localStorage.setItem('access_token', res.token);
        this.loggedIn.next(true);
      }));
  }

  logout() {
    localStorage.removeItem('access_token');
    this.loggedIn.next(false);
    this.router.navigate(['/login']);
  }

  get isLoggedIn() {
    return this.loggedIn.asObservable();
  }
}
```

#### 4.4. Componentes de Login e Logout

Crie componentes para login e logout:

```
bashCopy codeng generate component login
ng generate component logout
```

No componente `login.component.ts`:

```
typescriptCopy codeimport { Component } from '@angular/core';
import { AuthService } from '../auth.service';
import { Router } from '@angular/router';

@Component({
  selector: 'app-login',
  templateUrl: './login.component.html'
})
export class LoginComponent {
  constructor(private authService: AuthService, private router: Router) {}

  login(username: string, password: string) {
    this.authService.login(username, password).subscribe(() => {
      this.router.navigate(['/protected']);
    });
  }
}
```

No template `login.component.html`:

```
htmlCopy code<div>
  <h2>Login</h2>
  <form (submit)="login(username.value, password.value)">
    <label for="username">Username:</label>
    <input type="text" id="username" #username><br><br>
    <label for="password">Password:</label>
    <input type="password" id="password" #password><br><br>
    <button type="submit">Login</button>
  </form>
</div>
```

No componente `logout.component.ts`:

```
typescriptCopy codeimport { Component } from '@angular/core';
import { AuthService } from '../auth.service';

@Component({
  selector: 'app-logout',
  template: `<button (click)="logout()">Logout</button>`
})
export class LogoutComponent {
  constructor(private authService: AuthService) {}

  logout() {
    this.authService.logout();
  }
}
```

#### 4.5. Guards de Autenticação

Crie um guard de autenticação para proteger as rotas:

```
bash
Copy code
ng generate guard auth
```

No arquivo `auth.guard.ts`:

```
typescriptCopy codeimport { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';
import { AuthService } from './auth.service';
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {

  constructor(private authService: AuthService, private router: Router) {}

  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean> {
    return this.authService.isLoggedIn.pipe(map(isLoggedIn => {
      if (!isLoggedIn) {
        this.router.navigate(['/login']);
        return false;
      }
      return true;
    }));
  }
}
```

#### 4.6. Configuração das Rotas

Configure as rotas no arquivo `app-routing.module.ts`:

```
typescriptCopy codeimport { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { LoginComponent } from './login/login.component';
import { LogoutComponent } from './logout/logout.component';
import { AuthGuard } from './auth.guard';

const routes: Routes = [
  { path: 'login', component: LoginComponent },
  { path: 'logout', component: LogoutComponent },
  { path: 'protected', component: ProtectedComponent, canActivate: [AuthGuard] },
  { path: '', redirectTo: '/login', pathMatch: 'full' }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### 5. Testando a Aplicação

1. Inicie o servidor de desenvolvimento Angular:

```
bash
Copy code
ng serve
```

1. Acesse a aplicação em `http://localhost:4200`.
2. Tente acessar uma rota protegida sem estar logado e verifique se é redirecionado para a página de login.
3. Realize o login com as credenciais corretas e verifique se consegue acessar a rota protegida.

### 6. Conclusão

Nesta aula, cobrimos os conceitos de autenticação e autorização, configuramos um serviço de autenticação usando JWT, criamos componentes de login e logout, e protegemos rotas usando guards. A autorização específica pode ser implementada adicionando regras adicionais nos guards ou diretamente nos componentes, conforme a necessidade.

**Tarefas para Casa:**

1. Implemente uma verificação de autorização com base em roles (funções) do usuário.
2. Adicione um sistema de registro de novos usuários.

Se tiverem dúvidas, sintam-se à vontade para perguntar. Boa sorte!



Anonymous

Instrutor continue a aula de 'Autenticação e Autorização' em Angular com os seguintes assuntos:  Proteção de rotas.

ChatGPT

ChatGPT

Claro! Vamos continuar a aula sobre 'Autenticação e Autorização' em Angular, agora focando na proteção de rotas.

### Proteção de Rotas

A proteção de rotas em Angular é fundamental para assegurar que apenas usuários autenticados (e possivelmente autorizados) possam acessar determinadas partes da aplicação. Para isso, utilizamos os **guards** do Angular.

### 1. Configurando um Guard de Autenticação

Primeiramente, vamos criar um guard que verificará se o usuário está autenticado antes de permitir o acesso à rota.

#### 1.1. Criando o Guard

Se ainda não criamos um guard, podemos criar um utilizando o Angular CLI:

```
bash
Copy code
ng generate guard auth
```

#### 1.2. Implementação do Guard

No arquivo `auth.guard.ts` que foi gerado, vamos implementar a lógica para verificar se o usuário está autenticado:

```
typescriptCopy codeimport { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';
import { AuthService } from './auth.service';
import { Observable } from 'rxjs';
import { map, take } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {

  constructor(private authService: AuthService, private router: Router) {}

  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean> {
    return this.authService.isLoggedIn.pipe(
      take(1),
      map(isLoggedIn => {
        if (!isLoggedIn) {
          this.router.navigate(['/login']);
          return false;
        }
        return true;
      })
    );
  }
}
```

Este código verifica se o usuário está autenticado (`isLoggedIn`) e, caso contrário, redireciona para a página de login.

### 2. Configurando Rotas Protegidas

Agora, vamos configurar nossas rotas para utilizar o guard de autenticação.

No arquivo `app-routing.module.ts`:

```
typescriptCopy codeimport { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { LoginComponent } from './login/login.component';
import { LogoutComponent } from './logout/logout.component';
import { AuthGuard } from './auth.guard';
import { ProtectedComponent } from './protected/protected.component'; // Assumindo que você tem um componente protegido

const routes: Routes = [
  { path: 'login', component: LoginComponent },
  { path: 'logout', component: LogoutComponent },
  { path: 'protected', component: ProtectedComponent, canActivate: [AuthGuard] },
  { path: '', redirectTo: '/login', pathMatch: 'full' }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

Aqui, adicionamos a propriedade `canActivate` na rota `protected`, o que assegura que apenas usuários autenticados possam acessar essa rota.

### 3. Guard de Autorização com Base em Roles

Além da autenticação, muitas vezes precisamos de autorização baseada em roles (funções ou papéis de usuário). Vamos estender nosso exemplo para incluir essa funcionalidade.

#### 3.1. Adicionando Roles ao Serviço de Autenticação

Vamos modificar o serviço de autenticação (`auth.service.ts`) para incluir roles. Suponhamos que o backend retorna um JWT com a role do usuário.

```
typescriptCopy code@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private loggedIn = new BehaviorSubject<boolean>(false);
  private userRole = new BehaviorSubject<string | null>(null);

  constructor(private http: HttpClient, private router: Router) {}

  login(username: string, password: string): Observable<any> {
    return this.http.post<{token: string, role: string}>('http://localhost:3000/login', {username, password})
      .pipe(tap(res => {
        localStorage.setItem('access_token', res.token);
        this.userRole.next(res.role);
        this.loggedIn.next(true);
      }));
  }

  logout() {
    localStorage.removeItem('access_token');
    this.userRole.next(null);
    this.loggedIn.next(false);
    this.router.navigate(['/login']);
  }

  get isLoggedIn() {
    return this.loggedIn.asObservable();
  }

  get role() {
    return this.userRole.asObservable();
  }
}
```

#### 3.2. Guard de Autorização

Agora, vamos criar um guard específico para verificar roles. Criamos um novo guard:

```
bash
Copy code
ng generate guard role
```

E implementamos a lógica de verificação de role:

```
typescriptCopy codeimport { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';
import { AuthService } from './auth.service';
import { Observable } from 'rxjs';
import { map, take } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class RoleGuard implements CanActivate {

  constructor(private authService: AuthService, private router: Router) {}

  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean> {
    const expectedRole = next.data.expectedRole;
    return this.authService.role.pipe(
      take(1),
      map(role => {
        if (role !== expectedRole) {
          this.router.navigate(['/unauthorized']);
          return false;
        }
        return true;
      })
    );
  }
}
```

Neste guard, verificamos se a role do usuário corresponde à esperada (`expectedRole`).

#### 3.3. Configurando Rotas com Autorização por Role

Vamos agora proteger uma rota com base em roles:

```
typescriptCopy codeconst routes: Routes = [
  { path: 'login', component: LoginComponent },
  { path: 'logout', component: LogoutComponent },
  { path: 'admin', component: AdminComponent, canActivate: [RoleGuard], data: { expectedRole: 'admin' } },
  { path: 'protected', component: ProtectedComponent, canActivate: [AuthGuard] },
  { path: 'unauthorized', component: UnauthorizedComponent },
  { path: '', redirectTo: '/login', pathMatch: 'full' }
];
```

No exemplo acima, a rota `admin` está protegida pelo `RoleGuard` e só pode ser acessada por usuários com a role `admin`.

### 4. Conclusão

Nesta parte da aula, aprendemos a proteger rotas em Angular utilizando guards para autenticação e autorização. Implementamos:

1. Um **AuthGuard** para verificar se o usuário está autenticado.
2. Um **RoleGuard** para verificar se o usuário tem a role apropriada para acessar uma rota específica.

### Tarefas para Casa:

1. Implemente um componente `UnauthorizedComponent` para mostrar uma mensagem quando um usuário tenta acessar uma rota sem permissão.
2. Adicione mais roles e proteja outras rotas de acordo com diferentes roles de usuários.

Se tiverem dúvidas, sintam-se à vontade para perguntar. Boa sorte com a implementação!



Anonymous

Instrutor continue a aula de 'Autenticação e Autorização' em Angular com os seguintes assuntos:  Gerenciamento de tokens (JWT).

ChatGPT

ChatGPT

Claro! Vamos continuar nossa aula sobre 'Autenticação e Autorização' em Angular, agora focando no gerenciamento de tokens JWT (JSON Web Token). O gerenciamento de tokens é crucial para garantir a segurança da autenticação e autorização na aplicação.

### 1. Introdução ao JWT

O JWT é um padrão aberto (RFC 7519) que define uma maneira compacta e autônoma para transmitir informações de forma segura entre partes como um objeto JSON. Esses tokens são assinados usando um algoritmo criptográfico para garantir que as reivindicações (claims) não possam ser alteradas após a emissão.

### 2. Estrutura de um JWT

Um JWT é composto por três partes:

1. **Header (Cabeçalho)**: Contém o tipo de token e o algoritmo de assinatura.
2. **Payload (Carga)**: Contém as reivindicações (claims). Pode incluir informações como o identificador do usuário, roles, etc.
3. **Signature (Assinatura)**: É usada para verificar se o token não foi alterado.

### 3. Armazenamento do Token

Os tokens geralmente são armazenados no `localStorage` ou `sessionStorage`. O `localStorage` persiste o token até que seja explicitamente removido, enquanto o `sessionStorage` o mantém até que a aba do navegador seja fechada.

### 4. Implementação no Angular

#### 4.1. Configuração Inicial

Vamos configurar o Angular para armazenar e usar o token JWT. Já instalamos o pacote `@auth0/angular-jwt` na aula anterior. Vamos utilizá-lo para interceptar as requisições HTTP e adicionar o token no cabeçalho.

#### 4.2. Serviço de Autenticação

Atualize o `auth.service.ts` para incluir métodos de armazenamento e recuperação do token:

```
typescriptCopy codeimport { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Router } from '@angular/router';
import { Observable, BehaviorSubject } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private loggedIn = new BehaviorSubject<boolean>(this.hasToken());

  constructor(private http: HttpClient, private router: Router) {}

  login(username: string, password: string): Observable<any> {
    return this.http.post<{ token: string, role: string }>('http://localhost:3000/login', { username, password })
      .pipe(tap(res => {
        this.setToken(res.token);
        this.loggedIn.next(true);
      }));
  }

  logout() {
    this.removeToken();
    this.loggedIn.next(false);
    this.router.navigate(['/login']);
  }

  get isLoggedIn() {
    return this.loggedIn.asObservable();
  }

  private setToken(token: string): void {
    localStorage.setItem('access_token', token);
  }

  private getToken(): string | null {
    return localStorage.getItem('access_token');
  }

  private removeToken(): void {
    localStorage.removeItem('access_token');
  }

  private hasToken(): boolean {
    return !!this.getToken();
  }
}
```

#### 4.3. Interceptor de Token

Crie um interceptor para adicionar o token JWT nas requisições HTTP. Crie um arquivo chamado `token.interceptor.ts`:

```
typescriptCopy codeimport { Injectable } from '@angular/core';
import { HttpRequest, HttpHandler, HttpEvent, HttpInterceptor } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable()
export class TokenInterceptor implements HttpInterceptor {

  intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const token = localStorage.getItem('access_token');

    if (token) {
      request = request.clone({
        setHeaders: {
          Authorization: `Bearer ${token}`
        }
      });
    }

    return next.handle(request);
  }
}
```

#### 4.4. Registrando o Interceptor

No arquivo `app.module.ts`, registre o interceptor:

```
typescriptCopy codeimport { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
import { JwtModule } from '@auth0/angular-jwt';

import { AppComponent } from './app.component';
import { AuthService } from './auth.service';
import { TokenInterceptor } from './token.interceptor';

export function tokenGetter() {
  return localStorage.getItem('access_token');
}

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule,
    JwtModule.forRoot({
      config: {
        tokenGetter: tokenGetter,
        allowedDomains: ["localhost:4200"],
        disallowedRoutes: []
      }
    })
  ],
  providers: [
    AuthService,
    {
      provide: HTTP_INTERCEPTORS,
      useClass: TokenInterceptor,
      multi: true
    }
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### 5. Expiração do Token

É importante gerenciar a expiração do token para que os usuários não permaneçam autenticados indefinidamente. Vamos modificar o serviço de autenticação para lidar com tokens expirados.

#### 5.1. Decodificação do Token

Para verificar a expiração, precisamos decodificar o token. Podemos usar uma biblioteca como `jwt-decode`:

```
bash
Copy code
npm install jwt-decode
```

#### 5.2. Verificando a Expiração

Atualize o `auth.service.ts` para incluir a verificação de expiração:

```
typescriptCopy codeimport jwt_decode from 'jwt-decode';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private loggedIn = new BehaviorSubject<boolean>(this.hasValidToken());

  // ... outros métodos

  private hasValidToken(): boolean {
    const token = this.getToken();
    if (!token) {
      return false;
    }

    const decoded: any = jwt_decode(token);
    const expirationDate = decoded.exp * 1000;
    const currentTime = Date.now();

    return expirationDate > currentTime;
  }
}
```

#### 5.3. Atualizando o Guard

Certifique-se de que o guard verifica a validade do token:

```
typescriptCopy codeimport { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';
import { AuthService } from './auth.service';
import { Observable } from 'rxjs';
import { map, take } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {

  constructor(private authService: AuthService, private router: Router) {}

  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean> {
    return this.authService.isLoggedIn.pipe(
      take(1),
      map(isLoggedIn => {
        if (!isLoggedIn) {
          this.router.navigate(['/login']);
          return false;
        }
        return true;
      })
    );
  }
}
```

### 6. Conclusão

Nesta seção da aula, abordamos o gerenciamento de tokens JWT em Angular, incluindo:

1. Armazenamento do token no `localStorage`.
2. Adição do token nas requisições HTTP usando um interceptor.
3. Verificação da expiração do token para garantir a validade das sessões.

### Tarefas para Casa:

1. Implemente a renovação automática do token antes de sua expiração.
2. Adicione uma notificação para o usuário quando o token estiver prestes a expirar.

Se tiverem dúvidas ou precisarem de mais detalhes, sintam-se à vontade para perguntar. Boa sorte com a implementação!

[Sign up to chat](https://chatgpt.com/)

Report content|[Terms of use](https://openai.com/policies/terms-of-use)|[Privacy policy](https://openai.com/policies/privacy-policy)|

?




