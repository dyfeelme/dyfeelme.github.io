---
title: NodeJS入门笔记-forever
tags:
  - nodejs
  - javascript
categories:
  - NodeJS
date: 2015-10-05 15:29:27
---


forever是一个简单的nodejs进程管理工具，可以监控nodejs子进程。
<!-- more -->

## 安装 ##
``` bash
$ npm install forever -g
```

## 命令概览 ##
``` bash
 $ forever --help
  usage: forever [action] [options] SCRIPT [script-options]

  Monitors the script specified in the current process or as a daemon

  actions:
    start               Start SCRIPT as a daemon
    stop                Stop the daemon SCRIPT by Id|Uid|Pid|Index|Script
    stopall             Stop all running forever scripts
    restart             Restart the daemon SCRIPT
    restartall          Restart all running forever scripts
    list                List all running forever scripts
    config              Lists all forever user configuration
    set <key> <val>     Sets the specified forever config <key>
    clear <key>         Clears the specified forever config <key>
    logs                Lists log files for all forever processes
    logs <script|index> Tails the logs for <script|index>
    columns add <col>   Adds the specified column to the output in `forever list`
    columns rm <col>    Removed the specified column from the output in `forever list`
    columns set <cols>  Set all columns for the output in `forever list`
    cleanlogs           [CAREFUL] Deletes all historical forever log files

  options:
    -m  MAX          Only run the specified script MAX times
    -l  LOGFILE      Logs the forever output to LOGFILE
    -o  OUTFILE      Logs stdout from child script to OUTFILE
    -e  ERRFILE      Logs stderr from child script to ERRFILE
    -p  PATH         Base path for all forever related files (pid files, etc.)
    -c  COMMAND      COMMAND to execute (defaults to node)
    -a, --append     Append logs
    -f, --fifo       Stream logs to stdout
    -n, --number     Number of log lines to print
    --pidFile        The pid file
    --uid            Process uid, useful as a namespace for processes (must wrap in a string)
                     e.g. forever start --uid "production" app.js
                         forever stop production
    --sourceDir      The source directory for which SCRIPT is relative to
    --workingDir     The working directory in which SCRIPT will execute
    --minUptime      Minimum uptime (millis) for a script to not be considered "spinning"
    --spinSleepTime  Time to wait (millis) between launches of a spinning script.
    --colors         --no-colors will disable output coloring
    --plain          Disable command line colors
    -d, --debug      Forces forever to log debug output
    -v, --verbose    Turns on the verbose messages from Forever
    -s, --silent     Run the child script silencing stdout and stderr
    -w, --watch      Watch for file changes
    --watchDirectory Top-level directory to watch from
    --watchIgnore    To ignore pattern when watch is enabled (multiple option is allowed)
    -t, --killTree   Kills the entire child process tree on `stop`
    --killSignal     Support exit signal customization (default is SIGKILL),
                     used for restarting script gracefully e.g. --killSignal=SIGTERM
    -h, --help       You're staring at it

  [Long Running Process]
    The forever process will continue to run outputting log messages to the console.
    ex. forever -o out.log -e err.log my-script.js

  [Daemon]
    The forever process will run as a daemon which will make the target process start
    in the background. This is extremely useful for remote starting simple node.js scripts
    without using nohup. It is recommended to run start with -o -l, & -e.
    ex. forever start -l forever.log -o out.log -e err.log my-daemon.js
        forever stop my-daemon.js
```

## 配置 ##
``` bash
目录结构
.
├── forever
│   └── development.json
└── index.js
配置文件
// forever/development.json
{
    // Comments are supported
    "uid": "app",
    "append": true,
    "watch": true,
    "script": "index.js",
    "sourceDir": "/home/myuser/app"
}

命令启动
$ forever start ./forever/development.json
```

## forever-monitor ##
在不使用forever-cli的情况下，我们可以通过调用核心API函数来执行monitor。
### 安装###
``` bash
$ npm install forever-monitor
```

### 配置 ###
``` javascript
 var forever = require('forever-monitor');

  var child = new (forever.Monitor)('your-filename.js', {
    max: 3,
    silent: true,
    args: []
  });

  child.on('exit', function () {
    console.log('your-filename.js has exited after 3 restarts');
  });

  child.start();
```

可用的配置：
``` javascript
{
    //
    // Basic configuration options
    //
    'silent': false,            // Silences the output from stdout and stderr in the parent process
    'uid': 'your-UID',          // Custom uid for this forever process. (default: autogen)
    'pidFile': 'path/to/a.pid', // Path to put pid information for the process(es) started
    'max': 10,                  // Sets the maximum number of times a given script should run
    'killTree': true,           // Kills the entire child process tree on `exit`

    //
    // These options control how quickly forever restarts a child process
    // as well as when to kill a "spinning" process
    //
    'minUptime': 2000,     // Minimum time a child process has to be up. Forever will 'exit' otherwise.
    'spinSleepTime': 1000, // Interval between restarts if a child is spinning (i.e. alive < minUptime).

    //
    // Command to spawn as well as options and other vars
    // (env, cwd, etc) to pass along
    //
    'command': 'perl',         // Binary to run (default: 'node')
    'args':    ['foo','bar'],  // Additional arguments to pass to the script,
    'sourceDir': 'script/path',// Directory that the source script is in

    //
    // Options for restarting on watched files.
    //
    'watch': true,               // Value indicating if we should watch files.
    'watchIgnoreDotFiles': null, // Whether to ignore file starting with a '.'
    'watchIgnorePatterns': null, // Ignore patterns to use when watching files.
    'watchDirectory': null,      // Top-level directory to watch from.

    //
    // All or nothing options passed along to `child_process.spawn`.
    //
    'spawnWith': {
      customFds: [-1, -1, -1], // that forever spawns.
      setsid: false,
      uid: 0, // Custom UID
      gid: 0  // Custom GID
    },

    //
    // More specific options to pass along to `child_process.spawn` which
    // will override anything passed to the `spawnWith` option
    //
    'env': { 'ADDITIONAL': 'CHILD ENV VARS' },
    'cwd': '/path/to/child/working/directory',

    //
    // Log files and associated logging options for this instance
    //
    'logFile': 'path/to/file', // Path to log output from forever process (when daemonized)
    'outFile': 'path/to/file', // Path to log output from child stdout
    'errFile': 'path/to/file', // Path to log output from child stderr

    //
    // ### function parseCommand (command, args)
    // #### @command {String} Command string to parse
    // #### @args    {Array}  Additional default arguments
    //
    // Returns the `command` and the `args` parsed from
    // any command. Use this to modify the default parsing
    // done by 'forever-monitor' around spaces.
    //
    'parser': function (command, args) {
      return {
        command: command,
        args:    args
      };
    }
  }
```

## 参考 ##
[forever官方文档](https://github.com/foreverjs/forever)
[forever-monitor官方文档](https://github.com/foreverjs/forever-monitor)

