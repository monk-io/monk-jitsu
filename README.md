# Jitsu & Monk

This repository contains Monk.io template to deploy Jitsu & Monk either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

## Prerequisites

- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

## Make sure monkd is running

```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository

```bash
git clone https://github.com/monk-io/jitsu
```

## Load Template

```bash
cd jitsu
monk load MANIFEST
```

## Let's take a look at the themes I have installed

```bash
foo@bar:~$ monk list jitsu
✔ Got the list
Type      Template                           Repository  Version  Tags
runnable  jitsu/jitsu-configurator      local       -        -
runnable  jitsu/jitsu-server            local       -        -
runnable  jitsu/redis                   local       -        -
runnable  jitsu/redis-user-recognition  local       -        -
group     jitsu/stack                   local       -        -
```

## Deploy Stack

```bash
foo@bar:~$ monk run jitsu/stack
? Select tag to run [local/jitsu/stack] on: monk
✔ Starting the job: local/jitsu/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% redis:latest monk
✔ [================================================] 100% jitsucom/server:latest monk
✔ [================================================] 100% jitsucom/configurator:latest monk
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Starting containers DONE
✔ Starting containers DONE
✔ Started local/jitsu/stack

🔩 templates/local/jitsu/stack
 └─🧊 Peer monk
    ├─🔩 templates/local/jitsu/redis-user-recognition
    │  └─📦 9640ac28397a62b0408cc064f981efc5-u-redis-user-recognition-redis
    │     └─🧩 redis:latest
    ├─🔩 templates/local/jitsu/jitsu-server
    │  └─📦 5ebdbb89000d404b86873f97eed41d3c-jitsu-jitsu-server-server
    │     ├─🧩 jitsucom/server:latest
    │     ├─💾 /var/lib/monkd/volumes/jitsu/configurator/data/logs -> /home/configurator/data/logs
    │     └─🔌 open <ip>:8002 (0.0.0.0:8002) -> 8001
    ├─🔩 templates/local/jitsu/redis
    │  └─📦 0de28c9c597b0cf18f1a972fd949208c-local-jitsu-redis-redis
    │     └─🧩 redis:latest
    └─🔩 templates/local/jitsu/jitsu-configurator
       └─📦 dbe97fc975e68d2f837d5bea6c162b3d-itsu-configurator-configurator
          ├─🧩 jitsucom/configurator:latest
          ├─💾 /var/lib/monkd/volumes/jitsu/configurator/data/logs -> /home/configurator/data/logs
          └─🔌 open <ip>:8001 (0.0.0.0:8001) -> 7000

💡 You can inspect and manage your above stack with these commands:
 monk logs (-f) local/jitsu/stack - Inspect logs
 monk shell     local/jitsu/stack - Connect to the container's shell
 monk do        local/jitsu/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Check web gui

`http://<ip>:8002/`

## Variables

The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable          | Description              | Default |
| ----------------- | ------------------------ | ------- |
| jitsu_admin_token | Jitsu admin token        | monk    |
| jitsu_config_port | Jitsu configuration port | 8002    |
| jitsu_server_port | Jitsu server port        | 8001    |

## Stop, remove and clean up workloads and templates

```bash
monk purge jitsu
```
