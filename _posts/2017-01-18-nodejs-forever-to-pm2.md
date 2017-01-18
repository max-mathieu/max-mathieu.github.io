---
layout: post
title: Bye-bye forever, hello pm2
tags:
  - nodejs
  - express
  - nginx
  - devops
---
`forever` is a really fine and simple process management tool for nodejs app while `pm2` comes with a lot of features that not everyone needs.
Though, there's one killer feature that drove me to replace `forever` by `pm2`: being able to "reload" a node server without downtime.

## Graceful reload with pm2

`pm2` routes new requests to new nodes and spins down the old after some time (or when they exit) allowing a rolling restarts of the forks.
Doing so, it allows to remove the need for cluster or express-cluster, and to specify the number of instances right from the startup script.

On `SIGINT`, you want to close your db or queue connections, and try to exit as soon as possible.
To exit your API process as early as possible without breaking in-flight requests (always nice), you can keep track of open connections to your nodejs server:

```javascript
let openSockets = 0;

server.on('connection', socket => {
  openSockets++;
  socket.on('close', () => {
    openSockets--;
  });
});

process.once('SIGINT', () => {
  if (openSockets > 0) {
    return;
  }
  process.emit('graceful_shutdown');
  // give enough time to various process.once('graceful_shutdown') to close stuff, then exit
  setTimeout(() => {
    process.exit();
  }, 100);
});
```

as `pm2` will keep sending `SIGINT` every 100ms.

## pm2 is not fully giving you zero-downtime

Having something like nginx in front of multiple instances of `pm2` remains necessary for a fully zero-downtime (0.0-downtime?) deployment setup:

- you _have_ to restart if you change your `pm2` configuration
- `pm2` only gives you so much time, though configurable, to exit gracefully, but if you're in the middle of a long-running operation (say an upload), that may cut it in the middle, where as nginx would retry

Though having `pm2` allows you to not have to wait between restarts of the different instances, which can make your deployment way faster

## Final notes

- I did not profile the overhead of `pm2` vs `forever`. More features has to come at a price, right?
- I did not look yet into `pm2` monitoring abilities, but they look very interesting :)
- don't get confused: `--watch` with `pm2` does not do a reload, but a restart (30 minutes lost with that)
- you can use `pm2 startup` to create startup scripts, though it's quite easy to write them yourself. Also, I like having 1 startup script per component, where as `pm2` runs 1 for all of them
  - be warned: `pm2` CLI arguments can be very different from their JSON/yaml counterparts (`-x` means `exec_mode=fork`)

## Links

- [forever](https://github.com/foreverjs/forever)
- [pm2](http://pm2.keymetrics.io/)
