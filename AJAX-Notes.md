# AJAX Notes

AJAX ("Asynchronous JavaScript And XML") is an important front-end web technology that lets JavaScript communicate with a web server. It lets you update HTML without leaving or reloading the current page, creating a better, faster experience for users.

### Contents

- [Making an XHR Request](#making-an-xhr-request)
- [AJAX Properties](#ajax-properties)
  - [Event Handler Properties](#event-handler-properties)
  - [Other Settable Properties](#other-settable-properties)
  - [Read-only Properties](#read-only-properties)
- [AJAX Security Limitations](#ajax-security-limitations)
- [Further Resources](#further-resources)

-------------

## Making an XHR Request
> :bulb: AJAX is the process of using JavaScript to send a request to web server, receive a response, and then do something with that data.

AJAX programming relies heavily on the **[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) (XHR)** object to communicate with servers.
- It's predecessor `XMLHTTP` was first introduced 1999 by Microsoft with IE5.
- Despite its name, XHR can send and receive information in various formats, including JSON, XML, HTML, and text files.

##### 4 steps to creating & sending an XHR request:
1. Create an `XMLHttpRequest` object.
1. Define a callback function that should run when the server returns its response (typically this processes the returned data and updates the page). This callback is set up to respond to a given event, by assigning it to one of AJAX's built in [event handler properties](#event-handler-properties).
1. Open a request, providing the HTTP method to be used and the URL to which the request should be sent.
1. Send the request.

**Example** - loading HTML from a static file on the webserver: 
```js
// STEP 1
const request = new XMLHttpRequest();
// STEP 2
request.onreadystatechange = () => {
  if(request.readyState === 4) {
    const target = document.getElementById('target');
    target.innerHTML = request.responseText; // info sent back by the server
  }
};
// STEP 3
request.open('GET', 'sidebar.html');
// STEP 4
request.send();
```

:bulb: **NB:** You should create a new `XMLHttpRequest` object for each AJAX request you are making.

> `.open()` and `.send()` are the most commonly used methods. For other methods on `XMLHttpRequest`, e.g. for managing headers, [see MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest#Methods).

## AJAX Properties
The `XMLHttpRequest` object has a number of properties available to help with the request control flow & settings:

### Event Handler Properties
- `.onreadystatechange` - called whenever the `readyState` attribute changes.

- `.ontimeout` - called whenever the request times out.

> :point_right: `onreadystatechange` is supported in all browsers. A number of additional event handlers have been implemented in various browsers ( `onload`, `onerror`, `onprogress`, etc.). See [Using XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) for more detail.

### Other Settable Properties
- `.timeout` - an unsigned long representing the number of milliseconds a request can take before automatically being terminated.

- `.withCredentials` - a Boolean that indicates whether or not cross-site Access-Control requests should be made using credentials such as cookies or authorization headers.

### Read-only Properties
- [`.readyState`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/readyState) returns an unsigned short, the state of the request. `4` means the request has completed.

- `.response` - returns an ArrayBuffer, Blob, Document, JavaScript object, or a DOMString, depending on the value of `XMLHttpRequest.responseType`, that contains the response entity body.

- `.responseText` - returns a `DOMString` that contains the response to the request as text, or null if the request was unsuccessful or has not yet been sent.

- [`.status`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/status) - returns an unsigned short with the HTTP status code of the response of the request.

## AJAX Security Limitations
AJAX is usually limited by a web browser's ["same origin" policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy), which controls how JavaScript can access content from a web server and means the browser will prevent AJAX requests to web sites other than that which the page was retrieved from. 

Even switching protocols (HTTP <-> HTTPS), port numbers or hosts on the same server isn't allowed.

!["same origin" policy](/img/same-origin-policy.png)

### Options to circumvent this:
- route requests via a web proxy
- use JSONP (JSON with Padding), which relies on the ability to link to JS files across domains
- [CORS (Cross-Origin Resource Sharing)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) - W3C recommendation & already implemented in most browsers


## Further Resources:
- [MDN intro to AJAX](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started)
- [MDN on using XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)
