onFetchPosts() {
this.isFetching = true;
this.postService.fetchPosts().subscribe(
(posts) => {
this.isFetching = false;
this.loadedPosts = posts;
this.error = null;
},
(error) => {
this.error = error.message;
}
);
}

# this will run the error code if an error is recieved.

    <div class="row">
    <div class="col-xs-12 col-md-6 col-md-offset-3">
      <p *ngIf="loadedPosts.length < 1 && !isFetching">No posts available!</p>
      <ul class="list-gr" *ngIf="loadedPosts.length >= 1 && !isFetching">
        <li class="list-group-item" *ngFor="let post of loadedPosts">
          <h3>{{ post.title }}</h3>
          <p>{{ post.content }}</p>
        </li>
      </ul>
      <p *ngIf="isFetching && !error">Loading...</p>
      <div class="alert alert-danger" *ngIf="error">
        <h1>An Error Occured!</h1>
        <p>{{ error }}</p>
      </div>

# Can also use a subject

error = new Subject<string>();

ngOnInit() {
this.errorSub = this.postService.error.subscribe((errorMessage) => {
this.error = errorMessage;

this.http
.post<{ name: string }>(
"https://http-start-5f6d7-default-rtdb.firebaseio.com/posts.json",
postData
)
.subscribe(
(responseData) => {
console.log(responseData);
},
(error) => {
this.error.next(error.message);
console.log("Whoops");
}
);

# there are also some error commands from rxjs

import { map, catchError } from "rxjs/operators";
import { Subject, throwError } from "rxjs";

fetchPosts() {
return this.http
.get<{ [key: string]: Post }>(
"https://http-start-5f6d7-default-rtdb.firebaseio.com/posts.json"
)
.pipe(
map((responseData) => {
const postsArray: Post[] = [];
for (const key in responseData) {
if (responseData.hasOwnProperty(key)) {
postsArray.push({ ...responseData[key], id: key });
}
}
return postsArray;
}),
catchError((errorRes) => {
// send to analytics sever
return throwError(errorRes);
})
);
}

# Easy way to clear error

<div class="alert alert-danger" *ngIf="error">
        <h1>An Error Occured!</h1>
        <p>{{ error }}</p>
        <button (click)="onHandleError()" class="btn btn-danger">Okay</button>
      </div>

      onHandleError() {
    this.error = null;

}
