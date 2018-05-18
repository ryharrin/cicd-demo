## Manually Create Personal Access tokens

You can manually check them out here https://github.com/settings/tokens and create a new one with "repo" scope. Save it somewhere because you can't get it again (but you can delete and recreate it).

### Automatically Create Personal Access tokens

The next few steps follows the API's instructions at http://developer.github.com/v3/oauth/ under the sections "Non-Web Application Flow" and "Create a new authorization" to become authorized.

Note: This uses Basic Auth once to create an token http://developer.github.com/v3/oauth/#oauth-authorizations-api

Change the below example from "replaceme" to your github account id:

    curl https://api.github.com/authorizations \
    --user "replaceme" \
    --data '{"scopes":["repo"],"note":"Minikube-Jenkins-Demo"}'

If you have Multi-Factor Auth (aka MFA, 2FA, OTP) enabled, you will have to send this header along (change 123456 to your OTP code):

    curl -H "X-GitHub-OTP: 123456" \
    https://api.github.com/authorizations \
    --user "replaceme" \
    --data '{"scopes":["repo"],"note":"Minikube-Jenkins-Demo"}'

This will prompt you for your GitHub password and return your token in the response. It will also create a new Authorized application in your account settings https://github.com/settings/applications

Now that you have the token there are two ways to use the token to make requests that require authentication (replace "OAUTH-TOKEN" with your actual token)

    curl https://api.github.com/gists/starred?access_token=OAUTH-TOKEN
    curl -H "Authorization: token OAUTH-TOKEN" https://api.github.com/gists/starred

List the authorizations you already have (again replace replaceme)

    curl --user "replaceme" https://api.github.com/authorizations