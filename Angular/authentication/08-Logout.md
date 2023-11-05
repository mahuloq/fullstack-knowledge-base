# Pretty simple, this is a new method in the auth.service. Then redirects to the auth page.

logout() {
this.user.next(null);
this.router.navigate(['/auth']);
}

# Click listener on the header

  <li *ngIf="isAuthenticated">
          <a style="cursor: pointer" (click)="onLogout()">Logout</a>
        </li>

# with the method

onLogout() {
this.authService.logout();
}
