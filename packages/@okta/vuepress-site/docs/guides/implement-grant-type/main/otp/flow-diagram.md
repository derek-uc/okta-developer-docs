### Direct Authentication OTP flow

<div class="full">

![Sequence diagram that displays the back and forth between the resource owner, authorization server, and resource server for Authorization Code flow"](/img/authorization/oauth-otp-grant-flow.png)

</div>

<!-- Source for image. Generated using http://www.plantuml.com/plantuml/uml/

skinparam monochrome true
actor "Resource Owner (User)" as user
participant "Client App (Your App)" as client
participant "Authorization Server (Okta) " as okta

autonumber "<b>#."
client -> user: Prompts user for username and OTP
user -> client: Enters username and then OTP from authenticator app
client -> okta: Sends token request to /token endpoint
okta -> client: Sends access token (and optionally refresh token)

-->

At a high-level, this flow has the following steps:

1. Your client app prompts the user for their username and then an OTP from an authenticator app such as Okta Verify or Google Authenticator.
1. User enters username, opens authenticator app to get the OTP, and then enters the OTP.
1. Your app sends its client ID, the OTP, and the username as a `login_hint` to the Okta authorization server.

    You need to register your app so that Okta can accept the authorization request. See [Set up your app](#set-up-your-app) to register and configure your app with Okta. After registration, your app can make an authorization request to Okta. See [Request for tokens](#request-for-tokens).

1. If the OTP and username are accurate, Okta responds with the requested tokens.