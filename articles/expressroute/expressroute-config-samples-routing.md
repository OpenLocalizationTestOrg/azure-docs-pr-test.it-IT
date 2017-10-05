---
title: Esempi di configurazione di router ExpressRoute | Microsoft Docs
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
ms.openlocfilehash: 032e584dc5abf59e9e3e8d80673b402f1fbf721b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="32bba-103">Esempi di configurazione del router per l'impostazione e la gestione del routing</span><span class="sxs-lookup"><span data-stu-id="32bba-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="32bba-104">Questa pagina fornisce gli esempi di configurazione dell'interfaccia e del routing per i router Cisco IOS-XE e Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="32bba-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="32bba-105">Devono essere intesi come esempi a solo scopo informativo e non devono essere usati per altri scopi.</span><span class="sxs-lookup"><span data-stu-id="32bba-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="32bba-106">È possibile rivolgersi al fornitore per ottenere le configurazioni appropriate per la rete in uso.</span><span class="sxs-lookup"><span data-stu-id="32bba-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="32bba-107">Gli esempi inclusi in questa pagina devono essere intesi solo come linee guida.</span><span class="sxs-lookup"><span data-stu-id="32bba-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="32bba-108">È necessario collaborare con il team di vendita/tecnico del fornitore e il team di rete per ottenere le configurazioni appropriate in base alle specifiche esigenze.</span><span class="sxs-lookup"><span data-stu-id="32bba-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="32bba-109">Microsoft non offre supporto per i problemi relativi alle configurazioni elencate in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="32bba-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="32bba-110">È necessario contattare il fornitore del dispositivo per assistenza.</span><span class="sxs-lookup"><span data-stu-id="32bba-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="32bba-111">Impostazioni di MTU e TCP MSS sulle interfacce del router</span><span class="sxs-lookup"><span data-stu-id="32bba-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="32bba-112">Il valore MTU dell'interfaccia ExpressRoute è 1500, ovvero il valore predefinito di MTU tipico per un'interfaccia Ethernet su un router.</span><span class="sxs-lookup"><span data-stu-id="32bba-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="32bba-113">A meno che il router non abbia un valore MTU diverso per impostazione predefinita, non è necessario specificare un valore sull'interfaccia del router.</span><span class="sxs-lookup"><span data-stu-id="32bba-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span></span>
* <span data-ttu-id="32bba-114">A differenza di un Gateway VPN di Azure, non è necessario specificare il valore MSS TCP per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="32bba-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span></span>

<span data-ttu-id="32bba-115">Gli esempi di configurazione del router riportati di seguito si applicano a tutti i peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-115">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="32bba-116">Per altri dettagli sul routing, vedere [Peering di ExpressRoute](expressroute-circuit-peerings.md) e [Requisiti per il routing di ExpressRoute](expressroute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="32bba-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="32bba-117">Router basati su Cisco IOS-XE</span><span class="sxs-lookup"><span data-stu-id="32bba-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="32bba-118">Gli esempi in questa sezione si applicano a qualsiasi router che esegue la famiglia di sistemi operativi IOS-XE.</span><span class="sxs-lookup"><span data-stu-id="32bba-118">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="32bba-119">1. Configurazione di interfacce e sotto-interfacce</span><span class="sxs-lookup"><span data-stu-id="32bba-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="32bba-120">Sarà necessaria una sotto-interfaccia per peering in ogni router connesso a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32bba-120">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="32bba-121">Una sotto-interfaccia può essere identificata mediante un ID VLAN o una coppia in stack di ID VLAN e indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="32bba-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="32bba-122">**Definizione dell'interfaccia Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="32bba-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="32bba-123">Questo esempio fornisce la definizione della sotto-interfaccia per una sotto-interfaccia secondario con un ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="32bba-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="32bba-124">L'ID VLAN è univoco per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-124">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="32bba-125">L'ultimo ottetto dell'indirizzo IPv4 sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="32bba-125">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="32bba-126">**Definizione dell'interfaccia QinQ**</span><span class="sxs-lookup"><span data-stu-id="32bba-126">**QinQ interface definition**</span></span>

