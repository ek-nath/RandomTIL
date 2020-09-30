
## ssh_config 

It is located in `%userprofile%\.ssh`

## Prefer `ipv4` over `ipv6` WSL

Instead of disabling IPv6 completely, you can instruct Ubuntu to [prefer IPv4 connections to IPv6](https://askubuntu.com/questions/32298/prefer-a-ipv4-dns-lookups-before-aaaaipv6-lookups/38468#38468) by editing the precedence blocks in `/etc/gai.conf`.

Using this solution:

* You may access servers in Internet with IPv4 an IPv6 servers through a NAT or a router that only understand IPv4
* Use IPv4 and IPv6 in the local network
* Avoid errors, for instance, [installing gem files from rubygems.org](https://github.com/rubygems/rubygems/issues/2253#issuecomment-432111545)

---
**Preferring IPv4 over IPV6 addresses**

Modifying the precedences in the `gai.conf`, every time a program calls `getaddrinfo()` for resolving host names, Linux will prefer the IPv4 addreses. This is very useful when you try to contact a server with both IPv4 and IPv6 addresses from a machine behind a NAT or a router. In addition, you may use IPv6 locally.

1. Edit the `/etc/gai.conf`

```
$ sudo vi /etc/gai.conf
```

2. Uncomment the last lines. Check that file has the next uncommented lines.

```
#For sites which prefer IPv4 connections change the last line to
precedence ::ffff:0:0/96 100
...
#    For sites which use site-local IPv4 addresses behind NAT there is
#    the problem that even if IPv4 addresses are preferred they do not
#    have the same scope and are therefore not sorted first.  To change
#    this use only these rules:
#
scopev4 ::ffff:169.254.0.0/112  2
scopev4 ::ffff:127.0.0.0/104    2
scopev4 ::ffff:0.0.0.0/96       14
```

[src](https://askubuntu.com/a/1200257/14506)
