---
title: Creating a Custom Unity Package
author: ETdoFresh
date: 2021-09-07T00:00:00.000+00:00
excerpt: A tutorial on creating custom Unity Packages and why
#url: "/url"
featured_image: "/uploads/2021/09/image-20210907104059057.png"
#hide_featured_image: true
tags:
- Unity
- Project
- Unity-Package

---

# Creating a Custom Unity Package

Here is my github repository with more concise instructions...  
https://github.com/ETdoFresh/UnityPackageTemplateMinimum

I know there are already tutorials on how to do this, but sometimes, a different perspective can be helpful to other users out there! And writing down the instructions in my own words helps me a ton! So, here we go!

## What's up?

![image-20210907092159001](/uploads/2021/09/image-20210907092159001.png)

So, if you are unfamilar, starting a few years ago, there is a new section in Unity's Project Window called **Packages**.

![image-20210907100132077](/uploads/2021/09/image-20210907100132077.png)

These packages are driven via a file located in **{Project Folder}/Packages/manifest.json**.

There are a few things to consider when making your own custom packages, but I'll go over the two most important things when creating your own custom packages (in my opinion):

- package.json
- Assembly Definitions

## Create Package Folder

First, you will have to create a folder with package.json file inside of it. If you like, I have included a convenient zip file which has package.json and README.md files. Just unzip into your  **{Project Folder}/Packages/** directory.

[UnityPackageTemplateMinimum.zip](/uploads/2021/09/UnityPackageTemplateMinimum.zip) [2,188 bytes]

## Edit package.json

Ensure you edit the information to your liking. The "name" is using the naming convention as shown in the [Unity Manual - Naming your Package](https://docs.unity3d.com/Manual/cus-naming.html). Opening package.json in Unity (via Inspector GUI) may be more informative/intuitive.

```json
{
  "name": "com.etdofresh_unity.unity-package-template-min",
  "version": "1.0.0",
  "displayName": "Unity Package Template Minimum by ET",
  "description": "A minimum empty package template for Unity Package Manager.",
  "type": "library"
}
```

## Assembly Definitions

![image-20210907101804338](/uploads/2021/09/image-20210907101804338.png)One of the nice benefits of packages is that it can be reused in various projects. It is best practice to ensure you include an Assembly Definition in your package. This will create a seperate dll file for the package. I think the main benefit of this is that when compiling the rest of your project, these files won't have to recompiled as they are already nicely packaged in their own dll file. This assembly definition should use the same naming convention as above. More details can be found in the [Unity Manual - Assembly Definitions](https://docs.unity3d.com/Manual/ScriptCompilationAssemblyDefinitionFiles.html).

## Installing Packages into Other Projects

So, now that you have your package all wrapped up tied up with a nice little bow, what next? Use it! 

### Method 1: Copy Package Locally

The simplest way to use it is to copy the folder over into another Unity Project's Packages folder. For me, this is not the recommended way to do it for various reasons [listed later as pros of the next method]... however it is the quickest method.

### Method 2: Copy Package via git

The more robust way to use this package is to upload to a git repository. In my case, I'm using github. Once I'm satisfied, I'm also tagging my commit with a [semantic version number](https://semver.org/). Hence, I end up with a repository link [with version number] like the following:

https://github.com/ETdoFresh/UnityPackageTemplateMinimum.git#1.0.0

*Note - Please make sure you have meta files and that they don't conflict with possible existing meta files. For example, one of the main problems I run into is sometimes copying over SampleScene.meta which exists in all new projects.*

![image-20210907103147471](/uploads/2021/09/image-20210907103147471.png)

Then to install the package, you just have to paste the link in Package Manager as shown above.

Alternatively, you could paste a line similar to the one below in your **./Packages/manifest.json** inside the "dependencies" section.

```
    "com.etdofresh_unity.unity-package-template-min": "https://github.com/ETdoFresh/UnityPackageTemplateMinimum.git#1.0.0",
```

### Benefits of Method 2

1. I think the coolest thing about using packages via git repository is the custom package contents are not directly stored in your core Unity project git repository. It is simply referenced by your project. [and it is downloaded in your Library folder when project is first opened]
2. It allows for versioning, so your project is always grabbing the correct files.
3. (For Both) Having a seperate dll/code that doesn't have to be recompiled when changes are made in your core project code.

