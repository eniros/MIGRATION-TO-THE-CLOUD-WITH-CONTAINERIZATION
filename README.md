# MIGRATION-TO-THE-CLOUD-WITH-CONTAINERIZATION
MIGRATION TO THE СLOUD WITH CONTAINERIZATION

Until now, we have been using VMs (AWS EC2) in Amazon Virtual Private Cloud (AWS VPC) to deploy your web solutions, and it works well in many cases.

We have learned how easy to spin up and configure a new EC2 manually or with such tools as Terraform and Ansible to automate provisioning and configuration.

We have also deployed two different websites on the same VM; this approach is scalable, but to some extent; imagine what if you need to deploy many small applications (it can be web front-end, web-backend, processing jobs, monitoring, logging solutions, etc.) and some of the applications will require various OS and runtimes of different versions and conflicting dependencies – in such case you would need to spin up serves for each group of applications with the exact OS/runtime/dependencies requirements. When it scales out to tens/hundreds and even thousands of applications (e.g., when we talk of microservice architecture), this approach becomes very tedious and challenging to maintain.

In this project, we will learn how to solve this problem and practice the technology that revolutionized application distribution and deployment back in 2013! We are talking of Containers and imply Docker. Even though there are other application containerization technologies, Docker is the standard and the default choice for shipping your app in a container!

Section 1: Deploying Application Using Docker

1. Install Docker in your ubuntu instance by running the command;
```sudo snap install docker```
<img width="561" alt="Screenshot 2022-12-22 at 18 15 11" src="https://user-images.githubusercontent.com/61475969/209200263-703174d1-ac5b-4a36-af4c-34cc63096be6.png">


2. We can now pull the mysql image from the dockerhub repository(public) into our local server machine.

<img width="561" alt="Screenshot 2022-12-22 at 18 19 21" src="https://user-images.githubusercontent.com/61475969/209200298-88449421-0bd9-42e2-8634-d533607cc166.png">

We run a container from this image and setup the mysqldb environment variables with the following command;

```sudo docker run --name <container_name> -e MYSQL_ROOT_PASSWORD=<my-secret-pw> -d mysql/mysql-server:latest```

<img width="573" alt="Screenshot 2022-12-22 at 18 22 44" src="https://user-images.githubusercontent.com/61475969/209201865-246ad07b-c2db-45fd-aab9-fd7aa10f3e01.png">

To check the status of the container created, run the command;
``` sudo docker ps -a```

<img width="573" alt="Screenshot 2022-12-22 at 18 25 25" src="https://user-images.githubusercontent.com/61475969/209202279-0c8777d8-2067-48ac-aa6c-1b2f9662ebd7.png">

SECTION 2:CONNECTING TO THE MYSQL DOCKER CONTAINER

We can either connect directly to the container running the MySQL server or use a second container as a MySQL client. Let us see what the first option looks like.

Method 1

Connecting directly to the container running the MySQL server. We can use the following commands to achieve this;

```
$ docker exec -it mysql bash

or

$ docker exec -it mysql mysql -uroot -p
```
ERROR whilst connecting below;
<img width="756" alt="Screenshot 2022-12-22 at 18 36 53" src="https://user-images.githubusercontent.com/61475969/209203870-f27a84bf-adda-49d4-9f5b-23f7f04d1154.png">

To resolve this error,the following command was ran to start the container;

``` sudo docker container start --attach -i mysql_db```



