# Ansible role: AWS VPC Subnets

This role handles the creation of VPC subnets in AWS.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-subnet.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-subnet)

## Requirements

* Ansible 2.5


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable              | Description                     |
|-----------------------|---------------------------------|
| `aws_vpc_subnet_profile` | Boto profile name to be used |


## Example definition

#### Required parameter only

```yml
aws_vpc_subnets:
  - vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc"
    subnets:
      - cidr: 172.29.1.0/24
      - cidr: 172.29.2.0/24
```

#### All available parameter
```yml
aws_vpc_subnets:
  - vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc"
      - key: "tag:env"
        val: playground
      - key: "tag:department"
        val: devops
    region: eu-central-1
    subnets:
      - cidr: 172.29.1.0./24
        az: a
        public: True
        tags:
          - key: Name
            val: devops-test-subnet-a
          - key: env
            val: playground
          - key: department
            val: devops
      - cidr: 172.29.2.0./24
        az: b
        public: True
        tags:
          - key: Name
            val: devops-test-subnet-b
          - key: env
            val: playground
          - key: department
            val: devops
```
