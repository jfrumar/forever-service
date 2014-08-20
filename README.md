forever-service
===============

Make provisioning node script as a service simple. 

While node is great technology, and targetted towards server development. It is surprising to find that there is no standard tool to provision script as a service. Forever kind of tools comes close but they only daemonize the process and not provision as service; which can be automatically started. To make matter worse, each OS and Linux distro has its own unique way to provisioning the services correctly.

Goals
-----
1. Make an universal service installer across various Linux distros and other OS.
2. Configure other useful things such as Logrotation scripts, port monitoring scripts etc.

Platforms supported
-------------------
* Amazon Linux
* more to come..

Prerequsite
-----------
forever must be installed globally using 

```npm install -g forever```

Install
-------
```npm install -g forever-service```

Usage
-----
```
$ forever-service --help

forever-service version 0.x.x


  Usage: forever-service [options] [command]

  Commands:

    install [options] [service]
       Install node script (defaults to app.js in current directory) as service via forever
    
    
    
    delete [service]
       Delete all provisioned files for the service, will stop service if running before delete
    

  Options:

    -h, --help     output usage information
    -V, --version  output the version number
```

Install new service
-------------------
```
$ forever-service install --help

forever-service version 0.x.x


  Usage: install [options] [service]

  Options:

    -h, --help                         output usage information
    -s, --script [script]              Script to run as service e.g. app.js, defaults to app.js
                                       
    --minUptime [value]                Minimum uptime (millis) for a script to not be considered "spinning", default 5000
                                       
    --spinSleepTime [value]            Time to wait (millis) between launches of a spinning script., default 2000
                                       
    --noGracefulShutdown               Disable graceful shutdown
                                       
    -t --forceKillWaitTime [waittime]  Time to wait in milliseconds before force killing; after failed graceful stop
                                       defaults to 5000 ms, after which entire process tree is forcibly terminated
                                       
    -f --foreverOptions " [options]"   Extra command line options for forever
                                       e.g. -f " --watchDirectory /your/watch/directory -w -c /custom/cli" etc..
                                       NOTE: a mandatory space is required after double quotes, if begining with -
                                       
    --start                            Start service after provisioning
                                       
    --nologroate                       Do not generate logrotate script
                                       
    --logrotateFrequency [frequency]   Frequency of logrotation
                                       valid values are daily, weekly, monthly, "size 100k" etc, default daily
                                       
    --logrotateMax [value]             Maximm logrotated files to retain, default 10 (logrotate parameter)
                                       
    --logrotateCompress                Enable compression for logrotate

```

Delete service
--------------
```
$ forever-service delete --help

forever-service version 0.x.x


  Usage: delete [options] [service]

  Options:

    -h, --help  output usage information
```
Examples
--------
1. Provision a service 'test' with app.js script in current directory

```
$ forever-service install test
```


2. Provision a service 'test' with main.js script in current directory

```
$ forever-service install test --script main.js
```

3. Custom options for forever 

```
$ forever-service install test -f " -watchDirectory /your/watch/directoyr -w"
```

Roadmap
-------
Support other Linux distros, OSX, Windows 
Contirbutions are welcome, please send me pull requests
