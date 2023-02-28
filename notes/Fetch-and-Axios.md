# Data Fetching with Fetch and Axios
Both [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) and [Axios](https://github.com/axios/axios) are `Promise`-based, asynchronous approaches to data fetching (thus avoiding callback hell), and are modern replacements for [XHR](https://github.com/minkaotic/front-end-notes/blob/master/notes/AJAX-Notes.md)-based data fetching. All three approaches allow web applications to send/retrieve data from a server in the background, without reloading the current page.

## Fetch API
- the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) offers a data fetching interface that is native to the browser (i.e. no libraries needed to use it)
- it is an improvement over the `XMLHttpRequest` API, making it easier to make asynchronous requests and handle responses better
- well supported by modern browsers, but not at all by IE (can be [polyfilled](https://dev.to/adrianbdesigns/how-to-polyfill-javascript-fetch-function-for-internet-explorer-g46)) (and many build stacks automatically do this)

### Usage examples
- the Fetch API provides a global `fetch()` method that provides an easy, logical way to fetch resources asynchronously across the network
- `fetch()` takes one mandatory argument: the request URL, and an optional argument of request options
- 
```js
fetch("http://api.giphy.com/v1/gifs/trending?api_key=dc6zaTOxFJmzC")
    .then(response => response.json())
    .then(responseData => {
        // do something with responseData
    })
    // if something goes wrong with the fetch request
    .catch(error => {
        console.log("Error fetching and parsing data", error);
    });
```

The [`response` object](https://developer.mozilla.org/en-US/docs/Web/API/Response) provided by fetch represents the response to a request and we frequently interact with the following in our code:
- `response.json()` - returns the parsed response as JSON
- `response.status` - the HTTP status code of the response

#### 🔥 Note!
- The `.catch()` in a fetch chain will only be triggered if the request fails altogether (i.e. never returns) - if the request comes back with a failure HTTP status (e.g. 400 or 500), this won't go into the `.catch()` block.
- As a result, developers often don't use `.catch()` at all and just write their own failure handling logic.


## Axios
- [Axios](https://www.npmjs.com/package/axios) is a popular data fetching *library* with additional features over Fetch:
  - stronger browser support - incl. IE11
  - protection against XSRF attacks
  - built in support for download progress
  - "automatically" converts data to JSON
  - non-200 response codes automatically count as 'error'

### Usage examples
```js
axios.get('http://api.giphy.com/v1/gifs/trending?api_key=dc6zaTOxFJmzC')
    .then(response => {
        // data is exposed through response.data in Axios
        // do something with that here
    })
    .catch(error => {
        console.log('Error fetching and parsing data', error);
    });
```


## XHR vs. Fetch vs Axios feature matrix
![feature matrix](https://miro.medium.com/max/864/1*tQUlDPG6wBJ6TjwzMwd4CQ.png)


## Sources & further reading
- [Data Fetching in React](https://teamtreehouse.com/library/data-fetching-in-react) course on Treehouse
- https://www.pluralsight.com/guides/axios-vs-fetch
- https://www.geeksforgeeks.org/difference-between-fetch-and-axios-js-for-making-http-requests/
- https://blog.bitsrc.io/performing-http-requests-fetch-vs-axios-b62b44fed10d
- [S.Bangare: The Fetch API - A modern replacement for XMLHttpRequest](https://medium.com/beginners-guide-to-mobile-web-development/the-fetch-api-2c962591f5c)
- [GP Lee: An absolute Guide to JavaScript Http Requests](https://medium.com/javascript-in-plain-english/an-absolute-guide-to-javascript-http-requests-44c685edfa51)

