Routes allow your page to load different components when the web address changes at the top of the page.

To set up routes in your angular.json

import { RouterModule, Routes } from "@angular/router";

const appRoutes: Routes = [
{ path: "", component: HomeComponent },
{ path: "users", component: UsersComponent },
{ path: "servers", component: ServersComponent },
];

imports: [BrowserModule, FormsModule, RouterModule.forRoot(appRoutes)],

now when you type in the web address

http://localhost:4200/servers

or

http://localhost:4200/users

it loads that components
