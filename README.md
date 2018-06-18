# Ansible role: AWS VPC Subnets

This role handles the creation of VPC subnets in AWS.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-subnet.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-subnet)
[![Version](https://img.shields.io/github/tag/Flaconi/ansible-role-aws-vpc-subnet.svg)](https://github.com/Flaconi/ansible-role-aws-vpc-subnet/tags)
[![Ansible Galaxy](https://img.shields.io/ansible/role/d/25921.svg)](https://galaxy.ansible.com/Flaconi/aws-vpc-subnet/)

## Requirements

* Ansible 2.5


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                               | Description                     |
|----------------------------------------|---------------------------------|
| `aws_vpc_subnet_profile`               | Boto profile name to be used    |
| `aws_vpc_subnet_default_region`        | Default region to use           |
| `aws_vpc_subnet_default_public`        | Default visibility of subnets   |
| `aws_vpc_subnet_vpc_filter_additional` | Additional `key` `val` filter to add to `vpc_filter` and `vpc_name` by default. |

## Example definition

#### Required parameter only

```yml
aws_vpc_subnets:
  # Create subnets for a VPC by VPC name
  - vpc_name: devops-test-vpc
    subnets:
      - name: subnet-1
        cidr: 172.29.1.0/24
      - name: subnet-2
        cidr: 172.29.2.0/24
  # Create subnets for a VPC by VPC filter
  - vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc"
    subnets:
      - name: subnet-1
        cidr: 172.29.1.0/24
      - name: subnet-2
        cidr: 172.29.2.0/24
```

#### All available parameter
```yml
aws_vpc_subnets:
  # Create subnets for a VPC by VPC name
  - vpc_name: devops-test-vpc
    region: eu-central-1
    subnets:
      - name: subnet-1
        cidr: 172.29.1.0./24
        az: a
        public: True
        tags:
          - key: env
            val: playground
          - key: department
            val: devops
      - name: subnet-2
        cidr: 172.29.2.0./24
        az: b
        public: True
        tags:
          - key: env
            val: playground
          - key: department
            val: devops
  # Create subnets for a VPC by VPC name
  - vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc"
      - key: "tag:env"
        val: playground
      - key: "tag:department"
        val: devops
    region: eu-central-1
    subnets:
      - name: subnet-1
        cidr: 172.29.1.0./24
        az: a
        public: True
        tags:
          - key: env
            val: playground
          - key: department
            val: devops
      - name: subnet-2
        cidr: 172.29.2.0./24
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


## Testing

#### Requirements

* Docker
* [yamllint](https://github.com/adrienverge/yamllint)

#### Run tests

```bash
# Lint the source files
make lint

# Run integration tests with default Ansible version
make test

# Run integration tests with custom Ansible version
make test ANSIBLE_VERSION=2.4
```
