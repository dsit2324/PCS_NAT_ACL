# PCS - NAT a ACL

!- Defaultní routa musí být nastavená na všech routerech -! (ip route 0.0.0.0 0.0.0.0 <adresa portu sousedního routeru>) (u výchozího je to ta PUBLIC !)
VLAN 20, 30 a DMZ server:

Router0(config)# interface Gig0/2

Router0(config-if)# ip nat inside 

Router0(config)# interface Gig0/1
Router0(config-if)# ip nat inside

Router0(config)# interface Gig0/0
Router0(config-if)# ip nat outside



Router0(config)# access-list 40 permit 10.0.11.0 0.0.0.31
Router0(config)# access-list 40 permit 10.0.11.32 0.0.0.15
Router0(config)# access-list 40 permit 10.0.11.48 0.0.0.3
Router0(config)# access-list 40 deny any


Router0(config)# ip nat inside source list 40 interface Gig0/0 overload



Router0(config)# ip nat inside source static tcp 10.0.11.50 443 212.200.12.6 443


Vysvětlivky:

- inside - uvnitř mé sítě
- outside - ven z mé sítě

- 443 - identifikační číslo https protokolu podle zadání

- list - access-list zdroj z mé vnitřní sítě, jak se to má chovat
- static - pevně jedno zařízení


