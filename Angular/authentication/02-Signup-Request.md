# we setup an auth service

import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

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
return this.http.post<AuthResponseData>(
'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyAsYk5fP-Ilfbvjgf6Fw-xRLZqulMffK-g',
{
email: email,
password: password,
returnSecureToken: true,
}
);
}
}

# Than in the ts file

onSwitchMode() {
this.isLoginMode = !this.isLoginMode;
}

onSubmit(form: NgForm) {
if (!form.valid) {
return;
}

    if (this.isLoginMode) {
      // ...
    } else {
      const email = form.value.email;
      const password = form.value.password;

      this.authService.signUp(email, password).subscribe(
        (resData) => {
          console.log(resData);
        },
        (error) => {
          console.log(error);
        }
      );
    }
    form.reset();

}
}
