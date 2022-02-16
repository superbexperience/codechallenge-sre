# Superb Site Reliability Engineering Challenge

A fun and practical test for the SRE position at Superb.

## Introduction

Superb is growing. Today we have 4 applications organized in a [monorepo](https://en.wikipedia.org/wiki/Monorepo). They are:

- **[auth](./auth/)**: An HTTP API used to register and authenticate users that will use our platform. This is a high audience service and must have attention with it.
- **[booking](./booking/)**: A gRPC API responsible by manage restaurant bookings.
- **[graphql](./graphql/)**: This API is our border service. It make the bridge between frontend applications and our microservices.
- **[client](./client/)**: This API is a frontend app used to manage bookings.

## Prerequisites

1. An AWS account
2. region `Paris (eu-west-3)`
3. A valid route53 domain name - ie: `superb.io`

#### Install AWS CLI
1. Install AWS CLI
2. Get AWS CLI credentials
3. Go to AWS Console: IAM
4. Create a user that have `AdministratorAccess` IAM permission with access types Access key - Programmatic access and Password - AWS Management Console access
5. Select Security Credentials
6. Select Access Key ID and Secret access key
7. Configure AWS CLI, run aws configure using above parameters.

#### Create AWS resources from AWS console

1. An S3 bucket to host terraform infrastructure state named `fs-superb-app-state`.
2. An S3 bucket for frontend builds and use its name as `S3_REPOSITORY` value to github secrets.
3. A DynamoDB table to handle state locking named `superb-dynamodb-state-lock` and should have primary key LOCK_ID.
4. An IAM user that have `AmazonS3FullAccess` IAM permission, use his security credentials as `S3_ACCESS_KEY` and `S3_SECRET_ACCESS_KEY` values to github secrets.
5. Get AWS certificate ARN for `superb.io` in `us-east-1` region and export its value as `ACM_ARN_PROD` to github secrets.

#### Install Docker
You will need to install Docker and Docker Compose to get the app running locally in your machine.

#### Setup Github actions user

1. Go to AWS Console: IAM
2. Select Add users with only access type Access key - Programmatic access
3. Select Next Permissions
4. Select Create policy and give the user the custom IAM permission inside `github-policy/github-policy.json`
5. Select Access Key ID and Secret access key
6. Create two github secrets `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` using above parameters.
