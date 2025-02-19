# Troubleshooting Amazon Managed Workflows for Apache Airflow \(MWAA\)<a name="troubleshooting"></a>

This topic describes common issues and errors you may encounter when using Apache Airflow on Amazon Managed Workflows for Apache Airflow \(MWAA\) and recommended steps to resolve these errors\.

**Contents**
+ [Troubleshooting: DAGs, Operators, Connections, and other issues in Apache Airflow v2](t-apache-airflow-202.md)
  + [Connections](t-apache-airflow-202.md#troubleshooting-conn-202)
    + [I can't connect to Secrets Manager](t-apache-airflow-202.md#access-secrets-manager-202)
    + [How do I configure `secretsmanager:ResourceTag/<tag-key>` secrets manager conditions or a resource restriction in my execution role policy?](t-apache-airflow-202.md#access-secrets-manager-condition-keys-202)
    + [I can't connect to Snowflake](t-apache-airflow-202.md#missing-snowflake)
    + [I can't see my connection in the Airflow UI](t-apache-airflow-202.md#connection-type-missing)
  + [Web server](t-apache-airflow-202.md#troubleshooting-webserver-202)
    + [I see a 5xx error accessing the web server](t-apache-airflow-202.md#5xx-webserver-202)
    + [I see a 'The scheduler does not appear to be running' error](t-apache-airflow-202.md#error-scheduler-202)
  + [Tasks](t-apache-airflow-202.md#troubleshooting-tasks-202)
    + [I see my tasks stuck or not completing](t-apache-airflow-202.md#stranded-tasks-202)
  + [CLI](t-apache-airflow-202.md#troubleshooting-cli-202)
    + [I see a '503' error when triggering a DAG in the CLI](t-apache-airflow-202.md#cli-toomany-202)
    + [Why does the `dags backfill` Apache Airflow CLI command fail? Is there a workaround?](t-apache-airflow-202.md#troubleshooting-cli-backfill)
  + [Operators](t-apache-airflow-202.md#troubleshooting-operators-202)
    + [I received a `PermissionError: [Errno 13] Permission denied` error using the S3Transform operator](t-apache-airflow-202.md#op-s3-transform)
+ [Troubleshooting: DAGs, Operators, Connections, and other issues in Apache Airflow v1](t-apache-airflow-11012.md)
  + [Updating requirements\.txt](t-apache-airflow-11012.md#troubleshooting-dependencies)
    + [Adding `apache-airflow-providers-amazon` causes my environment to fail](t-apache-airflow-11012.md#t-requirements)
  + [Broken DAG](t-apache-airflow-11012.md#troubleshooting-broken-dags)
    + [I received a 'Broken DAG' error when using Amazon DynamoDB operators](t-apache-airflow-11012.md#missing-boto)
    + [I received 'Broken DAG: No module named psycopg2' error](t-apache-airflow-11012.md#missing-postgres-library)
    + [I received a 'Broken DAG' error when using the Slack operators](t-apache-airflow-11012.md#missing-slack)
    + [I received various errors installing Google/GCP/BigQuery](t-apache-airflow-11012.md#missing-bigquery-cython)
    + [I received 'Broken DAG: No module named Cython' error](t-apache-airflow-11012.md#broken-cython)
  + [Operators](t-apache-airflow-11012.md#troubleshooting-operators)
    + [I received an error using the BigQuery operator](t-apache-airflow-11012.md#bigquery-operator-ui)
  + [Connections](t-apache-airflow-11012.md#troubleshooting-connections)
    + [I can't connect to Snowflake](t-apache-airflow-11012.md#missing-snowflake)
    + [I can't connect to Secrets Manager](t-apache-airflow-11012.md#access-secrets-manager)
    + [I can't connect to my MySQL server on '<DB\-identifier\-name>\.cluster\-id\.<region>\.rds\.amazonaws\.com'](t-apache-airflow-11012.md#mysql-server)
  + [Web server](t-apache-airflow-11012.md#troubleshooting-web-server)
    + [I'm using the BigQueryOperator and it's causing my web server to crash](t-apache-airflow-11012.md#operator-biquery)
    + [I see a 5xx error accessing the web server](t-apache-airflow-11012.md#5xx-webserver)
    + [I see a 'The scheduler does not appear to be running' error](t-apache-airflow-11012.md#error-scheduler-11012)
  + [Tasks](t-apache-airflow-11012.md#troubleshooting-tasks)
    + [I see my tasks stuck or not completing](t-apache-airflow-11012.md#stranded-tasks)
  + [CLI](t-apache-airflow-11012.md#troubleshooting-cli-11012)
    + [I see a '503' error when triggering a DAG in the CLI](t-apache-airflow-11012.md#cli-toomany-11012)
+ [Troubleshooting: Creating and updating an Amazon MWAA environment](t-create-update-environment.md)
  + [Updating `requirements.txt`](t-create-update-environment.md#troubleshooting-reqs)
    + [I specified a new version of my `requirements.txt` and it's taking more than 20 minutes to update my environment](t-create-update-environment.md#t-requirements)
  + [Plugins](t-create-update-environment.md#troubleshooting-plugins)
    + [Does Amazon MWAA support implementing custom UI?](t-create-update-environment.md#custom-ui)
    + [I am able to implement custom UI changes on the [Amazon MWAA local runner](https://github.com/aws/aws-mwaa-local-runner) via plugins, yet when I try to do the same on Amazon MWAA, I do not see my changes nor any errors\. Why is this happening?](t-create-update-environment.md#custom-ui-local-runner)
  + [Create bucket](t-create-update-environment.md#troubleshooting-create-bucket)
    + [I can't select the option for S3 Block Public Access settings](t-create-update-environment.md#t-create-bucket)
  + [Create environment](t-create-update-environment.md#troubleshooting-create-environment)
    + [I tried to create an environment and it's stuck in the "Creating" state](t-create-update-environment.md#t-stuck-failure)
    + [I tried to create an environment but it shows the status as "Create failed"](t-create-update-environment.md#t-create-environ-failed)
    + [I tried to select a VPC and received a "Network Failure" error](t-create-update-environment.md#t-network-failure)
    + [I tried to create an environment and received a service, partition, or resource "must be passed" error](t-create-update-environment.md#t-service-partition)
    + [I tried to create an environment and it shows the status as "Available" but when I try to access the Airflow UI an "Empty Reply from Server" or "502 Bad Gateway" error is shown](t-create-update-environment.md#t-create-environ-empty-reply)
    + [I tried to create an environment and my user name is a bunch of random character names](t-create-update-environment.md#t-create-environ-random-un)
  + [Update environment](t-create-update-environment.md#troubleshooting-update-environment)
    + [I tried changing the environment class but the update failed](t-create-update-environment.md#t-rollback-billing-failure)
  + [Access environment](t-create-update-environment.md#troubleshooting-access-environment)
    + [I can't access the Apache Airflow UI](t-create-update-environment.md#t-no-access-airflow-ui)
+ [Troubleshooting: CloudWatch Logs and CloudTrail errors](t-cloudwatch-cloudtrail-logs.md)
  + [Logs](t-cloudwatch-cloudtrail-logs.md#troubleshooting-view-logs)
    + [I can't see my task logs or I received a 'Reading remote log from Cloudwatch log\_group' error](t-cloudwatch-cloudtrail-logs.md#t-task-logs)
    + [I see a 'ResourceAlreadyExistsException' error in CloudTrail](t-cloudwatch-cloudtrail-logs.md#t-cloudtrail)
    + [I see an 'Invalid request' error in CloudTrail](t-cloudwatch-cloudtrail-logs.md#t-cloudtrail-bucket)
    + [I see a 'Cannot locate a 64\-bit Oracle Client library: "libclntsh\.so: cannot open shared object file: No such file or directory' in Apache Airflow logs](t-cloudwatch-cloudtrail-logs.md#t-plugins-logs)
    + [I see psycopg2 'server closed the connection unexpectedly' in my Scheduler logs](t-cloudwatch-cloudtrail-logs.md#scheduler-postgres-library)
    + [I see 'Executor reports task instance %s finished \(%s\) although the task says its %s' in my DAG processing logs](t-cloudwatch-cloudtrail-logs.md#long-running-tasks)
    + [I see 'Could not read remote logs from log\_group: airflow\-\*\{\*environmentName\}\-Task log\_stream:\* \{\*DAG\_ID\}/\*\{\*TASK\_ID\}/\*\{\*time\}/\*\{\*n\}\.log\.' in my task logs](t-cloudwatch-cloudtrail-logs.md#t-task-fail-permission)