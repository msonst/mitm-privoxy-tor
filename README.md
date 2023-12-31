# mitm-privoxy-tor
dockerized setup of mitmproxy > privoxy > tor for aarch64.
Builds mitmproxy from source

# Enable system wide
```
export http_proxy="http://<IP>:8080"    
export https_proxy="https://<IP>:8080"
```

# Disable system wide
```
unset http_proxy
unset http_proxy
```
# Verify
```
unset http_proxy
unset http_proxy
curl -x http://<IP>:8080 -s "http://httpbin.org/ip"
curl -x http://<IP>:8118 -s "http://httpbin.org/ip"
curl -x socks5://<IP>:9050 -s "http://httpbin.org/ip"
export http_proxy="http://<IP>:8080"    
export https_proxy="https://<IP>:8080"
curl -x http://<IP>:8080 -s "http://httpbin.org/ip"
curl -x http://<IP>:8118 -s "http://httpbin.org/ip"
curl -x socks5://<IP>:9050 -s "http://httpbin.org/ip"
```

# Configure client to accept mitm cert
```
cp mitmproxy-ca-cert.cer mitmproxy-ca-cert.crt
sudo cp *.crt /usr/share/ca-certificates
sudo dpkg-reconfigure ca-certificates
sudo update-ca-certificates
```

#  Using a custom server certificate
You can use your own (leaf) certificate by passing the --certs [domain=]path_to_certificate option to mitmproxy. Mitmproxy then uses the provided certificate for interception of the specified domain instead of generating a certificate signed by its own CA.
```
openssl genrsa -out cert.key 2048
openssl req -new -x509 -key cert.key -out cert.crt
cat cert.key cert.crt > cert.pem
mitmdump -p 8080 --certs *=cert.pem
```
