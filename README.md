# Playground for trying localstack
- https://github.com/localstack/localstack
- https://docs.localstack.cloud/overview/
- https://hub.docker.com/r/localstack/localstack
- [Testing with LocalStack con Marta Arcones](https://www.youtube.com/watch?v=qSOU98dLKs8)
    - https://github.com/CodingIsCaring/test-local-stack

## How to run it
- `docker run --rm -it -p 4566:4566 -p 4571:4571 localstack/localstack`    
- `docker run --rm -it -p 4566:4566 -p 4571:4571 localstack/localstack -e "SERVICES=s3"`

## Verifying your docker-compose configuration using the command line
`localstack config validate --file=localstack-docker-compose.yml`

## Service health check
The service `/health` check endpoint on the edge port (http://localhost:4566/health by default) provides basic information about the status of each service (e.g., `{"s3":"running","es":"starting"}`). By default, the endpoint returns cached values that are determined during startup - the status values can be refreshed by adding the reload query parameter: http://localhost:4566/health?reload.
## Core configurations
- **SERVICES**: Comma-separated list of service names (APIs) to start up. 
- **DATA_DIR**: Local directory for saving persistent data (currently only supported for these services: Kinesis, DynamoDB, Elasticsearch, S3, Secretsmanager, SSM, SQS, SNS).
## S3
### Resources
- https://onexlab-io.medium.com/localstack-s3-e28ad393c09
- https://dev.to/adevintaspain/usando-aws-s3-en-local-con-localstack-4jjp