# haproxy_sandbox

1. Vagrant up #wait for all 3 hosts to complete, you will have 2 webservers and haproxy
2. Log into one of the web servers using "vagrant ssh web1" and run the following command:

```sudo cat /etc/ssl/private/apache-selfsigned.key > /tmp/haproxy.pem; sudo cat /etc/ssl/certs/apache-selfsigned.crt >> /tmp/haproxy.pem; sudo cat /etc/ssl/certs/dhparam.pem >> /tmp/haproxy.pem```

3. scp the haproxy.pem over to the haproxy server and place in /etc/haproxy/haproxy.pem
4. sudo systemctl restart harpoxy on the load balancer 
5. https://hostbox:4002 to hit loadbalancer for ssl && http://hostbox:9002
