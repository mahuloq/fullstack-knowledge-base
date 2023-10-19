import { Injectable } from "@angular/core";
import { Subject } from "rxjs";

@Injectable({ providedIn: "root" })
export class UserService {
activatedEmitter = new Subject<boolean>();
}

# app.component.ts

import { Component, OnInit, OnDestroy } from "@angular/core";
import { UserService } from "./user.service";
import { Subscription } from "rxjs";

@Component({
selector: "app-root",
templateUrl: "./app.component.html",
styleUrls: ["./app.component.css"],
})
export class AppComponent implements OnInit, OnDestroy {
userActivated = false;
private activatedSub: Subscription;

constructor(private userService: UserService) {}

ngOnInit() {
this.activatedSub = this.userService.activatedEmitter.subscribe(
(didActivate) => {
this.userActivated = didActivate;
}
);
}

ngOnDestroy(): void {
this.activatedSub.unsubscribe();
}
}

# app/component.html

<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <a routerLink="/">Home</a> |
      <a [routerLink]="['user', 1]"> User 1 </a>
      |
      <a [routerLink]="['user', 2]"> User 2 </a>
    </div>
  </div>
  <hr />
  <p *ngIf="userActivated">Activated!</p>
  <hr />
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
  </div>
</div>

# user.component.ts

import { Component, OnInit } from "@angular/core";
import { ActivatedRoute, Params } from "@angular/router";
import { UserService } from "../user.service";

@Component({
selector: "app-user",
templateUrl: "./user.component.html",
styleUrls: ["./user.component.css"],
})
export class UserComponent implements OnInit {
id: number;

constructor(
private route: ActivatedRoute,
private userService: UserService
) {}

ngOnInit() {
this.route.params.subscribe((params: Params) => {
this.id = +params.id;
});
}
onActivate() {
this.userService.activatedEmitter.next(true);
}
}

# user.component.html

<p>
  User with <strong>ID {{ id }}</strong> was loaded
</p>
<button class="btn btn-primary" (click)="onActivate()">Activate</button>
