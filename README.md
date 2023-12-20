## Descrição

Este repositório apresenta uma configuração Docker utilizando o Docker Compose, incluindo um arquivo de configuração com variáveis de ambiente. A composição inclui um container Nginx
1.13.3, um container PHP 7.1.9-fpm interligado ao Nginx por meio de um link e um container MySQL 5.7.19.

## Configuração Nginx

**1. Exposição de portas:**
- 80 e 443

**2. Volume (verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)**
- Aplicação: htdocs -> /var/www/html
- Logs: nginx/logs -> /var/log/nginx
- Virtual Host: nginx/sites -> /etc/nginx/conf.d
	
**3. Virtual Host**
- Criação do vhost modelo http://api.dev (vhost modificável)

## Configuração PHP

**1. Exposição de portas**
- 9000

**2. Volume (verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)**
- Aplicação: htdocs -> /var/www/html
	
**3. Bibliotecas**
- Habilitação de bibliotecas do PHP através de arquivo de configuração. Ex: MBSTRING, GD, MCRYPT, PDO_MYSQL, etc.
	
## Configuração Mysql

**1. Exposição de portas**
- 3306

**2. Volume (verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)**
- Aplicação: mysql/data -> /var/lib/mysql

**3. Configuração para conexão**
- MYSQL_DATABASE = default
- MYSQL_USER = default
- MYSQL_PASSWORD  = secret
- MYSQL_ROOT_PASSWORD = root
- MYSQL_PORT = 3306
	
## Como utilizar
**1. Copie o arquivo env-example para .env.**
> cp env-example .env 

**2. Rode seu container:**
> docker-compose up -d

**3. Adicione os domínios no arquivo de hosts do Windows.**
> 127.0.0.1 localhost

> 127.0.0.1 api.dev

**4. Abra no navegador**

http://localhost

http://api.dev

**5. Acessar o shell do container:**
> winpty docker exec -it nginx bash

> winpty docker exec -it php-fpm bash

> winpty docker exec -it mysql bash

**6. Acessar o BD dentro do container Mysql**
> mysql -u root -p

**7. Comandos básicos para utilizar o Banco de Dados:**
> show databases;

> create database teste;

> use teste;

> show tables;
