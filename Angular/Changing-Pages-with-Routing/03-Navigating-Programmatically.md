You can code navigation in like in following example.

<b class="btn btn-primary" (click)="onLoadServers()">Load Servers</b>

then within the TS file.

import { Component, OnInit } from "@angular/core";
import { Router } from "@angular/router";

@Component({
selector: "app-home",
templateUrl: "./home.component.html",
styleUrls: ["./home.component.css"],
})
export class HomeComponent implements OnInit {
constructor(private router: Router) {}

ngOnInit() {}

onLoadServers() {
//complex calculation

    this.router.navigate(["/servers"]);

}
}

So you have to inject routing with your constuctor, then call this.route.navigate(['with path here])

---

If you try to navigate to the page you are already on

import { Component, OnInit } from "@angular/core";
import { ServersService } from "./servers.service";
import { ActivatedRoute, Router } from "@angular/router";

constructor(
private serversService: ServersService,
private router: Router,
private route: ActivatedRoute
) {}

onReload() {
this.router.navigate(["servers"], { relativeTo: this.route });
}

this will give an error, but without relativeTo it will not, relativeTo tells the navigate method where to begin the navigation from. Make you sure import and inject ActivatedRoute
