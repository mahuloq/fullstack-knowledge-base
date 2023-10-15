## When the page is destroyed becuase you leave, Angular will destroy your subscirption if you are using the default observables, but if you dont, you may need to implement something like the following.

import { Component, OnInit } from "@angular/core";
import { ActivatedRoute, Params } from "@angular/router";

## Import this

import {Subscription} from 'rxjs/Subscription';

@Component({
selector: "app-user",
templateUrl: "./user.component.html",
styleUrls: ["./user.component.css"],
})

## Implement on Destroy

export class UserComponent implements OnInit, OnDestroy {
user: { id: number; name: string };

## Init a new property

paramsSubscription: Subscription;

constructor(private route: ActivatedRoute) {}

ngOnInit() {
this.user = {
id: this.route.snapshot.params["id"],
name: this.route.snapshot.params["name"],
};
this.paramsSubscription = this.route.params.subscribe((params: Params) => {
this.user.id = params["id"];
this.user.name = params["name"];
});
}
}

## Then use the following

ngOnDestroy(){
this.paramsSubscription.unsubscribe()'
}
