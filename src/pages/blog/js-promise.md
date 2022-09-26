---
layout: "../../layouts/BlogPost.astro"
title: "JavaScript: Promise"
pubDate: "Jul 15, 2022"
published: false
---

*Promises* give us a way to make sense out of asynchronous behavior. When making an asynchronous request, one of two things can happen: everything goes as we hope or there’s an error. There may be several different types of successful or unsuccessful requests. For example, we could try several ways to obtain the data to reach success. We could also receive multiple types of errors. Promises give us a way to simplify back to a simple pass or fail.

Let’s create an asynchronous promise for loading data from the `randomuser`.me API. This API has information like email address, name, phone number, location, and so on for fake members and is great to use as dummy data.

The `getFakeMembers` function returns a new promise. The promise makes a request to the API. If the promise is successful, the data will load. If the promise is unsuccessful, an error will occur

```javascript
const getFakeMembers = count => new Promise((resolves, rejects) => {
  const api = `https://api.randomuser.me/?nat=US&results=${count}`
  const request = new XMLHttpRequest()
  request.open('GET', api)
  request.onload = () => 
       (request.status === 200) ? 
        resolves(JSON.parse(request.response).results) : 
        reject(Error(request.statusText))
  request.onerror = (err) => rejects(err)
  request.send()
})
```

With that, the promise has been created, but it hasn’t been used yet. We can use the promise by calling the `getFakeMembers` function and passing in the number of members that should be loaded. The `then` function can be chained on to do something once the promise has been fulfilled. This is called composition. We’ll also use an additional callback that handles errors:


```javascript
getFakeMembers(5).then(
  members => console.log(members),
  err => console.error(
      new Error("cannot load members from randomuser.me"))
)
```

Promises make dealing with asynchronous requests easier, which is good, because we have to deal with a lot of asynchronous data in JavaScript. You’ll also see promises used heavily in Node.js, so a solid understanding of promises is essential for the modern JavaScript engineer.