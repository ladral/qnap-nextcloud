# qnap-nextcloud

## Requirements

- Latest QNAP Firmware Installed.
- Container Station Installed & Updated.
- Understand how to access your QNAP via SSH.  [Access my QNAP NAS using SSH](https://www.qnap.com/en/how-to/knowledge-base/article/how-do-i-access-my-qnap-nas-using-ssh)

## User Creation
Create a new user which will be used for docker containers, so that they are not running as root (primarily for security reasons). 
Go to "Users" from the main screen QTS, select "Create User" and create a user called "dockeruser"

![User Creation](.attachments/UserCreation.png)


## Folder Creation
Create a new shared folder that we will keep all docker appdata in. Load up "File Station" and create a new share by clicking on the `+` next to the Data Volume.

![Folder Creation](.attachments/FolderCreation.png)

Call the folder `Docker` and give full read/write access to this folder to the newly created `dockeruser`. Everything else can be left as default.

![Folder Privileges](.attachments/FolderPrivileges.png)

Once the `Docker` folder is created, create another folder called `nextcloud` within the `Docker` folder.


## Get User IDs
Now the UID/GID of the user `dockeruser` need to be figured out. Use your favourite method to ssh into the QNAP NAS and run the following command:

```console
id <username>
```

Replace <username> with the user you created earlier (dockeruser). The result of the command should look like this:

Result:
```console
[~] # id dockeruser
uid=500(dockeruser) gid=100(everyone) groups=100(everyone)
[~] #
```

Note the UID and the GID and replace the ID's in the docker-compose.yml file (see comments in the docker-compose file).


# Links
- [Access my QNAP NAS using SSH](https://www.qnap.com/en/how-to/knowledge-base/article/how-do-i-access-my-qnap-nas-using-ssh)
- [Setup QNAP user for Docker containers](https://www.linuxserver.io/blog/2017-09-17-how-to-setup-containers-on-qnap)

