
# SQL SERVER connection with laradock

## Change .env vars in laradock

```bash
# line 66
PHP_DOWNGRADE_OPENSSL_TLS_AND_SECLEVEL=true

# line 142
WORKSPACE_INSTALL_MSSQL=true

# line 242
PHP_FPM_INSTALL_MSSQL=true
```

## Build images and up container

```bash
docker-compose build --no-cache php-fpm workspace
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
