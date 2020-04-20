# Docker mysql + aws cli

Docker image with :

- AWS cli to send content to s3
- Service user uid 1001

## Test image

```
docker run --rm mikamboo/aws-mysql mysqldump --version
```
