<!-- Administration > Configuration > Server configuration > User management and access control > Password policy configuration -->

#### Password policy configuration

Starting with CloverDX version 7.2, access for users in the `clover` domain is secured by a default password policy that requires passwords to be at least **8 characters long** and to **include characters from at least two of the following categories**: *lowercase letters, uppercase letters, digits,* or *special characters*. All newly created passwords will enforce this policy.

By default, passwords do not expire, and there are no restrictions on the minimum number of days between password changes.

If you wish to modify this logic or disable it, you can do so by adding the following properties to the [configuration file](configuration-sources.md#configuration-file-on-specified-location). If any of these properties are modified, the application server needs to be restarted for the changes to take effect.

| Property | Description |
| --- | --- |
| [security.password.policy](list-of-properties.md#lop-security-password-policy) | Enables or disables the password policy. By default, the value is set to `true`, meaning the other properties below are used. If you want to turn off the policy and not set any rules, change the value to `false`. |
| [security.password.policy.min_length](list-of-properties.md#lop-security-password-policy-min-length) | Defines the minimum password lenght. By default, the limit is set to `8`. To remove the limit, set the value to `0`. Maximum password length is `1024` characters. |
| [security.password.policy.min_character_types](list-of-properties.md#lop-security-password-policy-min-character-types) | Defines the minimum number of distinct character types required in a password. Character types include lowercase letters (`a–z`), uppercase letters (`A–Z`), digits (`0–9`), and special characters (e.g., `!@#$%^&*()`). The default value is `2`, meaning the password must contain characters from at least two of these categories. To disable complexity requirements, set the value to `0`. |
| [security.password.policy.min_age](list-of-properties.md#lop-security-password-policy-min-age) | Specifies the minimum number of days a user must wait before they can change their password again. The default value is `0`, meaning the restriction is disabled. |
| [security.password.policy.max_age](list-of-properties.md#lop-security-password-policy-max-age) | Specifies the maximum number of days a password remains valid. After this period, users are required to set a new password upon login. The default value is `0`, meaning the restriction is disabled.  Users with the appropriate permissions can reset this limit for all users in the [User](users.md#reset-passwords-validity) module.  All users can view the number of days remaining until their password expires in their [user menu](user-profile.md). |

See below for an example of the password-related properties in a configuration file:

```properties
## Uncomment and modify the properties below to change the default password configuration.

## Enables or disables password policy.
## Default value is true.
#security.password.policy=true

## Minimum password length.
## Default value is 8.
#security.password.policy.min_length=8

## Minimum number of different character types.
## Default value is 2.
#security.password.policy.min_character_types=2

## Minimum number of days between password changes.
## Default value is 0 (feature is disabled)
#security.password.policy.min_age=0

## Maximum number of days a password remains valid.
## Default value is 0 (feature is disabled)
#security.password.policy.max_age=0
```
