---
title: pm2 node 服务器部署
date: 2017-03-12 22:02:31
tags:
---

# pm2 node 服务器部署

## 安装

`npm i -g pm2`

## 启动服务

基本的 `pm2 start app.js`

带参数 `pm2 ENV=production start app.js`


## 从 .config.js 文件启动 `pm2 start app.config.js`

```js
module.exports = {
  apps : [{
    name        : "worker",
    script      : "./worker.js",
    watch       : true,
    env: {
      "NODE_ENV": "development",
    },
    env_production : {
       "NODE_ENV": "production"
    }
  },{
    name       : "api-app",
    script     : "./api.js",
    instances  : 4,
    exec_mode  : "cluster"
  }]
}
```

## 从 json 文件启动 `pm2 start app.json`

```json
{
  "apps": [
    {
      "name": "lost100-dev",
      "script": "./scripts/server.js",
      "watch": true,
      "ignore_watch": [ "node_modules", "files", "public", "logs", "mongodb", "build", ".idea/", ".git"],
      "max_memory_restart": "150M",
      "instances": 2,
      "exec_mode": "cluster",
      "env": {
        "NODE_ENV": "dev",
        "PORT": 5566
      }
    }
  ]
}
```

## 可用的参数详情

General


|Field	|Type	|Example	|Description|
|:--:|:--:|:--:|:--:|
|name	|(string)|	“my-api”	|application name (default to script filename without extension)|
|script	|(string)	|”./api/app.js”	|script path relative to pm2 start|
|cwd	|(string)	|“/var/www/”	|the directory from which your app will be launched|
|args	|(string)	|“-a 13 -b 12”	|string containing all arguments passed via CLI to script|
|interpreter	|(string)	|“/usr/bin/python”|	interpreter absolute path (default to node)|
|interpreter_args	|(string)	|”–harmony”|	option to pass to the interpreter|
|node_args	|(string)	 |	|alias to interpreter_args|

Advanced features

|Field	|Type	|Example	|Description|
|:--:|:--:|:--:|:--:|
|instances	|number|	-1	|number of app instance to be launched|
|exec_mode|	string	|“cluster”	|mode to start your app, can be “cluster” or “fork”, default fork|
|watch	|boolean or []|	true	|enable watch & restart feature, if a file change in the folder or subfolder, your app will get reloaded|
|ignore_watch	|list	|[”[\/\\]\./”, “node_modules”]|	list of regex to ignore some file or folder names by the watch feature
|max_memory_restart|	string|	“150M”	|your app will be restarted if it exceeds the amount of memory specified. human-friendly format : it can be “10M”, “100K”, “2G” and so on…|
|env	|object	|{“NODE_ENV”: “development”, “ID”: “42”}	|env variables which will appear in your app|
|env_	|object	|{“NODE_ENV”: “production”, “ID”: “89”}|	inject when doing pm2 restart app.yml --env|
|source_map_support|	boolean	|true	|default to true, [enable/disable source map file]|
|instance_var	|string	|“NODE_APP_INSTANCE”	|see documentation|


Log files

|Field	|Type	|Example	|Description|
|:--:|:--:|:--:|:--:|
|log_date_format	|(string)	|“YYYY-MM-DD HH:mm Z”|	log date format (see log section)|
|error_file	|(string)	 	|error file path |(default to $HOME/.pm2/logs/XXXerr.log)
|out_file	|(string)	 |	output file path |(default to $HOME/.pm2/logs/XXXout.log)|
|combine_logs	|boolean	|true	|if set to true, avoid to suffix |logs/pid file with the process id|
|merge_logs|	boolean	|true	|alias to combine_logs|
|pid_file	|(string)	 	|pid file path |(default to $HOME/.pm2/pid/app-pm_id.pid)|


Control flow

|Field	|Type	|Example	|Description|
|:--:|:--:|:--:|:--:|
|min_uptime|	(string)|	 |	min uptime of the app to be considered started|
|listen_timeout|	number	|8000	|time in ms before forcing a reload if app not listening|
|kill_timeout	|number	|1600	|time in milliseconds before sending a final SIGKILL|
|wait_ready	|boolean|	false|	Instead of reload waiting for listen event, wait for process.send(‘ready’)|
|max_restarts	|number|	10	|number of consecutive unstable restarts (less than 1sec interval or custom time via min_uptime) before your app is considered errored and stop being restarted|
|restart_delay	|number	|4000	|time to wait before restarting a crashed app (in milliseconds). defaults to 0.|
|autorestart	|boolean	|false	|true by default. if false, PM2 will not restart your app if it crashes or ends peacefully|
|cron_restart	|string	|“1 0 * * *”	|a cron pattern to restart your app. Application must be running for cron feature to work|
|vizion	|boolean	|false	|true by default. if false, PM2 will start without vizion features (versioning control metadatas)|
|post_update	|list	|[“npm install”, “echo launching the app”]|	a list of commands which will be executed after you perform a Pull/Upgrade operation from Keymetrics dashboard|
|force	|boolean	|true	|defaults to false. if true, you can start the same script several times which is usually not allowed by PM2|











