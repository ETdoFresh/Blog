---
title: Setting up rclone docker on Synology NAS to copy to Google Drive
author: ETdoFresh
type: post
date: 2020-07-20T21:16:00Z
excerpt: I was trying to use Synology's Hyper Backup and it was taking months and still no results. So I gave up and decided to setup an rclone dokcer on my Synology NAS to sync my data to Google Drive. Here are the steps I took...
url: /setting-up-rclone-synology/
featured_image: https://unsplash.com/photos/40XgDxBfYXM/download
hide_featured_image: false
tags:
  - Rclone
  - Docker
  - Synology
  - Google Drive
---

## Introduction
I was trying to use Synology's Hyper Backup and it was taking months and still no results. So I gave up and decided to setup an rclone dokcer on my Synology NAS to sync my data to Google Drive. Here are the steps I took...

## Setup Folders

Create a folder where you will store your rclone/google-drive configuration `ex. /docker/rclone`

![image-20200720150106510](/uploads/2020/07/image-20200720150106510.png)

You will also need to know which folder you want to backup or sync. I'm doing a backup, but similar steps can be taken for sync. `ex. /ETdoFresh/sync`

## Download Docker rclone Image

Download the **rclone/rclone** Docker Image from the Registry

![image-20200720150255696](/uploads/2020/07/image-20200720150255696.png)

## Launch rclone Image

Launching an image creates a docker container. Launch the **rclone/rclone** Image. Click on **Advanced Settings**.

![image-20200720150600488](/uploads/2020/07/image-20200720150600488.png)

Mount the following volumes under the Volume tab.
`ex. ETdoFresh/sync => /sync` `ex. docker/rclone => /config/rclone`

![image-20200720150849411](/uploads/2020/07/image-20200720150849411.png)

Enter config under Command in the Environment Tab.

![image-20200720151333965](/uploads/2020/07/image-20200720151333965.png)

Apply. Next. Apply.

## Running the Configuration

At this point, rclone has already prompted you to enter an option. To verify this, check Logs and then goto Terminal.

![image-20200720151604424](/uploads/2020/07/image-20200720151604424.png)

![image-20200720151705000](/uploads/2020/07/image-20200720151705000.png)

Here is the console output of a succesful transaction:

