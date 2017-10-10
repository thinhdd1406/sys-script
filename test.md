## ====== Disable recursive DNS =======
### 1. Kloxo
 - Edit /var/named/chroot/etc/named.conf
   add them
```sh
options {
allow-recursion { localhost; };
};
```
 - /etc/init.d/named restart

### 2. Direct Admin
Open DNS Server allow recursive lookups

The error basically means that anyone can use your nameservers to do dns lookups on the internet.
It's considered a security risk to allow recursive lookups on an authoritative server.  You can disable the recursion by adding

```sh
allow-recursion {localnets; };
```
to the "options {" section in your named.conf file.Newer versions of named may require this setting instead

```sh
allow-query     { any; };
allow-transfer  { none; };
allow-recursion { localhost; };
recursion yes;
```
to allow local recursion, but block remote recursion.
http://help.directadmin.com/item.php?id=115
