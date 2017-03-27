## Installation
```
git clone -b feature-moodle-docker https://github.com/ricoh/si-apps-ex.git 
docker build -t moodle .
```

## Usage
To spawn a new instance of Moodle:

```
docker run -d --name DB -p 3306:3306 -e MYSQL_DATABASE=moodle -e MYSQL_USER=moodle -e MYSQL_PASSWORD=moodle centurylink/mysql
docker run -d -P --name moodle --link DB:DB -e MOODLE_URL=https://example.com -p 8080:80 k-tokiwa/moodle-nginx
```

You can visit the following URL in a browser to get started:

## Nginx setting

/etc/nginx/nginx.conf
```
location / {
    proxy_pass http://PrivateIP:8080;
    #index index.php index.html index.htm;
    proxy_set_header   X-Forwarded-Proto $scheme;
    proxy_set_header   Host              $http_host;
    proxy_set_header   X-Real-IP         $remote_addr;
    proxy_set_header   X-Forwarded-For   $proxy_add_x_forwarded_for;
    proxy_set_header   Host https://example.com;
    proxy_redirect     off;
}
```

### URL
```
https://example.com
```
