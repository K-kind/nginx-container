# nginx container
This is a simple setup for running nginx on Docker (Mac OS).

## Requirement
- Docker Desktop for Mac

## Getting Started
1. Clone this repository into `~/.nginx-container` .

```
git clone https://github.com/K-kind/nginx-container.git ~/.nginx-container
```

2. Add `~/.nginx-container/bin` to your `$PATH` for access to the `nginx-container` command-line utility.
  * For **Zsh**:
  ```
  echo 'export PATH="$PATH:$HOME/.nginx-container/bin"' >> ~/.zshrc
  ```

  * For **bash**:
  ```
  echo 'export PATH="$PATH:$HOME/.nginx-container/bin"' >> ~/.bash_profile
  ```

## Settings

### Example for using nginx as SSL reverse proxy

1. Place your certificates to `~/.nginx-container/conf/ssl/`

2. Edit settings in the `~/.nginx-container/conf/conf.d/server.conf` file

These settings enable requests to the `https://local.hoge.com` to be sent to `http://localhost:8080` .

```conf
server {
    listen       443 ssl;
    server_name  local.hoge.com;
    ssl_certificate /etc/nginx/ssl/local.hoge.com-cert.pem;
    ssl_certificate_key /etc/nginx/ssl/local.hoge.com-key.pem;

    location / {
        proxy_pass  http://host.docker.internal:8080/;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```

## Usage
- Start a container

```
nginx-container
```

- Stop the container

```
nginx-container stop
```

- Restart the container

```
nginx-container restart
```
