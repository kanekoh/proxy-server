# Install/Configure a proxy server on RHEL 7

NOTES: This playbook needs sudo without password for registering subscription and installing modules.

## Prerequisites

- ansible
- ansible module: mrlesmithjr.squid


## Prepare environment


Install modules using Yum.
```
$ sudo yum install ansible
```


Install Ansible Module from Galaxy
```
$ ansible-galaxy install mrlesmithjr.squid
```

## Install your proxy on a server

Copy and configure your inventory file.

```
$ cp hosts/sample-hosts.yaml hosts/proxy.yaml
```

Then, execute the playbook playbook.yaml.
```
$ ansible-playbook -i hosts/proxy.yaml playbook.yaml
```

## How to confirm the environment after install

Define HTTP_PROXY, HTTPS_PROXY environment variables and access a web site using curl.

```
$ export HTTP_PROXY=127.0.0.1:3128
$ export HTTPS_PROXY=127.0.0.1:3128
$ curl -vis https://google.com > /dev/null
```

You can see the connection via proxy as follows:

```
* About to connect() to proxy 127.0.0.1 port 3128 (#0)
*   Trying 127.0.0.1...
* Connected to 127.0.0.1 (127.0.0.1) port 3128 (#0)
* Establish HTTP proxy tunnel to www.google.com:443
> CONNECT www.google.com:443 HTTP/1.1
> Host: www.google.com:443
> User-Agent: curl/7.29.0
> Proxy-Connection: Keep-Alive
>
< HTTP/1.1 200 Connection established
<
* Proxy replied OK to CONNECT request
...
```


