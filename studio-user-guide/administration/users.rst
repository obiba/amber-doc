Users
=====

Amber has a local registry of users. The username is the email address. These users can be added manually by the administrator, but it is recommended to let the users register themselves using the **Sign up** procedure. The administrators will receive a notification email informing that a user just registered and that its operational role can be set. The user then does not need the administrator for password recovery or to change its preferences (preferred language for instance).

User roles
----------

There are built-in roles in Amber that grant different privileges:

* ``Guest``, can just login in the application, this is the landing role after a user has signed up,
* ``Interviewer``, has read-only access to Amber studies, forms and case report forms and has the permission to add new case report records,
* ``Manager``, is in charge of managing the content, i.e. the study and form design, and the recorded data extractions,
* ``Administrator``, is the super-user and then has read/write access on everything, from users registry to forms and recorded data.
* ``Inactive``, can't do anything, not even login. This role is convenient when a user is associated to recorded data, to keep track of who did what, even after a collaborator has left the project.

List users
----------

From the list of users the following operations are available:

Add a user
~~~~~~~~~~

Clicking on the Add user button opens a dialog with the user form to be filled in: first/last name, email, institution etc. Special attention must be taken on the email address, which will be used as the login name and will be the recipient of the automatic notifications (for password recovery for instance).

Note that when a user is added, he is automatically added to a group with the domain name, for instance: ``john@example.org`` will be added to the group ``example.org``.

Delete user(s)
~~~~~~~~~~~~~~

There are different ways of deleting a user:

* Either select one or more users in the list and press the Delete selected users button,
* Or press a specific user's Delete action button.

Group users
~~~~~~~~~~~

Grouping users can be convenient when specific permissions are to be granted, for instance when a Case Report Form has limited access.

Users can be put in a group by selecting them in the list and pressing the Group button. A dialog asks for selecting the destination group. Note that the group must exist. Note also that a user can belong to several groups.

Resend verification email
~~~~~~~~~~~~~~~~~~~~~~~~~

User email is the key of user management. It is necessary to have it validated, so that a user can manage its password itself. A verification email consists of sending a message to the user's personal mailbox with a special link that will prove the mailbox is accessible.

Reset password
~~~~~~~~~~~~~~

The Reset password procedure requires the email to have been validated. The password recovery email can be triggered manually by the administrator. The same operation is triggered when the user click on the Forgot password link on the login page and then provides its email.

(De)activate
~~~~~~~~~~~~

When the user's role is not ``Inactive``, pressing the Deactivate icon makes it inactive. Otherwise the Activate icon is visible and the user will be assigned the role ``Guest``.

Single user
-----------

To view the details of a user, select the user's email address or the pencil icon in the list. The user page proposes to update user's information (except its password, use the Reset password procedure for that).
