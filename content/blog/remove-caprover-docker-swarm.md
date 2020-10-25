---
title: "Remove Caprover, docker swarm and related artifacts from your linux machine"
date: 2020-10-25T11:47:45+05:30
draft: false
Description: "Getting rid of Caprover and all related artifacts from your server might be tricky. This post is a quick note on how to uninstall and remove all related artifacts."
Tags: ["caprover", "CI and CD"]
Categories: []
---
In my effort to learn CI & CD and after failing badly to install Dokku on my raspberry-pi (they don't provide precompiled binaries yet and I am not an expert in compiling linux binaries, do did not every think about that), I discovered Caprover. Its a nice little PAAS ecosystem that builds upon Docker and provides a handy dashboard (and cli tools as well if you prefer terminal) to configure, customize the application and related setups.
You can explore it further at the official link: https://caprover.com/.

So the story is after configuring a few apps (read as docker images) I realized, my raspberry-pi is struggling. So tried removing Caprover and all its Docker images from the Pi which was not a nice experience. Their docs has no references on how to uninstall it. I agree its all about Docker and Docker images but still, a section on this would have saved me 4 hours of wild hunting on the Internet.

I have, however, installed it on my Linode VPS and am happy with the setup.

1. First delete all containers including its volumes:
<div class="code" style="overflow-x:auto;">
{{< highlight bash >}}
docker rm -vf $(docker ps -a -q)
{{< / highlight >}} 
</div>

2. Then delete all the images
<div class="code" style="overflow-x:auto;">
{{< highlight bash >}}
docker rmi -f $(docker images -a -q)
{{< / highlight >}} 
</div>

3. Next remove all the docker services, exit swarm and prune the system. Also remove /captain from the filesystem.
<div class="code" style="overflow-x:auto;">
{{< highlight bash >}}
docker service rm $(docker service ls -q)
docker swarm leave --force
docker system prune -a
rm -rf /captain
{{< / highlight >}} 
</div>

This post is based on below thread from the caprover github <a href="https://github.com/caprover/caprover/issues/450#issuecomment-505740812" target="_blank">issues thread</a>.
