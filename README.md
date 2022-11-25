
# SQL SERVER connection with laradock

### Requirements

- For php7.2-fpm
    - for other versions https://github.com/microsoft/msphpsql/releases

## Change .env vars in laradock

```bash
# line 66
PHP_DOWNGRADE_OPENSSL_TLS_AND_SECLEVEL=true

# line 142
WORKSPACE_INSTALL_MSSQL=true

# line 242
PHP_FPM_INSTALL_MSSQL=true
```

## Extract this zip into your Workspace

## Build images and up container

```bash
docker-compose build --no-cache php-fpm workspace
```

## Get in php-fpm with bash

```bash
docker-compose exec php-fpm bash
```

## Paste the content from Ubuntu2004-7.2 into `/usr/local/lib/php/extensions/no-debug-non-zts-20170718`

## Install extensions

```bash
cd /usr/local/lib/php/extensions/no-debug-non-zts-20170718
pecl install sqlsrv-5.9.0preview1
pecl install pdo_sqlsrv-5.9.0preview1
```

## Edit `/etc/ssl/openssl.cnf`

```bash
# both in php-fpm container and workspace

# Add this line at the top
openssl_conf = openssl_init

# Add these lines at the end
[openssl_init]
ssl_conf = ssl_sect

[ssl_sect]
system_default = system_default_sect

[system_default_sect]
CipherString = DEFAULT@SECLEVEL=1
```
