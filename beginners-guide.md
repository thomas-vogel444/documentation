# Beginner's guide to NGINX

From https://nginx.org/en/docs/beginners_guide.html

NGINX has one master process and several worker process
- master process
    - Read and evaluate configuration
    - Maintain worder processes
- Worker processes
    - Process the requests

## Starting, Stopping and Reloading Configuration

Once started, NGINX can be controlled with the `-s` parameter.
```bash
nginx -s <signal>
```

signal:
    - stop: fast shutdown
    - quit: graceful shutdown
    - reload: reloads the configuration file
        - upon reload, the master process starts new worker nodes with the updated config and stops old worker nodes
    - reopen: reopening the log files

## Configuration file's stucture

NGINX consists of modules controlled by directives specifie in the configuration file.

Components of a config file
- simple directives
- block directives
- contexts
    - block directive containing block directives

## Serving Static Content

`server` block < `http` block < `location` blocks

NGINX can have multiple `server` blocks listening on different ports.

Example `server` configuration:
```nginx
server {
    listen       9000;
    server_name  localhost;

    location / {
        root /Users/thomasvogel/data/www;
    }

    location /images {
        root /Users/thomasvogel/data/;
    }
}
```


## Setting up a Simple Proxy server
























