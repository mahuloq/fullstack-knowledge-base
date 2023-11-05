# Auth Service, note that currently the error messages INVALID_PASSWORD and EMAIL_INVALID are not working on firebase, and have been combined into Invalid Credentials.

import { HttpClient, HttpErrorResponse } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { catchError } from 'rxjs/operators';
import { throwError } from 'rxjs';

export interface AuthResponseData {
kind: string;
idToken: string;
email: string;
refreshToken: string;
expiresIn: string;
localId: string;
registered?: boolean;
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
.pipe(catchError(this.handleError));
}

login(email: string, password: string) {
return this.http
.post<AuthResponseData>(
'https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=AIzaSyAsYk5fP-Ilfbvjgf6Fw-xRLZqulMffK-g',
{
email: email,
password: password,
returnSecureToken: true,
}
)
.pipe(catchError(this.handleError));
}

private handleError(errorRes: HttpErrorResponse) {
console.log(errorRes.error.error.message);
let errorMessage = 'An unknown error occured!';
if (!errorRes.error || !errorRes.error.error) {
return throwError(() => errorMessage);
}
switch (errorRes.error.error.message) {
case 'EMAIL_EXISTS':
errorMessage = 'This email already exists!';
break;
case 'EMAIL_NOT_FOUND':
errorMessage = 'This email does not exist.';
break;
case 'INVALID_PASSWORD':
errorMessage = 'This password is incorrect.';
break;
case 'INVALID_LOGIN_CREDENTIALS':
errorMessage = 'This email or password is incorrect.';
break;
}
return throwError(() => errorMessage);
}
}

# Auth Component

import { Component } from '@angular/core';
import { NgForm } from '@angular/forms';
import { AuthResponseData, AuthService } from './auth.service';
import { Observable } from 'rxjs';

@Component({
selector: 'app-auth',
templateUrl: './auth.component.html',
})
export class AuthComponent {
constructor(private authService: AuthService) {}

isLoginMode = true;
isLoading = false;
error: string = null;

onSwitchMode() {
this.isLoginMode = !this.isLoginMode;
}

onSubmit(form: NgForm) {
if (!form.valid) {
return;
}

    const email = form.value.email;
    const password = form.value.password;

    let authObs: Observable<AuthResponseData>;

    this.isLoading = true;
    if (this.isLoginMode) {
      authObs = this.authService.login(email, password);
    } else {
      authObs = this.authService.signUp(email, password);
    }
    authObs.subscribe(
      (resData) => {
        console.log(resData);
        this.isLoading = false;
        this.error = null;
      },
      (errorMessage) => {
        console.log(errorMessage);
        this.error = errorMessage;
        this.isLoading = false;
      }
    );
    form.reset();

}
}
