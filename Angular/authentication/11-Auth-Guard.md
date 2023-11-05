# Implement in auth guard to prevent access to recipes page unless the person is logged in.

import { Injectable } from '@angular/core';
import {
ActivatedRouteSnapshot,
CanActivate,
Router,
RouterStateSnapshot,
UrlTree,
} from '@angular/router';
import { Observable, map, take } from 'rxjs';
import { AuthService } from './auth.service';

@Injectable({ providedIn: 'root' })
export class AuthGuard implements CanActivate {
constructor(private authService: AuthService, private router: Router) {}

canActivate(
route: ActivatedRouteSnapshot,
state: RouterStateSnapshot
):
| boolean
| UrlTree
| Observable<boolean | UrlTree>
| Promise<boolean | UrlTree> {
return this.authService.user.pipe(
take(1),
map((user) => {
const isAuth = !!user;
if (isAuth) {
return true;
}
return this.router.createUrlTree(['/auth']);
})
);
}
}

# make sure you enable this auth guard in the route.

path: 'recipes',
component: RecipesComponent,
canActivate: [AuthGuard],
children: [
{ path: '', component: RecipeStartComponent },
{ path: 'new', component: RecipeEditComponent },
{
path: ':id',
component: RecipesDetailComponent,
resolve: [RecipesResolverService],
},
{
path: ':id/edit',
component: RecipeEditComponent,
resolve: [RecipesResolverService],
},
],
