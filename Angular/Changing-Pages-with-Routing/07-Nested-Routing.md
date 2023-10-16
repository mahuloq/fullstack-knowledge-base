## You can load child routes like follows

const appRoutes: Routes = [
{ path: "", component: HomeComponent },
{
path: "users",
component: UsersComponent,
children: [{ path: ":id/:name", component: UserComponent }],
},

{
path: "servers",
component: ServersComponent,
children: [
{ path: ":id", component: ServerComponent },
{ path: ":id/edit", component: EditServerComponent },
],
},
];

## And then use <router-outlet></router-outlet> to display them

## you can access the parems from nested components with

onEdit() {
this.router.navigate(["edit"], {
relativeTo: this.route,
queryParamsHandling: "preserve",
});
}
}

## with queryParamsHandling
