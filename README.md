# WordPress Multisite on with Subdomain on Docker
Docker compose file to create a WordPress Multisite Environment for your use.

### Pre-requisites

Need have installed docker compose on Server, if doesn't installed, please check out this link:

https://docs.docker.com/compose/install/

## Initial Instructions

1. Clone this project on a directory of your preference:

```sh
git clone https://github.com/joelcpinheiro/docker_wpmultisite.git
```

2. Execute the command to start the environment:

```sh
docker-compose up -d
```

At this moment will be created two containers on your stack, do you need to access the environment and enable the Multisite option:

Check _data directory of wordpress container and edit the wp-config.php file after the 88 line add the param below:

```sh
/* Multisite */
define( 'WP_ALLOW_MULTISITE', true );
```

3. Now, do you have to install WordPress as used to, click in TOOLS > NETWORK SETUP, edit the Network title and Email and click on Install to activate multisite.

4. Follow the instructions that are edit the wp-config.php and .htaccess files, respectively:

```sh
define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', false);
define('DOMAIN_CURRENT_SITE', 'mywpmultisite.com');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);
```

```sh
RewriteEngine On
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
RewriteBase /
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(wp-(content|admin|includes).*) $2 [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L]
RewriteRule . index.php [L]
```

5. Access WordPres Admin Panel and edit Network Settings default for all sites if you I'll create.

**OBS**: None

## Version

1.0

## Autor

 ***Joel Pinheiro** - *Github* - https://github.com/joelcpinheiro/

## License

Use where you think you will contribute.