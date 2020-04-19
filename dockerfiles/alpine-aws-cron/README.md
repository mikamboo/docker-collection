# Docker cron (supersonic) + aws cli

Cron docker image with :

- Supersonic to run crontab file (https://github.com/aptible/supercronic)
- AWS cli to send content to s3
- Timezone setup
- Service user uid 1001

## Usage

Create you crontab

```
echo "*/5 * * * * * * aws --version" > test.crontab
```

Run the cron tab

```
docker run --rm mikamboo/aws-cron test.crontab
```
## Links

* https://github.com/aptible/supercronic
* https://github.com/mikamboo/docker-collection
