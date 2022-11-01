---
title: AWS Terraform Deployment with Docker
date: "2022-10-31"
description: "Using Terraform Infrastrucure as a Code with Docker"
---

Head over to the link below to access the Module. Run the steps below on how to deploy Terraform AWS with Docker
https://developer.hashicorp.com/terraform/tutorials/aws-get-started/infrastructure-as-code


In the "Code Editor" tab, open the main.tf file.

Copy and paste the following configuration. Save your changes by clicking on the icon next to the filename above the editor window.

terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.15.0"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "tutorial"
  ports {
    internal = 80
    external = 8000
  }
}
In the "Terminal" tab, initialize the project, which downloads a plugin that allows Terraform to interact with Docker.

terraform init
Provision the NGINX server container with apply. When Terraform asks you to confirm, type yes and press ENTER.

terraform apply
Verify NGINX instance
Run docker ps to view the NGINX container running in Docker via Terraform.

docker ps
Destroy resources
To stop the container and destroy the resources created in this tutorial, run terraform destroy. When Terraform asks you to confirm, type yes and press ENTER.

terraform destroy
You have now provisioned and destroyed an NGINX webserver with Terraform.