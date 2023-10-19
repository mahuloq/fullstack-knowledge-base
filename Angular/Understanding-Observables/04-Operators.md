import { Component, OnDestroy, OnInit } from "@angular/core";
import { Subscription, interval, Observable } from "rxjs";
import { filter } from "rxjs/operators";
import { map } from "rxjs/operators/map";

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
        if (count == 5) {
          observer.complete();
        }
        if (count > 3) {
          observer.error(new Error("Count is greater 3!"));
        }
        count++;
      }, 1000);
    });

    this.firstObsSubscription = customIntervalObservable
      .pipe(
        filter((data) => {
          return data != 0;
        }),
        map((data: number) => {
          return "Round: " + data;
        })
      )
      .subscribe(
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

## Careful on auto importing, often chooses rxjs from compat, which makes the operators act differently.

# Also was unable to get .pipe(

# filter((data) => {

# return data > 0;

# }),

#

# to work as I get an error
