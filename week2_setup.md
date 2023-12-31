# The development environment

## I] Introduction

During this semester, we will be working on Visual Studio 2022 & GitHub. These two represent our development environment.

<div align = "center">
<center>
<img src="images/VisualStudioLogo.png" height = "100"/><img src="images/GitHubLogo.png" height = "100"/>

<ins>Images 1.1 & 1.2 : Visual Studio 2022 & GitHub</ins>
</center>
</div>

In this article we'll going to explain how we configured these two tools in the best possible way, and what the advantages of using them are.

<br>

## II] Environment configuration

First we need to install Visual Studio 2022, our text and code writing tool.
<br>
<br>

<div align = "center">
<center>
<img src="images/InstallationVS-1.png" height = "230"/>

<ins>Image 2.1 : Make sure you get the Community version.</ins>
</center>
</div>

<br>

Once the installation is complete, we need to log in with our Microsoft account. 
The application will then ask us to install a number of tools, which can be installed at any time.

<br>

To continue, we need to go to the GitHub website to log in to our account. 

<div align = "center">
<img src="images/SignInGitHub.png" height = "230"/>

<ins>Image 2.2 : We can choose a personal account or one linked to the university.</ins>
</div>

We'll then import the teacher's template, which we'll use as the basis for our portfolio. 
This is also known as a repository.

<div align = "center">
<img src="images/ImporterDepot-1.png" height = "230"/><img src="images/ImporterDepot-2.png" height = "230"/>

<ins>Images 2.3 & 2.4 : We recommend that you make the deposit private.</ins>
</div>

This will allow us to add our personal work over the weeks. There is a section for each week of the course.
For example, the work expected for week 2 must be included in the "week2_setup.md" file.

<br>

<i>But how do I add content to the GitHub repository?</i>

<br>

This is where the simultaneous use of Visual Studio and GitHub comes into its own.

So we're going to go back to Visual Studio to clone the GitHub repository we're working on. 
To do this, we click on "Clone repository..." in the Visual Studio start menu, and select the repository you want.

<div align = "center">
<img src="images/ClonerDepot-1.png" height = "150"/><img src="images/ClonerDepot-2.png" height = "150"/><img src="images/ClonerDepot-3.png" height = "150"/>

<ins>Images 2.5, 2.6 & 2.7 : Follow the steps wisely.</ins>
</div>

Of course, we'll need to log in to our GitHub account from within Visual Studio.

<b>Now we're all set! We can use Visual Studio and GitHub to build the files we want.</b>

<br>

## III] Reflection

<i>How are the features available on Visual Studio & GitHub relevant to the work ahead of us?</i>

<b>1. Teamwork</b>

We have a number of group projects lined up for this semester. 
Using a shared group repository will be very useful. 
Everyone will be able to code on their own on their personal computer, and will be able to collect the code on the common repository. 
This will save a phenomenal amount of time.

<b>2. Get an instant preview of your code</b>

The "Preversion" button in Visual Studio lets you see the result of your code in real time. 
So there's no need to constantly test your code from another application.

<div align = "center">
<img src="images/Preversion-1.png" height = "150"/><img src="images/Preversion-2.png" height = "150"/>

<ins>Images 3.1 & 3.2 : Another great time-saver!</ins>
</div>

<b>3. Double-backup</b>

If the work done on Visual Studio is lost, there will always be a copy on GitHub. And vice versa!
To ensure that your work is synchronised on both platforms, don't forget to push (from VS) or pull (from GitHub) the code after each commit.

<br>

<i>What were the difficulties encountered?</i>

We had trouble linking the GitHub repository of the Visual Studio clone. 

<div align = "center">
<img src="images/Error-1.png" height = "100"/>

<ins>Image 3.3 : Fatal error ! (Source : https://stackoverflow.com/questions/47465644/github-remote-permission-denied)</ins>
</div>

We had actually cloned the wrong repository.
So we restarted the configuration from scratch, and this time everything went smoothly.