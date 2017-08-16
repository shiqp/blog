---
title: UWP Notes
date: 2017-08-16 15:27:01
categories: UWP
---
# Reference UWP Class Library
For a UWP class library with XAML files, if we want to reference the dll in our UWP projects, we need not only the dll itself but also the `.xr.xml` file and some other files. Because in UWP environment, the resources are no longer embedded in the assembly but are placed next to the dll as content.
The files we need to reference:

* MyClassLibrary (Class Library name) Folder
    * MyClassLibrary.xr.xml
    * MyUserControl.xaml
* MyClassLibrary.dll
* MyClassLibrary.pri (Package Resource Index file)

To get these files, we can check the **Generate library layout** option in the **Build** configuration under the project's **Properties** page.
Copy these files to our UWP projects and add reference to the `MyClassLibrary.dll` file in the Visual Studio. Then, all of them will be added automatically.