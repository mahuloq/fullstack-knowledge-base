## You can accept parameters for a route like follows

const appRoutes: Routes = [
{ path: "", component: HomeComponent },
{ path: "users", component: UsersComponent },

{ path: "users/:id", component: UserComponent },

{ path: "servers", component: ServersComponent },

];

## if you put /:something after the path, it will accept parameters

## you can pull data by importing ActivatedRoute, Injecting it.

import { ActivatedRoute } from "@angular/router";

@Component({
selector: "app-user",
templateUrl: "./user.component.html",
styleUrls: ["./user.component.css"],
})
export class UserComponent implements OnInit {
user: { id: number; name: string };

constructor(private route: ActivatedRoute) {}

---

## And then get the data with snapshot.params

ngOnInit() {
this.user = {
id: this.route.snapshot.params["id"],
name: this.route.snapshot.params["name"],
};
}
}

## Say we made a button that changed the params. Like

<a [routerLink]="['/users', 10, 'Anna']">Load Anna(10)</a>

## If you click this the url will change, but no info on the page will, that is becuase how we are capturing the data is with snapshot. To make sure our updated data is passed to the page we need to use.

this.route.params.subscribe((params: Params) => {
this.user.id = params["id"];
this.user.name = params["name"];
});

## Params can be subscribed to like above, make sure to load the Params.
