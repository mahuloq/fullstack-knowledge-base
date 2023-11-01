# Currently if you dont do anything the data will be of type any, which is fine, but is limited in how you can access the data. Making a model such as follows

export interface Post {
title: string;
content: string;
id?: string;
}

# then using it here

private fetchPosts() {
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
console.log(posts);
});

# and here

onCreatePost(postData: Post) {
// Send Http request
this.http
.post<{ name: string }>(
"https://http-start-5f6d7-default-rtdb.firebaseio.com/posts.json",
postData
)
.subscribe((responseData) => {
console.log(responseData);
});
}
