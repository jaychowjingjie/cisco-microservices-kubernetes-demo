# Cisco Microservices Kubernetes Demo (please view in RAW format)

Demo microservices architecture with kubernetes

Different networking options within Docker:
1) Default docker bridge via docker 0
In a host: etho -- IP Tables/NAT -- Docker 0 -- container 1
                                             \
                                              \ container 2
                                              
2) User defined bridges to isolate containers in the same host
In a host: etho -- IP Tables/NAT -- Brnet1 -- container 1
                                 \
                                  \ Brnet2 -- container 2
                                  
3) Overlay Network
In host 1: etho -- IP Tables/NAT -- Docker 0 -- container 1
                                                           \
                                                             \ 
                                                               overlay(for containers to talk across multi hosts without NAT)
                                                               /
                                                              /
In host 2: etho -- IP Tables/NAT -- Docker 0 -- container 2
