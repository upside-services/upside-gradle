# Bakery AMI description

The bakery AMI is responsible:

1. creating or downloading an RPM containing a nebula packaged service 
2. Using aminator to create a new AMI from the service base ami and the RPM.
3. Publishing the new service AMI into EC2. 

## Directory Layout

```
[ec2-user@ip-172-31-20-135 pluginconf.d]$ tree /opt/upside/
/opt/upside/
├── bin
│   └── bake-image-from-source
└── deployment

2 directories, 1 file
```

## bake-image-from-source

This script runs the three core tasks for baking. Read the script in this repo for more detail. 

## Required Yum Configuration for bake and service base. 

Any process that can cause yum or apt to launch a process on the target service-base AMI must be disabled. A specific instance of this is the MOTD updater. Any bakery or service AMI must have the MOTD plugin disabled:

```
[ec2-user@ip-172-31-20-135 pluginconf.d]$ pwd
/etc/yum/pluginconf.d
[ec2-user@ip-172-31-20-135 pluginconf.d]$ cat update-motd.conf
[main]
enabled=0
[ec2-user@ip-172-31-20-135 pluginconf.d]$
```

If the MOTD plugin is not disabled bake tasks will fail b/c the target partition will not unmount due to a running process. 
