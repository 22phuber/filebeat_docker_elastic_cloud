# filebeat_docker_elastic_cloud

Read the Blog Post: https://supportblog.ch/filebeat-docker-image-mit-elastic-cloud/

### Build Filebeat Base Image

```bash
cd filebeat_base
# Build filebeat base container
# Check version in Dockerfile
filebeatVersion=7.6.1
docker build -t "base/filebeat:${filebeatVersion}" --no-cache .


# Optional:
# Tags for AWS ECR
docker tag "base/filebeat:${filebeatVersion}" "<aws_account_id>.dkr.ecr.<region>.amazonaws.com/base/filebeat:${filebeatVersion}"
```

### Build Filebeat Image

```bash
cd filebeat_project
docker build -t "<project_name>/filebeat:${tagVersion}" --no-cache .


# Optional:
# Tags for AWS ECR
docker tag "<project_name>/filebeat:${tagVersion}" "<aws_account_id>.dkr.ecr.<region>.amazonaws.com/<project_name>/filebeat:${tagVersion}"
# AWS ECR login (already logged in? => skip this step)
eval $(aws ecr get-login --no-include-email)
# push
docker push "<aws_account_id>.dkr.ecr.<region>.amazonaws.com/<project_name>/filebeat:${tagVersion}"
```
