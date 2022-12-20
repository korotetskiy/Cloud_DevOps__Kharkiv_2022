<h2>Containerization. Docker practice</h2>
<head>
<h3>Docker practice basics</h3>
1. Install using the repository</br><img src="https://github.com/korotetskiy/img/blob/main/d1.png">
2. Add Docker’s official GPG key:</br>
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg \</br>
| sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg</br>
Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.</br>
$ sudo apt-key fingerprint 0EBFCD88</br>
3. Installing Docker Engine</br>
<h3>$ sudo apt-get update</br>
$ sudo apt-get install docker-ce docker-ce-cli containerd.io</h3></br>
<img src="https://github.com/korotetskiy/img/blob/main/db1.png"></br>
<img src="https://github.com/korotetskiy/img/blob/main/db3.png">
4.


Create directory for Dockerfile(-s) and and dive into it.
$ mkdir dockerfiles
$ cd dockerfiles
Edit it and add the commands with nano:
$ nano Dockerfile
Finally build it:
$ docker build -t <tag> .

<h3>Create an account in Docker registry</h3></br><img src="https://github.com/korotetskiy/img/blob/main/d21.png">
Login to docker registry

Pushing to docker registry

Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-\
$(uname -m)" -o /usr/local/bin/docker-compose
Apply executable permissions to the binary:
sudo chmod +x /usr/local/bin/docker-compose

Create a docker-compose.yml file that starts your WordPress blog and a separate MySQL instance with a volume mount for data persistence:


Build the project In order to buil the project, run following command from your project directory.
docker-compose up -d
This runs docker-compose up in detached mode, pulls the needed Docker images, and starts the wordpress and database containers, as shown in the example below.

Docker Compose. Wordpress realization


Docker Compose. Use volumes
Create and manage volumes
You can create and manage volumes outside the scope of any container.
Create a volume:
$ docker volume create my-vol
List volumes:
$ docker volume ls
Inspect a volume:
$ docker volume inspect my-vol
Remove a volume:
$ docker volume rm my-vol
















Frequently used Docker commands
$ docker ps [-a]
$ docker stop $(docker ps -a -q)
$ docker rm 0fd99ee0cb61
$ docker images -a
$ docker rmi $(docker images -a -q)
#list
#stop all containers [you need stop before delete]
#remove a single container
# list
# remove all images
$ docker search tomcat
$ docker pull tomcat
$ docker search nginx
$ docker pull nginx
$ docker run -it -p 8889:8080 tomcat
$ docker run -it -p 8888:80 nginx
$ docker run -d -p 8890:80 nginx
