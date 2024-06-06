# nginx:stable-alpine + proxy_connect + lua

Modified from [rpardini/nginx-proxy-connect-stable-alpine](https://github.com/rpardini/nginx-proxy-connect-stable-alpine)

Upstreams: 
- [nginx:stable-alpine](https://github.com/nginxinc/docker-nginx/tree/master/stable/alpine) (due this has since long diverged)
- [ngx_http_proxy_connect_module](https://github.com/chobits/ngx_http_proxy_connect_module)
- [lua-nginx-module](https://github.com/openresty/lua-nginx-module.git)

I removed gpg sig verification for the sake of faster builds.
Also most modules with external dependencies were removed.

# master (`:latest`) is actually unstable

For stable versions, use the tagged builds, eg, `nginx-1.18.0-alpine-3.12.1`

## Usage

```bash 
docker run -it -p 8081:80 crestfallmax/nginx-proxy-connect-stable-alpine:latest
```

- Just like `nginx:stable-alpine`, but you can use `proxy_connect;`.
- Also `proxy_connect_address $someVar;` is supported; this has the "rewrite" version of the patch
- you can map on `$connect_host`
- log `$connect_addr` for host:port of the final destination

## Why?

I wanted a more contained way of doing DNS overrides.

If you can convince a client program to use an https proxy, and inject your own CA certificate as trusted, 
you can use `proxy_connect` to send traffic to a second nginx server and do caching, filtering, rewriting, 
and who knows what else there.
