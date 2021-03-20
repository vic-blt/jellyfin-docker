# Run Jellyfin with docker

## Setup
- Create `.env` file
```env
HOSTNAME=example.org
# as you may need to edit Content-Security-Policy header in order to allow some css files used by themes, it simpler to save the config in an environment variable
SECURITY="default-src https: data: blob:; style-src 'self' 'unsafe-inline'; script-src 'self' 'unsafe-inline' https://www.gstatic.com/cv/js/sender/v1/cast_sender.js blob:; worker-src 'self' blob:; connect-src 'self'; object-src 'none'; frame-ancestors 'self'"
```
- Execute `init-letsencrypt.sh` script to create an SSL certificate
**NB**: edit `domains` and `email` variables in the script before executing it
```sh
./init-letsencrypt.sh
```

## TODO
- Reload nginx when SSL cert is renewed.

  **NB**: `command` in `docker-compose.yml` is used as argument by [docker-entrypoint.sh](https://github.com/nginxinc/docker-nginx/blob/master/stable/alpine/docker-entrypoint.sh).
  So, `command: "/bin/sh -c 'while :; do sleep 6h & wait $${!}; nginx -s reload; done & nginx -g \"daemon off;\"'"` (used to reload nginx and use new cert) will prevent [envsubst script](https://github.com/nginxinc/docker-nginx/blob/master/stable/alpine/20-envsubst-on-templates.sh) from being executed.

## Resources
- https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71
- https://github.com/wmnnd/nginx-certbot
