  <div class="row">
    <div class="col-xs-12 col-md-6 col-md-offset-3">
      <p *ngIf="loadedPosts.length < 1 && !isFetching">No posts available!</p>
      <ul class="list-gr" *ngIf="loadedPosts.length >= 1 && !isFetching">
        <li class="list-group-item" *ngFor="let post of loadedPosts">
          <h3>{{ post.title }}</h3>
          <p>{{ post.content }}</p>
        </li>
      </ul>
      <p *ngIf="isFetching">Loading...</p>
    </div>
  </div>

export class AppComponent implements OnInit {
loadedPosts: Post[] = [];
isFetching = false;

    private fetchPosts() {
    this.isFetching = true;
    this.http
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
        })
      )
      .subscribe((posts) => {
        this.isFetching = false;
        this.loadedPosts = posts;
      });
