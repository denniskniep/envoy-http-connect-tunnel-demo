# Overview
Using [Envoyproxy](https://www.envoyproxy.io) to tunnel tcp traffic (in this case ssh) through http. This is done through an HTTPConnect Proxy.

[SSH-Client] --tcp--> [HTTP-Connect-Proxy-Client] --tcpOverHttp--> [Envoy] --tcp--> [SSH-Server]

# Run Demo

Start Envoy & SSH-Server 
```
docker-compose up
```

Install and run [HTTP-Connect-Proxy-Client](https://github.com/denniskniep/http-connect-proxy-client)
```
go install github.com/denniskniep/http-connect-proxy-client@latest

http-connect-proxy-client -s http://127.0.0.1:4444 -l 127.0.0.1 -p 5555
```

```
ssh admin@127.0.0.1 -p 5555
```

# References
* https://en.wikipedia.org/wiki/HTTP_tunnel
* https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/http/upgrades#tunneling-tcp-over-http
* https://github.com/envoyproxy/envoy/blob/ba81ae537e722ad99906599f5d3ad367ca854433/configs/encapsulate_in_http2_connect.yaml
* https://github.com/envoyproxy/envoy/blob/ba81ae537e722ad99906599f5d3ad367ca854433/configs/terminate_http2_connect.yaml
* https://github.com/envoyproxy/envoy/blob/ba81ae537e722ad99906599f5d3ad367ca854433/configs/proxy_connect.yaml