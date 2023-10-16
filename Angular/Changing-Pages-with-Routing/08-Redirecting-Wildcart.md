## can redirect to a page with the following syntax

{ path: "not-found", component: PageNotFoundComponent },
{ path: "\*\*", redirectTo: "not-found" },

Since the default matching strategy is "prefix" , Angular checks if the path you entered in the URL does start with the path specified in the route. Of course every path starts with '' (Important: That's no whitespace, it's simply "nothing").

To fix this behavior, you need to change the matching strategy to "full" :

{ path: '', redirectTo: '/somewhere-else', pathMatch: 'full' }
Now, you only get redirected, if the full path is '' (so only if you got NO other content in your path in this example).
