---
title: Recupero di tabelle ARP - Modello di distribuzione classica - Risoluzione dei problemi di Azure ExpressRoute | Documentazione Microsoft
description: Questa pagina fornisce istruzioni per ottenere le tabelle ARP tabelle per un circuito ExpressRoute.
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="681ee-103">Recupero di tabelle ARP nel modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="681ee-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="681ee-104">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="681ee-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="681ee-105">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="681ee-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="681ee-106">L’articolo illustra i passaggi per ottenere le tabelle ARP ( Address Resolution Protocol) per il circuito ExpressRoute di Azure.</span><span class="sxs-lookup"><span data-stu-id="681ee-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="681ee-107">Questo documento è progettato per aiutare l'utente a rilevare e risolvere i problemi semplici.</span><span class="sxs-lookup"><span data-stu-id="681ee-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="681ee-108">Non sostituisce tuttavia il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="681ee-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="681ee-109">Se le seguenti linee guida non permettono di risolvere il problema, aprire una richiesta di supporto con [Guida e supporto di Azure Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="681ee-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="681ee-110">ARP (Address Resolution Protocol) e tabelle ARP</span><span class="sxs-lookup"><span data-stu-id="681ee-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="681ee-111">ARP è un protocollo di livello 2 che viene definito in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="681ee-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="681ee-112">Il protocollo ARP viene usato per mappare un indirizzo Ethernet (indirizzo MAC) su un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="681ee-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="681ee-113">Una tabella ARP fornisce un mapping dell'indirizzo IPv4 e dell'indirizzo MAC per un particolare peering.</span><span class="sxs-lookup"><span data-stu-id="681ee-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="681ee-114">La tabella ARP del peering di un circuito ExpressRoute fornisce le informazioni seguenti per ogni interfaccia (primaria e secondaria):</span><span class="sxs-lookup"><span data-stu-id="681ee-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="681ee-115">Mapping dell'indirizzo IP dell'interfaccia del router locale all'indirizzo MAC</span><span class="sxs-lookup"><span data-stu-id="681ee-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="681ee-116">Mapping dell'indirizzo IP dell'interfaccia del router ExpressRoute all'indirizzo MAC</span><span class="sxs-lookup"><span data-stu-id="681ee-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="681ee-117">L’età del mapping</span><span class="sxs-lookup"><span data-stu-id="681ee-117">The age of the mapping</span></span>

