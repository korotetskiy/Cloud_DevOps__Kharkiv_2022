<h2>Containerization. Docker practice</h2>
<head>
<h3>Docker practice basics</h3>
1. Install using the repository</br><img src="https://github.com/korotetskiy/img/blob/main/d1.png"></br>
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
