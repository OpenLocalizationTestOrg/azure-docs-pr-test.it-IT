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
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="31216-103">Configurazione del router esempi tooset backup e gestire NAT</span><span class="sxs-lookup"><span data-stu-id="31216-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="31216-104">Questa pagina fornisce gli esempi di configurazione NAT per i router Cisco ASA e Juniper SRX.</span><span class="sxs-lookup"><span data-stu-id="31216-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="31216-105">Questi sono esempi di toobe previsto a scopo informativo e non deve essere utilizzati come è.</span><span class="sxs-lookup"><span data-stu-id="31216-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="31216-106">Per lavorare con il fornitore toocome con configurazioni appropriate per la rete.</span><span class="sxs-lookup"><span data-stu-id="31216-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="31216-107">Negli esempi inclusi in questa pagina sono previsti toobe esclusivamente per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="31216-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="31216-108">È necessario collaborare con il team di vendita / tecnico del fornitore e la rete toocome team backup con configurazioni appropriate toomeet le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="31216-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="31216-109">Microsoft non supporta i problemi correlati tooconfigurations elencati in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="31216-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="31216-110">È necessario contattare il fornitore del dispositivo per assistenza.</span><span class="sxs-lookup"><span data-stu-id="31216-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="31216-111">Esempi di configurazione router che seguono si applicano tooAzure peering di Microsoft e pubblici.</span><span class="sxs-lookup"><span data-stu-id="31216-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="31216-112">Non è necessario configurare NAT per il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="31216-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="31216-113">Per altri dettagli, vedere [Peering di ExpressRoute](expressroute-circuit-peerings.md) e [Requisiti NAT di ExpressRoute](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="31216-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="31216-114">È necessario utilizzare separato in un pool IP NAT per toohello connettività internet ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31216-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="31216-115">Utilizzando hello stesso IP NAT pool tra hello internet ed ExpressRoute comporterà asimmetriche routing e la perdita di connettività.</span><span class="sxs-lookup"><span data-stu-id="31216-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="31216-116">Firewall Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="31216-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="31216-117">Configurazione PAT per il traffico dal cliente rete tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="31216-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="31216-118">Configurazione PAT per il traffico dalla rete toocustomer Microsoft</span><span class="sxs-lookup"><span data-stu-id="31216-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="31216-119">**Interfacce e Direzione:**</span><span class="sxs-lookup"><span data-stu-id="31216-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="31216-120">**Configurazione:**</span><span class="sxs-lookup"><span data-stu-id="31216-120">**Configuration:**</span></span>

<span data-ttu-id="31216-121">Pool NAT:</span><span class="sxs-lookup"><span data-stu-id="31216-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="31216-122">Server di destinazione:</span><span class="sxs-lookup"><span data-stu-id="31216-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="31216-123">Gruppo dell’oggetto per gli indirizzi IP del cliente</span><span class="sxs-lookup"><span data-stu-id="31216-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="31216-124">Comandi NAT:</span><span class="sxs-lookup"><span data-stu-id="31216-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="31216-125">Router serie Juniper SRX</span><span class="sxs-lookup"><span data-stu-id="31216-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="31216-126">1. Creazione di interfacce Ethernet ridondante per cluster hello</span><span class="sxs-lookup"><span data-stu-id="31216-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
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


### <a name="2-create-two-security-zones"></a><span data-ttu-id="31216-127">2. Creare due aree di sicurezza</span><span class="sxs-lookup"><span data-stu-id="31216-127">2. Create two security zones</span></span>
* <span data-ttu-id="31216-128">Area attendibile per la rete interna e area non attendibile per la rete esterna esposta ai router perimetrali</span><span class="sxs-lookup"><span data-stu-id="31216-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="31216-129">Assegnare le interfacce appropriate toohello zone</span><span class="sxs-lookup"><span data-stu-id="31216-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="31216-130">Consenti ai servizi su interfacce hello</span><span class="sxs-lookup"><span data-stu-id="31216-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="31216-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="31216-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="31216-132">3. Creare criteri di sicurezza tra aree</span><span class="sxs-lookup"><span data-stu-id="31216-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="31216-133">4. Configurare i criteri NAT</span><span class="sxs-lookup"><span data-stu-id="31216-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="31216-134">Creare due pool NAT.</span><span class="sxs-lookup"><span data-stu-id="31216-134">Create two NAT pools.</span></span> <span data-ttu-id="31216-135">Uno sarà usato tooNAT il traffico in uscita tooMicrosoft e altri dal cliente toohello Microsoft.</span><span class="sxs-lookup"><span data-stu-id="31216-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="31216-136">Creare regole del traffico di rispettivi hello tooNAT</span><span class="sxs-lookup"><span data-stu-id="31216-136">Create rules tooNAT hello respective traffic</span></span>
  
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

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="31216-137">5. Configurare i selettivi prefissi degli spazi BGP tooadvertise in ciascuna direzione</span><span class="sxs-lookup"><span data-stu-id="31216-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="31216-138">Fare riferimento toosamples in [esempi di configurazione di Routing ](expressroute-config-samples-routing.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="31216-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="31216-139">6. Creare criteri</span><span class="sxs-lookup"><span data-stu-id="31216-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="31216-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31216-140">Next steps</span></span>
<span data-ttu-id="31216-141">Vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="31216-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

