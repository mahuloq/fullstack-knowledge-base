## path in routing module

{
path: "not-found",
component: ErrorPageComponent,
data: { message: "Page not Found!" },
},
{ path: "\*\*", redirectTo: "not-found" },

## error-page-component.ts

import { Component, OnInit } from "@angular/core";
import { ActivatedRoute, Data } from "@angular/router";

@Component({
selector: "app-error-page",
templateUrl: "./error-page.component.html",
styleUrls: ["./error-page.component.css"],
})
export class ErrorPageComponent implements OnInit {
errorMessage: string;
constructor(private route: ActivatedRoute) {}

ngOnInit(): void {
// this.errorMessage = this.route.snapshot.data["message"];
this.route.data.subscribe((data: Data) => {
this.errorMessage = data["message"];
});
}
}

# Dynamic Data

Renderer runs some code before comoponent is rendered

import {
ActivatedRouteSnapshot,
Resolve,
RouterStateSnapshot,
} from "@angular/router";
import { Observable } from "rxjs";
import { ServersService } from "../servers.service";
import { Injectable } from "@angular/core";

interface Server {
id: number;
name: string;
status: string;
}

@Injectable()
export class ServerResolver implements Resolve<Server> {
constructor(private serversService: ServersService) {}

resolve(
route: ActivatedRouteSnapshot,
state: RouterStateSnapshot
): Server | Observable<Server> | Promise<Server> {
return this.serversService.getServer(+route.params["id"]);
}
}

# Pull data in the server component at boot up

ngOnInit() {
this.route.data.subscribe((data: Data) => {
this.server = data["server"];
});
