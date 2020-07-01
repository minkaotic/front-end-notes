# ASP.NET Core and OAuth
*Securing ASP.Net Core applications using OAuth and OpenID Connect*

Notes based on [this Pluralsight course](https://app.pluralsight.com/library/courses/asp-dot-net-core-oauth/table-of-contents) and [IdentityServer Quickstarts](https://identityserver4.readthedocs.io/en/latest/quickstarts/0_overview.html).

## Contents
1. [Introduction to Token-based security](#introduction-to-token-based-security)
1. [OAuth & OpenId Connect](#oauth--openid-connect)
________________

## Introduction to Token-based security
:bulb: **Premise:** you don't want to have to be passing a user's user name and password around every time you need to call an endpoint to access some user's information.

**Common workflow to get around this in .NET Core:**
1. Use `[Authorization]` attribute on controllers / actions
1. Have website redirect the request to the authorisation server, where the user will be securely entering their user name + password
1. Redirect user back to our website with a token that can be used to interact with our API (passed in header of each request)
1. API checks validity of the token with the authorisation server whenever requested
1. (If a token is compromised, communicate this back to the authorisation server)

### Benefits
- prevents the need to repeatedly share a user's password around, incl. to 3rd parties
- instead, user securely authenticates themselves once, receiving a token that proves that they are verifiably themselves
- that token is then used to access any resources
- if a token gets lost or unduely exposed, we can simply revoke access for it
- tokens are typically short-lived to minimise security risks
- because tokens are typically signed, we can ensure that data isn't tampered with

![token based security overview](/img/token-based-security-overview.PNG)

### Keeping Tokens secure
> :fire: **Treat tokens like passwords**, as they do provide unrestricted access to a user's data, while they are valid

#### What's in a token?
- "Token" = JSON Web Token (JWT)
- Base64 encoded
- contains some user data, such as email address
- contains information about the authorisation server
- signed by the authorisation server

= this type of token is also referred to as **Access Token** or **Identity Token**

#### What's an authorisation server?
:point_right: an application using the [OAuth and OpenId Connect](#oauth--openid-connect) security protocols in order to trade a username and password (or other such credentials) for a secure token. The authorisation server signs the token with a private key that *only it has access to*. The public key can be accessed by any interacting application, and is used for token validation.

:fire: **It's the responsibility of the API receiving the token in the request (the consumer) to ensure that the signature is intact and the token is valid** (using the public key).

![signing tokens](/img/token-signing.PNG)


## OAuth & OpenId Connect
- Both are protocols stipulating how to build APIs such that they can be accessed to retrieve data in a common and secure manner
- **OAuth 2.0** is the industry-standard protocol for authorisation, focusing on client developer simplicity while providing specific authorisation flows for web apps, desktop apps, mobile devices IoT devices.



Authentication vs. Authorisation

What are flows, grants, claims and tokens?





