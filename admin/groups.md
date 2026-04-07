<!-- Administration > Configuration > Server configuration > User management and access control > Groups -->

#### Groups

CloverDX uses **Role-Based Access Control** (RBAC) to manage permissions for its users. The system allows admin to assign permissions to various roles (called **groups**) and then assign those roles to users (where each user can have multiple roles).

Group is therefore a basic unit which allows admin to define permissions for certain users in a simple way. This approach allows even very complex permissions setup and scales very well to large number of users.

Permissions apply on multiple levels:

- **Sandbox level permissions**: Read/Write/Execute permissions for sandboxes influence access to sandboxes for different users. For details, see [Sandbox content security and permissions](../operations/sandboxes.md#sandbox-content-security-and-permissions).
- **Operation/action permissions**: allow/disallow users to perform certain actions via user interface or API. These are configured as specific permissions assigned to user roles (groups) in the **Groups module**.
- **Data Services permissions***: permissions to launch specific service. For details, see [Data Services](../operations/data-services.md).

To help CloverDX administrators in common scenarios, several groups are created by default.

| Group name | Description |
| --- | --- |
| Administrator | Members of the Administrator group have complete and unrestricted access to **CloverDX Server**. By default, this group includes `clover` system user. |
| All users | This legacy group was intended to include all users; however, the assignment must be maintained by server administrator manually. If you need to handle all users, **use the Everyone group instead**. It is possible to remove users from this group, but it is not recommended. This group is useful mainly to simplify management of permissions to various sandboxes or other features which you may want to make available to all users. |
| Data App users | Members of the *Data App users* group have very limited permissions and can only access Data Apps user interface. |
| Data Manager administrator | Members of the *Data Manager administrator group* have access to Data Manager user interface and administration. Membership in this group does not grant access to **CloverDX Server Console**. |
| Data Manager users | Members of the *Data Manager users* group have access to Data Manager user interface. Membership in this group does not grant access to **CloverDX Server Console**. |
| Everyone | A special group with **auto-managed membership** - it always includes all users, and users cannot be removed from this group. Once installed, the group cannot be deleted or renamed. By default, it has no permissions. It can be used to set the **default permissions** that apply to everyone. |
| Job developer | Members of the *Job developer* group have broad access to **CloverDX Server**. The group is aimed at non-production environments and is designed for users who need to develop and test CloverDX solutions. |
| L1 support | Members of the *L1 support* group have limited access to **CloverDX Server**. The group is aimed at operators who help with basic Server maintenance – monitoring jobs, rerunning them, investigating production issues and so on. |
| L2 support | Members of the *L2 support* group have broad access permissions to **CloverDX Server** and can change many of its settings. The group is targeted at technical operators of the Server who need to solve various issues or who need to deploy new versions of code to the Server. |
| QA engineer | Members of the *QA engineer* group have broad access to **CloverDX Server**. The group is aimed at non-production environments and is designed for users who need to develop and test CloverDX solutions. |
| Read-only users | Members of the *Read-only users* group have very limited permissions. The group applies to users who need to monitor job execution on the Server or who want to see how the jobs work via Job Inspector. |
| Wrangler administrator | Members of the *Wrangler administrator* group have access to Wrangler user interface and can manage the shared workspace. Membership in this group does not grant access to **CloverDX Server Console**. |
| Wrangler | Members of the *Wrangler* group have access to Wrangler user interface and can create and run Wrangler jobs. Membership in this group does not grant access to **CloverDX Server Console**. |

Note that you may not have all these groups available on your system. You may have deleted some of them in the past or some of the groups may not have been created on your system depending on how you installed your CloverDX Server (e.g., certain groups are only created on new instances and are not created during upgrades).

##### Users assignment

Each user can belong to any number of groups, and each group can contain any number of users (i.e., this is typical N:M relationship).
> [!NOTE]
> Any change in user assignment to groups will automatically log out the affected users from all their active sessions and force them to log in again.

##### Group permissions

Group permissions are structured as a tree, where permissions are inherited from the root to leaves.

This means that if a node is enabled (blue dot), all permissions in its subtree are enabled as well. This means that more powerful permissions are nearer to the root of the permissions tree and more granular (less powerful) permissions are the leaves.

As an example, admin user that gets access to everything only needs one permission assigned - the top-level **All** permission that is the root of all permissions in the system. This will automatically assign all child permissions.
> [!NOTE]
> Any change in group permissions will automatically log out all users assigned to the affected group from all their active sessions and force them to log in again.

The following section describes what different permissions mean:

- **All permissions**
  The user with this permission has all available permissions. The **Admin** group has all permissions by default.
  - **Sandboxes - unlimited**
    Allows the user to perform operations on all sandboxes, even if the sandbox accessibility is not specified explicitly.
    This permission does not include the [*Suspend sandbox* permission](groups.md#permission-suspend-sandbox).
    - **Sandboxes**
      Allows the user to work with sandboxes.
      The user can perform operations only on their own sandboxes (where the user is the owner) or on sandboxes to which they have been explicitly granted access, see [Sandboxes](../operations/sandboxes.md).
      - **List sandboxes**
        In the Server web interface, it allows the user to list their sandboxes and sandboxes with **read** permission granted to the user’s group.
        In the Server web interface, this permission is necessary to create, edit, or delete sandboxes.
        Within a sandbox with the **write** access granted, the user can edit or remove files and create or delete directories even without this permission.
      - **Create sandbox**
        Allows the user to create new sandboxes.
        User must have the [*List sandboxes* permission](groups.md#permission-list-sandboxes) to create sandboxes.
      - **Delete sandbox**
        Allows the user to delete sandboxes.
        User must have the [*List sandboxes* permission](groups.md#permission-list-sandboxes) to be able to delete sandboxes.
      - **Edit sandbox**
        Allows the user to edit sandboxes.
        User must have the [*List sandboxes* permission](groups.md#permission-list-sandboxes) to be able to modify the sandbox.
      - **May delete files missing in uploaded ZIP**
        In **Sandbox** ****Upload ZIP**, it allows the user to use a checkbox to delete files missing in the ZIP to be uploaded. If the user does not have this permission, the checkbox to delete mission files in ZIP is not displayed.
        If a sandbox is to be uploaded from a ZIP file in the Server web interface, the user must have the [*List sandboxes* permission](groups.md#permission-list-sandboxes).
  - **Manage libraries**
    Allows the user to add and remove [Libraries](../operations/libraries.md). No special permission is required to use them, all authenticated users may use public subgraphs from installed Libraries in **CloverDX Designer**.
  - **Scheduling**
    Allows the user to manage schedules, see [Scheduling](../operations/scheduling.md).
    - **List schedules - unlimited**
      Allows the user to list all schedules.
      - **List schedules - limited**
        Allows the user to list the schedules of jobs from sandboxes that the user has read access to.
    - **Create schedule**
      Allows the user to create new schedules.
      The user must have the [*List schedules - limited* permission](groups.md#permission-list-schedules-limited) to access the scheduling section to create a new schedule.
    - **Delete schedule**
      Allows the user to delete schedules.
      The user must have the [*List schedules - limited* permission](groups.md#permission-list-schedules-limited) or [*List schedules - unlimited* permission](groups.md#permission-list-schedules-unlimited) to access the scheduling section to delete the schedule.
    - **Edit schedule**
      Allows the user to edit schedules.
      The user must have the [*List schedules - limited* permission](groups.md#permission-list-schedules-limited) or [*List schedules - unlimited* permission](groups.md#permission-list-schedules-unlimited) to access the scheduling section to edit the schedule.
  - **Event listeners**
    Allows the user to manage event listeners, see [Listeners](../operations/listeners.md).
    - **List event listeners**
      Allows the user to list all event listeners.
      - **List jobflow event listeners - unlimited**
        Allows the user to list jobflow event listeners.
        See [Jobflow Event Listeners](../operations/listeners.md#jobflow-event-listeners)
        - **List jobflow event listeners - limited**
          Allows the user to list jobflow event listeners of sandboxes the user can read from.
      - **List graph event listeners - unlimited**
        Allows the user to list all graph event listeners, see [Graph Event Listeners](../operations/listeners.md#graph-event-listeners).
        - **List graph event listeners - limited**
          Allows the user to list graph event listeners from sandboxes the user can read from.
      - **List file event listeners - unlimited**
        Allows the user to list all file event listeners, see [File Event Listeners (remote and local)](../operations/listeners.md#file-event-listeners-remote-and-local).
        - **List file event listeners - limited**
          Allows the user to list all file event listeners.
      - **List JMS event listeners - unlimited**
        Allows the user to list all JMS listeners, see [JMS Message Listeners](../operations/listeners.md#jms-message-listeners).
        - **List JMS event listeners - limited**
          Allows the user to list all JMS listeners.
      - **List Kafka message listeners - unlimited**
        Allows the user to list all Kafka listeners, see [Kafka Message Listeners](../operations/listeners.md#kafka-message-listeners).
        - **List Kafka event listeners - limited**
          Allows the user to list all Kafka listeners.
      - **List universal event listeners - unlimited**
        Allows the user to list all universal event listeners, see [Universal Event Listeners](../operations/listeners.md#universal-event-listeners).
        - **List universal event listeners - limited**
          Allows the user to list all universal event listeners.
          See [Universal Event Listeners](../operations/listeners.md#universal-event-listeners).
      - **List task event listeners - unlimited**
        Allows the user to list all task event listeners, see [Task Failure Listeners](../operations/listeners.md#task-failure-listeners).
        - **List task event listeners - limited**
          Allows the user to list all task event listeners from sandboxes the user can read from.
          See [Task Failure Listeners](../operations/listeners.md#task-failure-listeners).
    - **Create event listener**
      Allows the user to create event listeners.
      User must have permission to list event listeners of particular type to be able create them in the Server Console.
      - **Create jobflow event listener**
        Allows the user to create new Jobflow Event listeners.
        User must have the [*List jobflow event listeners - limited* permission](groups.md#permission-list-of-jobflow-event-listeners-limited) to create jobflow event listeners.
        See [Jobflow Event Listeners](../operations/listeners.md#jobflow-event-listeners).
      - **Create graph event listener**
        Allows the user to create graph event listeners.
        User must have the [*List graph event listeners - limited* permission](groups.md#permission-list-of-graph-event-listeners-limited) to create a graph event listener.
        See [Graph Event Listeners](../operations/listeners.md#graph-event-listeners).
      - **Create file event listener**
        Allows the user to create graph event listeners.
        User must have the [*List file event listeners - limited* permission](groups.md#permission-list-of-file-event-listeners-limited) to create a file event listener.
        See [File Event Listeners (remote and local)](../operations/listeners.md#file-event-listeners-remote-and-local).
      - **Create JMS message listener**
        Allows the user to create JMS event listeners.
        User must have the [*List JMS event listeners - limited* permission](groups.md#permission-list-of-jms-event-listeners-limited) to create a JMS event listener.
        See [JMS Message Listeners](../operations/listeners.md#jms-message-listeners).
      - **Create Kafka message listener**
        Allows the user to create Kafka message listeners.
        User must have the [*List Kafka event listeners - limited* permission](groups.md#permission-list-of-kafka-message-listeners-limited) to create a Kafka message listener.
        See [Kafka Message Listeners](../operations/listeners.md#kafka-message-listeners).
      - **Create universal event listener**
        Allows the user to create universal event listeners.
        User must have the [*List universal event listeners - limited* permission](groups.md#permission-list-of-universal-event-listeners-limited) to create a universal event listener.
        See [Universal Event Listeners](../operations/listeners.md#universal-event-listeners).
      - **Create task event listener**
        Allows the user to create task event listeners.
        User must have the [*List task event listeners - limited* permission](groups.md#permission-list-of-task-event-listeners-limited) to create a task event listener.
        See [Task Failure Listeners](../operations/listeners.md#task-failure-listeners).
    - **Edit event listener**
      Allows the user to edit event listeners.
      User must have permission to list event listeners of the particular type to be able tlo create them.
      - **Edit jobflow event listener**
        Allows the user to edit jobflow event listeners.
        User must have the [*List jobflow event listeners - limited* permission](groups.md#permission-list-of-jobflow-event-listeners-limited) to edit jobflow event listeners.
        See [Jobflow Event Listeners](../operations/listeners.md#jobflow-event-listeners).
      - **Edit graph event listener**
        Allows the user to edit graph event listeners.
        User must have the [*List graph event listeners - limited* permission](groups.md#permission-list-of-graph-event-listeners-limited) to edit graph event listeners.
        See [Graph Event Listeners](../operations/listeners.md#graph-event-listeners).
      - **Edit file event listener**
        Allows the user to edit file event listeners.
        User must have the [*List file event listeners - limited* permission](groups.md#permission-list-of-file-event-listeners-limited) to edit file event listeners.
        See [File Event Listeners (remote and local)](../operations/listeners.md#file-event-listeners-remote-and-local).
      - **Edit JMS message listener**
        Allows the user to edit JMS event listeners.
        User must have the [*List JMS event listeners - limited* permission](groups.md#permission-list-of-jms-event-listeners-limited) to edit JMS event listeners.
        See [JMS Message Listeners](../operations/listeners.md#jms-message-listeners).
      - **Edit Kafka message listener**
        Allows the user to edit Kafka event listeners.
        User must have the [*List Kafka event listeners - limited* permission](groups.md#permission-list-of-kafka-message-listeners-limited) to edit Kafka event listeners.
        See [Kafka Message Listeners](../operations/listeners.md#kafka-message-listeners).
      - **Edit universal event listener**
        Allows the user to edit universal event listeners.
        User must have permission [*List universal event listeners - limited* permission](groups.md#permission-list-of-universal-event-listeners-limited) to edit universal event listeners.
        See [Universal Event Listeners](../operations/listeners.md#universal-event-listeners).
      - **Edit task event listener**
        Allows the user to edit task event listeners.
        User must have permission [*List task event listeners - limited* permission](groups.md#permission-list-of-task-event-listeners-limited) to edit task event listeners.
        See [Task Failure Listeners](../operations/listeners.md#task-failure-listeners).
    - **Delete event listener**
      Allows the user to delete event listeners.
      - **Delete jobflow event listener**
        Allows the user to delete jobflow event listeners.
        User must have the [*List jobflow event listeners - limited* permission](groups.md#permission-list-of-jobflow-event-listeners-limited) to delete jobflow event listeners.
      - **Delete graph event listener**
        Allows the user to delete graph event listeners.
        User must have the [*List graph event listeners - limited* permission](groups.md#permission-list-of-graph-event-listeners-limited) to delete graph event listeners.
        See [Graph Event Listeners](../operations/listeners.md#graph-event-listeners).
      - **Delete file event listener**
        Allows the user to delete file event listeners.
        User must have the [*List file event listeners - limited* permission](groups.md#permission-list-of-file-event-listeners-limited) to delete file event listeners.
        See [File Event Listeners (remote and local)](../operations/listeners.md#file-event-listeners-remote-and-local).
      - **Delete JMS message listener**
        Allows the user to delete JMS message listeners.
        User must have the [*List JMS message listeners - limited* permission](groups.md#permission-list-of-jms-event-listeners-limited) to delete JMS message listeners.
      - **Delete Kafka message listener**
        Allows the user to delete Kafka message listeners.
        User must have the [*List Kafka message listeners - limited* permission](groups.md#permission-list-of-kafka-message-listeners-limited) to delete Kafka message listeners.
      - **Delete universal event listener**
        Allows the user to delete universal event listeners.
        User must have the [*List universal event listeners - limited* permission](groups.md#permission-list-of-universal-event-listeners-limited) to delete universal event listeners.
        See [Universal Event Listeners](../operations/listeners.md#universal-event-listeners).
      - **Delete task event listener**
        Allows the user to delete task event listeners.
        User must have the [*List task event listeners - limited* permission](groups.md#permission-list-of-task-event-listeners-limited) to delete task event listeners.
        See [Task Failure Listeners](../operations/listeners.md#task-failure-listeners).
    - **Manual task execution**
      Allows the user to manually execute a task (send an email, execute a script, etc.) with an immediate effect.
      See [Manual task execution](../operations/manual-task-execution.md).
  - **Unlimited access to execution history**
    Allows the user to perform the same operations as [*Unlimited access to execution history list* permission](groups.md#permission-unlimited-access-to-execution-history-list).
    - **Unlimited access to execution history list**
      Allows the user to view execution history of all jobs.
      - **Limited access to execution history list**
        Allows the user to view execution history of jobs from sandboxes the user can read from. In Designer, this permission is required to be able to view **Execution log** in Designer’s console and execution history in **Execution** tab.
  - **View edge debug data**
    Allows the user to view edge debug data in [Job Inspector - Data Inspector panel in CloverDX Server](../operations/execution-history-main.md#job-inspector) and in the Data Inspector in **CloverDX Designer**.
  - **Data Service**
    Allows the user to access the **Data service** section, see [Data Services](../operations/data-services.md).
    - **List Data Services**
      Allows the user to list data services.
    - **Manage Data Services**
      Allows the user to manage data services.
    - **Execute and access documentation**
      Allows the user to execute and access documentation.
    - **Manage HTTPS connectors**
      Allows the user to manage HTTPS connectors.
- **Data Manager**
  Permissions related to the CloverDX Data Manager. For more information on these permissions, refer [here](../admin/data-manager-administration.md#data-manager-permissions-in-cloverdx-server).
  - **Manage Data Sets in Server Console**
    Allows the user to view and manage data sets within the CloverDX Server Console in **Transactional Data Sets** and **Reference Data Sets** modules without requiring full Data Manager access. Note that users logged into the CloverDX Server Console on [remote servers](data-manager-administration.md#data-manager-configuration) can only view data sets but cannot manage them.
    - **View data sets in Server Console**
      Allows the user to monitor data sets in the CloverDX Server Console in **Transactional Data Sets** and **Reference Data Sets** modules, but it does not allow the user to enable or disable data sets.
  - **Unlimited access to all data sets**
    Allows the user to fully manage [data sets](../user/data-manager-introduction.md#data-set) within the Data Manager or using [the Data Manager API](../operations/part4.md). User can create, modify, and delete any data set, acting as data set administrator.
    - **Create new data sets**
      Allows the user to create new data sets within the Data Manager or using [the Data Manager API](../operations/part4.md).
  - **Access to Data Manager app**
    Gives the user ability to log in to the Data Manager. This permission will require a Data Manager seat (see [Data Manager licensing](data-manager-administration.md#data-manager-licensing) for more details).
- **Tasks history**
  Allows the user to access the **Tasks history** section, see [Tasks](../operations/tasks.md).
- **Monitoring full access**
  Grants the user all its sub-permissions.
  - **Monitoring UI**
    Allows the user to access the Monitoring section. For the [Operations Dashboard](../operations/ops-dashboard.md), the [List dashboards and monitors permission](groups.md#permission-monitoring-list-dashboards-and-monitors) is also required.
    See [Monitoring](../operations/monitoring-intro.md).
  - **Operations dashboard write access**
    Allows the user to create, edit and delete dashboards and monitors.
    - **Mark issues as resolved**
      Allows the user to reset error state on triggers and monitors.
    - **List dashboards and monitors**
      Allows the user to see dashboards and monitors via API and UI.
  - **Suspend**
    Allows the user to suspend the server, a Cluster node, or a sandbox.
    The user must have the [*Monitoring UI* permission](groups.md#permission-monitoring-section) to access the Monitoring section.
    - **Suspend Server**
      Allows the user to suspend or resume the server.
      The user must have the [*Monitoring UI* permission](groups.md#permission-monitoring-section) to access the Monitoring section.
    - **Suspend Cluster node**
      Allows the user to suspend or resume a Cluster node.
      The user must have the [*Monitoring UI* permission](groups.md#permission-monitoring-section) to access the Monitoring section.
    - **Suspend sandbox**
      Allows the user to suspend a sandbox. The user must have [*List sandboxes* permission](groups.md#permission-list-sandboxes) to view the sandboxes to suspend them.
      See also [Sandboxes](../operations/sandboxes.md).
  - **Reset caches**
    Deprecated.
  - **Run jobs - unlimited**
    User must also have the [*List sandboxes* permission](groups.md#permission-list-sandboxes) to be able to run jobs from the Server Console.
    - **Run jobs - limited**
      User must also have the [*List sandboxes* permission](groups.md#permission-list-sandboxes) to be able to run jobs from the Server Console.
- **Configuration**
  Allows the user to access the configuration section.
  - **Users**
    This permission allow user to access the **Users** section and configure user accounts.
    - **List users**
      Allows the user to list users and access to the **Users** administration section (**Configuration** ****Users**)
    - **Change passwords**
      Allows the user to change his password and to change password of another user.
      To see list of users, the user needs the [*List users* permission](groups.md#permission-list-users).
    - **Edit user**
      Allows the user to change group assignment and edit other properties of a user account.
      To see the list of users, the user must have the [*List users_* permission](groups.md#permission-list-users).
      - **Edit own profile and password**
        Allows the user to change their profile (first name, last name, email, and password).
        The user can access their profile in Server Console via the "person" icon in the upper right corner of the page. See [user profile](user-profile.md) for more information.
    - **Unlock user**
      Allows the user to unlock a user.
      The user must have the [*List users* permission](groups.md#permission-list-users) to list available users.
    - **Delete user**
      Allows the user to disable a user.
      The user must have the [*List users* permission](groups.md#permission-list-users) to list available users.
    - **Create user**
      Allows the user to create a new user.
      User must also have the [*List users* permission](groups.md#permission-list-users) to be able to create new users in Server Console.
    - **Assign groups**
      Allows the user to assign users to groups.
      The user must have the [*Edit user* permission](groups.md#permission-edit-user) to be able to change the assignment of users to groups.
      User must have the [*List users_* permission](groups.md#permission-list-users) to be able to create other users in Server Console.
  - **Groups**
    Allows the user to manage groups: list groups, create groups, delete groups, edit groups, assign users to groups, and change group permissions.
    - **List groups**
      Allows the user to list groups. This permission is necessary for use of other options from the **Groups** group.
    - **Create group**
      Allows the user to create a new user group.
      User must have the [*List groups* permission](groups.md#permission-list-groups) to create new groups in Server Console.
    - **Delete group**
      Allows the user to delete a user group.
      Only empty groups can be deleted. User must have the [*List groups* permission](groups.md#permission-list-groups) to be able to delete groups in Server Console.
    - **Edit group**
      This permission allow user to edit user groups.
      This permission does not include **User assignment** and **Assign permissions**.
      TO edit groups via Server Console, the user must have the [*List groups* permission](groups.md#permission-list-groups).
    - **Assign users**
      Allows the user to assign users to groups.
      The user also needs [*Edit group* permission](groups.md#permission-edit-group) and [*List groups* permission](groups.md#permission-list-groups) to change user assignment via Server Console.
    - **Assign permissions**
      Allows the user to configure group **Permissions**.
      The user also needs have the [*Edit group* permission](groups.md#permission-edit-group) and [*List groups* permission](groups.md#permission-list-groups) to change user permissions via Server Console.
  - **Secure parameters administration**
    - **Secure parameters**
      Allows the user to change the value of a secure parameter.
      The user can use secure parameters in graphs even without this permission.
  - **Unlimited access to Secret Managers**
    Allows the user to create, edit and delete [Secret Managers](secret-managers.md).
  - **CloverDX/System info sections**
    Allows the user to view **System Info** and **CloverDX Info** sections.
  - **CloverDX Server properties**
    Allows the user to view **Server Properties** tab in **CloverDX Info** section.
    The user must have the [*CloverDX/System info sections* permission](groups.md#permission-cloverdx-system-info-sections) to access **CloverDX Info** section.
  - **Reload license**
    Allows the user to view and reload the Server license.
    The user must have the [*CloverDX/System info sections* permission](groups.md#permission-cloverdx-system-info-sections) to access the **Configuration** section.
  - **Upload license**
    Allows the user to update the Server license.
    The user must have the [*CloverDX/System info sections* permission](groups.md#permission-cloverdx-system-info-sections) to access the **Configuration** section.
    See [Activation](production-server.md#activation).
  - **Server configuration management**
    Allows the user to import and export the server configuration.
    See [Server Configuration Migration](server-config.md).
    - **Export Server configuration**
      Allows the user to export the server configuration.
      See [Server Configuration Export](server-config.md#server-configuration-export).
    - **Import Server configuration**
      Allows the user to import the server configuration.
      See [Server Configuration Import](server-config.md#server-configuration-import).
  - **Temp space management**
    Allows the user to access **Temp Space Management** section.
    See [Temp Space Management](tempspace.md).
  - **Server setup**
    Allows the user to access the server setup.
    See [Setup](setup.md).
  - **Heap memory dump**
    Allows the user to create a **Thread dump** and a **Heap Memory Dump**.
    See [Diagnostics](../operations/diagnostics.md#).

- **Open Server Console**
  Allows the user to log into the **Server Console**.
- **Wrangler**
  Main permission for the Wrangler. Users with this permission will have full access to Wrangler user interface and will be able to manage Wrangler workspaces.
  - **Access to Wrangler app**
    Allows user to login to **Wrangler** app.
    Users with this permission will require Wrangler seat (the seat will be automatically "consumed" once they login to Wrangler for the first time). Users with this permission cannot manage shared workspace in Wrangler, but they can access it provided Wrangler workspace admin gave them permission to access the workspace.
  - **Shared workspace administrator**
    Allows user to manage permission of Wrangler’s shared workspace via **Wrangler** app.
    Users with this permission also require [*Access to Wrangler app* permission](groups.md#permission-access-wrangler) and therefore will consume one Wrangler seat once they login at least once.
