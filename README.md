# Cisco Microservices Kubernetes Demo (please view in RAW format)

Demo microservices architecture with kubernetes

Different networking options within Docker:
1) Default docker bridge via docker 0
In a host: eth0 -- IP Tables/NAT -- Docker 0 -- container 1
                                             \
                                              \ container 2
                                              
2) User defined bridges to isolate containers in the same host
In a host: eth0 -- IP Tables/NAT -- Brnet1 -- container 1
                                 \
                                  \ Brnet2 -- container 2
                                  
3) Overlay Network
In host 1: eth0 -- IP Tables/NAT -- Docker 0 -- container 1
                                                           \
                                                             \ 
                                                               overlay(for containers to talk across multi hosts without NAT)
                                                               /
                                                              /
In host 2: eth0 -- IP Tables/NAT -- Docker 0 -- container 2

Why do we need Docker?

- Faster development process
- Application encapsulation
- The same behaviour on local machine, dev, staging, production servers
- Easy and clear monitoring
    Easy to scale
