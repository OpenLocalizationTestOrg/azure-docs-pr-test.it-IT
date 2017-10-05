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
# <a name="router-configuration-samples-to-set-up-and-manage-nat"></a><span data-ttu-id="91e83-103">Esempi di configurazione del router per l'impostazione e la gestione NAT</span><span class="sxs-lookup"><span data-stu-id="91e83-103">Router configuration samples to set up and manage NAT</span></span>
<span data-ttu-id="91e83-104">Questa pagina fornisce gli esempi di configurazione NAT per i router Cisco ASA e Juniper SRX.</span><span class="sxs-lookup"><span data-stu-id="91e83-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="91e83-105">Devono essere intesi come esempi a solo scopo informativo e non devono essere usati per altri scopi.</span><span class="sxs-lookup"><span data-stu-id="91e83-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="91e83-106">È possibile rivolgersi al fornitore per ottenere le configurazioni appropriate per la rete in uso.</span><span class="sxs-lookup"><span data-stu-id="91e83-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="91e83-107">Gli esempi inclusi in questa pagina devono essere intesi solo come linee guida.</span><span class="sxs-lookup"><span data-stu-id="91e83-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="91e83-108">È necessario collaborare con il team di vendita/tecnico del fornitore e il team di rete per ottenere le configurazioni appropriate in base alle specifiche esigenze.</span><span class="sxs-lookup"><span data-stu-id="91e83-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="91e83-109">Microsoft non offre supporto per i problemi relativi alle configurazioni elencate in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="91e83-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="91e83-110">È necessario contattare il fornitore del dispositivo per assistenza.</span><span class="sxs-lookup"><span data-stu-id="91e83-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="91e83-111">Gli esempi di configurazione di router riportati di seguito si applicano al peering pubblico di Azure e al peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91e83-111">Router configuration samples below apply to Azure Public and Microsoft peerings.</span></span> <span data-ttu-id="91e83-112">Non è necessario configurare NAT per il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="91e83-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="91e83-113">Per altri dettagli, vedere [Peering di ExpressRoute](expressroute-circuit-peerings.md) e [Requisiti NAT di ExpressRoute](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="91e83-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="91e83-114">È necessario usare pool di IP NAT separati per la connettività a Internet ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91e83-114">You MUST use separate NAT IP pools for connectivity to the internet and ExpressRoute.</span></span> <span data-ttu-id="91e83-115">L'uso dello stesso pool di IP NAT a livello di Internet ed ExpressRoute comporterà un routing asimmetrico e la perdita di connettività.</span><span class="sxs-lookup"><span data-stu-id="91e83-115">Using the same NAT IP pool across the internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="91e83-116">Firewall Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="91e83-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-to-microsoft"></a><span data-ttu-id="91e83-117">Configurazione PAT per il traffico dalla rete del cliente a Microsoft</span><span class="sxs-lookup"><span data-stu-id="91e83-117">PAT configuration for traffic from customer network to Microsoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-to-customer-network"></a><span data-ttu-id="91e83-118">Configurazione PAT per il traffico da Microsoft alla rete del cliente</span><span class="sxs-lookup"><span data-stu-id="91e83-118">PAT configuration for traffic from Microsoft to customer network</span></span>

<span data-ttu-id="91e83-119">**Interfacce e Direzione:**</span><span class="sxs-lookup"><span data-stu-id="91e83-119">**Interfaces and Direction:**</span></span>

    Source Interface (where the traffic enters the ASA): inside
    Destination Interface (where the traffic exits the ASA): outside

<span data-ttu-id="91e83-120">**Configurazione:**</span><span class="sxs-lookup"><span data-stu-id="91e83-120">**Configuration:**</span></span>

<span data-ttu-id="91e83-121">Pool NAT:</span><span class="sxs-lookup"><span data-stu-id="91e83-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="91e83-122">Server di destinazione:</span><span class="sxs-lookup"><span data-stu-id="91e83-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="91e83-123">Gruppo dell’oggetto per gli indirizzi IP del cliente</span><span class="sxs-lookup"><span data-stu-id="91e83-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="91e83-124">Comandi NAT:</span><span class="sxs-lookup"><span data-stu-id="91e83-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="91e83-125">Router serie Juniper SRX</span><span class="sxs-lookup"><span data-stu-id="91e83-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-the-cluster"></a><span data-ttu-id="91e83-126">1. Creare interfacce Ethernet ridondanti per il cluster</span><span class="sxs-lookup"><span data-stu-id="91e83-126">1. Create redundant Ethernet interfaces for the cluster</span></span>
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


### <a name="2-create-two-security-zones"></a><span data-ttu-id="91e83-127">2. Creare due aree di sicurezza</span><span class="sxs-lookup"><span data-stu-id="91e83-127">2. Create two security zones</span></span>
* <span data-ttu-id="91e83-128">Area attendibile per la rete interna e area non attendibile per la rete esterna esposta ai router perimetrali</span><span class="sxs-lookup"><span data-stu-id="91e83-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="91e83-129">Assegnare le interfacce appropriate alle aree</span><span class="sxs-lookup"><span data-stu-id="91e83-129">Assign appropriate interfaces to the zones</span></span>
* <span data-ttu-id="91e83-130">Abilitare i servizi nelle interfacce</span><span class="sxs-lookup"><span data-stu-id="91e83-130">Allow services on the interfaces</span></span>

    <span data-ttu-id="91e83-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="91e83-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="91e83-132">3. Creare criteri di sicurezza tra aree</span><span class="sxs-lookup"><span data-stu-id="91e83-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="91e83-133">4. Configurare i criteri NAT</span><span class="sxs-lookup"><span data-stu-id="91e83-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="91e83-134">Creare due pool NAT.</span><span class="sxs-lookup"><span data-stu-id="91e83-134">Create two NAT pools.</span></span> <span data-ttu-id="91e83-135">Uno verrà usato per il traffico NAT in uscita verso Microsoft e l'altro per il traffico da Microsoft al cliente.</span><span class="sxs-lookup"><span data-stu-id="91e83-135">One will be used to NAT traffic outbound to Microsoft and other from Microsoft to the customer.</span></span>
* <span data-ttu-id="91e83-136">Creare regole NAT il traffico corrispondente</span><span class="sxs-lookup"><span data-stu-id="91e83-136">Create rules to NAT the respective traffic</span></span>
  
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

### <a name="5-configure-bgp-to-advertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="91e83-137">5. Configurare BGP per pubblicare prefissi selettivi in ciascuna direzione</span><span class="sxs-lookup"><span data-stu-id="91e83-137">5. Configure BGP to advertise selective prefixes in each direction</span></span>
<span data-ttu-id="91e83-138">Fare riferimento agli esempi riportati nella pagina [Esempi di configurazione del routing ](expressroute-config-samples-routing.md) .</span><span class="sxs-lookup"><span data-stu-id="91e83-138">Refer to samples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="91e83-139">6. Creare criteri</span><span class="sxs-lookup"><span data-stu-id="91e83-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="91e83-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="91e83-140">Next steps</span></span>
<span data-ttu-id="91e83-141">Per altre informazioni, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="91e83-141">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

