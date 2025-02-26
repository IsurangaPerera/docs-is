# Customizing Authentication Error Messages

The Identity Server has standard error messages for different
authentication errors that are encountered. See [Error Codes and
Descriptions](https://docs.wso2.com/display/IS540/Error+Codes+and+Descriptions)
for more information on the standard error codes and descriptions of
those errors. There are three types of custom errors handled here:

-   Invalid credentials
-   Invalid User
-   Account Lock

!!! note
    
    **Note** : Account Lock errors are returned only when account locking is
    enabled on the server. Refer [User Account Locking and Account
    Disabling](https://docs.wso2.com/display/IS540/User+Account+Locking+and+Account+Disabling)
    document to enable account locking.
    

Do the following to customize these error messages.

Enable the following parameter in the
`         <IS_HOME>/repository/conf/identity/application-authentication.xml        `
file if you need customized error messages.

``` xml
<AuthenticatorConfig name="BasicAuthenticator" enabled="true"> 
    <Parameter name="showAuthFailureReason">true</Parameter>
</AuthenticatorConfig>
```

We send the following query parameters to the authentication endpoint
web application.

-   errorCode
-   failedUsername
-   remainingAttempts

So you can customize the error messages which you show in the pages
like " `         authenticationendpoint/login.jsp        ` " according
to the above query parameters.
