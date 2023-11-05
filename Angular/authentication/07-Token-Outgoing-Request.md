# Change the fetch method in data-storage to send the token with its outgoing request.This used a couple new things, like take, which subscribes for one pull of info, then unsubscribes. Becuase you cant have mutliple observers returned, you have to rearrange your code and use the exhaustMap, which lets you return another observable after one runs.

fetchRecipes() {
return this.authService.user.pipe(
take(1),
exhaustMap((user) => {
return this.http.get<Recipe[]>(
'https://ng-course-recipe-book-ebc37-default-rtdb.firebaseio.com/recipes.json',
{
params: new HttpParams().set('auth', user.token),
}
);
}),
map((recipes) => {
return recipes.map((recipe) => {
return {
...recipe,
ingredients: recipe.ingredients ? recipe.ingredients : [],
};
});
}),
tap((recipes) => {
this.recipeService.setRecipes(recipes);
})
);
}

# We can simplify our data storage, by returning it to how it was.

fetchRecipes() {
return this.http
.get<Recipe[]>(
'https://ng-course-recipe-book-ebc37-default-rtdb.firebaseio.com/recipes.json'
)
.pipe(
map((recipes) => {
return recipes.map((recipe) => {
return {
...recipe,
ingredients: recipe.ingredients ? recipe.ingredients : [],
};
});
}),
tap((recipes) => {
this.recipeService.setRecipes(recipes);
})
);
}

# But adding an interceptor, which modifies the requests.

import { Injectable } from '@angular/core';
import {
HttpHandler,
HttpInterceptor,
HttpParams,
HttpRequest,
} from '@angular/common/http';
import { AuthService } from './auth.service';
import { exhaustMap, take } from 'rxjs/operators';

@Injectable()
export class AuthInterceptorService {
constructor(private authService: AuthService) {}

intercept(req: HttpRequest<any>, next: HttpHandler) {
return this.authService.user.pipe(
take(1),
exhaustMap((user) => {
if (!user) {
return next.handle(req);
}
const modifiedReq = req.clone({
params: new HttpParams().set('auth', user.token),
});
return next.handle(modifiedReq);
})
);
}
}
