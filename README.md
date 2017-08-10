# Postfix MTA with TLS encryption and DKIM in Docker container
Simple in usage isolated SMTP server

# Link on Docker Hub
https://hub.docker.com/r/terenchukv/postfix/

# REQUIREMENTS
- Docker
- Docker compose 

# INSTALLATION 
- clone this repo
- copy and edit .env file with yours variables
```
cp .env.dist .env
``` 

- For example your domain: mail.example.com
```
MAIL_HOST=mail    <--- container hostname
MAIL_DOMAIN=example.com  <--- domain name which point A record to your host
MAIL_SENDERS=mail.example.com <--- MAIL_HOST + MAIL_DOMAIN
SENDER_HOST=mail.example.com  <--- MAIL_HOST + MAIL_DOMAIN
CERT_COUNTRY=Ukraine
CERT_STATE=Kiev
CERT_CITY=Kiev
CERT_COMPANY=my_awsome_company
```

- build docker container
```
docker-compose build
```
- start container
```
docker-compose up -d
```

- NOTE! If you use firewall open 25 port. For example:
```
iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 25 -j ACCEPT
```

- Find DKIM record in /var/db/dkim/your_domain/default.txt and add this record in yor domain registrator
```
docker exec -it mail sh -c "cat /var/db/dkim/your_domain/default.txt"
```

# TEST SMTP
- connect to container
```
docker exec -it mail sh
```
- send test mail
```
echo 'Subject: test' | /usr/sbin/sendmail your_mail@test.com
```


