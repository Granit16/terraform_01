# Домашнее задание к занятию «Введение в Terraform»

<details><summary>Чек-лист готовности к домашнему заданию</summary>


   1. Версия Terraform
      
   ![](https://github.com/Granit16/terraform_01/blob/main/screenshots/terraform_version.png)

      
   2. Копия git-репозитория выполнена
   
   ![](https://github.com/Granit16/terraform_01/blob/main/screenshots/git.png)

      
   3. Версия Docker

   ![](https://github.com/Granit16/terraform_01/blob/main/screenshots/docker_version.png)

</details>



<details><summary>Задание 1</summary>
   
   Cекретное содержимое созданного ресурса **random_password**:
   
   
   ```"result": "AYPtqdoMSKtwHD09"```
   
   Исправленный фрагмент кода:
   ```
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string.result}"

  ports {
    internal = 80
    external = 9090
  }
```


   
   Вывод команды `docker ps`:
```
damir@terraform:~/ter-homeworks/01/src$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS         PORTS                  NAMES
49ff85206f0e   a72860cb95fd   "/docker-entrypoint.…"   17 seconds ago   Up 3 seconds   0.0.0.0:9090->80/tcp   example_AYPtqdoMSKtwHD09
```

Опция -auto-approve нужна чтобы создавать объекты без дополнительного подтверждения, что в некоторых случая помогает автоматизировать развертывание инфраструктуры, но из-за обхода проверки, упускается возможность проверки изменений до их применения, что может привести к непреднамеренным изменениям в вашей инфраструктуре.

   Вывод команды `docker ps` после изменения имени контейнера в коде и выполнения команды `terraform apply -auto-approve`:
```
damir@terraform:~/ter-homeworks/01/src$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                  NAMES
a3905d226e24   a72860cb95fd   "/docker-entrypoint.…"   40 seconds ago   Up 38 seconds   0.0.0.0:9090->80/tcp   hello_world
```

После выполнения команды `terrform destroy` файл tarraform.tfstate выглядит следующим образом:
```
{
  "version": 4,
  "terraform_version": "1.8.5",
  "serial": 11,
  "lineage": "6010e595-8b45-961a-ce01-36a923c2ec37",
  "outputs": {},
  "resources": [],
  "check_results": null
}
```

</details>



<details><summary>Задание 2</summary>

</details>



<details><summary>Задание 3</summary>

</details>
