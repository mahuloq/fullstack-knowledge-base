# In Auth Service

autoLogout(expirationDuration: number) {
console.log(expirationDuration);
this.tokenExpirationTimer = setTimeout(() => {
this.logout();
}, expirationDuration);}

# Put this in both the auto login, and the handleAuthentication, to start the timer.

    private handleAuthentication(
    email: string,
    userId: string,
    token: string,
    expiresIn: number

) {
const expirationDate = new Date(new Date().getTime() + expiresIn _ 1000);
const user = new User(email, userId, token, expirationDate);
this.user.next(user);
this.autoLogout(expiresIn _ 1000);
localStorage.setItem('userData', JSON.stringify(user));
}

# Auto Login

    autoLogin() {
    const userData: {
      email: string;
      id: string;
      _token: string;
      _tokenExpirationDate: string;
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
      const expirationDuration =
        new Date(userData._tokenExpirationDate).getTime() -
        new Date().getTime();
      this.autoLogout(expirationDuration);
    }

}
