# Professional Resume Site Deployment
Professional WordPress Website running Docker Containers, Wordpress, Nginx, MySQL, &amp; Certbot

The files in this repository were used to configure the network depicted below.

![images/Topology.PNG]

These files have been used to generate a Wordpress website on Linode.   

| Script Name             | Script Description                                      |
|-------------------------|---------------------------------------------------------|
| docker-compose.yml      | Playbook used to create all docker containers           |
| .dockerignore           | File used to exclude files from uploading to containers |
| .env                    | File used to store MySQL variables                      |
| .gitignore              | File used to exclude files from GitHub                  |
| nginx-config/nginx.conf | nginx configuration file                                |
| ssh_renewal.sh          | Certbot certificate renewal script                      |

This document contains the following details:
- Description of the Topology
- Access Policies
- Using Docker Compose

### Description of the Topology

The main purpose of this network is to utilize containers to separate the functions of a Wordpress installation on a cost effective platform.

I used docker-compose to deploy multiple containers.  This simplified the sped up the setup process, compared to installing all the necessary compoents individualy.  

| Name      | Function            | External IP   | Operating System |
|-----------|---------------------|---------------|------------------|
| Web01     | Container Host      | 170.187.148.4 | Ubuntu 21.04     |
| webserver | Webserver           | 170.187.148.4 | Alpine v3.9      |
| wordpress | Wordpress server    | 170.187.148.4 | Alpine v3.9      |
| db        | Database server     |               | Alpine v3.9      |
| certbot   | Certificate Renewal |               | Debian 10        |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only Web01, and the Webserver can accept connections from the Internet.  Access to this machien is only allowed from the management machine.

Machines within the internal network can be accessed from Web01 via docker exec.  A summary of the access polices in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Address          |
|-----------|---------------------|-----------------------------|
| Web01     | Container Host      | 170.187.148.4 -> SSH        |
| webserver | Webserver           | 170.187.148.4 -> HTTP/HTTPS |
| wordpress | Webserver           | webserver -> HTTPS          |
| db        | Database server     | wordpress -> MySQL          |
| certbot   | Certificate Renewal | webserver <-> HTTP          |

### Using Docker Compose
In order to use docker-compose, it must be installed along with Docker on the container host.  I am assuming you already have a domain and DNS specified, as well as a subscription created on Linode.

SSH into Web01, and follow the steps below:
- Review the following files docker-compose.yml, .dockerignore, .env, .gitignore, ssh_renewal.sh, nginx.conf and customize them to your installation
- Create a directory /root/wordpress
- Copy docker-compose.yml, .dockerignore, .env, .gitignore, ssh_renewal.sh, nginx-config/nginx.conf
- Run docker-compose up
- Check website at http://YourEXTIP













# prof-resume-site
