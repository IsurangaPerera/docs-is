# Setting Up ReCaptcha

[reCaptcha](https://developers.google.com/recaptcha/) is a free service
provided by Google that can be used for protection against spam or other
forms of internet abuse by verifying whether a user is a human or a
robot. It comes in the form of a widget. The following section guides
you through setting up reCaptcha with the WSO2 Identity Server and how
to use it in different scenarios.

-   [How it works](#SettingUpReCaptcha-Howitworks)
-   [Configuring reCaptcha API
    keys](#SettingUpReCaptcha-ConfiguringreCaptchaAPIkeys)

### How it works

First, you will need to register and create an API key pair for the
required domain. The key pair consists of a site key and secret. The
site key is what is used when a reCaptcha widget is displayed on a page.
After verification, a new parameter called
`         g-recaptcha-response        ` appears on the form which the
user submits. From the server side, you can verify the submitted captcha
response by calling the Google API with the secret key.

Follow the steps provided below to configure this.

### Configuring reCaptcha API keys

1.  Go to <https://www.google.com/recaptcha/admin> .

2.  You will see the following window. Fill in the fields to register
    your identity server domain and click **Register**. The following
    are sample values:
    -   **Label:** WSO2 Identity Server
    -   Select the reCAPTCHA V2 or Invisible reCAPTCHA option.
    -   **Domains:** is.wso2.com  

    ![]( ../../assets/img/103330586/103330587.png) 
3.  Take note of the site key and secret that you receive.
    ![]( ../../assets/img/103330586/103330588.png) 
4.  Open the c `            aptcha-config.properties           ` file
    located in the
    `            <IS_HOME>/repository/conf/identity/           `
    directory and configure the following properties.

    ``` java
    # Google reCAPTCHA settings

    # Enable Google reCAPTCHA
    recaptcha.enabled=true

    # reCaptcha API URL
    recaptcha.api.url=https://www.google.com/recaptcha/api.js

    # reCaptcha verification URL
    recaptcha.verify.url=https://www.google.com/recaptcha/api/siteverify

    # reCaptcha site key
    recaptcha.site.key=6Lc8THgUAAAAAPekxT991FGFXRrsiPCMNv5PwZHB

    # reCaptcha secret key
    recaptcha.secret.key=6Lc8THgUAAAAAEu83iOwSin_CSt6gqe97aa7EGFd

    # reCaptcha failed redirect URL
    #recaptcha.failed.redirect.urls=
    ```

    !!! note
    
        If you have additional authorization endpoints, you need to include
        the [login.do](http://login.do) URL paths of these endpoints in the
        **captcha-config.properties** file in the following pattern. Here,
        url\_path is the URL without the host parameters.
    
        ``` java
            recaptcha.failed.redirect.urls=url1_path,url2_path
        ```
    
        Below is an example of how to include the URL paths of additional
        authorization end points.
    
        ``` java
            recaptcha.failed.redirect.urls=/authenticationendpointone/login.do,/authenticationendpointtwo/login.do
        ```
    

5.  Restart the WSO2 IS server.

You have successfully set up reCaptcha for your site. You can now
configure reCaptcha with any of the following:

-   [Configuring Google reCaptcha for single
    sign-on](_Configuring_reCaptcha_for_Single_Sign_On_)
-   [Configuring Google reCaptcha for self
    registration](_Configuring_reCaptcha_for_Self_Registration_)
-   [Configuring Google reCaptcha for security-question based password
    recovery](_Configuring_Google_reCaptcha_for_Security-Question_Based_Password_Recovery_)
    (password recovery with secret questions)
