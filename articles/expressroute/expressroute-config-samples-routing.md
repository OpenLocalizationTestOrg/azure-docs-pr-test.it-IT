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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="0b6f9-103">Configurazione del router esempi tooset backup e la gestione del routing</span><span class="sxs-lookup"><span data-stu-id="0b6f9-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="0b6f9-104">Questa pagina fornisce gli esempi di configurazione dell'interfaccia e del routing per i router Cisco IOS-XE e Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="0b6f9-105">Questi sono esempi di toobe previsto a scopo informativo e non deve essere utilizzati come è.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="0b6f9-106">Per lavorare con il fornitore toocome con configurazioni appropriate per la rete.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0b6f9-107">Negli esempi inclusi in questa pagina sono previsti toobe esclusivamente per informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="0b6f9-108">È necessario collaborare con il team di vendita / tecnico del fornitore e la rete toocome team backup con configurazioni appropriate toomeet le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="0b6f9-109">Microsoft non supporta i problemi correlati tooconfigurations elencati in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="0b6f9-110">È necessario contattare il fornitore del dispositivo per assistenza.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="0b6f9-111">Impostazioni di MTU e TCP MSS sulle interfacce del router</span><span class="sxs-lookup"><span data-stu-id="0b6f9-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="0b6f9-112">Hello MTU per l'interfaccia di ExpressRoute hello è 1500, hello tipico valore MTU predefinito per un'interfaccia Ethernet su un router.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="0b6f9-113">A meno che nel router sia una MTU diversi per impostazione predefinita, non è presente alcun toospecify necessario un valore sull'interfaccia router hello.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="0b6f9-114">A differenza di un Gateway VPN di Azure, hello MSS TCP per un circuito ExpressRoute non è necessario toobe specificato.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="0b6f9-115">Esempi di configurazione router che seguono si applicano tooall peering.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="0b6f9-116">Per altri dettagli sul routing, vedere [Peering di ExpressRoute](expressroute-circuit-peerings.md) e [Requisiti per il routing di ExpressRoute](expressroute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="0b6f9-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="0b6f9-117">Router basati su Cisco IOS-XE</span><span class="sxs-lookup"><span data-stu-id="0b6f9-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="0b6f9-118">esempi di Hello in questa sezione si applicano a qualsiasi router famiglia del sistema operativo IOS XE hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="0b6f9-119">1. Configurazione di interfacce e sotto-interfacce</span><span class="sxs-lookup"><span data-stu-id="0b6f9-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="0b6f9-120">Sarà necessaria un'interfaccia sub per peering ogni router è connettersi tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="0b6f9-121">Una sotto-interfaccia può essere identificata mediante un ID VLAN o una coppia in stack di ID VLAN e indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="0b6f9-122">**Definizione dell'interfaccia Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="0b6f9-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="0b6f9-123">In questo esempio fornisce definizione di interfaccia secondario hello per un'interfaccia secondario con un ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="0b6f9-124">ID VLAN Hello è univoco per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="0b6f9-125">l'ottetto ultimo Hello dell'indirizzo IPv4 sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="0b6f9-126">**Definizione dell'interfaccia QinQ**</span><span class="sxs-lookup"><span data-stu-id="0b6f9-126">**QinQ interface definition**</span></span>

