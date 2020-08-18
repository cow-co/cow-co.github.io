---
layout: post
title: BROWNIE TUB, A Generic Web Shell Manager
categories: security
---

BROWNIE TUB is an Electron app that I have developed, to facilitate management of HTTP(S) web shells. This post will quickly go through why the app exists, how the app works, and how to use it.

## Purpose

The idea behind BROWNIE TUB is to allow the user to manage and interact with multiple HTTP(S) web shells from a single interface. This makes it easier to manage large campaigns crossing multiple target domains and organisations. The key design considerations were:

- Ease of use. The application should be useable with minimal guidance. This will also encourage users to run BROWNIE TUB rather than using CLI tools.
- Flexibility. BROWNIE TUB needed to be able to handle any given web shell (within reason) running over HTTP.
- Cross-platform. BROWNIE TUB needed to be able to run on Mac, Linux, and Windows platforms.

With these design requirements in mind, I proceeded to build the application.

## Design

I decided on building BROWNIE TUB using Electron, a framework for building desktop apps with JavaScript. This gave me cross-platform builds pretty easily, which is nice. It also meant it was fairly easy to make a UI that looked decent (I used the React and Material-UI frameworks).

As far as UI design was concerned, I went for a three-column layout: left column for listing web shells, middle column for interaction with the target, and the right-hand column for info on the target. The centre column was further split into an upper section for interacting with the target's filesystem, and a lower section for generic command-line interaction with the target.

For CI/CD, I eventually settled on using Appveyor for Windows builds, and TravisCI for Linux builds. When merging into `master` with a draft release ready in GitHub, the electron-pack package builds the binaries for the chosen platforms, and pushes the binaries onto the GitHub release; I then manually publish the release. I also integrated with Snyk, for checking dependencies for known vulnerabilities.

## How to use BROWNIE TUB

### Creating a Shell Instance

Your first port of call is to create a web shell instance; to do this you first click on the `+` icon on the left-hand column. This will bring up a modal window to allow you to fiddle with the settings for the shell. These settings include:

- the path to the shell
- what sort of HTTP request it takes
- in which parameter of the request to put the command
- whether the data passed to it needs encoding
- how to pass any password it needs

Once these are all set up, you can click the "Submit" button, and your shell is created!

![Create a Shell Instance](../../images/security/brownie-tub/create-shell.png)

### Interacting with the Filesystem

To select a shell with which to interact, click the computer icon next to the shell name on the left-hand column. After some time, during which some requests are sent to the shell, you should see the central panel get populated with the contents of the directory in which the shell lies. From there, you can click on files to view them, or click on directories to enter them.

### Command-Line Interaction

The terminal-looking part at the bottom allows you to enter arbitrary commands (within reason; I wouldn't try anything too complex) to be sent to the target. For example, you could enter a `whoami` command.

## Conclusion

Hopefully you find BROWNIE TUB useful; if you find bugs, or have an idea for improving it, either fork the repo, or raise an issue in GitHub and I'll try to get round to it.
