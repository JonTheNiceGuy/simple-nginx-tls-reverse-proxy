Simple nginx TLS Reverse Proxy
==============================

This role installs nginx, and then configures it to proxy to an HTTP only web service. It is currently designed for CentOS 7.4 to proxy Ansible AWX, but should work with any HTTP only services.

Requirements
------------

None

Role Variables
--------------

Here are the values which can be set, and the default values they are set to.

```
tls_certificate (The certificate file to use in the TLS termination. e.g. /etc/ssl/certs/dummy-cert)
tls_certificate_key (The key file to use in the TLS termination. e.g. /etc/ssl/certs/dummy-cert)
nginx_server_name (The SNI name to reply to. e.g. myserver.lan)
nginx_user (Which user nginx runs as. e.g. nginx)
nginx_error_log (Where to send error logs to. e.g. /var/log/nginx/error.log)
nginx_access_log (Where to send access logs to. e.g. /var/log/nginx/access.log)
nginx_pidfile (Where the pidfile is stored. e.g. /run/nginx.pid)
nginx_port (What port or server:port to respond to. e.g. 443 or 192.0.2.1:443)
nginx_upstream (Where should inbound HTTPS requests be directed. e.g. http://127.0.0.1)
```

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: jontheniceguy.simple-nginx-tls-reverse-proxy, nginx_upstream: http://192.0.2.1:8080 }

    - hosts: tls_terminators
      roles:
         - role: jontheniceguy.simple-nginx-tls-reverse-proxy
           nginx_upstream: http://198.51.100.2
           tls_certificate: /etc/ssl/certs/your_certificate
           tls_certificate_key: /etc/ssl/private/your_key


License
-------

[The Unlicense](https://github.com/JonTheNiceGuy/simple-nginx-tls-reverse-proxy/blob/master/LICENSE)
