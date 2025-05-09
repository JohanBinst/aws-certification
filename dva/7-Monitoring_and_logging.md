# 7 - Monitoring and Logging
1. CloudWatch: CloudWatch Data, CloudWatch Alarms, CloudWatch Logs
2. X-Ray
3. VPC Flow Logs

## 1. CloudWatch

### 1.1 Definition
Cloudwatch is used for Ingestion, Storage and Management of Metrics. 
Is AWS Public service -> can be accessed from public space endpoints (using IGW or VPC interface endpoint)
AWS services are integrated with Cloudwatch for management data

#### CloudWatch Agent:
If you need to monitor internal data (e.g. data inside EC2 instance like logs or memory usage) you need to install a CW agent.
Or if you need to integrate On premise data to AWS -> install agent + give required permissions to store data

#### Use cases:
- View logged metric data via console UI, CLI, API or dashboard
- Anomaly detection
- Alarms -> react to metric alarm (OK, NOK) with notification or perform action

### 1.2 CloudWatch Data
Cloudwatch data uses following definitions to manage the data:
 - **Namespace**: container for metrics -> used to diferentiate same metric for different services or applications. Allows for grouping of metrics based on namespace.
    - AWS namespaces use always with `AWS/service` : eg. AWS/EC2, AWS/Lambda for AWS services
    - There is no default namespace
    - user can create own namespace
- **Metric**: A time ordered set of data points -> the fundamental concept of CloudWatch. Every metric has a MetricName (CPUUtilization) and a namespace (AWS/EC2)
- **Datapoint**: Every datapoint has a Timestamp, Value and optionally a Unit key
- **Dimension**: name/value pair that is part of the identity of the metric -> makes metric unique. EC2 uses InstanceId dimension. Dimensions can be combined (see below).
- **Resolution**: granularity of metric = smallest time period you can retrieve of metric
    - Standard (60s) = used for all AWS Service metrics (AWS/service)
    - high (1s) = can be used for custom metrics
    --> If you want 1s granularity for AWS Service metric you have to create a custom metric with high (1s) resolution. Costs more
- **Statistics**: Aggregation of data over a period of time. For example
    - Min
    - Max
    - Sum
    - Average
    - ...
 - **Percentile**: Recover percentile data eg: 95% percentile or 75% percentile. To get better view of distibution of data and identify outliers.

Dimension combination example: Server and Domain dimensions makes CloudWatch treat each combination as seperate metric (because unique combination).
```
Dimensions: Server=Prod, Domain=Frankfurt, Unit: Count, Timestamp: 2016-10-31T12:30:00Z, Value: 105
Dimensions: Server=Beta, Domain=Frankfurt, Unit: Count, Timestamp: 2016-10-31T12:31:00Z, Value: 115
Dimensions: Server=Prod, Domain=Rio,       Unit: Count, Timestamp: 2016-10-31T12:32:00Z, Value: 95
Dimensions: Server=Beta, Domain=Rio,       Unit: Count, Timestamp: 2016-10-31T12:33:00Z, Value: 97
```

#### Data retention
CloudWatch has a sort of automatic lifecycle policy: 1s data metric is first stored for 3, then 15 days with 60s resolution etc.
- sub 60s data is retained for 3h
- 60s (1min) retained for 15 days
- 300s (5min) retained for 63 days
- 3600s (1h) retained for 455 days

Reason: precision is less important the older the data gets.

### 1.3 CloudWatch Alarms
- Cloudwatch alarms watches a metric over a period of time. 
- 2 states: OK or Alarm state
- compares value of metric vs threshold over time
- you can define one or more actions
- has alarm resolution (must be equal or greater than metric resolution)

### 1.4 CloudWatch Logs
Public service to store, monitor and access logging data
- Used for AWS services, On-Premise applications, IOT or any application
- Install CloudWatch agent if you need application logging or custom system logging
- Can also be used to ingest logs from 
  - VPC Flow Logs
  - CloudTrail
  - Elastic Beanstalk
  - ECS Container Logs
  - API Gateway
  - Lambda execution logs
  - Route53: log DNS request
- Logging data is stored in Region where service is used or us-east-1/us-west-1 if global service (Route53, CloudFront, IAM, Organisations )
 
 EXAM: CloudWatch logs should be default answer to any logging related question within AWS (or even on-premises)

#### Components:
- Log Group = multiple log streams
- Log streams = group of log events from logging source
- Log event =  Timestamp + raw message created in logging source (application or service)

Retention, Permissions and Encryption is mangaged at the Log Group level -> handle access, retention time and encryption with KMS based on log

#### Metric filter
Use a metric filter to recover a certain log event and then handle metric like any other CloudWatch metric: generate alarm or take action -> SSH connection failure or app crash log -> CW alarm -> sends email to devs with SNS  
Metric filters are defined on log group

#### Getting data out of CloudWatch
To get data out of Cloudwatch the default is to export to S3: 
- Can take up to 12 hours so data is NOT real time
- encryption only with SSE-S3 (NOT KMS)

If faster export is required use a **Subscription filter**, 4 solutions possible
- Near-real time: CloudWatch -> Kinesis Data Firehose -> S3
- Real time: CloudWatch -> AWS Managed Lambda -> ElasticSearch
- Real time: CloudWatch -> Custom Lambda -> Application
- Real time: CloudWatch -> Kinesis Data Streams -> system that integrates with Kinesis Data streams

Common use case for subscription filter: logging aggregation of multiple applications to 1 Kinesis Data Stream:  
app 1 cw agent -> CW sub filter -> Kinesis Data Stream  
app 2 cw agent -> CW sub filter -> Kinesis Data Stream  
app 3 cw agent -> CW sub filter -> Kinesis Data Stream  

Then: Kinesis Data Stream -> Kinesis Data Firehose -> S3

## 2. X-Ray

X-Ray helps developers analyze and debug distributed applications (applications that use microservice architecture).

X-Ray allows to troubleshoot the root cause of performance issues and errors by giving an end-to-end view of requests as they travel through your application.

Components:
- **Tracing Header**: Used to track request through distributed application with trace ID. Is generated by first service.
- **Segments**: Data blocks sent by service into X-Ray, contains host/IP, request, response, work done (times), issues
- **Subsegments**: More granular version of segment: shows different calls to other services as part parent segment (endpoints used etc)
- **Service Graphs**: JSON Document detailing services and resources that make up your application
- **Service Map**: visualizes request in "web like" representation of application, uses Service Graph JSON as input. Shows response time, requests and errors/issues (from segments)

### Supported services:
- Lambda: enable X-Ray option
- API Gateway: per stage
- SNS
- SQS
- Elastic Beanstalk: X-Ray agent is preinstalled
- Elastic Load Balancing
- EventBridge
- AWS Distro for OpenTelemetry (ADOT)
- EC2: with X-Ray agent
- ECS: X-Ray agent in tasks

**Important**:
To use X-Ray in services you need to give IAM Permissions --> IAM Role

## 3. VPC Flow logs
See section Advanced networking
- EXAM: Flow logs captures only packet metadata (publicly available): NOT packet CONTENTS
- EXAM: Flow logs are NOT realtime