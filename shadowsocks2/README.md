### Example
``` sh
docker run --restart=always -dt -p 8490:8490 mritd/shadowsocks2 -s "ss://AEAD_CHACHA20_POLY1305:your-password@:8490"
```

``` yaml
# Server: -s ss://AEAD_CHACHA20_POLY1305:PASSWORD@:26 -verbose
# Client: -c ss://AEAD_CHACHA20_POLY1305:PASSWORD@[server_address]:26 \
#           -socks :26 -udptun :8053=8.8.8.8:53,:8054=8.8.4.4:53 \
#           -tcptun :8053=8.8.8.8:53,:8054=8.8.4.4:53 -verbose
version: '3.6'
services:
  shadowsocks:
    image: kayuii/shadowsocks2
    restart: always
    ports:
      - "26:26"
      - "26:26/udp"
      - "8053:8053"
      - "8053:8053/udp"
      - "8054:8054"
      - "8054:8054/udp"
    command: "-c ss://AEAD_CHACHA20_POLY1305:PASSWORD@[server_address]:26 -socks :26 -udptun :8053=8.8.8.8:53,:8054=8.8.4.4:53 -tcptun :8053=8.8.8.8:53,:8054=8.8.4.4:53 -verbose"
```
