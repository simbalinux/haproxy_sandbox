# haproxy_sandbox

1. Vagrant up wait for all 3 hosts to complete, you will have 2 webservers apache ssl and haproxy configured for http and https.
2. Log into one of the web servers using "vagrant ssh web1" and run the following command to combine your key/crt to haproxy.pem

```
sudo cat /etc/ssl/private/apache-selfsigned.key > /tmp/haproxy.pem; sudo cat /etc/ssl/certs/apache-selfsigned.crt >> /tmp/haproxy.pem; sudo cat /etc/ssl/certs/dhparam.pem >> /tmp/haproxy.pem
```

3. scp the haproxy.pem over to the haproxy server and place in /etc/haproxy/haproxy.pem
4. sudo systemctl restart harpoxy on the load balancer 
5. https://hostbox:4002 to hit loadbalancer for ssl && http://hostbox:9002 for non ssl traffic

Remember hostbox is the machine that hosts vagrant aka host not the guest ip.

#This will give you 2 web servers configured for ssl on the backedn as well as to haproxy.

**Haproxy will send XFF's via the traffic relay to apache, by default apache is not formatted default to accept this data....herefore apache "LogFormat" will need to be changed. Haproxy passes the field name "X-Forwarded-For" needs to be exact.**

*snippet of the httpd.conf file in apache to accept XFF's*

```
./httpd.conf:    LogFormat "%{X-Forwarded-For}i %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
```
