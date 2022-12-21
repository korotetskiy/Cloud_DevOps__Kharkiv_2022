<h2>Containerization. Docker practice</h2>
<head>
<h3>Docker practice basics</h3>
1. Install using the repository <h4>$ sudo apt-get update</br>$ sudo apt install docker.io</h4><img src="https://github.com/korotetskiy/img/blob/main/d1.png"><h3>2. Add Docker’s official GPG key:</br></h3>
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg \</br>
| sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg</br>
Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.</br>
$ sudo apt-key fingerprint 0EBFCD88</br>
<h3>3. Installing Docker Engine</br>
<h3>$ sudo apt-get update</br>
$ sudo apt-get install docker-ce docker-ce-cli containerd.io runc</h3><img src="https://github.com/korotetskiy/img/blob/main/d34.png">
<h4>Verify that Docker Engine is installed correctly by running the hello-world image.</h4><h3>$ sudo docker run hello-world</br></h3></h4><img src="https://github.com/korotetskiy/img/blob/main/d31.png">
<h3>4. Docker practice basics</h3><img src="https://github.com/korotetskiy/img/blob/main/d36.png"><img src="https://github.com/korotetskiy/img/blob/main/d37.png">
<h3>5. Create an account in Docker registry</h3><img src="https://github.com/korotetskiy/img/blob/main/d21.png">
<h3>6.Login to docker registry</br><img src="https://github.com/korotetskiy/img/blob/main/d33.png"></h3>

Pushing to docker registry

<h3>7.Install Docker Compose</h3>
<h4>sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-\</br>
$(uname -m)" -o /usr/local/bin/docker-compose</h4>
Apply executable permissions to the binary:
<h4>sudo chmod +x /usr/local/bin/docker-compose</h4><img src="https://github.com/korotetskiy/img/blob/main/d38.png">

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



</h3>
