## can-deactivate-guard.service.ts

import {
ActivatedRouteSnapshot,
CanDeactivate,
RouterStateSnapshot,
} from "@angular/router";
import { Observable } from "rxjs";

export interface CanComponentDeactivate {
canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
}

export class CanDeactivateGuard
implements CanDeactivate<CanComponentDeactivate>
{
canDeactivate(
component: CanComponentDeactivate,
currentRoute: ActivatedRouteSnapshot,
currentState: RouterStateSnapshot,
nextState?: RouterStateSnapshot
): boolean | Observable<boolean> | Promise<boolean> {
return component.canDeactivate();
}
}

import { NgModule } from "@angular/core";
import { Routes, RouterModule, Router } from "@angular/router";
import { HomeComponent } from "./home/home.component";
import { PageNotFoundComponent } from "./page-not-found/page-not-found.component";
import { EditServerComponent } from "./servers/edit-server/edit-server.component";
import { ServerComponent } from "./servers/server/server.component";
import { ServersComponent } from "./servers/servers.component";
import { UserComponent } from "./users/user/user.component";
import { UsersComponent } from "./users/users.component";
import { AuthGuard } from "./auth-guard.service";
import { CanDeactivateGuard } from "./servers/edit-server/can-deactivate-guard.service";

const appRoutes: Routes = [
{ path: "", component: HomeComponent },
{
path: "users",
component: UsersComponent,
children: [{ path: ":id/:name", component: UserComponent }],
},

{
path: "servers",
// canActivate: [AuthGuard],
canActivateChild: [AuthGuard],
component: ServersComponent,
children: [
{ path: ":id", component: ServerComponent },
{
path: ":id/edit",
component: EditServerComponent,
canDeactivate: [CanDeactivateGuard],
},
],
},
{ path: "not-found", component: PageNotFoundComponent },
{ path: "\*\*", redirectTo: "not-found" },
];

@NgModule({
imports: [RouterModule.forRoot(appRoutes)],
exports: [RouterModule],
})
export class AppRoutingModule {}
