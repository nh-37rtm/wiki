# initiate a request using custom dns name

to test a dns name reverse proxy or ingress you can use this

````
curl -L http://grafana.acedigitale.local --resolve grafana.acedigitale.local:80:10.10.17.73
````
this avoid the change of the ``hosts`` file each time for only a test query moreover you don't need to add the host dns name to the global dns

## Reference
- https://dev.to/peterc/how-to-make-curl-request-a-site-from-a-different-ip-than-in-dns-4n45