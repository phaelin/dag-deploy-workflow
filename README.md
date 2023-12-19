# Basic DAG Deployment Workflow

This workflow is used to automatically deploy Apache Airflow DAGs stored in the 
dags folder to an S3 bucket used by an Amazon MWAA environment whenever code is pushed to the main branch.

## Prerequisites
- An Amazon MWAA environment configured to use an S3 bucket as the source for DAGs. See the AWS documentation on [creating an MWAA environment](https://docs.aws.amazon.com/mwaa/latest/userguide/create-environment.html).
- The S3 bucket ARN and DAGs folder path specified in the MWAA environment.
- The GitHub repository containing the DAG code.

## Workflow Jobs
The workflow contains a `DAG Validation` job as well as a `Deploy DAGs` job.

### Validation Job
This job calls a Custom GitHub Action called `DAG Validation Action` in order to run standard validation against the DAGs.
### Deploy Job
This job checks out the repository, installs dependencies, and uses the AWS CLI to sync the `dags` folder to the corresponding environment folder in S3.

## Secrets
The workflow requires the following secrets to be configured:

`AWS_ACCESS_KEY_ID` - AWS access key with permissions to upload to the S3 bucket.
`AWS_SECRET_ACCESS_KEY` - Corresponding AWS secret access key.
`S3_BUCKET` - the name of the S3 bucket to target for deployment.