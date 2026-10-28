variables.tf

```
#Nom de profil AWS
variable "profile" {
  #Valeur par dÃ©faut
  default = "default"
}

variable "ip" {
  #Sans valeur par dÃ©faut
}
```


vpc.tf

```
#CrÃ©ation d'une ressource "my-vpc" qui utilise des adresses ip en 192.168.0.0/24, donc de 
#192.168.0.0 Ã  192.168.0.254 (l'adresse 192.168.0.255 Ã©tant celle de broadcast).
resource "aws_vpc" "my-vpc" {
  cidr_block           = "192.168.0.0/24"
  #Desactiver les noms d'hÃ´tes DNS (false par dÃ©faut, redondant).
  enable_dns_hostnames = false
  #Activer le support DNS (true par dÃ©faut, redondant).
  enable_dns_support   = true
  #Gestion de l'instance, par dÃ©faut. Possible d'avoir un VPC "dedicated", mais nettement plus cher.
  instance_tenancy     = "default"

  #Tags, un systÃ¨me clÃ©:valeur au choix pour trier ses ressources.
  tags = {
    Name = "my-vpc"
  }
}

#CrÃ©ation d'une internet gateway pour garantir l'accÃ¨s internet depuis ce VPC
resource "aws_internet_gateway" "my-vpc-iwg" {
  #RÃ©fÃ©rence au nom du VPC
  vpc_id = aws_vpc.my-vpc.id

  tags = {
    Name = "my-vpc-iwg"
  }
}

#Ajout du subnet dÃ©sirÃ©
resource "aws_subnet" "my-vpc-subnet" {
  #A nouveau, le VPC dans lequel on crÃ©e le subnet. On prÃ©fÃ¨re une rÃ©fÃ©rence Ã  hard-coder le 
  #nom du VPC, ce qui rend les changements faciles.
  vpc_id                  = aws_vpc.my-vpc.id
  #Ce subnet prend tout l'espace CIDR du VPC
  cidr_block              = "192.168.0.0/24"
  #Permet de fixer l'availability zone utilisÃ©e, facultatif. 
  availability_zone       = "us-east-1a"
  #Ce paramÃ¨tre permet de faire en sorte qu'une instance lancÃ©e dans ce subnet n'a, par dÃ©faut, pas 
  #d'IP publique sauf si autrement spÃ©cifiÃ©.
  map_public_ip_on_launch = false

  tags = {
    Name = "my-vpc-subnet"
  }
}

#On crÃ©e une table de routage afin de garantir que les paquets soient envoyÃ©s sur internet
resource "aws_route_table" "my-vpc-routing-table" {
  #Il est bien sÃ»r possible de crÃ©er plusieurs routes
  route {
    #Tous les packets
    cidr_block = "0.0.0.0/0"
    #RedirigÃ©s vers l'internet gateway
    gateway_id = aws_internet_gateway.my-vpc-iwg.id
  }
  vpc_id = aws_vpc.my-vpc.id
  
  tags = {
    Name = "my-vpc-routing-table"
  }
}

#Une particularitÃ© de terraform. L'association se fait automatiquement par la console AWS  
#gÃ©nÃ©ralement, mais il est requis de la dÃ©clarer sur terraform.
resource "aws_route_table_association" "my-vpc-routing-table-association" {
  #On associe le subnet crÃ©Ã©...
  subnet_id      = aws_subnet.my-vpc-subnet.id
  #Avec la table de routage prÃ©cÃ©dente.
  route_table_id = aws_route_table.my-vpc-routing-table.id
}

#On crÃ©e une access control list pour le VPC (elle sera peu utile ici)
resource "aws_network_acl" "my-vpc-acl" {
  #Il est nÃ©cessaire d'y assigner le subnet et le VPC dÃ©sirÃ©
  vpc_id     = aws_vpc.my-vpc.id
  subnet_ids = [aws_subnet.my-vpc-subnet.id]

  #Permet de contrÃ´ler les entrÃ©es: AutorisÃ©es de tout port vers tout port, tout protocole, toute IP
  ingress {
    from_port  = 0
    to_port    = 0
    rule_no    = 100
    action     = "allow"
    protocol   = "-1"
    cidr_block = "0.0.0.0/0"
  }

  #Idem pour les sorties: Tout port, tout protocole, toute IP
  egress {
    from_port  = 0
    to_port    = 0
    rule_no    = 100
    action     = "allow"
    protocol   = "-1"
    cidr_block = "0.0.0.0/0"
  }

  tags = {
    Name = "my-vpc-acl"
  }
}
```



