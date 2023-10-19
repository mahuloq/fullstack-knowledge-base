# Observables - userinput, events, http requests, triggered in vode

# Observer - You write the code which gets executed to , handle date, handle an error, handle completion

# params is an observable, stream of route paramaters. We setup a custom observable as follows

import { Component, OnDestroy, OnInit } from "@angular/core";
import { Subscription, interval } from "rxjs";

# Importing them from rxjs

@Component({
selector: "app-home",
templateUrl: "./home.component.html",
styleUrls: ["./home.component.css"],
})

export class HomeComponent implements OnInit, OnDestroy {
private firstObsSubscription: Subscription;

constructor() {}

ngOnInit() {
this.firstObsSubscription = interval(1000).subscribe((count) => {
console.log(count);
});
}

ngOnDestroy(): void {
this.firstObsSubscription.unsubscribe();
}
}

# We use onDestroy to stop the observable after we navigate away.
