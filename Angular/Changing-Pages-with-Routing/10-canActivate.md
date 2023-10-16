## Can create an AuthGuard to restrict showing routes

import { Injectable } from "@angular/core";
import {
CanActivate,
ActivatedRouteSnapshot,
RouterStateSnapshot,
Router,
} from "@angular/router";
import { Observable } from "rxjs";
import { AuthService } from "./auth.service";

@Injectable()
export class AuthGuard implements CanActivate {
constructor(private authService: AuthService, private router: Router) {}

canActivate(
route: ActivatedRouteSnapshot,
state: RouterStateSnapshot
): Observable<boolean> | Promise<boolean> | boolean {
return this.authService.isAuthenticate().then((authenticated: boolean) => {
if (authenticated) {
return true;
} else {
this.router.navigate(["/"]);
}
});
}
}

## linking to an auth.service.ts file

export class AuthService {
loggedIn = false;

isAuthenticate() {
const promise = new Promise((resolve, reject) => {
setTimeout(() => {
resolve(this.loggedIn);
}, 800);
});
return promise;
}

login() {
this.loggedIn = true;
}

logout() {
this.loggedIn = false;
}
}

## If you want to allow the main route to be accessed, but not the child

export class AuthGuard implements CanActivate, CanActivateChild {
constructor(private authService: AuthService, private router: Router) {}

canActivate(
route: ActivatedRouteSnapshot,
state: RouterStateSnapshot
): Observable<boolean> | Promise<boolean> | boolean {
return this.authService.isAuthenticate().then((authenticated: boolean) => {
if (authenticated) {
return true;
} else {
this.router.navigate(["/"]);
}
});
}
canActivateChild(
route: ActivatedRouteSnapshot,
state: RouterStateSnapshot
): Observable<boolean> | Promise<boolean> | boolean {
return this.canActivate(route, state);
}
}
