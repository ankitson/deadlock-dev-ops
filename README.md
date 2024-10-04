# Devops tooling for deadlock-dev

This repo holds the operations related tooling for the deadlock-dev project. Right now, it creates an instance on Hetzner Cloud with Docker installed using Terraform.

## Dependencies

- [Terraform](https://developer.hashicorp.com/terraform/install?product_intent=terraform)

## Setup

- Install dependencies above

- Generate an API key from your Hetzner cloud console. Create a new file named `secrets.auto.tfvars` containing the API token like this:
```
hcloud_token = "<token here>"
```

- Create a `keys` folder, and put the private SSH key in `keys/deadlock.pem` with `600` permissions.

- Run `terraform init` to setup terraform and install the hetzner providers

## Usage

To bring up an instance and connect to it:

```
> terraform plan
> terraform apply
...
Outputs:

server_ip = "<server_ip>"
server_status = "running"
ssh_command = "ssh -o StrictHostKeyChecking=no -i keys/deadlock.pem dev@<server_ip>"
> ssh -o StrictHostKeyChecking=no -i keys/deadlock.pem dev@<server_ip>
```

To destroy the instance:
```
terraform destroy
```
