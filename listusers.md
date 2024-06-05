To list all users on a Linux system, you can use the following methods:

### List All Users
1. **View the /etc/passwd File:**
   The `/etc/passwd` file contains information about user accounts. You can list all users by displaying the contents of this file.
   ```
   cat /etc/passwd
   ```
   This will show a list of all user accounts on the system along with their details. Each line represents a user, with fields separated by colons (`:`). The first field is the username.

2. **Extract Only Usernames:**
   To display only the usernames from the `/etc/passwd` file, you can use the `cut` command:
   ```
   cut -d: -f1 /etc/passwd
   ```

### Filter Human Users
To filter out system users and show only human users (those with a home directory under `/home`), you can use the following command:
```
awk -F: '$3 >= 1000 && $3 < 60000 {print $1}' /etc/passwd
```
This command assumes that user IDs (UIDs) for regular users start at 1000 and end before 60000, which is common on many Linux distributions.

### List Currently Logged-In Users
1. **Using the `who` Command:**
   ```
   who
   ```

2. **Using the `w` Command:**
   ```
   w
   ```

3. **Using the `users` Command:**
   ```
   users
   ```

### Get Detailed User Information
1. **Using the `id` Command for a Specific User:**
   ```
   id <username>
   ```

2. **Using the `getent` Command:**
   The `getent` command can be used to retrieve user account information from databases configured in the `nsswitch.conf` file, including `/etc/passwd`:
   ```
   getent passwd
   ```

These commands should help you list and get detailed information about user accounts on your Linux system.
