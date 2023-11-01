ngOnInit() {
this.isFetching = true;
this.postService.fetchPosts().subscribe((posts) => {
this.isFetching = false;
this.loadedPosts = posts;
});
}

onFetchPosts() {
this.isFetching = true;
this.postService.fetchPosts().subscribe((posts) => {
this.isFetching = false;
this.loadedPosts = posts;
});
}

# We subscribe in the component if the component cares about the data

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
})
);
}
