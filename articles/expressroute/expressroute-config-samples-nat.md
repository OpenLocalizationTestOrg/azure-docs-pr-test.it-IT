---
title: Esempi di configurazione di router ExpressRoute | Documentazione Microsoft
description: In questa pagina vengono forniti esempi di configurazione di router per router Cisco e Juniper.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 83a7da2db537a3c900e90432455d59e8ac56d917
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-nat"></a>Esempi di configurazione del router per l'impostazione e la gestione NAT
Questa pagina fornisce gli esempi di configurazione NAT per i router Cisco ASA e Juniper SRX. Devono essere intesi come esempi a solo scopo informativo e non devono essere usati per altri scopi. È possibile rivolgersi al fornitore per ottenere le configurazioni appropriate per la rete in uso. 

> [!IMPORTANT]
> Gli esempi inclusi in questa pagina devono essere intesi solo come linee guida. È necessario collaborare con il team di vendita/tecnico del fornitore e il team di rete per ottenere le configurazioni appropriate in base alle specifiche esigenze. Microsoft non offre supporto per i problemi relativi alle configurazioni elencate in questa pagina. È necessario contattare il fornitore del dispositivo per assistenza.
> 
> 

* Gli esempi di configurazione di router riportati di seguito si applicano al peering pubblico di Azure e al peering Microsoft. Non è necessario configurare NAT per il peering privato di Azure. Per altri dettagli, vedere [Peering di ExpressRoute](expressroute-circuit-peerings.md) e [Requisiti NAT di ExpressRoute](expressroute-nat.md).

* È necessario usare pool di IP NAT separati per la connettività a Internet ed ExpressRoute. L'uso dello stesso pool di IP NAT a livello di Internet ed ExpressRoute comporterà un routing asimmetrico e la perdita di connettività.


## <a name="cisco-asa-firewalls"></a>Firewall Cisco ASA
### <a name="pat-configuration-for-traffic-from-customer-network-to-microsoft"></a>Configurazione PAT per il traffico dalla rete del cliente a Microsoft
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-to-customer-network"></a>Configurazione PAT per il traffico da Microsoft alla rete del cliente

**Interfacce e Direzione:**

    Source Interface (where the traffic enters the ASA): inside
    Destination Interface (where the traffic exits the ASA): outside

**Configurazione:**

Pool NAT:

    object network outbound-PAT
        host <NAT-IP>

Server di destinazione:

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

Gruppo dell’oggetto per gli indirizzi IP del cliente

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

Comandi NAT:

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a>Router serie Juniper SRX
### <a name="1-create-redundant-ethernet-interfaces-for-the-cluster"></a>1. Creare interfacce Ethernet ridondanti per il cluster
    interfaces {
        reth0 {
            description "To Internal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "To Microsoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "To Microsoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a>2. Creare due aree di sicurezza
* Area attendibile per la rete interna e area non attendibile per la rete esterna esposta ai router perimetrali
* Assegnare le interfacce appropriate alle aree
* Abilitare i servizi nelle interfacce

    security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }


### <a name="3-create-security-policies-between-zones"></a>3. Creare criteri di sicurezza tra aree
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a>4. Configurare i criteri NAT
* Creare due pool NAT. Uno verrà usato per il traffico NAT in uscita verso Microsoft e l'altro per il traffico da Microsoft al cliente.
* Creare regole NAT il traffico corrispondente
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       to routing-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       to routing-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-to-advertise-selective-prefixes-in-each-direction"></a>5. Configurare BGP per pubblicare prefissi selettivi in ciascuna direzione
Fare riferimento agli esempi riportati nella pagina [Esempi di configurazione del routing ](expressroute-config-samples-routing.md) .

### <a name="6-create-policies"></a>6. Creare criteri
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md) .

