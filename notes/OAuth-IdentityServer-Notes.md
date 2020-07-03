# ASP.NET Core and OAuth
*Securing ASP.Net Core applications using OAuth and OpenID Connect*

Notes based on [this Pluralsight course](https://app.pluralsight.com/library/courses/asp-dot-net-core-oauth/table-of-contents) and [IdentityServer Quickstarts](https://identityserver4.readthedocs.io/en/latest/quickstarts/0_overview.html).

## Contents
1. [Introduction to Token-based security](#introduction-to-token-based-security)
1. [OAuth & OpenID Connect](#oauth--openid-connect)
1. [Obtaining, inspecting and working with Access Tokens](#obtaining-inspecting-and-working-with-access-tokens)
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
- `/authorize`- used to request tokens via the browser - typically involving authentication of the end-user and user-agent redirection
- `/token` - used to programmatically request a new access token; additionally allows refreshing an access token & trading an authorisation code for an access token
- `/revocation` - revoke (access or refresh) token (described in the additional [RFC 7009](https://tools.ietf.org/html/rfc7009))

**OpenID Connect** additionally allows us to work with the identity of the user that is currently authorised:
- `/userinfo` - get information about the user
- `/checksession` - check the session for the current user
- `/endsession` - end the session for the current user
- `/.well-known/openid-configuration` - information about our authorisation server, i.e. list of all our endpoints and configurations
- `/.well-known/jwks` - information about JWTs and the public keys - used for token validation


## Obtaining, inspecting and working with Access Tokens
Demo example:
1. Call `/token` endpoint with a POST request containing `client_id`, `client_secret`, `grant_type`, `username` and `password` in a form-urlencoded body
1. Receive a response containing the `access_token`, `expires_in` and `token_type` ("Bearer")
1. Use the access token to requests resources that that user is authorised for from our API: GET request to relevant resource endpoint with an `Authorization` header specifying the type of token (Bearer) and token itself

### Inside the Access Token
> :bulb: You can inspect any token on [jwt.io](https://jwt.io/)!

Tokens break down into:
- **Header** - Information about how the token is structured
- **Payload** - *a.k.a. Claims*, containing any relevant information about the user; commonly contains details about:
  - Issuer
  - Audience
  - Expiry
  - Valid from
  - Client ID
  - Scopes (which parts of an API access is granted to)
  - Custom data (could include pretty much anything that is persistent and won't change between the the token being issued and it being used)
- **Signature** - ensures payload is intact

#### Scopes
- Scopes limit access to functionality
- Clients use scope values as defined in [3.3 of OAuth 2.0 [RFC6749]](https://tools.ietf.org/html/rfc6749#section-3.3) to specify what access privileges are being requested for Access Tokens. The scopes associated with Access Tokens determine what resources will be available when they are used to access OAuth 2.0 protected endpoints. 
- [OpenID Connect Scope](https://openid.net/specs/openid-connect-basic-1_0.html#Scopes) values include for example: `openid`, `profile`, `email`, `address` and `offline_access`
- We can also define **custom scopes**, for example `read` and `write` scopes - or anything else pertaining to different access levels applicable to our domain

### Choosing a Flow
OAuth provides different flows for retrieving an access token ("authorisation flows"):

#### Redirect Flows
- **Implicit Grant** (sequence diagram below) - Redirect the user to the authorisation server, where they provide their user name and password. They are then redirected back to website with an access token which allows them to have logged-in access (best for JavaScript clients / browser-based flows)
- **Authorisation Code** flow - similar to Implicit Grant, but instead of getting an access token when redirected to the website, we get an authorisation code instead. This authorisation code can then be traded by the website for an access token, by providing Client Credentials (see below) to the authorisation server (adds an extra layer of security; best for server based applications where you want to be able to continue to refresh the access token)

#### Credential Flows
- **Resource Owner Password Credentials** flow - trades user name and password
- **Client Credentials** flow - each client is issued a client Id and secret, which can be traded for an access token, these can be used:
  - as part of the Authorisation Code flow (above) in order to get an access token
  - to access resources on an API without a particular user connected to that session (incl. creating a user!)

:bulb: We can **combine different flows & grants** in our system in order to grant access to our API, for example when creating a new user:
1. First, use *Client Credentials* flow to get an access token that can be used to create a user on the API
1. Then use *Resource Owner Password Credentials* flow (using the new user's user name and password) to retrieve an access token for that user

![sequence diagram for Implicit Grant redirect flow](/img/oauth-redirect-flow.PNG)

### TO DO
Read "Protocol Flow", "Authorization Grant" and "Endpoint" sections in RFC
- Flows vs Grants?
- Which of these would use a POST to auth server to request a new token?
- Confirm delineation between browser-based and programmatic flows
- Add links to RFC
