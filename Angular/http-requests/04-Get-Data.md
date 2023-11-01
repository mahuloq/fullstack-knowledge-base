# This is how you can fetch data.

private fetchPosts() {
this.http
.get("https://http-start-5f6d7-default-rtdb.firebaseio.com/posts.json")
.subscribe((posts) => {
console.log(posts);
});

# then put fetchPosts inside

       onFetchPosts() {
    // Send Http request
    this.fetchPosts();

}

# and

    ngOnInit() {
    this.fetchPosts();

}

# Howevor that does work to actually get the posts you need to

private fetchPosts() {
this.http
.get("https://http-start-5f6d7-default-rtdb.firebaseio.com/posts.json")
.pipe(
map((responseData) => {
const postsArray = [];
for (const key in responseData) {
if (responseData.hasOwnProperty(key)) {
postsArray.push({ ...responseData[key], id: key });
}
}
})
)
.subscribe((posts) => {
console.log(posts);
});
