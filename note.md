### Forms
- on the request object, there are two methods to parse the form. 
- r.FormValue is a convenience function. It calls ParseForm if it has to
- r.Form and r.PostForm are two different fields. They are bothe url.Values types (which itself is a map[string][]string underneath). 
  The difference is that the latter also includes values from the query parameters while PostForm only includes values from the Body of PUT, POST, and PATCH 
- r.ParseForm populates both Form and PostForm
- [This blog post](https://javarevisited.blogspot.com/2017/06/difference-between-applicationx-www-form-urlencoded-vs-multipart-form-data.html) explains the diff between the two MIME types: url-encoded, and multipart
- url-encoded is encodes just like query parameters. multipart-from encodes by using an impossible-in-the-chosen-encodin-scheme character to mark boundaries
- ParseForm thus populates Form and PostForm. but only checks the body for url-encoded MIME headers specified. In any cases, it checks the query (and thus populates r.Form)
- in a case where the req is not Post/put/patch, or the header did not state url-encoded, ParseForm does not check the body
- ParseMultipartForm focuses on the body. It parses multipartencoded forms. It might call ParseForm. and if by calling ParseForm, theres an error it still oes on to parse the body

