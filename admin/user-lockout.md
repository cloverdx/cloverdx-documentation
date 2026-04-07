<!-- Administration > Configuration > Server configuration > User management and access control > User lockout configuration -->

#### User lockout configuration

**CloverDX** can lock out users after a set number of unsuccessful login attempts as a way of protecting against brute force attacks on users' credentials.

The lockout occurs only in **CloverDX**. For example, if LDAP user authentication is set up in **CloverDX**, it will not affect the actual LDAP accounts.

Information regarding user lockout is stored in the **USER_ACTION** server log. **CloverDX Server** can be set up to send an email notification when a user account gets locked. However, it is first necessary to set up a connection to an SMTP server in the [E-mail](setup.md#e-mail) tab of the **Setup GUI**.

The lockout feature is enabled by default and it can be turned off and controlled by several properties in the [configuration file](configuration-sources.md#configuration-file-on-specified-location). If any of these properties are modified, the application server needs to be restarted for the changes to take effect.

| Property | Description |
| --- | --- |
| [security.lockout.login.attempts](list-of-properties.md#lop-security-lockout-login-attempts) | Limits the number of login attempts. The next failed login attempt will lock the user’s account. When setting the value, keep in mind that **CloverDX Designer** with several server projects can attempt to log in multiple times.  The recommended value is `5`. Change the value to `0` to disable the feature. |
| [security.lockout.reset.period](list-of-properties.md#lop-security-lockout-reset-period) | Represents the period (in seconds) during which failed login attempts are counted. If no such attempt occurs during this period, the counter of failed login attempts is reset to `0`. This way, users do not have to worry about accidentally locking themselves out of the system after a certain number of failed login attempts over an extended period of time.  The default value is `300` (5 minutes). Change the value to `0` to make the period unlimited. |
| [security.lockout.unlock.period](list-of-properties.md#lop-security-lockout-unlock-period) | Represents the period (in seconds) after which a successful login attempt will release the lock. After this period, users will be able to log in using their credentials again without the need of having their account unlocked by the administrator. This property protects the system against denial of service (DoS) attacks and should be set to a reasonable value to prevent getting locked out of the system for too long, in case the administrator’s account is affected by the attack.  The default value is `300` (5 minutes). Change the value to `0` to make the period unlimited. |
| [security.lockout.notification.email](list-of-properties.md#lop-security-lockout-notification-email) | The property represents a comma-separated list of emails of people who should be notified when a user lockout occurs. This parameter should be set, for example, to an administrators' mail group to make them aware of the situation. The locked out users receive the notification email automatically if an email address is populated in their user profile. Please note that email notifications will be sent only if a SMTP connection is configured under **Configuration > Setup > Email**. |

The recommended default values are set in such a way as to efficiently protect the system against brute force attacks, prevent complete lockout of the administrator’s account and not limit users in their standard usage of **CloverDX Server**.

See below for an example of the lockout-related properties in a configuration file:

```properties
## Uncomment and modify the properties below to change the default user lockout values.

## Number of failed login attempts after which a next failed login attempt will lock the user.
## 0 means feature is switched off
## Default value is 5
#security.lockout.login.attempts=5

## Period of time during which the failed login attempts are counted.
## Default value is 300s (5 min)
#security.lockout.reset.period=300

## Period of time after which a successful login attempt will unlock a previously locked user.
## Default value is 300s (5 min)
#security.lockout.unlock.period=300
```