```bash
2020/07/20 19:44:38 NOTICE: Config file "/config/rclone/rclone.conf" not found - using defaults
No remotes found - make a new one
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n

name> google

Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / 1Fichier
   \ "fichier"
 2 / Alias for an existing remote
   \ "alias"
 3 / Amazon Drive
   \ "amazon cloud drive"
 4 / Amazon S3 Compliant Storage Provider (AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, etc)
   \ "s3"
 5 / Backblaze B2
   \ "b2"
 6 / Box
   \ "box"
 7 / Cache a remote
   \ "cache"
 8 / Citrix Sharefile
   \ "sharefile"
 9 / Dropbox
   \ "dropbox"
10 / Encrypt/Decrypt a remote
   \ "crypt"
11 / FTP Connection
   \ "ftp"
12 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
13 / Google Drive
   \ "drive"
14 / Google Photos
   \ "google photos"
15 / Hubic
   \ "hubic"
16 / In memory object storage system.
   \ "memory"
17 / Jottacloud
   \ "jottacloud"
18 / Koofr
   \ "koofr"
19 / Local Disk
   \ "local"
20 / Mail.ru Cloud
   \ "mailru"
21 / Mega
   \ "mega"
22 / Microsoft Azure Blob Storage
   \ "azureblob"
23 / Microsoft OneDrive
   \ "onedrive"
24 / OpenDrive
   \ "opendrive"
25 / OpenStack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
26 / Pcloud
   \ "pcloud"
27 / Put.io
   \ "putio"
28 / QingCloud Object Storage
   \ "qingstor"
29 / SSH/SFTP Connection
   \ "sftp"
30 / Sugarsync
   \ "sugarsync"
31 / Tardigrade Decentralized Cloud Storage
   \ "tardigrade"
32 / Transparently chunk/split large files
   \ "chunker"
33 / Union merges the contents of several upstream fs
   \ "union"
34 / Webdav
   \ "webdav"
35 / Yandex Disk
   \ "yandex"
36 / http Connection
   \ "http"
37 / premiumize.me
   \ "premiumizeme"
38 / seafile
   \ "seafile"
Storage> 13

** See help for drive backend at: https://rclone.org/drive/ **
Google Application Client Id
Setting your own is recommended.
See https://rclone.org/drive/#making-your-own-client-id for how to create your own.
If you leave this blank, it will use an internal key which is low performance.
Enter a string value. Press Enter for the default ("").
client_id> *Redacted* (Note use Ctrl+A before Ctrl+V to paste in Synology Terminal)
Google Application Client Secret
Setting your own is recommended.
Enter a string value. Press Enter for the default ("").
client_secret> *Redacted* (Note use Ctrl+A before Ctrl+V to paste in Synology Terminal)
Scope that rclone should use when requesting access from drive.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / Full access all files, excluding Application Data Folder.
   \ "drive"
 2 / Read-only access to file metadata and file contents.
   \ "drive.readonly"
   / Access to files created by rclone only.
 3 | These are visible in the drive website.
   | File authorization is revoked when the user deauthorizes the app.
   \ "drive.file"
   / Allows read and write access to the Application Data folder.
 4 | This is not visible in the drive website.
   \ "drive.appfolder"
   / Allows read-only access to file metadata but
 5 | does not allow any access to read or download file content.
   \ "drive.metadata.readonly"
scope> 1

ID of the root folder
Leave blank normally.
Fill in to access "Computers" folders (see docs), or for rclone to use
a non root folder as its starting point.
Note that if this is blank, the first time rclone runs it will fill it
in with the ID of the root folder.
Enter a string value. Press Enter for the default ("").
root_folder_id>

Service Account Credentials JSON file path
Leave blank normally.
Needed only if you want use SA instead of interactive login.
Enter a string value. Press Enter for the default ("").
service_account_file>
Edit advanced config? (y/n)
y) Yes
n) No (default)
y/n> n

Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine
y) Yes (default)
n) No
y/n> n

Please go to the following link: https://accounts.google.com/o/oauth2/auth?access_type=offline&client_id=*Redacted*&redirect_uri=*Redacted*&response_type=code&scope=*Redacted*
Log in and authorize rclone for access
Enter verification code> 4/2QH5SZUSk3_SbufbSLOJhhjb9iHz_hDBrI4BERv3GIkbWAd62jmqq_Y
Configure this as a team drive?
y) Yes
n) No (default)
y/n> n

--------------------
[google]
type = drive
client_id = *Redacted*
client_secret = *Redacted*
scope = drive
token = {"access_token":"*Redacted*","expiry":"*Redacted*"}
--------------------
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y

Current remotes:

Name                 Type
====                 ====
google               drive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q
```

## Verify Configuration

You should now have a **rclone.conf** in your configuration directory.

![image-20200720153531298](/uploads/2020/07/image-20200720153531298.png)

## Change Command Line

Now we will change the command line from configuration to backup. To do this, we **edit** the rclone-rclone1 container to...

Well, I just found out, you can't change the command line :(

So, repeat [Launch rclone Image](Launch rclone Image) using the following instead of config on the last step...

```
copy --update --verbose --transfers 30 --checkers 8 --contimeout 60s --timeout 300s --retries 3 --low-level-retries 10 --stats 1s "/sync" "google:sync"
```

Notice `"google:sync"` which is the `{name-you-gave-during-rclone-config}:{directory-on-google}`

Arguments and their descriptions can be found here:

https://rclone.org/commands/rclone_copy/

## Conclusion

This is the first steps to getting rclone working with your synology. The setup we have is manual. You have to run the docker everytime you want to backup. It will then shutdown when complete.

If you want to automate this, here are some options.

1. Check the Enable auto-restart option in **Edit**
   ![image-20200720155253535](/uploads/2020/07/image-20200720155253535.png)
   The info is particular interesting as it will slow down when there is nothing to sync. It's what I have currently setup, but will probably do Option #2 in the future.
2. Extend the rclone/rclone Docker image to use crond/crontabs to schedule a nightly backup.