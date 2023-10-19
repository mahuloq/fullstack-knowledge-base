import { Component, OnDestroy, OnInit } from "@angular/core";
import { Subscription, interval, Observable } from "rxjs";

@Component({
selector: "app-home",
templateUrl: "./home.component.html",
styleUrls: ["./home.component.css"],
})
export class HomeComponent implements OnInit, OnDestroy {
private firstObsSubscription: Subscription;

constructor() {}

ngOnInit() {
// this.firstObsSubscription = interval(1000).subscribe((count) => {
// console.log(count);
// });

    const customIntervalObservable = Observable.create((observer) => {
      let count = 0;
      setInterval(() => {
        observer.next(count);
        if (count == 2) {
          observer.complete();
        }
        if (count > 3) {
          observer.error(new Error("Count is greater 3!"));
        }
        count++;
      }, 1000);
    });
    this.firstObsSubscription = customIntervalObservable.subscribe(
      (data) => {
        console.log(data);
      },
      (error) => {
        console.log(error);
        alert(error.message);
      },
      () => {
        console.log("Mission Complete");
      }
    );

}

ngOnDestroy(): void {
this.firstObsSubscription.unsubscribe();
}
}

# This is how you do error and complete observables. You dont HAVE to unsubscribe from error or complete obs as when they trigger they do so automatically, but it is still a good practice to do so as they will still run if you switch pages.
