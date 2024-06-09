

https://chatgpt.com/share/c46d5401-f5be-4d8b-b577-4c84b3321a43



# Formulários Template-Driven Angular

May 26, 2024

Meu professor, poço que me ê a aula do Módulo 5: Formulários que é: Formulários Template-Driven que aborda os assuntos abaixo:  Criação e validação de formulários usando o template

ChatGPT

Claro! Vamos abordar a criação e validação de formulários template-driven em Angular, que é um tópico do Módulo 5: Formulários. Este método de criação de formulários utiliza diretivas Angular para criar e validar formulários no template.

### Introdução aos Formulários Template-Driven

Formulários template-driven são uma abordagem simples para criar formulários no Angular, utilizando o template HTML. Eles são ideais para formulários simples e são uma boa forma de começar a trabalhar com formulários no Angular.

### Passos para Criar e Validar Formulários Template-Driven

#### 1. Importar o Módulo FormsModule

Para utilizar formulários template-driven, você precisa importar o `FormsModule` no módulo principal da sua aplicação.

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms'; // Importar FormsModule

import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule], // Adicionar FormsModule aos imports
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

#### 2. Criar um Template HTML para o Formulário

No template HTML, utilize diretivas Angular como `ngModel` para ligar os dados do formulário ao componente.

```html
<form #userForm="ngForm" (ngSubmit)="onSubmit(userForm)">
  <div>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" ngModel required>
  </div>
  <div>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" ngModel required email>
  </div>
  <div>
    <label for="age">Age:</label>
    <input type="number" id="age" name="age" ngModel>
  </div>
  <button type="submit" [disabled]="!userForm.valid">Submit</button>
</form>
```

#### 3. Acessar os Dados do Formulário no Componente

No componente TypeScript, você pode acessar os dados do formulário e validar as entradas.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  onSubmit(form: any): void {
    console.log('Form Data:', form.value);
  }
}
```

### Validação de Formulários Template-Driven

#### 1. Validações Padrão

Angular oferece validações padrão como `required`, `minlength`, `maxlength`, `pattern`, etc.

```html
<div>
  <label for="password">Password:</label>
  <input type="password" id="password" name="password" ngModel required minlength="6">
  <div *ngIf="userForm.controls.password?.invalid && userForm.controls.password?.touched">
    <small *ngIf="userForm.controls.password?.errors?.required">Password is required.</small>
    <small *ngIf="userForm.controls.password?.errors?.minlength">Password must be at least 6 characters long.</small>
  </div>
</div>
```

#### 2. Validações Personalizadas

Você também pode criar validações personalizadas usando diretivas.

```typescript
import { Directive } from '@angular/core';
import { NG_VALIDATORS, Validator, AbstractControl, ValidationErrors } from '@angular/forms';

@Directive({
  selector: '[appCustomValidator]',
  providers: [{ provide: NG_VALIDATORS, useExisting: CustomValidatorDirective, multi: true }]
})
export class CustomValidatorDirective implements Validator {
  validate(control: AbstractControl): ValidationErrors | null {
    // Exemplo de validação: valor deve ser "custom"
    const isValid = control.value === 'custom';
    return isValid ? null : { customError: true };
  }
}
```

E no template:

```html
<div>
  <label for="customField">Custom Field:</label>
  <input type="text" id="customField" name="customField" ngModel appCustomValidator>
  <div *ngIf="userForm.controls.customField?.errors?.customError">
    <small>Custom field must have the value "custom".</small>
  </div>
</div>
```

### Conclusão

Os formulários template-driven no Angular são uma maneira poderosa e fácil de criar e validar formulários. Esta abordagem é ideal para formulários simples, onde a lógica de validação pode ser facilmente gerenciada diretamente no template HTML.

Ao seguir os passos acima, você pode criar formulários, utilizar validações padrão e personalizadas, e gerenciar os dados do formulário de forma eficaz. Esta introdução deve ajudá-lo a começar a trabalhar com formulários template-driven no Angular.

[Get started with ChatGPT](https://chatgpt.com/)

Report content|[Terms of use](https://openai.com/policies/terms-of-use)|[Privacy policy](https://openai.com/policies/privacy-policy)|









