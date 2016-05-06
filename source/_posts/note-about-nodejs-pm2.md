---
title: NodeJS入门-pm2
tags:
  - nodejs
  - javascript
categories:
  - NodeJS
date: 2016-05-06 10:27:38
---


[PM2](http://pm2.keymetrics.io/),即P(rocess) M(anager) 2，是一款可用于生产环境的NodeJs进程管理工具，提供了负载均衡等高级功能。
<!-- more -->

## 快速开始 ##
``` bash
$ npm install pm2 -g
$ pm2 start app.js
```

## 命令概览 ##
``` bash
$ pm2 -h
Usage: pm2 [cmd] app
  Commands:

    start [options] <file|json|stdin|app_name|pm_id...>                  start and daemonize an app
    deploy <file|environment>                                            deploy your json
    startOrRestart <json>                                                start or restart JSON file
    startOrReload <json>                                                 start or gracefully reload JSON file
    startOrGracefulReload <json>                                         start or gracefully reload JSON file
    stop [options] <id|name|all|json|stdin...>                           stop a process (to start it again, do pm2 restart <app>)
    restart [options] <id|name|all|json|stdin...>                        restart a process
    scale <app_name> <number>                                            scale up/down a process in cluster mode depending on total_number param
    reload <name|all>                                                    reload processes (note that its for app using HTTP/HTTPS)
    gracefulReload <name|all>                                            gracefully reload a process. Send a "shutdown" message to close all connections.
    id <name>                                                            get process id by name
    delete <name|id|script|all|json|stdin...>                            stop and delete a process from pm2 process list
    sendSignal <signal> <pm2_id|name>                                    send a system signal to the target process
    ping                                                                 ping pm2 daemon - if not up it will launch it
    updatePM2                                                            update in-memory PM2 with local PM2
    update                                                               (alias) update in-memory PM2 with local PM2
    install|module:install <module|git:/>                                install or update a module and run it forever
    module:update <module|git:/>                                         update a module and run it forever
    module:generate [app_name]                                           Generate a sample module in current folder
    uninstall|module:uninstall <module>                                  stop and uninstall a module
    publish|module:publish                                               Publish the module you are currently on
    set <key> <value>                                                    sets the specified config <key> <value>
    multiset <value>                                                     multiset eg "key1 val1 key2 val2
    get [key]                                                            get value for <key>
    conf [key] [value]                                                   get / set module config values
    config <key> [value]                                                 get / set module config values
    unset <key>                                                          clears the specified config <key>
    interact [options] [secret_key|command] [public_key] [machine_name]  linking action to keymetrics.io - command can be stop|info|delete|restart
    link [options] [secret_key|command] [public_key] [machine_name]      linking action to keymetrics.io - command can be stop|info|delete|restart
    web                                                                  launch a health API on port 9615
    dump                                                                 dump all processes for resurrecting them later
    save                                                                 (alias) dump all processes for resurrecting them later
    resurrect                                                            resurrect previously dumped processes
    startup [platform]                                                   auto resurrect process at startup. [platform] = ubuntu, centos, redhat, gentoo, systemd, darwin, amazon
    logrotate                                                            copy default logrotate configuration
    generate                                                             generate an ecosystem.json configuration file
    ecosystem                                                            generate an ecosystem.json configuration file
    reset <name|id|all>                                                  reset counters for process
    describe <id>                                                        describe all parameters of a process id
    desc <id>                                                            (alias) describe all parameters of a process id
    info <id>                                                            (alias) describe all parameters of a process id
    show <id>                                                            (alias) describe all parameters of a process id
    list                                                                 list all processes
    ls                                                                   (alias) list all processes
    l                                                                    (alias) list all processes
    status                                                               (alias) list all processes
    jlist                                                                list all processes in JSON format
    prettylist                                                           print json in a prettified JSON
    monit                                                                launch termcaps monitoring
    m                                                                    (alias) launch termcaps monitoring
    flush                                                                flush logs
    reloadLogs                                                           reload all logs
    logs [options] [id|name]                                             stream logs file. Default stream all logs
    kill                                                                 kill daemon
    pull <name> [commit_id]                                              updates repository for a given app
    forward <name>                                                       updates repository to the next commit for a given app
    backward <name>                                                      downgrades repository to the previous commit for a given app
    gc                                                                   force PM2 to trigger garbage collection
    deepUpdate                                                           performs a deep update of PM2
    *                                                                  

  Options:

    -h, --help                           output usage information
    -V, --version                        output the version number
    -v --version                         get version
    -s --silent                          hide all messages
    -m --mini-list                       display a compacted list without formatting
    -f --force                           force actions
    -n --name <name>                     set a <name> for script
    -i --instances <number>              launch [number] instances (for networked app)(load balanced)
    -l --log [path]                      specify entire log file (error and out are both included)
    -o --output <path>                   specify out log file
    -e --error <path>                    specify error log file
    -p --pid <pid>                       specify pid file
    -k --kill-timeout <delay>            delay before sending final SIGKILL signal to process
    --max-memory-restart <memory>        specify max memory amount used to autorestart (in megaoctets)
    --restart-delay <delay>              specify a delay between restarts (in milliseconds)
    --env <environment_name>             specify environment to get specific env variables (for JSON declaration)
    -x --execute-command                 execute a program using fork system
    -u --user <username>                 define user when generating startup script
    --hp <home path>                     define home path when generating startup script
    -c --cron <cron_pattern>             restart a running process based on a cron pattern
    -w --write                           write configuration in local folder
    --interpreter <interpreter>          the interpreter pm2 should use for executing app (bash, python...)
    --interpreter-args <arguments>       interpret options (alias of --node-args)
    --log-date-format <momentjs format>  add custom prefix timestamp to logs
    --no-daemon                          run pm2 daemon in the foreground if it doesn't exist already
    --skip-env                           do not refresh environmnent on restart/reload
    --source-map-support                 force source map support
    --only <application-name>            with json declaration, allow to only act on one application
    --disable-source-map-support         force source map support
    --merge-logs                         merge logs from different instances but keep error and out separated
    --watch [paths]                      watch application folder for changes
    --ignore-watch <folders|files>       folder/files to be ignored watching, chould be a specific name or regex - e.g. --ignore-watch="test node_modules "some scripts""
    --node-args <node_args>              space delimited arguments to pass to node in cluster mode - e.g. --node-args="--debug=7001 --trace-deprecation"
    --no-color                           skip colors
    --no-vizion                          start an app without vizion feature (versioning control)
    --no-autorestart                     start an app without automatic restart
    --no-treekill                        Only kill the main process, not detached children
    --no-pmx                             start an app without pmx
    --no-automation                      start an app without pmx
```

## 示例 ##
``` bash
Start an app using all CPUs available + set a name :
$ pm2 start app.js -i 0 --name "api"

Restart the previous app launched, by name :
$ pm2 restart api

Stop the app :
$ pm2 stop api

Restart the app that is stopped :
$ pm2 restart api

Remove the app from the process list :
$ pm2 delete api

Kill daemon pm2 :
$ pm2 kill

Update pm2 :
$ npm install pm2@latest -g ; pm2 update

List all processes
$ pm2 list

Monitoring all processes launched
$ pm2 monit
```

## 参考 ##
[PM2官网](http://pm2.keymetrics.io/)
