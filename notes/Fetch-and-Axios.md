# Data Fetching with Fetch and Axios
Both [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) and [Axios](https://github.com/axios/axios) are `Promise`-based approaches to data fetching (thus avoiding callback hell), and are modern replacements for [XHR](https://github.com/minkaotic/front-end-notes/blob/master/notes/AJAX-Notes.md)-based data fetching. All three approaches allow web applications to send/retrieve data from a server asynchronously in the background, without reloading the current page.

## Fetch API
- data fetching interface that is native to the browser
- it is an improvement over the `XMLHttpRequest` API, making it easier to make asynchronous requests and handle responses better
- well supported by modern browsers, but not at all by IE (can be [polyfilled](https://github.com/github/fetch))

### Usage examples
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

## Axios
- popular data fetching library ("HTTP client for the browser and node.js") with additional features over Fetch:
  - stronger browser support - incl. IE11
  - intercept request and response
  - automatically converts data to JSON
  - supports protection against XSRF attacks

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


## Sources
- [Data Fetching in React](https://teamtreehouse.com/library/data-fetching-in-react) course on Treehouse
- [S.Bangare: The Fetch API - A modern replacement for XMLHttpRequest](https://medium.com/beginners-guide-to-mobile-web-development/the-fetch-api-2c962591f5c)
- [GP Lee: An absolute Guide to JavaScript Http Requests](https://medium.com/javascript-in-plain-english/an-absolute-guide-to-javascript-http-requests-44c685edfa51)
