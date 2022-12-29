# fargate-nginx-php-fpm-for-laravel


## Features

・Laravel on AWS ECS Fargate

## ECS Task Containers

- Nginx
- PHP-FPM
- Fluentbit
- amazon/aws-xray-daemon
- aws-appmesh-envoy


## Usage

- Build and deploy with Codebuild using CodePipeline
- Please use CodeBuild to build with CodePipeline. Then you need to set the following environment variables.
- Docker HubのtokenをParameter store

### Require CodeBuild ENVIRONMENT
key:  
ENVIRONMENT

value:  
enum:[develop|staging|production]

### Require Setting ./buildspec_build.yml

- Set it directly to the variable in the config file
- Please set in Parameter Store in the configuration file