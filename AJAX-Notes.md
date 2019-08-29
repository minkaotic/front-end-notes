# AJAX Notes

AJAX ("Asynchronous JavaScript And XML") is an important front-end web technology that lets JavaScript communicate with a web server. It lets you update HTML without leaving or reloading the current page, creating a better, faster experience for users.

### Contents

- [Overview](#overview)
- [Further Resources](#further-resources)

-------------

## Overview
> :bulb: AJAX is the process of using JavaScript to send a request to web server, receive a response, and then do something with that data.

AJAX programming relies heavily on the **[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) (XHR)** object to communicate with servers.
- This was first introduced 1999 by Microsoft with IE5.
- Despite its name, XHR can send and receive information in various formats, including JSON, XML, HTML, and text files.

##### 4 steps to creating & sending an XHR request:
1. Create an `XMLHttpRequest` object
1. Define a callback function that should run when the server returns its response (typically this processes the returned data and updates the page)
1. Open a request, providing the HTTP method to be used and the URL to which the request should be sent
1. Send the request


## Further Resources:
- [MDN intro to AJAX](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started)
