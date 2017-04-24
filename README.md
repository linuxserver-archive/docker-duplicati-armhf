[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://www.duplicati.com
[hub]: https://hub.docker.com/r/lsioarmhf/duplicati/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/duplicati
[![](https://images.microbadger.com/badges/version/lsioarmhf/duplicati.svg)](https://microbadger.com/images/lsioarmhf/duplicati "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/duplicati.svg)](http://microbadger.com/images/lsioarmhf/duplicati "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/duplicati.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/duplicati.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-duplicati)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-duplicati/)

[Duplicati][appurl] works with standard protocols like FTP, SSH, WebDAV as well as popular services like Microsoft OneDrive, Amazon Cloud Drive & S3, Google Drive, box.com, Mega, hubiC and many others.

[![duplicati](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/duplicati-icon.png)][appurl]

## Usage

```
docker create \
  --name=duplicati \
  -v <path to data>:/config \
  -v <path to data>:/backups \
  -v <path to data>:/source \
  -e PGID=<gid> -e PUID=<uid>  \
  -p 8200:8200 \
  lsioarmhf/duplicati
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 8200` - the port(s)
* `-v /config` - path for duplicati config files
* `-v /backups` - path to store local backups
* `-v /source` - path to source for files to backup
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on ubuntu xenial with s6 overlay, for shell access whilst the container is running do `docker exec -it duplicati /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

The webui is at `<your ip>:8200` , create backup jobs etc via the webui, for local backups select `/backups` as the destination. For more information see [Duplicati][appurl].

## Info

* Shell access whilst the container is running: `docker exec -it duplicati /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f duplicati`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' duplicati`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/duplicati`

## Versions

+ **24.04.17:** Initial Release.