<span data-ttu-id="681ee-118">Le tabelle ARP consentono di convalidare la configurazione di livello 2 e la risoluzione dei problemi di connettività di base di livello 2.</span><span class="sxs-lookup"><span data-stu-id="681ee-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="681ee-119">Di seguito è riportato un esempio di tabella ARP:</span><span class="sxs-lookup"><span data-stu-id="681ee-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="681ee-120">La sezione seguente fornisce informazioni su come visualizzare le tabelle ARP visibili tramite i router perimetrali di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="681ee-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="681ee-121">Prerequisiti per l'utilizzo delle tabelle ARP</span><span class="sxs-lookup"><span data-stu-id="681ee-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="681ee-122">Prima di continuare, verificare che siano presenti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="681ee-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="681ee-123">Un circuito ExpressRoute valido configurato con almeno un peer.</span><span class="sxs-lookup"><span data-stu-id="681ee-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="681ee-124">Il circuito deve essere completamente configurato dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="681ee-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="681ee-125">L'utente o il provider di connettività deve configurare almeno un peer (privato di Azure, pubblico di Azure e Microsoft) su questo circuito.</span><span class="sxs-lookup"><span data-stu-id="681ee-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="681ee-126">Gli intervalli degli indirizzi IP usati per la configurazione del peer (privato di Azure, pubblico di Azure e Microsoft).</span><span class="sxs-lookup"><span data-stu-id="681ee-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="681ee-127">Consultare gli esempi di assegnazione dell'indirizzo IP in [Requisiti per il routing di ExpressRoute](expressroute-routing.md) per ottenere informazioni sul mapping degli indirizzi IP verso le interfacce sul lato utente e sul lato ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="681ee-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="681ee-128">È possibile ottenere informazioni sulla configurazione del peering consultando la [pagina sulla configurazione del peering di ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="681ee-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="681ee-129">Informazioni dal team di rete o provider di connettività sugli indirizzi MAC delle interfacce usate con questi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="681ee-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="681ee-130">Il più recente modulo PowerShell per Azure (versione 1.50 o successiva).</span><span class="sxs-lookup"><span data-stu-id="681ee-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="681ee-131">Le tabelle ARP per il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="681ee-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="681ee-132">In questa sezione vengono fornite le istruzioni su come visualizzare le tabelle ARP per ciascun tipo di peering tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="681ee-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="681ee-133">Prima di continuare, il peering deve essere configurato dall’utente o dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="681ee-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="681ee-134">Ogni circuito ha due percorsi (primario e secondario).</span><span class="sxs-lookup"><span data-stu-id="681ee-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="681ee-135">È possibile controllare la tabella ARP di ogni percorso in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="681ee-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="681ee-136">Tabelle ARP per il peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="681ee-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="681ee-137">Il cmdlet seguente fornisce le tabelle ARP per il peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="681ee-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="681ee-138">Di seguito è illustrato un esempio di output per uno dei percorsi:</span><span class="sxs-lookup"><span data-stu-id="681ee-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="681ee-139">Tabelle ARP per il peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="681ee-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="681ee-140">Il cmdlet seguente fornisce le tabelle ARP per il peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="681ee-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="681ee-141">Di seguito è illustrato un esempio di output per uno dei percorsi:</span><span class="sxs-lookup"><span data-stu-id="681ee-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="681ee-142">Di seguito è illustrato un esempio di output per uno dei percorsi:</span><span class="sxs-lookup"><span data-stu-id="681ee-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="681ee-143">Tabelle ARP per il peering di Microsoft</span><span class="sxs-lookup"><span data-stu-id="681ee-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="681ee-144">Il cmdlet seguente fornisce le tabelle ARP per il peering di Microsoft</span><span class="sxs-lookup"><span data-stu-id="681ee-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="681ee-145">Di seguito è illustrato un esempio di output per uno dei percorsi:</span><span class="sxs-lookup"><span data-stu-id="681ee-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="681ee-146">Procedura: Come usare queste informazioni</span><span class="sxs-lookup"><span data-stu-id="681ee-146">How to use this information</span></span>
<span data-ttu-id="681ee-147">La tabella ARP di un peer può essere usata per convalidare la connettività e la configurazione di livello 2 valide.</span><span class="sxs-lookup"><span data-stu-id="681ee-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="681ee-148">Questa sezione offre una panoramica dell'aspetto delle tabelle ARP in scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="681ee-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="681ee-149">La tabella ARP quando un circuito è in stato operativo (previsto)</span><span class="sxs-lookup"><span data-stu-id="681ee-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="681ee-150">La tabella ARP contiene una voce per il lato locale con gli indirizzi IP e MAC validi e una voce simile per il lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="681ee-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="681ee-151">L'ultimo ottetto dell'indirizzo IP locale è sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="681ee-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="681ee-152">L'ultimo ottetto dell'indirizzo IP Microsoft è sempre un numero pari.</span><span class="sxs-lookup"><span data-stu-id="681ee-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="681ee-153">Lo stesso indirizzo MAC viene visualizzato sul lato Microsoft per tutti i 3 peer (principale/secondario).</span><span class="sxs-lookup"><span data-stu-id="681ee-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="681ee-154">La tabella ARP quando il lato locale o del provider di connettività presenta problemi</span><span class="sxs-lookup"><span data-stu-id="681ee-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="681ee-155">Viene visualizzata solo una voce nella tabella ARP.</span><span class="sxs-lookup"><span data-stu-id="681ee-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="681ee-156">Mostra il mapping tra gli indirizzi MAC e IP usati sul lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="681ee-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="681ee-157">Se si verifica un problema simile, aprire una richiesta di supporto con il provider di connettività per risolverlo.</span><span class="sxs-lookup"><span data-stu-id="681ee-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="681ee-158">La tabella ARP quando il lato Microsoft presenta problemi</span><span class="sxs-lookup"><span data-stu-id="681ee-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="681ee-159">Se sono presenti problemi sul lato Microsoft, non verrà visualizzata la tabella ARP illustrata per il peering.</span><span class="sxs-lookup"><span data-stu-id="681ee-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="681ee-160">Aprire una richiesta di supporto con [Guida e supporto di Azure Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="681ee-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="681ee-161">Specificare che si è riscontrato un problema di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="681ee-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="681ee-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="681ee-162">Next steps</span></span>
* <span data-ttu-id="681ee-163">Convalidare le configurazioni di livello 3 per il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="681ee-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="681ee-164">Ottenere un riepilogo del routing per determinare lo stato delle sessioni BGP.</span><span class="sxs-lookup"><span data-stu-id="681ee-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="681ee-165">Ottenere la tabella del routing per stabilire i prefissi pubblicati in ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="681ee-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="681ee-166">Convalidare il trasferimento dei dati controllando i byte in ingresso e uscita.</span><span class="sxs-lookup"><span data-stu-id="681ee-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="681ee-167">Aprire una richiesta di supporto con [Guida e supporto di Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se continuano a verificarsi problemi.</span><span class="sxs-lookup"><span data-stu-id="681ee-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

