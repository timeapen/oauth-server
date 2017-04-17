# OAuth Server

Sample project illustrating the use of the [Spring Security OAuth](http://projects.spring.io/spring-security-oauth/) library.

The sample project was created by following the following tutorial [SSO with OAuth2](https://spring.io/blog/2015/02/03/sso-with-oauth2-angular-js-and-spring-security-part-v)

# Details
## Enabling the Auth Server
Spring Security OAuth provides a handy annotion, `@EnableAuthorizationServer` which enables the authorization server in the current Application Context.
The annotation provides two endpoints used for Authorization (`/oauth/authorize`) and Token operations (`/oauth/token`).
## Default User
The application is set up with a default `user` and default `password`.
## Testing the Auth Server
The authorization code token grant can be intiated by visting the `/oauth/authorize` endpoint:

http://localhost:9999/uaa/oauth/authorize?response_type=code&client_id=acme&redirect_uri=http://example.com

In the above example, we are requesting authorization with a response type of `code` for the acme client and redirecting to our client uri.  Typically the redirect uri is used
for directing users to web-server or mobile applications.  In the above example, http://example.com is used for illustrative purposes.

After successful authorization, the user should be redirected to a uri such as:  http://example.com/?code=aMAgDG.

This code can then be exchanged for an access token using the acme client's secret

```
curl acme:acmeSecret@localhost:9999/uaa/oauth/token  -d grant_type=authorization_code -d client_id=acme  -d redirect_uri=http://example.com -d code=aMAgDG
{"access_token":"0a93440f-f56c-4976-80c3-3f6eecc9b930","token_type":"bearer","refresh_token":"15c449a4-c855-4274-812b-8aef9bfdae95","expires_in":43199,"scope":"openid"}
``` 
