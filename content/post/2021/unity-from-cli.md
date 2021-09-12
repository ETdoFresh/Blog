---
title: Launch Unity Project from Command Line Interface (CLI)
author: ETdoFresh
date: 2021-09-12T00:00:00.000+00:00
excerpt: A quick how-to on setting up Windows or Mac to open a Unity Project
#url: "/url"
featured_image: "/uploads/2021/09/image-20210912180401820.png"
#hide_featured_image: true
tags:
- Unity

---

Sometimes, you want to launch unity from the command line, but typing the entire path to your unity executable can be a pain in the butt! So, here is a quick tip if you want to setup a simple  `unity` command that will open a project in your current directory.

## Windows

### Step 1 - Create a Scripts Folder

In my case, I'm going to create "C:\Users\etgarcia\Documents\My Scripts".

### Step 2 - Create the Script

Now, In my favorite text editor I'll create the script "C:\Users\etgarcia\Documents\My Scripts\unity.cmd".

```
@start "Unity" "C:\Program Files\Unity\Hub\Editor\2020.3.15f2\Editor\Unity.exe" -projectPath .
```

*Note: Please ensure you are pointing to the desired Unity.exe executable*

I use the *@start* command so it immediately brings us back to command line silently (and doesn't wait for Unity window to close). "Unity" is just the title of the new command line window. And then, I use the argument -projectPath . to open the unity project at the current directory.

### Step 3 - Add Script Folder to System Path

Click Start Button, Run, and run command:  
` "C:\Windows\system32\rundll32.exe" sysdm.cpl,EditEnvironmentVariables`

Edit your User Variable Path:

![image-20210912172857431](/uploads/2021/09/image-20210912172857431.png)

Click New. Click Browse. Select your Scripts folder.

![image-20210912173123140](/uploads/2021/09/image-20210912173123140.png)

### Step 4 - Run your Unity Project

![image-20210912173240700](/uploads/2021/09/image-20210912173240700.png)

Now you can simply run your unity projects by navigating to your Unity Project folder and then typing `unity`.

## Mac OS

### Step 1 - Create a Scripts Folder

In my case, I'm going to create /Users/etgarcia/Documents/MyScripts.

### Step 2 - Create the Script

Now, In my favorite text editor I'll create the script /Users/etgarcia/Documents/MyScripts/unity.

```
#!/bin/sh
/Applications/Unity/Hub/Editor/2020.3.15f2/Unity.app/Contents/MacOS/Unity >/dev/null 2>&1 -projectPath . &

```

*Note: Please ensure you are pointing to the desired Unity.exe executable*

I use the `>/dev/null 2>&1 *args* &` parameters so it immediately brings us back to command line (and doesn't wait for Unity window to close). And then, I use the argument -projectPath . to open the unity project at the current directory.

### Step 3 - Add Script Folder to System Path

I add the following line to my `~/.zshrc` file

```
export PATH=$PATH:~/Documents/MyScripts
```

### Step 4 - Run your Unity Project

![image-20210912180401820](/uploads/2021/09/image-20210912180401820.png)

Now you can simply run your unity projects by navigating to your Unity Project folder and then typing `unity`.

