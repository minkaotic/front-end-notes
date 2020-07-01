# ASP.NET Core and OAuth
*Securing ASP.Net Core applications using OAuth and OpenID Connect*

Notes based on [this Pluralsight course](https://app.pluralsight.com/library/courses/asp-dot-net-core-oauth/table-of-contents) and [IdentityServer Quickstarts](https://identityserver4.readthedocs.io/en/latest/quickstarts/0_overview.html).

## Introduction
:bulb: **Premise:** you don't want to have to be passing a user's user name and password around every time you need to call an endpoint to access some user's information.

**Common workflow to get around this in .NET Core:**
1. Use `[Authorization]` attribute on controllers / actions
1. Have website redirect the request to the authorisation server, where the user will be securely entering their user name + password
1. Be redirected back to our website with a token that can be used to interact with our API
1. (If a token is compromised, communicate this back to the authorisation server)

**Benefits of token-based security**
- prevents the need to repeatedly share a user's password around, incl. to 3rd parties
- instead, user securely authenticates themselves once, receiving a token that proves that they are verifiably themselves
- that token is then used to access any resources
- if a token gets lost or unduely exposed, we can simply revoke access for it
- tokens may be short-lived to minimise security risks

![token based security overview](/img/token-based-security-overview.PNG)

> :fire: **Treat tokens like passwords**, as they do provide unrestricted access to a user's data, while they are valid


Authentication vs. Authorisation

Why do we need Authorisation servers such as IdentityServer?


What are flows, grants, claims and tokens?





