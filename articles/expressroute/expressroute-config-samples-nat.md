---
title: esempi di configurazione router cliente aaaExpressRoute | Documenti Microsoft
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
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a>Configurazione del router esempi tooset backup e gestire NAT
Questa pagina fornisce gli esempi di configurazione NAT per i router Cisco ASA e Juniper SRX. Questi sono esempi di toobe previsto a scopo informativo e non deve essere utilizzati come è. Per lavorare con il fornitore toocome con configurazioni appropriate per la rete. 

> [!IMPORTANT]
> Negli esempi inclusi in questa pagina sono previsti toobe esclusivamente per informazioni aggiuntive. È necessario collaborare con il team di vendita / tecnico del fornitore e la rete toocome team backup con configurazioni appropriate toomeet le proprie esigenze. Microsoft non supporta i problemi correlati tooconfigurations elencati in questa pagina. È necessario contattare il fornitore del dispositivo per assistenza.
> 
> 

* Esempi di configurazione router che seguono si applicano tooAzure peering di Microsoft e pubblici. Non è necessario configurare NAT per il peering privato di Azure. Per altri dettagli, vedere [Peering di ExpressRoute](expressroute-circuit-peerings.md) e [Requisiti NAT di ExpressRoute](expressroute-nat.md).

* È necessario utilizzare separato in un pool IP NAT per toohello connettività internet ed ExpressRoute. Utilizzando hello stesso IP NAT pool tra hello internet ed ExpressRoute comporterà asimmetriche routing e la perdita di connettività.


## <a name="cisco-asa-firewalls"></a>Firewall Cisco ASA
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a>Configurazione PAT per il traffico dal cliente rete tooMicrosoft
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

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a>Configurazione PAT per il traffico dalla rete toocustomer Microsoft

**Interfacce e Direzione:**

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

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
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a>1. Creazione di interfacce Ethernet ridondante per cluster hello
    interfaces {
        reth0 {
            description "tooInternal Network";
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
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a>2. Creare due aree di sicurezza
* Area attendibile per la rete interna e area non attendibile per la rete esterna esposta ai router perimetrali
* Assegnare le interfacce appropriate toohello zone
* Consenti ai servizi su interfacce hello

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
* Creare due pool NAT. Uno sarà usato tooNAT il traffico in uscita tooMicrosoft e altri dal cliente toohello Microsoft.
* Creare regole del traffico di rispettivi hello tooNAT
  
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
                       toorouting-instance External-ExpressRoute;
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
                       toorouting-instance Internal;
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

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a>5. Configurare i selettivi prefissi degli spazi BGP tooadvertise in ciascuna direzione
Fare riferimento toosamples in [esempi di configurazione di Routing ](expressroute-config-samples-routing.md) pagina.

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
Vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md) per altri dettagli.

