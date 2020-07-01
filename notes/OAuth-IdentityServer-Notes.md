# ASP.NET Core and OAuth
*Securing ASP.Net Core applications using OAuth and OpenID Connect*
Notes based on [this Pluralsight course](https://app.pluralsight.com/library/courses/asp-dot-net-core-oauth/table-of-contents) and [IdentityServer Quickstarts](https://identityserver4.readthedocs.io/en/latest/quickstarts/0_overview.html).

## Introduction
Premise: you don't want to have to be passing a user's user name and password around every time you need to call an endpoint to access some user's information.

Common workflow to get around this in .NET Core:
1. Use `[Authorization]` attribute on controllers / actions
1. Have website redirect the request to the authorisation server, where the user will be securely entering their user name + password
1. Be redirected back to our website with a token that can be used to interact with our API


Authentication vs. Authorisation

Why do we need Authorisation servers such as IdentityServer?


What are flows, grants, claims and tokens?


Working with token-based security


