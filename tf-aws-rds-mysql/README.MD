# terraform-aws-rds-mysql

Terraform module which creates MySQL RDS resources on AWS.

## Description

Provision [RDS DB Instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.html),
[Option Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithOptionGroups.html) and
[Parameter Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithParamGroups.html).

This module provides recommended settings:

- Enable deletion protection
- Enable Multi-AZ
- Enable encryption
- Enable IAM database authentication
- Enable automated backups
- Sufficient backup retention period
- Disable publicly accessible

### Minimum

```hcl
module "rds_mysql" {
  source            = "https://github.com/tal-lightlytics/eks-sops-demo/tree/main/tf-aws-rds-mysql"
  identifier        = "your-identifier"
  engine_version    = "5.7.28"
  instance_class    = "db.t2.small"
  allocated_storage = 20
  username          = "your-username"
  password          = "your-password!"
  subnet_ids         = var.subnets
  vpc_id             = var.vpc_id
  source_cidr_blocks = var.source_cidr_blocks
}
```

### Complete

```hcl
module "rds_mysql" {
  source            = "https://github.com/tal-lightlytics/eks-sops-demo/tree/main/tf-aws-rds-mysql"
  identifier        = "your-identifier"
  engine_version    = "5.7.28"
  instance_class    = "db.t2.small"
  allocated_storage = 20
  username          = "your-username"
  password          = "your-password!"
  subnet_ids         = var.subnets
  vpc_id             = var.vpc_id
  source_cidr_blocks = var.source_cidr_blocks

  maintenance_window                  = "mon:10:10-mon:10:40"
  backup_window                       = "09:10-09:40"
  apply_immediately                   = false
  multi_az                            = false
  port                                = 3306
  name                                = "example"
  storage_type                        = "gp2"
  iops                                = 0
  auto_minor_version_upgrade          = false
  allow_major_version_upgrade         = false
  backup_retention_period             = 0
  storage_encrypted                   = false
  kms_key_id                          = ""
  deletion_protection                 = false
  final_snapshot_identifier           = "final-snapshot"
  skip_final_snapshot                 = true
  enabled_cloudwatch_logs_exports     = []
  monitoring_interval                 = 0
  monitoring_role_arn                 = ""
  iam_database_authentication_enabled = false
  copy_tags_to_snapshot               = false
  publicly_accessible                 = true
  license_model                       = "general-public-license"
  major_engine_version                = "5.7"
  description                         = "This is example"

  tags = {
    Environment = "production"
  }
}
```
### Configure environment variables

```shell
export AWS_ACCESS_KEY_ID=XXXXXXXXXXXXXXXXX
export AWS_SECRET_ACCESS_KEY=XXXXXXXXXXXXXXXXXXXXXXXX
export AWS_DEFAULT_REGION=us-east-1
```

### Creation

```shell
terraform init 
terraform apply 
```

