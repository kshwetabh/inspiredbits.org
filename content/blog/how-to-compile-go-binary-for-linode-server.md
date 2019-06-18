---
title: "How to compile Go program binary to run on your Linux box or Linode Server"
date: 2019-06-06T17:04:51+05:30
Description: "TL;DR Follow these simple steps to compile a binary for running on Linode VPS machines."
Tags: ["linode", "golang", "linux", "binary"]
Categories: []

---

# How to compile Go program binary for running on your Linode Server

I use Linode VPS for running my experiments and hosting websites. My primary development machine is Windows 10 and very frequently I need to cross-compile go program binaries to Linux OS that is the primary OS on Linode servers. Instead of doing a google search each time I need to do the cross-compilation, I thought to document the steps here so that I can refer it whenever I need.

Here are the steps that needs to be executed on the Windows Command Prompt:

<div class="code">
{{< highlight bash >}}
set GOARCH=amd64    #Target Processor architecture [amd64, 386, arm]
set GOOS=linux      #Target Operating System where program will run [linux, darwin, windows] 
go build -v         #Start build in verbose mode
{{< / highlight >}} 
</div>
Flag -v is verbose mode and compiler prints the names of the packages as they are compiled

You can lookup other flags like -a, etc. on [golang.org](https://golang.org/cmd/go/) website.

We can do better. We can make use of Windows batch script so that we won't have to type those individual commands each time on the console.
