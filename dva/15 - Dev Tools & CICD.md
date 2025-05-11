# 15 - AWS CLI, Dev Tools & CICD

## CI/CD
AWS CodePipeline is used to create a CI/CD pipeline in AWS, a pipeline consists of following steps and uses following AWS Services:
1. Code (CodeCommit): push code to CodeCommit repo
2. Build (CodeBuild): build project using AWS CodeBuild
3. Test (CodeBuild): run test using AWS CodeBuild
4. Deploy (CodeDeploy): Deploy project using AWS CodeDeploy

## AWS CodeCommit
Git repo on AWS

Still used ?

## AWS CodePipeline
AWS CodePipeline is a continuous delivery service you can use to model, visualize, and automate the steps required to release your software. You can quickly model and configure the different stages of a software release process. CodePipeline automates the steps required to release your software changes continuously.

- Pipelines are built from **stages**.
- Each stage has 1 or more **actions**, actions can be single (1 action), parallel or sequential.
- Movement between stages can require manual approval
- **Artifacts** are storen in S3 and are the output or input (consumed by action) for an action.
- Stages state changes (success, Failed or Cancelled) are sent to EvenBridge
- Console UI or CloudTrail can be used to view or interact with the pipeline.

## AWS CodeBuild
AWS CodeBuild is a fully managed continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy. With CodeBuild, you don’t need to provision, manage, and scale your own build servers. CodeBuild scales continuously and processes multiple builds concurrently, so your builds are not left waiting in a queue

- Pay only for the ressources consumed during builds.
- integrates with other AWS services required for builds : IAM, KMS, VPC, CloudTrail, S3, ...
- Uses Docker by default for build environment but can be customized

Architecture :
- CodeBuild recovers code from git repository : Github, CodeCommit, CodePipeline or S3
- It runs builds and tests (test is build with build environment variables)
- EXAM: It is customized using **buildspec.yaml** file (specific name) that must be in the **root of source**
- build logs can be output to S3 or CloudWatch logs
- build metrics can be stored in CloudWatch
- events related to build can be sent to EventBridge -> event-driven response: eg sent e-mail on build failure or run Lambda function
- build control comes from:
  - CLI
  - SDK
  - Pipeline

### buildspec.yaml file
- buildspec.yaml file customizes build (and test) process
- buildspec file constains:
  - 4 main phases of build process
  - environment variable keys and where to find values
  - info for artifacts
- EXAM: 4 main phases in the file:
  - **install**: install packages in the build environment (frameworks or other toolings (Sonar?)) -> not app dependencies
  - **pre_build**: sign-in to things and install app dependencies
  - **build**: commands run during the build process -> build the actual app
  - **post_build**: do things required after build -> e.g. package things up, push Docker image, explicit notifications
- In buildspec you also define the environment variables required for the build. The values for the variable can come from:
  - shell commands
  - global environment variables
  - AWS Parameter Store
  - AWS Secrets Manager
- Artifacts part of file: Define what to store and where to store it
