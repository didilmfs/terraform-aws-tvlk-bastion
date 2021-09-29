# terraform-aws-tvlk-bastion


[![Terraform Version](https://img.shields.io/badge/Terraform%20Version->=0.12.0,<=0.12.31-blue.svg)](https://releases.hashicorp.com/terraform/)
[![Release](https://img.shields.io/github/release/traveloka/terraform-aws-tvlk-bastion.svg)](https://github.com/traveloka/terraform-aws-tvlk-bastion/releases)
[![Last Commit](https://img.shields.io/github/last-commit/traveloka/terraform-aws-tvlk-bastion.svg)](https://github.com/traveloka/terraform-aws-tvlk-bastion/commits/master)
[![Issues](https://img.shields.io/github/issues/traveloka/terraform-aws-tvlk-bastion.svg)](https://github.com/traveloka/terraform-aws-tvlk-bastion/issues)
[![Pull Requests](https://img.shields.io/github/issues-pr/traveloka/terraform-aws-tvlk-bastion.svg)](https://github.com/traveloka/terraform-aws-tvlk-bastion/pulls)
[![License](https://img.shields.io/github/license/traveloka/terraform-aws-tvlk-bastion.svg)](https://github.com/traveloka/terraform-aws-tvlk-bastion/blob/master/LICENSE)
![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.png?v=103)

## Description

Terraform module to create ASG bastion host using ssm session manager on top of golden bastion AMI baked by site-infra team.
This module creates following resources:
* [aws_autoscaling_group](https://www.terraform.io/docs/providers/aws/r/autoscaling_group.html).
To stop or start an instances, you can change the asg_capacity value.
* [aws_launch_template](https://www.terraform.io/docs/providers/aws/r/launch_template.html).
* [aws_security_group](https://www.terraform.io/docs/providers/aws/r/security_group.html).
Several security group will be created by this module, to give access from this bastion, you need to attach the share security group to your database.

## Table of Content
* [terraform-aws-tvlk-bastion](#terraform-aws-tvlk-bastion)
   * [Description](#description)
   * [Table of Content](#table-of-content)
   * [Prerequisites](#prerequisites)
   * [Dependencies](#dependencies)
   * [Terraform Versions](#terraform-versions)
   * [Requirements](#requirements)
   * [Providers](#providers)
   * [Modules](#modules)
   * [Resources](#resources)
   * [Inputs](#inputs)
   * [Outputs](#outputs)
   * [Authors](#authors)
   * [Contributing](#contributing)
   * [License](#license)

## Prerequisites
* An existing vpc.
* An existing subnet, recommended using private subnet.
* IAM Policy to grants access to use session manager and send logs to s3.

## Dependencies

This Terraform module uses another Terraform module, here is the list of Terraform module dependencies:

* [traveloka/terraform-aws-autoscaling](https://github.com/traveloka/terraform-aws-autoscaling)
* [traveloka/terraform-aws-iam-role](https://github.com/traveloka/terraform-aws-iam-role)


## Terraform Versions

This module was created on 16/10/2018.
The latest stable version of Terraform which this module tested working is Terraform 0.12.31 on 29/09/2021.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_aws-autoscaling_bastion_asg"></a> [aws-autoscaling\_bastion\_asg](#module\_aws-autoscaling\_bastion\_asg) | github.com/traveloka/terraform-aws-autoscaling | v0.3.4 |
| <a name="module_bastion"></a> [bastion](#module\_bastion) | github.com/traveloka/terraform-aws-iam-role.git//modules/instance | v2.0.2 |

## Resources

| Name | Type |
|------|------|
| [aws_iam_role_policy.policy_dynamodb_access](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy) | resource |
| [aws_security_group.bastion](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group.elasticsearch](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group.memcached](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group.mongod](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group.mysql](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group.postgres](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group.redis](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group_rule.bastion_http_all](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.bastion_https_all](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.bastion_ssh_all](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.egress_from_bastion_to_elasticsearch_443](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.egress_from_bastion_to_memcached_11211](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.egress_from_bastion_to_mongod_27017](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.egress_from_bastion_to_mysql_3306](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.egress_from_bastion_to_postgres_5432](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.egress_from_bastion_to_redis_6379](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_from_bastion_to_elasticsearch_443](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_from_bastion_to_memcached_11211](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_from_bastion_to_mongod_27017](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_from_bastion_to_mysql_3306](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_from_bastion_to_postgres_5432](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_security_group_rule.ingress_from_bastion_to_redis_6379](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule) | resource |
| [aws_ami.bastion_ami](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ami) | data source |
| [aws_caller_identity.aws_account](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity) | data source |
| [aws_iam_policy_document.dynamodb_access](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_region.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/region) | data source |
| [aws_subnet_ids.subnet](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnet_ids) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_additional_asg_tags"></a> [additional\_asg\_tags](#input\_additional\_asg\_tags) | The created ASG (and spawned instances) will have these tags, merged over the default | `list(map(string))` | `[]` | no |
| <a name="input_ami_name_prefix"></a> [ami\_name\_prefix](#input\_ami\_name\_prefix) | prefix for ami filter | `string` | `"tvlk/ubuntu-20/tsi/bastion*"` | no |
| <a name="input_ami_owner_account_id"></a> [ami\_owner\_account\_id](#input\_ami\_owner\_account\_id) | aws account id who owns the golden bastion AMI owner. | `string` | n/a | yes |
| <a name="input_asg_capacity"></a> [asg\_capacity](#input\_asg\_capacity) | capacity of ec2 instances for autoscaling group | `string` | n/a | yes |
| <a name="input_asg_default_cooldown"></a> [asg\_default\_cooldown](#input\_asg\_default\_cooldown) | Time, in seconds, the minimum interval of two scaling activities | `string` | `"300"` | no |
| <a name="input_asg_health_check_grace_period"></a> [asg\_health\_check\_grace\_period](#input\_asg\_health\_check\_grace\_period) | Time, in seconds, to wait for new instances before checking their health | `string` | `"300"` | no |
| <a name="input_asg_health_check_type"></a> [asg\_health\_check\_type](#input\_asg\_health\_check\_type) | healthchek type for autoscaling group | `string` | `"EC2"` | no |
| <a name="input_asg_wait_for_capacity_timeout"></a> [asg\_wait\_for\_capacity\_timeout](#input\_asg\_wait\_for\_capacity\_timeout) | A maximum duration that Terraform should wait for ASG instances to be healthy before timing out | `string` | `"0m"` | no |
| <a name="input_description"></a> [description](#input\_description) | description for this cluster | `string` | n/a | yes |
| <a name="input_ebs_optimized"></a> [ebs\_optimized](#input\_ebs\_optimized) | whether ec2 instance using ebs optimized or not | `string` | `"false"` | no |
| <a name="input_enable_detailed_monitoring"></a> [enable\_detailed\_monitoring](#input\_enable\_detailed\_monitoring) | wheter to enable detailed monitoring for ec2 instances or not | `string` | `"false"` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | environment for this resources. | `string` | n/a | yes |
| <a name="input_instance_type"></a> [instance\_type](#input\_instance\_type) | instance type for bastion hosts. | `string` | `"t2.medium"` | no |
| <a name="input_launch_template_overrides"></a> [launch\_template\_overrides](#input\_launch\_template\_overrides) | List of nested arguments provides the ability to specify multiple instance types. See https://www.terraform.io/docs/providers/aws/r/autoscaling_group.html#override<br>  When using plain launch template, the first element's instance\_type will be used as the launch template instance type. | `list(map(string))` | <pre>[<br>  {<br>    "instance_type": "t3a.nano"<br>  },<br>  {<br>    "instance_type": "t3.nano"<br>  }<br>]</pre> | no |
| <a name="input_mixed_instances_distribution"></a> [mixed\_instances\_distribution](#input\_mixed\_instances\_distribution) | Specify the distribution of on-demand instances and spot instances. See https://docs.aws.amazon.com/autoscaling/ec2/APIReference/API_InstancesDistribution.html | `map(string)` | <pre>{<br>  "on_demand_allocation_strategy": "prioritized",<br>  "on_demand_base_capacity": "0",<br>  "on_demand_percentage_above_base_capacity": "100",<br>  "spot_allocation_strategy": "lowest-price",<br>  "spot_instance_pools": "2",<br>  "spot_max_price": ""<br>}</pre> | no |
| <a name="input_product_domain"></a> [product\_domain](#input\_product\_domain) | product domain who own this ec2 instances. | `string` | n/a | yes |
| <a name="input_service_name"></a> [service\_name](#input\_service\_name) | service name for the instance | `string` | n/a | yes |
| <a name="input_subnet_tier"></a> [subnet\_tier](#input\_subnet\_tier) | tier of subnet where bastion ec2 instance reside, we recommend to use the subnet with tier app, as it is private. | `string` | `"app"` | no |
| <a name="input_user_data"></a> [user\_data](#input\_user\_data) | The spawned instances will have this user data. Use the rendered value of a terraform's `template_cloudinit_config` data | `string` | `" "` | no |
| <a name="input_volume_size"></a> [volume\_size](#input\_volume\_size) | size for root volume instances. | `string` | `"8"` | no |
| <a name="input_volume_type"></a> [volume\_type](#input\_volume\_type) | type of ebs volume for root volume instances. | `string` | `"gp3"` | no |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | vpc id where ec2 instances reside. | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_asg_bastion_name"></a> [asg\_bastion\_name](#output\_asg\_bastion\_name) | The name of the auto scaling group for bastion |
| <a name="output_instance_role_name"></a> [instance\_role\_name](#output\_instance\_role\_name) | role name for the instances. |
| <a name="output_sg_bastion_id"></a> [sg\_bastion\_id](#output\_sg\_bastion\_id) | id of security group for bastion instance. |
| <a name="output_shared_sg_elasticsearch_id"></a> [shared\_sg\_elasticsearch\_id](#output\_shared\_sg\_elasticsearch\_id) | id of shared security group for elasticsearch. |
| <a name="output_shared_sg_memcached_id"></a> [shared\_sg\_memcached\_id](#output\_shared\_sg\_memcached\_id) | id of shared security group for memcached. |
| <a name="output_shared_sg_mongod_id"></a> [shared\_sg\_mongod\_id](#output\_shared\_sg\_mongod\_id) | id of shared security group for mongod. |
| <a name="output_shared_sg_mysql_id"></a> [shared\_sg\_mysql\_id](#output\_shared\_sg\_mysql\_id) | id of shared security group for mysql. |
| <a name="output_shared_sg_postgres_id"></a> [shared\_sg\_postgres\_id](#output\_shared\_sg\_postgres\_id) | id of shared security group for postgres. |
| <a name="output_shared_sg_redis_id"></a> [shared\_sg\_redis\_id](#output\_shared\_sg\_redis\_id) | id of shared security group for redis. |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Authors
* [Bernard Siahaan](https://github.com/SiahaanBernard)

## Contributing

This module accepting or open for any contributions from anyone, please see the [CONTRIBUTING.md](https://github.com/traveloka/terraform-aws-tvlk-bastion/blob/master/CONTRIBUTING.md) for more detail about how to contribute to this module.

## License

This module is under Apache License 2.0 - see the [LICENSE](https://github.com/traveloka/terraform-aws-tvlk-bastion/blob/master/LICENSE) file for details.
