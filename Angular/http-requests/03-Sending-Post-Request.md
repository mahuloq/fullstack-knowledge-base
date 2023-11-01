# NEed to make sure your app.module has HttpRequestClient imported, then take your URL given on firebase

onCreatePost(postData: { title: string; content: string }) {
// Send Http request
this.http
.post(
"https://http-start-5f6d7-default-rtdb.firebaseio.com/posts.json",
postData
)
.subscribe((responseData) => {
console.log(responseData);
});
}

# Have to subscribe to aquire the data.
