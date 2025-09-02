![[../assets/20250902153359.png]]
```
[root@localhost kana]# dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
Adding repo from: https://download.docker.com/linux/rhel/docker-ce.repo
```
![[../assets/20250902154541.png]]
```
[root@localhost kana]# systemctl start docker
[root@localhost kana]# systemctl enable docker
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /usr/lib/systemd/system/docker.service.
[root@localhost kana]# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2025-09-02 15:47:11 KST; 29s ago
     Docs: https://docs.docker.com
 Main PID: 277795 (dockerd)
    Tasks: 8
   Memory: 98.7M
   CGroup: /system.slice/docker.service
           └─277795 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

```

```
[root@localhost kana]# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete 
Digest: sha256:a0dfb02aac212703bfcb339d77d47ec32c8706ff250850ecc0e19c8737b18567
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

```