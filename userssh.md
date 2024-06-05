### Enabling SSH Access for a User on a Linux System

This document outlines the steps to enable SSH access for a user on a Linux system.

#### 1. Change the User Password
To set or change the password for the user, use the following command:
```sh
sudo passwd <username>
```
Replace `<username>` with the actual username. You will be prompted to enter and confirm the new password.

#### 2. Ensure SSH Service is Running
Verify that the SSH service is running on your system:
```sh
sudo systemctl status ssh
```
If the service is not running, start it with:
```sh
sudo systemctl start ssh
```

#### 3. Check SSH Configuration
Edit the SSH configuration file to ensure the user is allowed to log in via SSH:
```sh
sudo nano /etc/ssh/sshd_config
```

Look for the `AllowUsers` directive. If it is present, add the new user to this directive. For example, if the line currently reads:
```sh
AllowUsers existing_user
```
Modify it to include the new user:
```sh
AllowUsers existing_user new_user
```
Replace `existing_user` and `new_user` with the actual usernames.

If the `AllowUsers` directive is not present, you can add it at the end of the file:
```sh
AllowUsers new_user
```
This allows the specified users to log in via SSH.

#### 4. Save and Close the Configuration File
Save the changes and close the text editor. In `nano`, you can do this by pressing `Ctrl+X`, then `Y` to confirm changes, and `Enter` to save.

#### 5. Restart the SSH Service
Apply the changes by restarting the SSH service:
```sh
sudo systemctl restart ssh
```

#### 6. Ensure User Has a Home Directory and Shell
Verify that the user has a valid home directory and shell. Check the `/etc/passwd` file:
```sh
grep <username> /etc/passwd
```
The output should look similar to:
```
username:x:1001:1001:User Name,,,:/home/username:/bin/bash
```
Ensure that `/home/username` exists and `/bin/bash` (or another valid shell) is set.

#### 7. Test SSH Login
Test the SSH login for the user from another machine:
```sh
ssh <username>@<server_ip>
```
Replace `<username>` with the actual username and `<server_ip>` with the server's IP address. Enter the password when prompted to ensure the user can log in successfully.

