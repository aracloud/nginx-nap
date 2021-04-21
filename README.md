## nginx-nap container build and test

https://docs.nginx.com/nginx-app-protect/admin-guide/install/#docker-deployment

### prep backend and syslog

docker run  -dit --cap-add SYSLOG -p 515:514 -p 515:514/udp --name rsyslog mysyslog
<br>
docker run -dit --name dvwa -p 8080:80 aracloud/docker-dvwa

(check 200 OK return code)
<br>
curl -I http://localhost:8080/login.php


### pull nap container

git clone https://github.com/aracloud/nginx-nap.git

cd nginx-nap

!!! Eval keys nginx-repo.crt / nginx-repo.key !!!

cat nginx.conf
<br>
cat Dockerfile


### build / run container

docker build --no-cache -t nginx-nap .
<br>
docker run --network host --name nap -p 80:80 -d nginx-nap


(check 200 OK return code)
<br>
curl -I http://localhost/login.php



### check out syslog

docker exec -it rsyslog bash
<br>
find /var/log/remote*