<span data-ttu-id="0b6f9-127">In questo esempio fornisce definizione di interfaccia secondario hello per un'interfaccia con un due ID VLAN secondario.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="0b6f9-128">Hello outer ID VLAN (s-tag), se utilizzato rimane hello stesso in tutti i peering di hello.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="0b6f9-129">è univoco per ogni peering interna Hello ID di VLAN (c-tag).</span><span class="sxs-lookup"><span data-stu-id="0b6f9-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="0b6f9-130">l'ottetto ultimo Hello dell'indirizzo IPv4 sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="0b6f9-131">2. Impostazione delle sessioni eBGP</span><span class="sxs-lookup"><span data-stu-id="0b6f9-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="0b6f9-132">È necessario impostare una sessione BGP con Microsoft per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="0b6f9-133">esempio Hello seguente permette di toosetup una sessione BGP con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="0b6f9-134">Se l'indirizzo IPv4 utilizzato per l'interfaccia sub hello era a.b.c. d, l'indirizzo IP hello del router adiacente BGP hello (Microsoft) sarà a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="0b6f9-135">ottetti di ultima Hello dell'indirizzo IPv4 del router adiacente di hello BGP sarà sempre un numero pari.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="0b6f9-136">3. Impostazione toobe prefissi annunciati sessione BGP hello</span><span class="sxs-lookup"><span data-stu-id="0b6f9-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="0b6f9-137">È possibile configurare il tooMicrosoft di prefissi selezionare tooadvertise router.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="0b6f9-138">È possibile effettuare questa operazione utilizzando hello esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="0b6f9-139">4. Mappe di routing</span><span class="sxs-lookup"><span data-stu-id="0b6f9-139">4. Route maps</span></span>
<span data-ttu-id="0b6f9-140">È possibile usare mappe di route e prefisso sono elencati i prefissi toofilter propagati nella rete.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="0b6f9-141">È possibile utilizzare l'esempio hello sotto attività hello tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="0b6f9-142">Assicurarsi di avere impostato gli elenchi di prefissi appropriati.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="0b6f9-143">Router serie Juniper MX</span><span class="sxs-lookup"><span data-stu-id="0b6f9-143">Juniper MX series routers</span></span>
<span data-ttu-id="0b6f9-144">esempi di Hello in questa sezione si applicano per tutti i router della serie MX Juniper.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="0b6f9-145">1. Configurazione di interfacce e sotto-interfacce</span><span class="sxs-lookup"><span data-stu-id="0b6f9-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="0b6f9-146">**Definizione dell'interfaccia Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="0b6f9-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="0b6f9-147">In questo esempio fornisce definizione di interfaccia secondario hello per un'interfaccia secondario con un ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="0b6f9-148">ID VLAN Hello è univoco per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="0b6f9-149">l'ottetto ultimo Hello dell'indirizzo IPv4 sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="0b6f9-150">**Definizione dell'interfaccia QinQ**</span><span class="sxs-lookup"><span data-stu-id="0b6f9-150">**QinQ interface definition**</span></span>

<span data-ttu-id="0b6f9-151">In questo esempio fornisce definizione di interfaccia secondario hello per un'interfaccia con un due ID VLAN secondario.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="0b6f9-152">Hello outer ID VLAN (s-tag), se utilizzato rimane hello stesso in tutti i peering di hello.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="0b6f9-153">è univoco per ogni peering interna Hello ID di VLAN (c-tag).</span><span class="sxs-lookup"><span data-stu-id="0b6f9-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="0b6f9-154">l'ottetto ultimo Hello dell'indirizzo IPv4 sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="0b6f9-155">2. Impostazione delle sessioni eBGP</span><span class="sxs-lookup"><span data-stu-id="0b6f9-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="0b6f9-156">È necessario impostare una sessione BGP con Microsoft per ogni peering.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="0b6f9-157">esempio Hello seguente permette di toosetup una sessione BGP con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="0b6f9-158">Se l'indirizzo IPv4 utilizzato per l'interfaccia sub hello era a.b.c. d, l'indirizzo IP hello del router adiacente BGP hello (Microsoft) sarà a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="0b6f9-159">ottetti di ultima Hello dell'indirizzo IPv4 del router adiacente di hello BGP sarà sempre un numero pari.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="0b6f9-160">3. Impostazione toobe prefissi annunciati sessione BGP hello</span><span class="sxs-lookup"><span data-stu-id="0b6f9-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="0b6f9-161">È possibile configurare il tooMicrosoft di prefissi selezionare tooadvertise router.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="0b6f9-162">È possibile effettuare questa operazione utilizzando hello esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-162">You can do so using hello sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="0b6f9-163">4. Mappe di routing</span><span class="sxs-lookup"><span data-stu-id="0b6f9-163">4. Route maps</span></span>
<span data-ttu-id="0b6f9-164">È possibile usare mappe di route e prefisso sono elencati i prefissi toofilter propagati nella rete.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="0b6f9-165">È possibile utilizzare l'esempio hello sotto attività hello tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="0b6f9-166">Assicurarsi di avere impostato gli elenchi di prefissi appropriati.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0b6f9-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b6f9-167">Next Steps</span></span>
<span data-ttu-id="0b6f9-168">Vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="0b6f9-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

