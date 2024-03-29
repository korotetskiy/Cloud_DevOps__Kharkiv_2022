<h2>Containerization. Docker practice</h2>
<head>
<h3>Docker practice basics</h3>
<h3>1. Install using the repository</h3>

```
$ sudo apt-get update
$ sudo apt install docker.io
```

<img src="https://github.com/korotetskiy/img/blob/main/d1.png"><h3>

2. Add Docker’s official GPG key:</br></h3>

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
| sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.</br>

```
$ sudo apt-key fingerprint 0EBFCD88</br>
```

<h3>2. Installing Docker Engine</br></h3>

```
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io runc
```

<img src="https://github.com/korotetskiy/img/blob/main/d34.png">
<h4>Verify that Docker Engine is installed correctly by running the hello-world image.</h4>

```
$ sudo docker run hello-world
```

<img src="https://github.com/korotetskiy/img/blob/main/d31.png">
<h3>3. Docker practice basics</h3><img src="https://github.com/korotetskiy/img/blob/main/d36.png"><img src="https://github.com/korotetskiy/img/blob/main/d37-1.png"><img src="https://github.com/korotetskiy/img/blob/main/d4.png">
<h3>4. Create an account in Docker registry</h3><img src="https://github.com/korotetskiy/img/blob/main/d21.png">
<h3>5. Login to docker registry</br><img src="https://github.com/korotetskiy/img/blob/main/d33.png"></h3>
<h3>6. Webapps with Docker</h3>
<img src="https://github.com/korotetskiy/img/blob/main/d9.png">
<h3>7. Pushing to docker registry</h3>
<img src="https://github.com/korotetskiy/img/blob/main/d91.png">
<h3>8. Install Docker Compose</h3>

```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-\
$ (uname -m)" -o /usr/local/bin/docker-compose
```

Apply executable permissions to the binary:

```
$ sudo chmod +x /usr/local/bin/docker-compose
````

<img src="https://github.com/korotetskiy/img/blob/main/d38.png">
Create a docker-compose.yml file that starts your WordPress blog and a separate MySQL instance with a volume mount for data persistence:<img src="https://github.com/korotetskiy/img/blob/main/d44.png">
<h3>Docker Compose. Wordpress realization</h3>
This runs docker-compose up in detached mode, pulls the needed Docker images, and starts the wordpress and database containers, as shown in the example below.</br><img src="https://github.com/korotetskiy/img/blob/main/d41.png"><img src="https://github.com/korotetskiy/img/blob/main/n42.png"><img src="https://github.com/korotetskiy/img/blob/main/d43.png">
<img src="https://github.com/korotetskiy/img/blob/main/D49.png">
<h3>9. Docker Compose. Using volumes</h3></br>
Create a volume:</br>

```
$ docker volume create my-vol
```

List volumes:</br>

```
$ docker volume ls
```

Inspect a volume:</br>

```
$ docker volume inspect my-vol
```

Remove a volume:</br>

```
$ docker volume rm my-vol
```

<img src="https://github.com/korotetskiy/img/blob/main/d45.png"></br>
