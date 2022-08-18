# **Photoprism with MariaDb (Custom Install)**
In order to have photoprism with MariaDB, you will need to install 2 dockers

> Go in App Store and click on Custom Install.
Firstly install MariaDb.
Now you can complete like this..

## MariaDB install for Photoprism

On my server I have nextcloud installed with already a dedicated MariaDB docker. So I installed a second MariaDB docker for Photoprism in order to have the database on the same external hard drive as the one where I already have my photos (it's a personal choice but it seems interesting to me to be able to separate the different databases) So I use different port Host

- **Docker Image**\
`lscr.io/linuxserver/mariadb:latest`
- **App name**\
`MariaDB for Photoprism`
- **Icon URL**\
`https://cdn.jsdelivr.net/gh/IceWhaleTech/AppIcon@main/all/mariadb.png`
- **Web UI**\
`select the appropriate IP:Port`
- **Network**\
`bridge`
- **Ports**\
`Host=3312` => Select the port you want use\
`Container=3306`\
`Protocol=TCP`
- **Volumes**\
`Host= Select the folder you  want use for photoprism database`\
`Container=/config`
- **Environment Variables**\
`PUID=1000`\
`GUID=1000`\
`TZ= Select your Time Zone`\
`MYSQL_ROOT_PASSWORD=ChangeMe`\
`MYSQL_DATABASE=photoprism` => choose a name for database\
`MYSQL_USER=photoprism` => choose a user name for your database\
`MYSQL_PASSWORD=photoprism` => choose a password
- **Memory Limit**\
At maximum
- **CPU Shares**\
`Medium`
- **Restart Policy**\
`unless-stopped`
- **Container Hostname**\
`MariadbPhotoprism`
> **Click Install**

> Now we will do the same to install PhotoPrism in order to use this database we just created.

## PhotoPrism using MariaDB
- **Docker Image**\
`photoprism/photoprism:latest`
- **App name**\
`PhotoPrism`
- **Icon URL**\
`https://cdn.jsdelivr.net/gh/IceWhaleTech/CasaOS-AppStore@main/Apps/PhotoPrism/icon.svg`
- **Web UI**\
`your local IP:2342`
- **Network**\
`bridge`
- **Ports**\
`Host=2342` => Select the port you want use\
`Container=2342`\
`Protocol=TCP`
- **Volumes**\
`Container=/photoprism/storage`  <=>  `Host=Select the folder for PhotoPrism metadata`
Need large space available..\
`Container=/photoprism/originals`  <=>  `Host=Select your main Photo folder (/mnt/My_Photo_Disk)`\
If you have more one main folder you can use this\
`Container=/photoprism/originals/my_other_folder  <=>  Host=/mnt/my_other_folder`
- **Environment Variables**\
`PUID=1000`\
`GUID=1000`\
`TZ= Select your Time Zone`\
`PHOTOPRISM_UPLOAD_NSFW=true`\
`PHOTOPRISM_ADMIN_PASSWORD=casaos`\
`PHOTOPRISM_DATABASE_DRIVER=mysql`\
`PHOTOPRISM_DATABASE_SERVER=your_local_IP:3312` or the port used by your MariaDB for photoprism..\
`MYSQL_DATABASE=photoprism`\
`MYSQL_USER=photoprism`\
`MYSQL_PASSWORD=photoprism`
- **Container Command**\
`/opt/photoprism/bin/photoprism`\
`start`
- **Memory Limit**\
At maximum
- **CPU Shares**\
`Medium`
- **Restart Policy**\
`always`
- **Container Hostname**\
`PhotoPrism`
> **Click Install**

****Enjoy..!****
