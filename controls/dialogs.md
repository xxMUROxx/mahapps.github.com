---
layout: no-sidebar
title: Dialogs
---

Since the built-in WPF dialogs are unstyleable, we had to create our own implementation. You will find our dialogs within the MahApps.Metro.Controls.Dialogs namespace.

<img src="{{site.baseurl}}/images/dialog.png" style="width: 800px;"/>

All dialogs in MahApps.Metro are called asynchronously.  
If you're on .NET 4.5 you have the luck of using the `async` keyword, 
if you're stuck with .NET 4.0, you'll have to use continuations when using the dialogs.  
This tutorial uses .NET 4.5
If you really want to use `async/await` with .NET 4.0, you can install [Microsoft Async](http://www.nuget.org/packages/microsoft.bcl.async)

### Message dialog

Simple message dialogs can be displayed with the `ShowMessageAsync` method. It is an extension method for `MetroWindow`, so call it from your window class.

```c#
await this.ShowMessageAsync("This is the title", "Some message");
```
    
There are additional optional paramaters for simple buttons, such as `Ok` and `Cancel` and settings for the color theme and animation options.

### Progress dialog

There is a built-in dialog that displays a progress bar at the bottom of the dialog. Call it like this:

```c#
var controller = await this.ShowProgressAsync("Please wait...", "Progress message");
```
    
This method returns a `ProgressDialogController` object that exposes the `SetProgress` method, use it to set the current progress.

A picture of the progress dialog in the demo:

<img src="{{site.baseurl}}/images/progressdialog.png" style="width: 800px;"/>

### Dialog with icon

```c#
await this.ShowMessageAsync("This is a MessageDialog with an icon", "Left you see the ERROR icon", icon: MessageDialogIcon.Error);
```

<img src="{{site.baseurl}}/images/dialog-withIcon.png" style="width: 800px;"/>

The `icon` parameter is of type `object`. This means you can pass any object.

To make it easier to use predefined icons you can use a predefined enumeration `MessageDialogIcon` with the following members:

* None
* Error
* Hand
* Information
* Question
* Warning

> NOTE: For the object passed as `icon` parameter the `DataTemplate` for the type of the icon is used. If there is no `DataTemplate` found the value returned by `ToString()` is displayed.