# Claim Management

A claim is a piece of information about a particular subject. It can be
anything that the subject is owned by or associated with, such as name,
group, preferences, etc. A claim provides a single and general notion to
define the identity information related to the subject. Claim-based
identity is a common way for any application to acquire the identity
information. It provides a consistent approach for all applications by
hiding the lower level implementation. Claims are also used in identity
propagation which is the replication of authenticated **identities**,
by packaging the claims into one or more tokens (such as SAML). These
tokens are then issued by an issuer (eg., [security token
service](https://docs.wso2.com/display/IS540/Single+Sign-On+and+Identity+Federation#SingleSign-OnandIdentityFederation-WS-Trust)
(STS) ).

The Claim Management component of [WSO2
Carbon](https://docs.wso2.com/display/Carbon4411/WSO2+Carbon+Documentation)
allows you to map a set of attributes from the underlying user store to
a set of defined claims. The underlying user store can either be an
internal or external JDBC user store, Active Directory or LDAP user
store. You can configure the [primary user store using the user-mgt.xml
file](Configuring-the-Primary-User-Store_103330320.html#ConfiguringthePrimaryUserStore-SettingupthePrimaryUserStore)
. Each claim can be uniquely identified within the claim dialect by the
Claim URI. Claim URIs are independent from the user store and each claim
URI can be mapped into any desired attribute in the user store.
Therefore, at the application level we would know about the claims, but
not the attribute of the user store. An advantage of this is that we do
not need to be concerned about the user store level when we develop an
application as it is hidden by the claim management.

In case of every tenant startup, including the super tenant, the claim
configurations are read directly from the
`          <IS_HOME>/repository/conf/claim-config.xml         ` file. So
claims mapped for SCIM in the super tenant's [management
console](../../setup/getting-started-with-the-management-console) are not seen by
a newly created tenant as the [User
Realm](_Configuring_the_System_Administrator_) is always built using the
configuration found in the **claim-config.xml** file. So the recommended
approach is to do the claim mapping in the
`          <IS_HOME>/repository/conf/claim-config.xml         ` file.
However, you must note that the claim-config.xml file is only read
during the first startup of the server. Any modifications made to this
file after the first startup would not have any effect.

For more information on SCIM, click
[here](https://docs.wso2.com/display/IS540/Identity+Provisioning+and+its+Standards)
.

A set of claims is identified as a dialect. Different dialects represent
the same piece of information with different claim URIs.

With the help of the Claim Management feature, different claims can be
mapped with the attributes of the user that are associated with their
profile.

You can do the following tasks with the Claim Management feature.

-   [Configuring Claim Dialects](_Configuring_Claim_Dialects_)
-   [Configuring Claims](_Configuring_Claims_)
-   [Configuring Claims for a Service
    Provider](_Configuring_Claims_for_a_Service_Provider_)
-   [Configuring Claims for an Identity
    Provider](_Configuring_Claims_for_an_Identity_Provider_)
