# DESPLIEGUE


Vamos a utilizar terraform.
Lo primero es habilitar los proveedores, desde la carpeta donde se encuentra terraform

```
cd iac
```

```
terraform init
```

Luego de habilitar los proovedores procedemos a configurar nuestros docker_containers en Terraform, en este caso:
 - api.tf
 - web.tf
 - bd.tf

 Verificamos que nuestro plan de Terraform este correcto y completo con el comando:
 
```
terraform plan
```

Si todo esta correcto ponemos el comando:
```
terraform apply 
```

Nos pedira una confirmacion:
```
yes
```

Si todo sale bien nos saldra: Apply complete! 

Ahora pasamos al tema de variables:

terraform.tfvars:
web_port={
    localhost = 4001
    dev = 5001
}
api_port={
    localhost = 4002
    dev = 5002
}

db_port={
    localhost = 4003
    dev = 5003
}

Luego de configurar nuestras variables procedemos a crear el networking:

network.tf
resource "docker_network" "app_network" {
  name = "app_network"
}

refactorizamos nuestros archivos api.tf, web.tf y db.tf añadiendo:
networks_advanced {
    name = docker_network.app_network.name
  }

Luego podemos hacer un terraform destroy y luego terraform apply para asegurarnos que todo este bien

Comandos importantes:

terraform workspace select
terraform apply
terraform destroy
docker ps
docker build 

