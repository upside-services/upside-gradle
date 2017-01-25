# Service Base AMI

The service base AMI provides a template for installation if a service RPM. Generally the base service AMI needs:

0. Daemontools on the system path. 
1. A way to download configuration at bake time. (from s3 for example)
2. A way to start dropwizard with configuration using daemon tools at runtime.

## Daemontools

The service base AMI has an install of https://cr.yp.to/daemontools.html to allow services to log and be restarted when/if they fail. 


## Directory setup

Install base:
```
[ec2-user@ip-172-31-27-115 ~]$ tree /etc/upside/
/etc/upside/
└── service
```

Helper scripts:

```
[ec2-user@ip-172-31-27-115 ~]$ tree /opt/upside/
/opt/upside/
└── bin
    ├── bootstrap-service-config
    └── start-upside-service
```

Daemontools linked to `/usr/local/bin`

```
[ec2-user@ip-172-31-27-115 command]$ cd /usr/local/bin
[ec2-user@ip-172-31-27-115 bin]$ ll
total 0
lrwxrwxrwx 1 root root 15 Sep  4 16:22 envdir -> /command/envdir
lrwxrwxrwx 1 root root 18 Sep  4 16:22 envuidgid -> /command/envuidgid
lrwxrwxrwx 1 root root 15 Sep  4 16:22 fghack -> /command/fghack
lrwxrwxrwx 1 root root 17 Sep  4 16:22 multilog -> /command/multilog
lrwxrwxrwx 1 root root 17 Sep  4 16:22 pgrphack -> /command/pgrphack
lrwxrwxrwx 1 root root 22 Sep  4 16:22 readproctitle -> /command/readproctitle
lrwxrwxrwx 1 root root 16 Sep  4 16:22 setlock -> /command/setlock
lrwxrwxrwx 1 root root 18 Sep  4 16:22 setuidgid -> /command/setuidgid
lrwxrwxrwx 1 root root 18 Sep  4 16:22 softlimit -> /command/softlimit
lrwxrwxrwx 1 root root 18 Sep  4 16:22 supervise -> /command/supervise
lrwxrwxrwx 1 root root 12 Sep  4 16:22 svc -> /command/svc
lrwxrwxrwx 1 root root 13 Sep  4 16:22 svok -> /command/svok
lrwxrwxrwx 1 root root 15 Sep  4 16:22 svscan -> /command/svscan
lrwxrwxrwx 1 root root 19 Sep  4 16:22 svscanboot -> /command/svscanboot
lrwxrwxrwx 1 root root 15 Sep  4 16:22 svstat -> /command/svstat
lrwxrwxrwx 1 root root 15 Sep  4 16:22 tai64n -> /command/tai64n
lrwxrwxrwx 1 root root 20 Sep  4 16:22 tai64nlocal -> /command/tai64nlocal
[ec2
```

## bootstrap-service-config

This script is used to download all the service configuration from s3. It is run when the RPM is installed onto the AMI at bake time. 

## start-upside-service

This script is used to start an upside service via daemontools. It combines daemontools + dropwizard + configuration into a running service daemon. 

