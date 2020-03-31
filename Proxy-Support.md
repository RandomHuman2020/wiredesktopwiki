**Testing**

```
docker run --name squid -d --restart=always --publish 3128:3128 -e AUTH=true -e USERNAME=foo -e PASSWORD=bar babim/squid
```