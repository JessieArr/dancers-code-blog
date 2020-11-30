---
title: "Versioning NPM Packages in TFS"
author: Shawn
date: "2018-07-25"
categories: [Programming]
tags: [TFS, NPM]
---

So I recently needed to build an NPM package with TFS, and wanted the version number to be updated automatically on build. But after searching, I couldn’t find a good example of how to do it, and TFS seemed to have no tools built in to help.

So I finally I just wrote a simple Powershell script to handle it, and wanted to reproduce it here for the benefit of others who have the same issue:

``` powershell
cd $env:BUILD_SOURCESDIRECTORY
$a = Get-Content 'package.json' -raw | ConvertFrom-Json
$a.version=$a.version.Substring(0, $a.version.LastIndexOf(\\".\\")) + \\".\\" + $env:BUILD_BUILDID
$a | ConvertTo-Json  | set-content 'package.json'
```

Or, if you use GitVersion like we do, after running the GitVersion build step, you will have new environment variables with version numbers in different formats available, which can be used like so:

``` powershell
cd $env:BUILD_SOURCESDIRECTORY
$a = Get-Content 'package.json' -raw | ConvertFrom-Json
$a.version = $env:GITVERSION_NuGetVersion
$a | ConvertTo-Json  | set-content 'package.json'
```

Hope this helps anyone trying to build and publish NPM packages as part of a TFS build!
