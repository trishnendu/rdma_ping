# rping

An utility to test ib device and rdma connection

# How to test!

### Check rdma_rxe driver 
```
[abc@fed ~]$ modinfo rdma_rxe
filename:       /lib/modules/5.6.6-300.fc32.x86_64/kernel/drivers/infiniband/sw/rxe/rdma_rxe.ko.xz
alias:          rdma-link-rxe
license:        Dual BSD/GPL
description:    Soft RDMA transport
```

 ### Load driver
 ```
 [abc@fed ~]$ modprobe rdma_rxe
 [abc@fed ~]$ lsmod | grep rdma_rxe
rdma_rxe              139264  0
ib_uverbs             147456  2 rdma_rxe,rdma_ucm
ip6_udp_tunnel         16384  1 rdma_rxe
udp_tunnel             16384  1 rdma_rxe
ib_core               405504  13 rdma_cm,ib_ipoib,rdma_rxe,rpcrdma,ib_srpt,ib_srp,iw_cm,ib_iser,ib_umad,ib_isert,rdma_ucm,ib_uverbs,ib_cm
```

### Add soft rdma links
```
[abc@fed ~]$ sudo rdma link add roce8 type rxe netdev enp0s8
[abc@fed ~]$ rdma link 
link rocep0s8/1 state ACTIVE physical_state LINK_UP netdev enp0s8 
```
### Check rping
```
[abc@fed ~]$ ./rping -c -a 192.168.1.219 -d -C 1
[abc@fed ~]$ ./rping -s -d -C 1
```

## Main Repos
| Repo | link |
| ------ | ------ |
| rdma-core | https://github.com/linux-rdma/rdma-core |
| librdmacm | https://github.com/ofiwg/librdmacm |