# Run Jellyfin with docker

## Setup
- Create `.env` file
```env
HOSTNAME=example.org
# as you may need to edit Content-Security-Policy header in order to allow some css files used by themes, it simpler to save the config in an environment variable
SECURITY="default-src https: data: blob:; style-src 'self' 'unsafe-inline'; script-src 'self' 'unsafe-inline' https://www.gstatic.com/cv/js/sender/v1/cast_sender.js blob:; worker-src 'self' blob:; connect-src 'self'; object-src 'none'; frame-ancestors 'self'"
```
- Execute `init-letsencrypt.sh` script to create an SSL certificate
```sh
./init-letsencrypt.sh example.org [admin@example.org]
```

## Resources
- https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71
- https://github.com/wmnnd/nginx-certbot
