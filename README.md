# Challenge Part 1: Delete Functionality

After logging into a user or admin account, you will see a redirection link with the heading **"Want to Delete Users"**. Follow these steps:
1. **Click the Link**: Press the link labeled **"Want to Delete Users"**.
2. **Redirection**: You will be redirected to a page specifically designed for user deletion.
3. **Delete User**: On this deletion page, you can enter the username of the person whose account needs to be removed.

This flow allows users or admins to easily access the deletion functionality after logging in, enabling quick removal of user accounts when necessary.

<br>

# Challenge Part 2: Is "This delete user functionality can be done after authentication" a Good Idea?

**Authentication** is essential for identifying who the user is, but it is not sufficient on its own to authorize a sensitive action like deleting a user account. <br><br>
To properly secure such an action, **Authorization** must also be enforced. This ensures that only users with the correct permissions (such as an admin or the account owner) can delete a user.

## Authentication vs. Authorization

### 1. Authentication
- **Definition**: Authentication is the process of verifying the identity of a user. It answers the question, “Who are you?”
- **How It Works**: Usually involves checking credentials like username/password, tokens, or biometrics.
- **Example**: When you log in to a website with your username and password, the system authenticates you to confirm your identity.

### 2. Authorization
- **Definition**: Authorization determines what an authenticated user is allowed to do. It answers the question, “What are you allowed to do?”
- **How It Works**: After authentication, the system checks what resources or actions the user has permission to access or perform.
- **Example**: Even if you're logged in (authenticated), you might not have the permissions to delete another user's account unless you're an admin.

## Why This Distinction Matters for Deleting a User

- **Authentication Alone Is Not Enough**:  
  If an application allows a user to delete an account simply based on being logged in (authenticated), any authenticated user could potentially delete any account, leading to significant security risks.

- **Authorization Must Be Checked**:
  - **Role-Based Access Control (RBAC)**: For instance, only users with the role of 'admin' or the owner of the account should have the ability to delete it.
  - **Fine-Grained Permissions**: Beyond roles, sometimes you need to check specific permissions like `can_delete_user` to ensure the user is truly allowed to perform this action.

## Example Scenario

- **Without Authorization**:
  - Alice logs in (authenticated) and gains access to the system.
  - The system allows any authenticated user to delete a user account.
  - Alice could delete Bob’s account, even though she should not have this permission.

- **With Proper Authorization**:
  - Alice logs in (authenticated).
  - The system checks if Alice has the `admin` role or specific permissions to delete users.
  - If Alice doesn’t have the necessary permissions, the system denies the delete request.

## Visual Representation

To clarify the difference, here’s a simplified flowchart:

```plaintext
                +-------------------+
                |   User Logs In    |
                +-------------------+
                         |
                         v
                +-------------------+
                |   Authentication   |
                |  (Who is the user?)|
                +-------------------+
                         |
                         v
                +-------------------+
                |   Authorization   |
                |  (What can the user|
                |       do?)        |
                +-------------------+
                         |
        +----------------+----------------+
        |                                 |
        v                                 v
+-------------------+           +-------------------+
|   Can Delete User |           | Cannot Delete User|
|     (Proceed)     |           |    (Reject)       |
+-------------------+           +-------------------+

```

## Why Authorization is Crucial
- **Security**: It prevents unauthorized users from performing sensitive actions like deleting accounts.
- **Compliance**: In some industries, authorization is necessary for compliance with laws and regulations.
- **User Trust**: Proper authorization mechanisms help maintain user trust by protecting their data and accounts from unauthorized actions.

## Conclusion
To conclude, while authentication is necessary to identify users, it is insufficient by itself to control access to sensitive actions like deleting user accounts. Incorporating proper authorization ensures that only the right users can perform such actions, enhancing the security and integrity of the system.

This approach protects against unauthorized access and ensures that actions taken within the system are appropriate for the user’s role and permissions.
