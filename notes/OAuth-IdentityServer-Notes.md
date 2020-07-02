# ASP.NET Core and OAuth
*Securing ASP.Net Core applications using OAuth and OpenID Connect*

Notes based on [this Pluralsight course](https://app.pluralsight.com/library/courses/asp-dot-net-core-oauth/table-of-contents) and [IdentityServer Quickstarts](https://identityserver4.readthedocs.io/en/latest/quickstarts/0_overview.html).

## Contents
1. [Introduction to Token-based security](#introduction-to-token-based-security)
1. [OAuth & OpenID Connect](#oauth--openid-connect)
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
- "Token" = JSON Web Token (JWT), Base64 encoded
- contains some user data, such as email address
- contains information about the authorisation server
- signed by the authorisation server

= this type of token is also referred to as **Access Token** or **Identity Token**

#### What's an authorisation server?
:point_right: an application using the [OAuth and OpenID Connect](#oauth--openid-connect) security protocols in order to trade a username and password (or other such credentials) for a secure token. The authorisation server signs the token with a private key that *only it has access to*. The public key can be accessed by any interacting application, and is used for token validation.

:fire: **It's the responsibility of the API receiving the token in the request (the consumer) to ensure that the signature is intact and the token is valid** (using the public key).

![signing tokens](/img/token-signing.PNG)


## OAuth & OpenID Connect
Both are protocols stipulating how to build APIs such that they can be accessed to retrieve data in a common and secure manner. 

- **[OAuth 2.0](https://oauth.net/2/)** is a token-based security protocol. It is the industry-standard protocol for authorisation, focusing on client developer simplicity while providing specific authorisation flows for web apps, desktop apps, mobile devices IoT devices. It's *not backwards compatible* with older versions of OAuth.
- **[OpenID Connect](https://openid.net/connect/)** complements OAuth 2.0, by providing a simple identity layer on top of it, which allows clients to: 
  - verify the identity of an end-user based on the authentication performed by an authorisation server
  - obtain basic profile information about the end-user

### Authentication vs. Authorisation
- Authorisation is about gaining access (to certain resources / to data / to a building etc.)
- Authentication is about proving who we are (our identity), i.e. via our user name and password

> :bulb: **OAuth is all about *authorisation*** - a way to prove that someone has access to something. **OpenID Connect is about *authentication*** - allowing us to identify who the user is.**

### Applying these protocols
Three options are:
1. **Roll your own** implementation (avoid if possible)
1. Use a **framework/library such as [IdentityServer](https://identityserver.io/)**, an open source product that implements the OAuth & OpenID Connect protocols and allows you to easily build a server application to handle authentication and authorization
1. Use a **managed SaaS/PaaS** solution (e.g. [Amazon Cognito](https://aws.amazon.com/cognito/), [Auth0](https://auth0.com/), [Okta](https://www.okta.com/))

### Available endpoints

**OAuth Endpoints** (described in **[RFC 6749](https://tools.ietf.org/html/rfc6749)**) allow us to work with the Authorisation server:
- `/authorize`- supports multiple different authorisation flows, for example:
  - POST to authorisation server to request a new access token
  - redirect to enter user name and password, then redirect back to original website
  - provide credentials that identify software to retrieve access
- `/token` - also allows performing a new access token request; but additionally allows refreshing an access token, & trading an authorisation code for an access token
- `/revocation` - revoke (access or refresh) token (described in the additional [RFC 7009](https://tools.ietf.org/html/rfc7009))

**OpenID Connect** additionally allows us to work with the identity of the user that is currently authorised:
- `/userinfo` - get information about the user
- `/checksession` - check the session for the current user
- `/endsession` - end the session for the current user
- `/.well-known/openid-configuration` - information about our authorisation server, i.e. list of all our endpoints and configurations
- `/.well-known/jwks` - information about JWTs and the public keys - used for token validation


What are flows, grants, claims and tokens?





