# Cisco EIGRP(Enhanced Interior Gateway Routing Protocol) Routing

Bu protokol IGRP'nin yetersiz kalması ile geliştirilmiş bir protokoldür. EIGRP tüm rota hesaplamalarında DUAL (DUAL-Diffusing Update Algorithm) algoritmasını kullanır. Bu algoritma döngüsüz ve yedekli rotalar sağlar. DUAL kullanılarak hedef ağa giden tüm yedek rotalar kayıt edilir ve ihtiyaç duyulduğunda kullanılır. Bu bilgiler topoloji tablosunda tutulur.



Yapılandırmalara Geçelim:

# Network Yapılandırmaları

## PC 

- **Ankara Network:**
  - **Ip Adres:** 192.168.10.10
  - **Ağ Maskesi:** 255.255.255.0
  - **Ağ Geçidi:** 192.168.10.1

- **İstanbul Network:**
  - **Ip Adres:** 192.168.20.10
  - **Ağ Maskesi:** 255.255.255.0
  - **Ağ Geçidi:** 192.168.20.1


- **İzmir Network:**
  - **Ip Adres:** 192.168.30.10
  - **Ağ Maskesi:** 255.255.255.0
  - **Ağ Geçidi:** 192.168.30.1
 


## Router

### Ankara Router
```
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface gigabitEthernet 0/0
Router(config-if)#ip address 192.168.10.1 255.255.255.0
Router(config-if)#exit
Router(config)interface serial 0/1/0
Router(config-if)#ip address 10.1.1.1 255.0.0.0
```

### İstanbul Router 

```
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface gigabitEthernet 0/0
Router(config-if)#ip address 192.168.20.1 255.255.255.0
Router(config-if)#exit
Router(config)interface serial 0/1/0
Router(config-if)#ip address 10.1.1.2 255.0.0.0
Router(config-if)#exit
Router(config)interface serial 0/1/1
Router(config-if)#ip address 20.1.1.1 255.0.0.0
```

### İzmir Router
```
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface gigabitEthernet 0/0
Router(config-if)#ip address 192.168.30.1 255.255.255.0
Router(config-if)#exit
Router(config)interface serial 0/1/1
Router(config-if)#ip address 20.1.1.2 255.0.0.0
```



## EIGRP

### Ankara Router
```
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#router eigrp  100
Router(config-router)#network 192.168.10.0 0.0.0.255  // iç networkü tanıtıyoruz
Router(config-router)#network 10.1.1.1 0.255.255.255  // İstanbulla iletşimde olan dış networkü tanıtıyoruz
Router(config-router)#
```

### İstanbul Router
```
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#router eigrp  100
Router(config-router)#network 192.168.20.0 0.0.0.255  // iç networkü tanıtıyoruz
Router(config-router)#network 10.1.1.2 0.255.255.255  // İstanbulla iletişimde olan dış networkü tanıtıyoruz
Router(config-router)#network 20.1.1.1 0.255.255.255  // İzmirle iletişimde olan dış networkü tanıtıyoruz
Router(config-router)#
```

### İzmir Router
```
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#router eigrp  100
Router(config-router)#network 192.168.30.0 0.0.0.255  // iç networkü tanıtıyoruz
Router(config-router)#network 20.1.1.2 0.255.255.255  // İstanbulla iletşimde olan dış networkü tanıtıyoruz
Router(config-router)#
```





