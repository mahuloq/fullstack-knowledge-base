# Added to Auth Service we add some storage to the handleAuthenticaion

private handleAuthentication(
email: string,
userId: string,
token: string,
expiresIn: number
) {
const expirationDate = new Date(new Date().getTime() + expiresIn \* 1000);
const user = new User(email, userId, token, expirationDate);
this.user.next(user);
localStorage.setItem('userData', JSON.stringify(user));
}

# Then we request that data back with autologin, and set a user to the data we pull. The date is now a string, so we have to turn it back into a date.

autoLogin() {
const userData: {
email: string;
id: string;
\_token: string;
\_tokenExpirationDate: string;
} = JSON.parse(localStorage.getItem('userData'));

    if (!userData) {
      return;
    }
    const loadedUser = new User(
      userData.email,
      userData.id,
      userData._token,
      new Date(userData._tokenExpirationDate)
    );
    if (loadedUser.token) {
      this.user.next(loadedUser);
    }

}

# Then run this in an NgOnInit early in the sites lifecycle, like app.component.

import { Component, OnInit } from '@angular/core';
import { AuthService } from './auth/auth.service';

@Component({
selector: 'app-root',
templateUrl: './app.component.html',
styleUrls: ['./app.component.css'],
})
export class AppComponent implements OnInit {
constructor(private authService: AuthService) {}

ngOnInit(): void {
this.authService.autoLogin();
}
}