ec2.tf:

```
provider "aws" {
	region = "us-east-1"
}


#Permet de dÃ©clarer un group de sÃ©curitÃ© pour EC2, sans quoi il ne sera pas possible d'y accÃ©der
resource "aws_security_group" "my-security-group" {
  #Il est nÃ©cessaire de nommer le security group, mais optionnel de lui donner une description
  name        = "my-security-group"
  description = "Allow whitelisted IP in"
  #On rattache le security group au VPC crÃ©Ã© prÃ©cÃ©demment
  vpc_id      = aws_vpc.my-vpc.id

  #Sert Ã  dÃ©finir une rÃ¨gle d'entrÃ©e: L'accÃ¨s Ã  tous les ports, vers tous les ports, tous 
  #protocoles, est possible depuis un certain bloc CIDR
  ingress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    #Ceci est une variable! C'est un type particulier de rÃ©fÃ©rence que nous aborderons ensuite
    cidr_blocks = ["${var.ip}/32"]
  }

  ingress {
    from_port       = 22
    to_port         = 22
    protocol        = "tcp"
    security_groups = []
    self            = true
  }

  #Sert Ã  dÃ©finir une rÃ¨gle de sortie: Il est possible de sortir vers n'importe oÃ¹, tous protocoles
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

}

#CrÃ©ons maintenant notre premiÃ¨re instance EC2: le bastion
resource "aws_instance" "my-ec2-bastion" {
  #Cette AMI (amazon machine image) correspond Ã  Amazon Linux version 2 pour eu-west-1
  ami                         = "ami-08a0d1e16fc3f61ea"
  availability_zone           = "us-east-1a"
  ebs_optimized               = false
  #Les t2.micro sont les plus petites instances disponibles. L'avantage: elles rentrent dans 
  #le free tier de AWS.
  instance_type               = "t2.micro"
  #Inutile de surveiller en dÃ©tail l'instance (et cela sort du free tier)
  monitoring                  = false
  #On utilise la clÃ© gÃ©nÃ©rÃ©e prÃ©cÃ©demment
  key_name                    = "nr-c"
  #L'instance est placÃ©e dans le subnet crÃ©Ã© prÃ©cÃ©demment
  subnet_id                   = aws_subnet.my-vpc-subnet.id
  #Et on utilise le security group qu'on a crÃ©Ã©
  vpc_security_group_ids      = [aws_security_group.my-security-group.id]
  #Comme on veut SSH dans l'instance depuis l'internet, il est nÃ©cessaire d'associer une IP publique
  associate_public_ip_address = true

  #Il faut un disque de dÃ©marrage pour l'instance. On choisit un disque de la taille minimale (8GB), 
  #effacÃ© ors de l'arrÃªt de l'instance, et de type gp2, c'est Ã  dire "general purpose SSD". La 
  #valeur par dÃ©faut Ã©tant "standard", ce qui correspond Ã  un disque magnÃ©tique, on prÃ©fÃ¨re 
  #utiliser un SSD.
  root_block_device {
    volume_type           = "gp2"
    volume_size           = 8
    delete_on_termination = true
  }

}

#DerniÃ¨rement, crÃ©ons l'autre instance EC2 Ã  laquelle on veut accÃ©der Ã  travers le bastion
resource "aws_instance" "my-ec2-server" {
  ami                         = "ami-08a0d1e16fc3f61ea"
  availability_zone           = "us-east-1a"
  ebs_optimized               = false
  instance_type               = "t2.micro"
  monitoring                  = false
  key_name                    = "nr-c"
  subnet_id                   = aws_subnet.my-vpc-subnet.id
  vpc_security_group_ids      = [aws_security_group.my-security-group.id]
  #Puisque cette instance doit rester privÃ©e, on n'assigne pas d'IP publique
  associate_public_ip_address = false
  #Enfin, on peut Ã©galement assigner une IP privÃ©e fixÃ©e de maniÃ¨re Ã  SSH plus simplement.
  private_ip                  = "192.168.0.28"

  root_block_device {
    volume_type           = "gp2"
    volume_size           = 8
    delete_on_termination = true
  }

  #Permet de spÃ©cifier un script de dÃ©marrage. Ici, pour l'exemple, on peut Ã©crire un fichier 
  #dans /home/ec2-user
  user_data = <<-EOF
	#!/bin/bash
  echo "Hello!" > hello.txt
	EOF
}
```
