# networking

## Overview

Terraform AWS module for creating VPCs with Public and Private subnets backed by NAT Gateway instances

## NOTES:

* If you are migrating from 1.x.x you need to have more EIPs than the AWS stock as the terraform apply is going to regenerate the NAT Gateways

## Usage

```
source        = "../../modules/tf-aws-vpc-with-dhcp-options"

cidr_block    = "${var.base_vpc_cidr_block}"
azs_list      = [ "us-east-1a", "us-east-1b" ]

tags          = {
  prefix                  = "${var.prefix["puppetpoc"]}"
  finance_region          = "${var.tags["finance_region"]}"
  finance_profitcenter_id = "${var.tags["finance_profitcenter_id"]}"
  finance_costcenter_id   = "${var.tags["finance_costcenter_id"]}"
}
```

## Inputs

| Name | Description | Default | Required |
|------|-------------|:-----:|:-----:|
| azs_list | List of Availability Zones (provides a way to specify the AZ where subnets will be created). | - | yes |
| cidr_block | CIDR block that the VPC should cover | - | yes |
| newbits | Number of bits that the CIDR should be extended with when creating subnets | `8` | no |
| enable_dns_support | Should DNS resolution be supported for the VPC | `true` | no |
| enable_dns_hostnames | Should instances launched inside the VPC be assigned DNS names | `true` | no |
| vpc_zone_name | The suffix domain name to use by default when resolving non Fully Qualified Domain Names | `""` | no |
| vpc_dns_server | DNS Server for the VPC | `"AmazonProvidedDNS"` | no |
| tags | A mapping of tags to assign to the resource | - | yes |

## Outputs

| Name | Description |
|------|-------------|
| availability_zones | List of the AZs that will be used |
| vpc_id | Identifier of the VPC created |
| vpc_cidr_block | CIDR block that the VPC covers |
| public_nat_gateways | Elastic IP addresses associated to the NAT gateways |
| public_subnet_ids | List of public subnets identifiers |
| private_subnet_ids | List of private subnets identifiers |
| public_subnets_cidr_blocks | List of public subnets CIDR blocks |
| private_subnets_cidr_blocks | List of private subnets CIDR blocks |
| public_route_table_id | Identifier of the route table used by all the public subnets |
| private_route_tables_ids | Identifier of the route table used by all the private subnets |
