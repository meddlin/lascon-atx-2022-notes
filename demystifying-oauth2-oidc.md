# Demystifying OAuth2 and OIDC

> LASCON Recorded video: [https://www.youtube.com/watch?v=bhvJ1z-ye6E](https://www.youtube.com/watch?v=bhvJ1z-ye6E)

_It’s all about trust_

We live in a “trust no one” world
- but there needs to be a “trust someone” reality

think of “trust” structures we already use

- child asking a parent for a pice of candy
- Costco checking membershiop
- police officer asking for driver’s license

In software, web accounts

- the username/password with email is pretty common
- but OAuth is becoming more popular and quickly
    - _this is all about “do you trust me?”_

The Basics

- OAuth2
    - authorization code
    - implicit
    - resource owner password credentials
    - client credentials
    - refresh token
- OpenID Connect
- JWT SPEC, JWS SPEC
- Bearer Token
- _There’s a LOT here. You generally don’t want to implement this yourself because to follow the spec correctly is a ridiculous amount of work. And big risk to get it wrong._
- Try to use
    - Okta, etc.
    - some provider of these capabilities

OAuth2

- created about 7-8 years ago
- protocol, authorization, simplicity, specific flows
    - it’s a simple authorization protocol
    - there are multiple implementations
- Authentication == validating identity
- Authorization == validating access (or granting access)
- Access Token—a way to represent authorization
    - _but showing that a user is authorized without exposing any identifying data is tricky_

Authorization Code

- most recommended OAuth workflow
- there is a registration process between App server and Authorization server
    - this is why the “grant code” is protected. because only the App server and authorization server should be aware of it.
- tokens are kept on the server side

Implicit

- this is less secure because tokens are exposed to the browser
- no longer recommended

Resource Owner Password Credentials

Client Credentials

- there are no user credentials exchanged
- this is the most simplistic workflow
- tokens aren’t exposed to browsers because there are no browsers. this is for app-to-app.

Refresh token

- tokens are by design, short-lived
- you want them to be short-lived
- if those tokens expire, how do you get a new one without asking for users to re-authenticate?
- OAuth defines a means for getting a refresh token

_**There are other ways to use OAuth2 workflows, but these 5 are the most commonly used.**_

## OpenID Connect (OIDC)

- OIDC is a _simple identity layer on top of the OAuth2 protocol_
- So, it’s “an extension of the OAuth2 protocol”
    - it’s easy for people to use these interchangeably, but they are _very different things_

- Access token—OAuth2 token
- ID token—OIDC token
    - information about the entity

- The idea of having 2 tokens is so that you can accomplish both, but don’t have to send a person (or entity’s) identifying information to all back-end, supporting servers

## JSON Web Token (JWT)

compact secure and digitally signed JSON object* that can be trusted

- they are cryptographically signed by a token server
- tokens are immutable
- so, if used correctly, only the authorization server can issue the signed token

take a look at jwt.io

- great tool for debugging JWTs

if using JWTs for access and ID tokens

- beware of what goes in the payload section
- does email need to go in an access token? NO. You don’t need someone’s email to say they “are allowed to do something”

## Bearer token

- this is just a single type of access token
- Bearer tokens are incredibly common though—largely most common
- Defines: how you use that token, and how you validate that token