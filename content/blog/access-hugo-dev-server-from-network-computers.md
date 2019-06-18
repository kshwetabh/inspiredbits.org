---
title: "Access Hugo Dev Server From Any Device On The Same Network"
date: 2019-06-18T11:47:45+05:30
draft: false
Description: "A quick blog post explaining how to make Hugo server accessible across multiple devices on the same network for testing or development."
Tags: ["hugo", "static website", "static site generator"]
Categories: []
---
So while developing themes or testing different layouts we might need to test the website on multiple devices and different form-factors. Running command **Hugo server** by default is not accessible over the network on different devices like your smartphone or tablet.

In order to access the website from other devices we need to bind the server to its network interface IP (instead of the loopback IP i.e. 127.0.0.1) using the **--bind** argument.
Also pass the **--baseURL** argument to make sure all pages and links work as expected.

<div class="code" style="overflow-x:auto;">
{{< highlight bash >}}
hugo server --bind=<IP-Of-Dev-Machine> --baseURL=http://<IP-Of-Dev-Machine>:<PORT>  
# eg. hugo serve --bind=192.168.1.2 --baseURL=http://192.168.1.2:1313
{{< / highlight >}} 
</div>


This blog post is based on below thread from hugo discourse thread:<br>
https://discourse.gohugo.io/t/hugo-server-only-serves-to-host-computer/5664/7