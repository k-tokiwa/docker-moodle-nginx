# docker-moodle-nginx

## Installation

```
git clone https://github.com/jda/docker-moodle
cd docker-moodle
docker build -t moodle .
```

## Usage

To spawn a new instance of Moodle:

```
docker run -d --name DB -p 3306:3306 -e MYSQL_DATABASE=moodle -e MYSQL_USER=moodle -e MYSQL_PASSWORD=moodle centurylink/mysql
docker run -d -P --name moodle --link DB:DB -e MOODLE_URL=https://sample.com -p 8080:80 k-tokiwa/moodle
```

You can visit the following URL in a browser to get started:

```
https://sample.com
```
## Nginx
```
location / {
    proxy_pass http://PrivateIP:8080;
    #index index.php index.html index.htm;
    proxy_set_header   X-Forwarded-Proto $scheme;
    proxy_set_header   Host              $http_host;
    proxy_set_header   X-Real-IP         $remote_addr;
    proxy_set_header   X-Forwarded-For   $proxy_add_x_forwarded_for;
    proxy_set_header   Host https://sample.com;
    proxy_redirect     off;
}
```
