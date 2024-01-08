1. Create a VUE js / nuxt js Project. VS code or codesandbox.io
2. Execute a HTTP GET of JSON data from the following API:
https://dummyjson.com/posts
This will return a json array of posts
3. Display the posts as a HTML table with the following columns: id, title body, userId
4. Add a clickable button to each row
When the button is clicked, you will make another rest call to view the comments
associated with the row. Note you will have to use an actual postId instead of
“:postId” in the url
https://dummyjson.com/posts/:postId/comments
E.g.
https://dummyjson.com/posts/1/comments
Display the comment data somewhere on the screen