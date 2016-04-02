---
layout: docs-default
---

# Authorization/Authentication Endpoint

The authorization endpoint can be used to request either access tokens or authorization codes (implicit and authorization code flow). You either use a web browser or a web view to start the process.

### Supported Parameters

See [spec](http://openid.net/specs/openid-connect-core-1_0.html#AuthRequest).

- `client_id` (required)
    - identifier of the client
- `scope` (required)
    - one or more registered scopes
- `redirect_uri` (required)
    - must exactly match one of the allowed redirect URIs for that client
- `response_type` (required)
    - `code` requests an authorization code
    - `token` requests an access token (only resource scopes are allowed)
    - `id_token token` requests an identity token and an access token (both resource and identity scopes are allowed)
- `response_mode` (optional)
    - `form_post` sends the token response as a form post instead of a fragment encoded redirect 
- `state` (recommended)
    - idsrv will echo back the state value on the token response, this is for correlating request and response
- `nonce` (required for identity tokens using implicit flow)
    - idsrv will echo back the nonce value in the identity token, this is for correlating the token to the request)
- `prompt` (optional)
    - `none` no UI will be shown during the request. If this is not possible (e.g. because the user has to sign in or consent) an error is returned
    - `login` the login UI will be shown, even if the user is already signed-in and has a valid session
- `code_challenge` (required when using proof keys - added in v2.5)
    - send the code challenge for proof key flows)
- `code_challenge_method` (optional - default to plain when using proof keys - added in v2.5)
    - `plain` indicates that the challenge is using plain text (not recommended)
    - `S256` indicates the the challenge is hashed with SHA256
- `login_hint` (optional)
    - can be used to pre-fill the username field on the login page
- `ui_locales` (optional)
    - gives a hint about the desired display language of the login UI
- `max_age` (optional)
    - if the user's logon session exceeds the max age (in seconds), the login UI will be shown
- `acr_values` (optional)
    - allows to pass additional authentication related information to the user service - there are also values with special meaning:
        - `idp:name_of_idp` bypasses the login/home realm screen and forwards the user directly to the selected identity provider (if allowed per client configuration)
        - `tenant:name_of_tenant` can be used to pass a tenant name to the user service

### Example
(URL encoding removed for readability)

```
GET /connect/authorize?client_id=client1&scope=openid email api1&response_type=id_token token&redirect_uri=https://myapp/callback&state=abc&nonce=xyz
```
