# What is this project?

[todo]

# Things before launching

## 1. Bring or generate your own certifacte

To enable https on nginx instance, you must provide certificate files: .crt and .key to `./volumes/nginx_volume/certificates/` .

If you don't have these, you can generate temporary certificates using following commands:
```
openssl req \
       -newkey rsa:2048 -nodes -keyout certificate.key \
       -x509 -days 365 -out certificate.crt
```

If your certificate file name is different than `certificate`, you need to change this in `docker-compose.yml` file in following section:
```
proxy:
    [...]
    environment:
        "SSL_CERTIFICATE_NAME": file_name_here_without_extension
    [...]
```

## 2. Copy init data to volumes folder

Tools like Gitlab and Artifacts needs to have initial configuration copied to volumes folder. In order to do that, please, add execute permission to file `copy_init_data.sh` and then run it:

```
chmod +x copy_init_data.sh
./copy_init_data.sh
```

# Configuration

## Gitlab

Gitlab has initial configuration loaded. Default root credentials are:
```
username: root
password: passwd
```

Artifactory and jenkins initial credentials are:
```
username: admin
password: passwd
```

Artifactory user for resolving:
```
username: resolver
password: w?cBd^Y6~KhfWrRF
```
