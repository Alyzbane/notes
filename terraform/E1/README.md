Sure thing! Here's a raw markdown file for your Terraform beginner notes:

# Terraform Notes

## Initial Setup
```bash
terraform init     # Initialize a directory

terraform fmt      # Format your configuration
terraform validate # Syntactically valid and internally consistent
```

## Create Infrastructure
Using the written configuration.

```bash
terraform apply 
```
Before applying the configuration, it will print the `execution plan`, the output is similar to git with `+` and `known after apply`.

After updating the file with new configuration, just apply the same command.

## Destroying the Built Infrastructure
```bash
terraform destroy
```

## Variables
Terraform configurations can include variables to make your configuration more dynamic and flexible.

### Define Input Variables
Create a new file called `variables.tf` with a block defining a new variable.

```bash
variable "container_name" {
  description = "Value of the name for the Docker container"
  type        = string
  default     = "ExampleNginxContainer"
}
```

### Use Variables in Configuration
Update your main configuration file to use the new variable.

```diff
resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
- name = 'demo'
+ name  = var.container_name
  ports {
    internal = 80
    external = 8080
  }
}
```

> In Terraform, variables can be referenced across different files within the same directory.

### Apply Configuration with Variables
Apply the configuration, overriding the default variable value if needed.

```bash
terraform apply -var "container_name=YetAnotherName"
```

## Outputs
Terraform can output values to help you understand the state of your infrastructure.

### Define Output Values
Create a new file called `outputs.tf` with a block defining a new output value.

```bash
output "container_id" {
  description = "The ID of the Docker container"
  value       = docker_container.nginx.id
}
```

### View Output Values
After applying the configuration, view the output values.

```bash
terraform output
```

Feel free to customize it further to suit your needs! If you have any other questions or need more help, just let me know.