<span data-ttu-id="32bba-127">Questo esempio fornisce la definizione della sotto-interfaccia per una sotto-interfaccia con due ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="32bba-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="32bba-128">L'ID VLAN esterno (s-tag), se usato, rimane invariato in tutti i peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="32bba-129">L'ID VLAN interno (c-tag) è univoco per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-129">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="32bba-130">L'ultimo ottetto dell'indirizzo IPv4 sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="32bba-130">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="32bba-131">2. Impostazione delle sessioni eBGP</span><span class="sxs-lookup"><span data-stu-id="32bba-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="32bba-132">È necessario impostare una sessione BGP con Microsoft per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="32bba-133">L'esempio seguente consente di configurare una sessione BGP con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32bba-133">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="32bba-134">Se l'indirizzo IPv4 usato per la sotto-interfaccia è a.b.c.d, l'indirizzo IP del router adiacente BGP (Microsoft) sarà a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="32bba-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="32bba-135">L'ultimo ottetto dell'indirizzo IPv4 del router adiacente BGP sarà sempre un numero pari.</span><span class="sxs-lookup"><span data-stu-id="32bba-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="32bba-136">3. Impostazione dei prefissi da pubblicare tramite la sessione BGP</span><span class="sxs-lookup"><span data-stu-id="32bba-136">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="32bba-137">È possibile configurare il router per pubblicare i prefissi di selezione a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32bba-137">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="32bba-138">Per eseguire questa operazione, usare l'esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="32bba-138">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="32bba-139">4. Mappe di routing</span><span class="sxs-lookup"><span data-stu-id="32bba-139">4. Route maps</span></span>
<span data-ttu-id="32bba-140">È possibile usare le mappe di routing e gli elenchi di prefissi per filtrare i prefissi propagati nella rete.</span><span class="sxs-lookup"><span data-stu-id="32bba-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="32bba-141">È possibile usare l'esempio riportato di seguito per completare l'attività.</span><span class="sxs-lookup"><span data-stu-id="32bba-141">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="32bba-142">Assicurarsi di avere impostato gli elenchi di prefissi appropriati.</span><span class="sxs-lookup"><span data-stu-id="32bba-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="32bba-143">Router serie Juniper MX</span><span class="sxs-lookup"><span data-stu-id="32bba-143">Juniper MX series routers</span></span>
<span data-ttu-id="32bba-144">Gli esempi in questa sezione si applicano a tutti i router serie Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="32bba-144">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="32bba-145">1. Configurazione di interfacce e sotto-interfacce</span><span class="sxs-lookup"><span data-stu-id="32bba-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="32bba-146">**Definizione dell'interfaccia Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="32bba-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="32bba-147">Questo esempio fornisce la definizione della sotto-interfaccia per una sotto-interfaccia secondario con un ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="32bba-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="32bba-148">L'ID VLAN è univoco per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-148">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="32bba-149">L'ultimo ottetto dell'indirizzo IPv4 sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="32bba-149">The last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="32bba-150">**Definizione dell'interfaccia QinQ**</span><span class="sxs-lookup"><span data-stu-id="32bba-150">**QinQ interface definition**</span></span>

<span data-ttu-id="32bba-151">Questo esempio fornisce la definizione della sotto-interfaccia per una sotto-interfaccia con due ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="32bba-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="32bba-152">L'ID VLAN esterno (s-tag), se usato, rimane invariato in tutti i peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="32bba-153">L'ID VLAN interno (c-tag) è univoco per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-153">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="32bba-154">L'ultimo ottetto dell'indirizzo IPv4 sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="32bba-154">The last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="32bba-155">2. Impostazione delle sessioni eBGP</span><span class="sxs-lookup"><span data-stu-id="32bba-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="32bba-156">È necessario impostare una sessione BGP con Microsoft per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="32bba-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="32bba-157">L'esempio seguente consente di configurare una sessione BGP con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32bba-157">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="32bba-158">Se l'indirizzo IPv4 usato per la sotto-interfaccia è a.b.c.d, l'indirizzo IP del router adiacente BGP (Microsoft) sarà a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="32bba-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="32bba-159">L'ultimo ottetto dell'indirizzo IPv4 del router adiacente BGP sarà sempre un numero pari.</span><span class="sxs-lookup"><span data-stu-id="32bba-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="32bba-160">3. Impostazione dei prefissi da pubblicare tramite la sessione BGP</span><span class="sxs-lookup"><span data-stu-id="32bba-160">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="32bba-161">È possibile configurare il router per pubblicare i prefissi di selezione a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="32bba-161">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="32bba-162">Per eseguire questa operazione, usare l'esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="32bba-162">You can do so using the sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="32bba-163">4. Mappe di routing</span><span class="sxs-lookup"><span data-stu-id="32bba-163">4. Route maps</span></span>
<span data-ttu-id="32bba-164">È possibile usare le mappe di routing e gli elenchi di prefissi per filtrare i prefissi propagati nella rete.</span><span class="sxs-lookup"><span data-stu-id="32bba-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="32bba-165">È possibile usare l'esempio riportato di seguito per completare l'attività.</span><span class="sxs-lookup"><span data-stu-id="32bba-165">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="32bba-166">Assicurarsi di avere impostato gli elenchi di prefissi appropriati.</span><span class="sxs-lookup"><span data-stu-id="32bba-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="32bba-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32bba-167">Next Steps</span></span>
<span data-ttu-id="32bba-168">Per altre informazioni, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="32bba-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

