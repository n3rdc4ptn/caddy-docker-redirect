# Caddy Docker Redirect
A simple docker container to redirect http traffic from one hostname to another.
Can be used after changing to a new domain name and redirecting the user from the old domain to the new one.

## How to use
Inside that docker container a simple caddy webserver is running. This can be configured using the environment variables on run.
You must specify the target and what redirect type to use.

A warning here, if you switch the redirect type to permanent, the browser caches the redirect and will no longer check if your target has changed! Do this only if you dont want to use the previous domain no longer.

```yaml
services:
  web:
    build: .
    ports:
      - "3000:80"
    environment:
      - REDIRECT_TYPE=temporary
      - REDIRECT_TARGET=https://www.mydomain.com
```


The underlying Caddy Configuration looks like this:
```Caddyfile
:80

redir {$REDIRECT_TARGET}{uri} {$REDIRECT_TYPE}
```


## Caddy
Caddy is a simple webserver written in Go. You can find more information about it here: https://caddyserver.com.
