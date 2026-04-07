<!-- Administration > Configuration > Server configuration > User management and access control -->

### User management and access control

The **CloverDX Server** has a built-in security module that manages users and groups. [User groups](groups.md) control access permissions to individual server elements and operations the users can perform on the Server, including authenticated calls to Server API functions. A single user can belong to multiple groups.

By default, all users are created in the `clover` domain. You can optionally configure [LDAP](ldap-authentication.md), [Active directory](ldap-authentication.md#active-directory) or [SAML](saml-authentication.md) for user authentication.

You can manage users under **Configuration > Users** and groups under **Configuration > Groups**. Please note that you need the *List users* and *List groups* permissions, respectively, to manager users or user groups.
