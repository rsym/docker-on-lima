# docker-on-lima

### usage

Before using this repository, please install lima and docker client.

 - lima:https://github.com/lima-vm/lima
 - docker client:https://docs.docker.com/engine/install/binaries/#install-client-binaries-on-macos

Clone this repository.
```
git clone https://github.com/rsym/docker-on-lima.git
```

Create instance with `docker-on-lima/docker-vm.yaml`
```
limactl start docker-on-lima/docker-vm.yaml
```

Export `DOCKER_HOST` to connect to docker daemon on lima.
```
export DOCKER_HOST='tcp://127.0.0.1:2375'
```

### example (systemctl on CentOS7)

I confirmed we can use systemctl of CentOS7 with `docker-vm.yaml` simply.

```
$ docker run -itd --privileged --name centos7 centos:7 /sbin/init
cadb0f349dc55d7d398b51398f3a411d8e94fcadf8b4499b9d2fb4050d2602d1

$ docker exec -it centos7 systemctl status
● cadb0f349dc5
    State: starting
     Jobs: 6 queued
   Failed: 0 units
    Since: Tue 2022-01-18 02:56:21 UTC; 10s ago
   CGroup: /docker/cadb0f349dc55d7d398b51398f3a411d8e94fcadf8b4499b9d2fb4050d260
2d1
           ├─1 /sbin/init
           └─system.slice
             ├─systemd-udevd.service
             │ └─32 /usr/lib/systemd/systemd-udevd
             ├─systemd-journald.service
             │ └─21 /usr/lib/systemd/systemd-journald
             ├─dbus.service
             │ └─60 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nop
idfile --systemd-activation
             ├─system-getty.slice
             │ └─getty@tty1.service
             │   └─69 (agetty)
             └─systemd-logind.service
               └─65 /usr/lib/systemd/systemd-logind

```
