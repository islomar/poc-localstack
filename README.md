# Playground for trying localstack
- https://github.com/localstack/localstack
- https://docs.localstack.cloud/overview/
- https://hub.docker.com/r/localstack/localstack
- [Testing with LocalStack con Marta Arcones](https://www.youtube.com/watch?v=qSOU98dLKs8)
    - https://github.com/CodingIsCaring/test-local-stack

## How to run it
- **IMPORTANT**: you need to configure the credentials (test/test): https://github.com/localstack/localstack#setting-up-local-region-and-credentials-to-run-localstack
- `docker run --rm -it -p 4566:4566 -p 4571:4571 localstack/localstack`    
- `docker run --rm -it -p 4566:4566 -p 4571:4571 localstack/localstack -e "SERVICES=s3"`
- `docker-compose -f docker-compose-s3.yml up`
## Using Docker
- https://github.com/localstack/localstack/blob/master/README.md#aws-cli-v2-with-docker-and-localstack
    - `docker network create localstack`

  
## AWS CLI v2
`docker run --network localstack --rm -it amazon/aws-cli --endpoint-url=http://localstack:4566`

## Terraform
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/guides/custom-service-endpoints#localstack

## Verifying your docker-compose configuration using the command line
`localstack config validate --file=localstack-docker-compose.yml`

## Service health check
The service `/health` check endpoint on the edge port (http://localhost:4566/health by default) provides basic information about the status of each service (e.g., `{"s3":"running","es":"starting"}`). By default, the endpoint returns cached values that are determined during startup - the status values can be refreshed by adding the reload query parameter: http://localhost:4566/health?reload.
## Core configurations
- **SERVICES**: Comma-separated list of service names (APIs) to start up. 
- **DATA_DIR**: Local directory for saving persistent data (currently only supported for these services: Kinesis, DynamoDB, Elasticsearch, S3, Secretsmanager, SSM, SQS, SNS).
## S3
- **Create a S3 bucket**
    - `aws --endpoint-url=http://localhost:4566 s3 mb s3://my-bucket`
    - `aws s3 --endpoint-url=http://localhost:4566 ls`
- **Upload a file to the bucket**
    - `aws --endpoint-url=http://localhost:4566 s3 cp text-test.txt s3://my-bucket`
    - `aws s3 --endpoint-url=http://localhost:4566 ls my-bucket`

### Resources
- https://onexlab-io.medium.com/localstack-s3-e28ad393c09
- https://dev.to/adevintaspain/usando-aws-s3-en-local-con-localstack-4jjp
    - https://github.com/alextremp/s3-storage-service-demo
- https://dev.to/goodidea/how-to-fake-aws-locally-with-localstack-27me
- https://github.com/localstack/awscli-local
    - This package provides the awslocal command, which is a thin wrapper around the aws command line interface for use with LocalStack.

## Other interesting resources
- https://docs.aws.amazon.com/sdk-for-php/v3/developer-guide/guide_credentials_profiles.html
- Integration with JetBrains "AWS Explorer": https://github.com/aws/aws-toolkit-jetbrains/issues/1883
