# aws-rds-postgresql-database

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 3.5.0](https://img.shields.io/badge/AppVersion-3.5.0-informational?style=flat-square)

AWS RDS PostgreSQL database Helm chart for the [Terraform-operator](https://github.com/isaaguilar/terraform-operator).

## Prerequisites
```bash
helm repo add isaaguilar https://isaaguilar.github.io/helm-charts
helm repo update
helm upgrade --install terraform-operator isaaguilar/terraform-operator \
  --version v0.2.1 --namespace tf-system --create-namespace
```

<!-- ## Get Repo Info
```bash
helm repo add appvia-community https://...
helm repo update
``` -->

## Install Chart
```bash
helm install [RELEASE_NAME] [CHART] \
  --namespace [NAMESPACE] \
  --create-namespace \
  --set aws.region=[AWS_REGION] \
  --set aws.credentials=[AWS_CREDENTIALS] \
  --set rds.identifier=[RDS_IDENTIFIER] \
  --set rds.db_name=[RDS_DB_NAME] \
  --set rds.username=[RDS_DB_ADMIN] \
  --set rds.subnet_ids=[RDS_SUBNET_IDS] \
  --set rds.vpc_security_group_ids=[RDS_VPC_SECURITY_GROUPS]
```

## Upgrade Chart
```bash
helm upgrade --install [RELEASE_NAME] [CHART] \
  --namespace [NAMESPACE] \
  --create-namespace \
  --set aws.region=[AWS_REGION] \
  --set aws.credentials=[AWS_CREDENTIALS] \
  --set rds.identifier=[RDS_IDENTIFIER] \
  --set rds.db_name=[RDS_DB_NAME] \
  --set rds.username=[RDS_DB_ADMIN] \
  --set rds.subnet_ids=[RDS_SUBNET_IDS] \
  --set rds.vpc_security_group_ids=[RDS_VPC_SECURITY_GROUPS]
```

## Uninstall Chart
```bash
helm uninstall [RELEASE_NAME]
```


## Example Usage
```bash
helm upgrade --install aws-rds-postgresql-database . \
  --namespace my-ns \
  --set aws.region=eu-west-2 \
  --set rds.identifier=mydbinst \
  --set rds.db_name=mydb \
  --set rds.username=mydbadmin \
  --set "rds.subnet_ids={subnet-1c247675,subnet-49df4133,subnet-5971dc15}" \
  --set "rds.vpc_security_group_ids={sg-070ec2d06b4802b38}" \
  --set aws.credentials[0].secretNameRef.key=data,aws.credentials[0].secretNameRef.name=tf-aws-secrets,aws.credentials[0].secretNameRef.namespace=my-ns
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| aws.credentials | object | `{}` | The AWS credentials to be used for provisioning the RDS PostgreSQL database |
| aws.region | string | `""` | The AWS region where the RDS PostgreSQL database should be created |
| rds.allocated_storage | string | `"10"` | The allocated storage in gigabytes [MUTABLE]|
| rds.backup_retention_period | int | `0` | The days to retain backups for [MUTABLE]|
| rds.backup_window | string | `"03:00-06:00"` | The daily time range (in UTC) during which automated backups are created if they are enabled. Example: '09:46-10:16'. Must not overlap with maintenance_window [MUTABLE]|
| rds.create_db_option_group | bool | `false` | Specifies whether a database option group should be created [MUTABLE]|
| rds.create_db_parameter_group | bool | `false` | Specifies whether a database parameter group should be created [MUTABLE]|
| rds.create_random_password | bool | `true` | Specifies whether to create a random password for the master DB user [MUTABLE]|
| rds.db_name | string | `""` | The DB name to create. If omitted, no database is created initially [IMMUTABLE]|
| rds.engine | string | `"postgres"` | The database engine to use [IMMUTABLE]|
| rds.engine_version | string | `"13.4"` | The engine version to use [MUTABLE]|
| rds.family | string | `"postgres13"` | The family of the DB parameter group [MUTABLE]|
| rds.identifier | string | `""` | identifier	The name of the RDS instance, if omitted, Terraform will assign a random, unique identifier [IMMUTABLE]|
| rds.instance_class | string | `"db.t3.micro"` | The instance type of the RDS instance [MUTABLE]|
| rds.maintenance_window | string | `"Mon:00:00-Mon:03:00"` | The window to perform maintenance in. Syntax: 'ddd:hh24:mi-ddd:hh24:mi'. Eg: 'Mon:00:00-Mon:03:00' [MUTABLE]|
| rds.major_engine_version | string | `"13"` | Specifies the major version of the engine that this option group should be associated with [MUTABLE]|
| rds.port | int | `5432` | The port on which the DB accepts connections [MUTABLE]|
| rds.random_password_length | int | `12` | The length of the random password to create [MUTABLE]|
| rds.subnet_ids | string | `nil` | A list of VPC subnet IDs [MUTABLE]|
| rds.username | string | `""` | Username for the master DB user [MUTABLE]|
| rds.vpc_security_group_ids | list | `[]` | List of VPC security groups to associate [MUTABLE]|
| terraform.module | string | `"https://github.com/terraform-aws-modules/terraform-aws-rds.git"` | The HashiCorp official Terraform module |
| terraform.moduleVersion | string | `"v3.5.0"` | The version of the Terraform module used to create an RDS PostgreSQL database |
| terraform.version | string | `"1.1.4"` | The version of Terraform used |

:warning: A change to an `IMMUTABLE` parameter after initial creation will force a re-creation of the AWS RDS PostgreSQL database. However a `MUTABLE` parameter is a configurable option by design and can be changed.

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.7.0](https://github.com/norwoodj/helm-docs/releases/v1.7.0)
