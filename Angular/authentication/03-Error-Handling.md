# The TS File

import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { catchError } from 'rxjs/operators';
import { throwError } from 'rxjs';

interface AuthResponseData {
kind: string;
idToken: string;
email: string;
refreshToken: string;
expiresIn: string;
localId: string;
}

@Injectable({ providedIn: 'root' })
export class AuthService {
constructor(private http: HttpClient) {}

signUp(email: string, password: string) {
return this.http
.post<AuthResponseData>(
'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyAsYk5fP-Ilfbvjgf6Fw-xRLZqulMffK-g',
{
email: email,
password: password,
returnSecureToken: true,
}
)
.pipe(
catchError((errorRes) => {
let errorMessage = 'An unknown error occured!';
if (!errorRes.error || !errorRes.error.error) {
return throwError(errorMessage);
}
switch (errorRes.error.error.message) {
case 'EMAIL_EXISTS':
errorMessage = 'This email already exists.';
}
return throwError(errorMessage);
})
);
}
}

# With the Auth service looking like

import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { catchError } from 'rxjs/operators';
import { throwError } from 'rxjs';

interface AuthResponseData {
kind: string;
idToken: string;
email: string;
refreshToken: string;
expiresIn: string;
localId: string;
}

@Injectable({ providedIn: 'root' })
export class AuthService {
constructor(private http: HttpClient) {}

signUp(email: string, password: string) {
return this.http
.post<AuthResponseData>(
'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyAsYk5fP-Ilfbvjgf6Fw-xRLZqulMffK-g',
{
email: email,
password: password,
returnSecureToken: true,
}
)
.pipe(
catchError((errorRes) => {
let errorMessage = 'An unknown error occured!';
if (!errorRes.error || !errorRes.error.error) {
return throwError(errorMessage);
}
switch (errorRes.error.error.message) {
case 'EMAIL_EXISTS':
errorMessage = 'This email already exists.';
}
return throwError(errorMessage);
})
);
}
}

# with the HTML file looking like

<div class="row">
  <div class="col-xs-12 col-md-6 cold-md-offset-3">
    <div class="alert alert-danger" *ngIf="error">
      <p>{{ error }}</p>
    </div>
    <div *ngIf="isLoading" style="text-align: center">
      <app-loading-spinner></app-loading-spinner>
    </div>
    <form #authForm="ngForm" (ngSubmit)="onSubmit(authForm)" *ngIf="!isLoading">
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
