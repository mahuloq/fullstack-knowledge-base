# Basic Auth Page

<div class="row">
  <div class="col-xs-12 col-md-6 cold-md-offset-3">
    <form #authForm="ngForm" (ngSubmit)="onSubmit(authForm)">
      <div class="form-group">
        <label for="email">Email</label>
        <input
          class="form-control"
          type="email"
          id="email"
          ngModel
          name="email"
          required
          email
        />
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input
          class="form-control"
          type="password"
          id="password"
          ngModel
          name="password"
          required
          minlength="6"
        />
      </div>
      <div>
        <button
          class="btn btn-primary"
          type="submit"
          [disabled]="!authForm.valid"
        >
          {{ isLoginMode ? "Login" : "Sign Up" }}
        </button>
        |
        <button class="btn btn-primary" type="button" (click)="onSwitchMode()">
          Switch to {{ isLoginMode ? "Sign Up" : "Login" }}
        </button>
      </div>
    </form>
  </div>
</div>

# Auth PAge Ts

import { Component } from '@angular/core';
import { NgForm } from '@angular/forms';

@Component({
selector: 'app-auth',
templateUrl: './auth.component.html',
})
export class AuthComponent {
isLoginMode = true;

onSwitchMode() {
this.isLoginMode = !this.isLoginMode;
}

onSubmit(form: NgForm) {
console.log(form.value);
form.reset();
}
}

# TO turn on auth on firebase, in authentication turn email on, and in rules set read and write to

{
"rules": {
".read": "auth != null",
".write": "auth != null"
}
}
