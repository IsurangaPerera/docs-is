# Configuring the Realm

User management functionality is provided by default in all WSO2
Carbon-based products and is configured in the
`         user-mgt.xml        ` file found in the
`         <PRODUCT_HOME>/repository/conf/        ` directory. The
following documentation explains the configurations that should be done
in WSO2 products in order to set up the User Management module.

The complete functionality and contents of the User Management module is
called a **user** **realm**. The realm includes the user management
classes, configurations and repositories that store information.
Therefore, configuring the User Management functionality in a WSO2
product involves setting up the relevant repositories and updating the
relevant configuration files.

The following diagram illustrates the required configurations and
repositories:  
![]( ../../assets/img/45941259/46202975.png)

For more information on Configuring master-datasources.xml, click
[here](https://docs.wso2.com/display/Carbon440/Configuring+master-datasources.xml)
.

See the following topics for instructions on setting up user stores:

-   [Configuring the Authorization
    Manager](_Configuring_the_Authorization_Manager_)
-   [Configuring the System
    Administrator](_Configuring_the_System_Administrator_)
-   [Configuring User Stores](_Configuring_User_Stores_)
