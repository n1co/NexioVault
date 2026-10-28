dl site officiel, binaire dans /usr/bin ou path osef

la doc officielle merde sur les parametres statiques
faut utiliser genre gateway_id = "${}"



Déclaration du provider:

```
provider "aws" {

  region = "us-east-1"

}
```

#### Delete:
```shell
#Planifie la destruction des ressources et affiche ce qui sera supprimé 
terraform plan -destroy -out=destroy-plan # Applique la destruction des ressources 
terraform apply "destroy-plan"
```


KEY API:

Vocareum -> AWS Details

https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build

creer machine avec clé secgroup:

```hcl
terraform {

  required_providers {

    aws = {

      source  = "hashicorp/aws"

      version = "~> 4.16"

    }

  }

  

  required_version = ">= 1.2.0"

}

  

provider "aws" {

  region = "us-east-1"

}

  

resource "aws_instance" "app_server" {

  ami           = "ami-04b70fa74e45c3917"

  instance_type = "t2.micro"

  vpc_security_group_ids = ["sg-0505f40789fbc44be"]

  subnet_id              = "subnet-06dd4f43ff70ad888"

  key_name                    = "nr-c"

  tags = {

    Name = "HelloTF3"

  }

}
```




terraform plan -> planif

Create VPC:

```hcl
resource "aws_vpc" "main" {
 cidr_block = "10.0.0.0/16"
 
 tags = {
   Name = "Project VPC"
 }
}
```

Create SubNet (variables.tf):

```hcl
variable "public_subnet_cidrs" {
 type        = list(string)
 description = "Public Subnet CIDR values"
 default     = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
}
 
variable "private_subnet_cidrs" {
 type        = list(string)
 description = "Private Subnet CIDR values"
 default     = ["10.0.4.0/24", "10.0.5.0/24", "10.0.6.0/24"]
}
```

https://blog.stack-labs.com/code/terraform_deployer_infra_en_quelques_commandes/