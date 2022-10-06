# Useful tips for web delivery

tags: #nginx #performance #wsgi

Set `Expires` and `Cache-Control` headers with the `expires` 
[directive](http://nginx.org/en/docs/http/ngx_http_headers_module.html#expires)
    - Remove unnecessary head requests

Gzip, gzip, gzip. And optimize [images](https://tinypng.com/)!

```
gzip on;
gzip_disable "msie6";
gzip_min_length 1000;
gzip_http_version 1.0;
gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;
```

Let nginx use the resources available to handle multiple connections

```
worker_processes auto;
events {
    use epoll;
    worker_connections 1024;
    multi_accept on;
}
```

Let browsers keep connections open to remove the overhead of handshakes with the keepalive_timeout 
[directive](http://nginx.org/en/docs/http/ngx_http_core_module.html#keepalive_timeout)


If using nginx as a proxy to another service, like wsgi processes, let nginx
handle the response in a single go by increasing the buffer size

```
location / {
    proxy_buffers 8 24k;
    proxy_buffer_size 2k;
    proxy_pass http://127.0.0.1:8000;
}
```

When possible, avoid a TCP connection and use a plain socket instead.

[Source](https://www.revsys.com/12days/)
[Rate limit](https://lincolnloop.com/blog/rate-limiting-nginx/) *haven't read this one yet* 👀





