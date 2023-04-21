
# hola :)

```bash
# Examen - Alejandro Araya Jiménez

# VLSM
# A > 1500 HOST
# B > 450 HOST
# C > 250 HOST
# D > 100 HOST
# RED -> 172.30.50.10/20

# -------------------------------------------------

# A	1500 2046	172.30.48.0/21		255.255.248.0		172.30.48.1 - 172.30.55.254		172.30.55.255
# B	450	510		172.30.56.0/23		255.255.254.0		172.30.56.1 - 172.30.57.254		172.30.57.255
# C	250	254		172.30.58.0/24		255.255.255.0		172.30.58.1 - 172.30.58.254		172.30.58.255
# D	100	126		172.30.59.0/25		255.255.255.128		172.30.59.1 - 172.30.59.126		172.30.59.127
# E	2	2		172.30.59.128/30	255.255.255.252		172.30.59.129 - 172.30.59.130	172.30.59.131




# A 2003:DB8:CAFE:A::/64
# B 2003:DB8:CAFE:B::/64
# C 2003:DB8:CAFE:C::/64
# D 2003:DB8:CAFE:D::/64
# D 2003:DB8:CAFE:1::/64


# -------------------------------------------------


# CONFIG SanPedro
en
conf t
interface g0/0/0
ip address 172.30.48.1 255.255.248.0
ipv6 address FE80::1 link-local
no shutdown
interface g0/0/1
ip address 172.30.56.1 255.255.254.0
ipv6 address FE80::1 link-local
no shutdown
interface s0/1/0
clock rate 64000
ip address 172.30.59.129 255.255.255.252
ipv6 address 2003:DB8:CAFE:1::1/64
ipv6 address FE80::1 link-local
no shutdown
exit
ipv6 unicast-routing
hostname SanPedro
banner motd "Solo personal autorizado"
enable secret class
line console 0
password cisco
line vty 0 4
password cisco
service password-encryption
ip route 172.30.58.0 255.255.255.0 172.30.59.130
ip route 172.30.59.0 255.255.255.128 172.30.59.130
ipv6 route 2003:DB8:CAFE:C::/64 2003:DB8:CAFE:1::2
ipv6 route 2003:DB8:CAFE:D::/64 2003:DB8:CAFE:1::2
do wr

# CONFIG HEREDIA
en
conf t
interface g0/0/0
ip address 172.30.58.1 255.255.255.0
ipv6 address FE80::2 link-local
no shutdown
interface g0/0/1
ip address 172.30.59.1 255.255.255.128
ipv6 address FE80::2 link-local
no shutdown
interface s0/1/0
ip address 172.30.59.130 255.255.255.252
ipv6 address 2003:DB8:CAFE:1::2/64
ipv6 address FE80::2 link-local
no shutdown
exit
ipv6 unicast-routing
hostname Heredia
banner motd "Solo personal autorizado"
enable secret class
line console 0
password cisco
line vty 0 4
password cisco
service password-encryption
ip route 172.30.48.0 255.255.248.0 172.30.59.129
ip route 172.30.56.0 255.255.254.0 172.30.59.129
ipv6 route 2003:DB8:CAFE:A::/64 2003:DB8:CAFE:1::1
ipv6 route 2003:DB8:CAFE:B::/64 2003:DB8:CAFE:1::1
do wr

# CONFIG SW

# CONFIG SW3
en
conf t
interface vlan 1
ip address 172.30.59.126 255.255.255.128
no shutdown
exit
do wr

# 255.255.248.0		172.30.48.1 - 172.30.55.254
# 255.255.254.0		172.30.56.1 - 172.30.57.254
# 255.255.255.0		172.30.58.1 - 172.30.58.254
# 255.255.255.128		172.30.59.1 - 172.30.59.126
# 255.255.255.252		172.30.59.129 - 172.30.59.130
```
