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


## Container Creation
Create a new container based on the docker-compose.yml file.

![Container Creation](.attachments/ContainerCreation.png)

Open the `Container Station` and select `Create` from the management menu. Click on the `Create Application` button.

![Create Container Application](.attachments/CreateContainerApplication.png)

Download the docker-compose.yml from the repository and replace the passwords and the dockeruser id/group (see comments in the docker-compose file).

Choose a name for the Container and paste the content of the docker-compose.yml into the YAML section and click on the create button.

## Setup Nextcloud 
After the container is created, open the nextcloud web interface on https://NAS-IP:9443/

![Nextcloud Settings](.attachments/NextcloudSettings.png)

Fill in the credentials for the administrator account.

Select MySQL/MariaDB as database and use the database credentials defined in the docker-compose.yml file.
(MYSQL_USER, MYSQL_PASSWORD, MYSQL_DATABASE, container_name)

Click `Install` to finish the nextcloud setup.


## Update Container

To keep everything up to date the containers and the Nextcloud installation have to be updated.

![Stop Container](.attachments/StopContainer.png)

Stop the running Nextcloud container.

![Edit Container](.attachments/EditContainer.png)

Press on `edit` and copy the docker-compose file of the Nextcloud container (which contains the actual passwords, user Id, user group).

![Delete Container](.attachments/DeleteContainer.png)

Press on `delete` to delete the existing Container (Alle user specific data is stored outside of the container).

![Remove Images](.attachments/RemoveImages.png)

Select `Images` from the management menu and remove the images linuxserver/nextcloud and linuxserver/mariadb.

![Container Creation](.attachments/ContainerCreation.png)

Select `Create` from the management menu. Click on the `Create Application` button.

![Create Container Application](.attachments/CreateContainerApplication.png)

Choose a name for the Container and paste the previously copied docker-compose file into the YAML section and click on the create button.

After the container is created, it uses the latest images.


# Links
- [Access my QNAP NAS using SSH](https://www.qnap.com/en/how-to/knowledge-base/article/how-do-i-access-my-qnap-nas-using-ssh)
- [Setup QNAP user for Docker containers](https://www.linuxserver.io/blog/2017-09-17-how-to-setup-containers-on-qnap)
- [How to use Container Station](https://www.qnap.com/en/how-to/tutorial/article/how-to-use-container-station)
