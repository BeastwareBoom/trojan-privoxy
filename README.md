# trojan-privoxy

trojan client with privoxy for http proxy

## How to use

```bash
# https://stackoverflow.com/questions/36075525/how-do-i-run-a-docker-instance-from-a-dockerfile
# create image from Dockerfile, name is trojan_privoxy
docker build --tag trojan_privoxy .
docker image ls

docker run \
    --name my_proxy \
    -e REMOTE_ADDR="your host" \
    -e REMOTE_PORT="server port" \
    -e PASSWORD="your password" \
    -p TROJAN_PORT:1086 \
    -p PRIVOXY_PORT:1087 \
    trojan_privoxy:latest
```

TROJAN_PORT and PRIVOXY_PORT are proxy ports on HOST.

## use proxy

```bash
export http_proxy=http://127.0.0.1:PRIVOXY_PORT
export https_proxy=http://127.0.0.1:PRIVOXY_PORT
```

## with proxychains
```bash
apt install proxychains

# edit /etc/proxychains.conf
sed -i '/^socks4/d' /etc/proxychains.conf
echo "socks5 127.0.0.1 TROJAN_PORT" >> /etc/proxychains.conf
proxychains curl -4 ip.sb
```
