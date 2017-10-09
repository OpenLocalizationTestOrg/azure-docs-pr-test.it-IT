---
title: esempi di configurazione router cliente aaaExpressRoute | Documenti Microsoft
description: In questa pagina vengono forniti esempi di configurazione di router per router Cisco e Juniper.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>Configurazione del router esempi tooset backup e la gestione del routing
Questa pagina fornisce gli esempi di configurazione dell'interfaccia e del routing per i router Cisco IOS-XE e Juniper MX. Questi sono esempi di toobe previsto a scopo informativo e non deve essere utilizzati come è. Per lavorare con il fornitore toocome con configurazioni appropriate per la rete. 

> [!IMPORTANT]
> Negli esempi inclusi in questa pagina sono previsti toobe esclusivamente per informazioni aggiuntive. È necessario collaborare con il team di vendita / tecnico del fornitore e la rete toocome team backup con configurazioni appropriate toomeet le proprie esigenze. Microsoft non supporta i problemi correlati tooconfigurations elencati in questa pagina. È necessario contattare il fornitore del dispositivo per assistenza.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>Impostazioni di MTU e TCP MSS sulle interfacce del router
* Hello MTU per l'interfaccia di ExpressRoute hello è 1500, hello tipico valore MTU predefinito per un'interfaccia Ethernet su un router. A meno che nel router sia una MTU diversi per impostazione predefinita, non è presente alcun toospecify necessario un valore sull'interfaccia router hello.
* A differenza di un Gateway VPN di Azure, hello MSS TCP per un circuito ExpressRoute non è necessario toobe specificato.

Esempi di configurazione router che seguono si applicano tooall peering. Per altri dettagli sul routing, vedere [Peering di ExpressRoute](expressroute-circuit-peerings.md) e [Requisiti per il routing di ExpressRoute](expressroute-routing.md).


## <a name="cisco-ios-xe-based-routers"></a>Router basati su Cisco IOS-XE
esempi di Hello in questa sezione si applicano a qualsiasi router famiglia del sistema operativo IOS XE hello in esecuzione.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Configurazione di interfacce e sotto-interfacce
Sarà necessaria un'interfaccia sub per peering ogni router è connettersi tooMicrosoft. Una sotto-interfaccia può essere identificata mediante un ID VLAN o una coppia in stack di ID VLAN e indirizzo IP.

**Definizione dell'interfaccia Dot1Q**

In questo esempio fornisce definizione di interfaccia secondario hello per un'interfaccia secondario con un ID VLAN. ID VLAN Hello è univoco per ogni peering. l'ottetto ultimo Hello dell'indirizzo IPv4 sarà sempre un numero dispari.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**Definizione dell'interfaccia QinQ**

In questo esempio fornisce definizione di interfaccia secondario hello per un'interfaccia con un due ID VLAN secondario. Hello outer ID VLAN (s-tag), se utilizzato rimane hello stesso in tutti i peering di hello. è univoco per ogni peering interna Hello ID di VLAN (c-tag). l'ottetto ultimo Hello dell'indirizzo IPv4 sarà sempre un numero dispari.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. Impostazione delle sessioni eBGP
È necessario impostare una sessione BGP con Microsoft per ogni peering. esempio Hello seguente permette di toosetup una sessione BGP con Microsoft. Se l'indirizzo IPv4 utilizzato per l'interfaccia sub hello era a.b.c. d, l'indirizzo IP hello del router adiacente BGP hello (Microsoft) sarà a.b.c.d+1. ottetti di ultima Hello dell'indirizzo IPv4 del router adiacente di hello BGP sarà sempre un numero pari.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Impostazione toobe prefissi annunciati sessione BGP hello
È possibile configurare il tooMicrosoft di prefissi selezionare tooadvertise router. È possibile effettuare questa operazione utilizzando hello esempio riportato di seguito.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. Mappe di routing
È possibile usare mappe di route e prefisso sono elencati i prefissi toofilter propagati nella rete. È possibile utilizzare l'esempio hello sotto attività hello tooaccomplish. Assicurarsi di avere impostato gli elenchi di prefissi appropriati.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a>Router serie Juniper MX
esempi di Hello in questa sezione si applicano per tutti i router della serie MX Juniper.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Configurazione di interfacce e sotto-interfacce

**Definizione dell'interfaccia Dot1Q**

In questo esempio fornisce definizione di interfaccia secondario hello per un'interfaccia secondario con un ID VLAN. ID VLAN Hello è univoco per ogni peering. l'ottetto ultimo Hello dell'indirizzo IPv4 sarà sempre un numero dispari.

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


**Definizione dell'interfaccia QinQ**

In questo esempio fornisce definizione di interfaccia secondario hello per un'interfaccia con un due ID VLAN secondario. Hello outer ID VLAN (s-tag), se utilizzato rimane hello stesso in tutti i peering di hello. è univoco per ogni peering interna Hello ID di VLAN (c-tag). l'ottetto ultimo Hello dell'indirizzo IPv4 sarà sempre un numero dispari.

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a>2. Impostazione delle sessioni eBGP
È necessario impostare una sessione BGP con Microsoft per ogni peering. esempio Hello seguente permette di toosetup una sessione BGP con Microsoft. Se l'indirizzo IPv4 utilizzato per l'interfaccia sub hello era a.b.c. d, l'indirizzo IP hello del router adiacente BGP hello (Microsoft) sarà a.b.c.d+1. ottetti di ultima Hello dell'indirizzo IPv4 del router adiacente di hello BGP sarà sempre un numero pari.

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Impostazione toobe prefissi annunciati sessione BGP hello
È possibile configurare il tooMicrosoft di prefissi selezionare tooadvertise router. È possibile effettuare questa operazione utilizzando hello esempio riportato di seguito.

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a>4. Mappe di routing
È possibile usare mappe di route e prefisso sono elencati i prefissi toofilter propagati nella rete. È possibile utilizzare l'esempio hello sotto attività hello tooaccomplish. Assicurarsi di avere impostato gli elenchi di prefissi appropriati.

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a>Passaggi successivi
Vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md) per altri dettagli.

