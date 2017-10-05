---
title: Recupero di tabelle ARP - Resource Manager - Risoluzione dei problemi di Azure ExpressRoute | Documentazione Microsoft
description: Questa pagina fornisce istruzioni su come ottenere tabelle ARP tabelle per un circuito ExpressRoute
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: a65b1ba2998eae33b3e73bd2492fbbf025eb5946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-resource-manager-deployment-model"></a><span data-ttu-id="98ee2-103">Recupero di tabelle ARP nel modello di distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="98ee2-103">Getting ARP tables in the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98ee2-104">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="98ee2-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="98ee2-105">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="98ee2-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="98ee2-106">Questo articolo illustra i passaggi per apprendere le tabelle ARP per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="98ee2-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="98ee2-107">Questo documento è progettato per aiutare l'utente a rilevare e risolvere i problemi semplici.</span><span class="sxs-lookup"><span data-stu-id="98ee2-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="98ee2-108">Non sostituisce tuttavia il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98ee2-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="98ee2-109">Se non si riesce a risolvere il problema tramite la procedura descritta di seguito, è necessario aprire un ticket di assistenza al [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .</span><span class="sxs-lookup"><span data-stu-id="98ee2-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable to solve the problem using the guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="98ee2-110">ARP (Address Resolution Protocol) e tabelle ARP</span><span class="sxs-lookup"><span data-stu-id="98ee2-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="98ee2-111">ARP (Address Resolution Protocol) è un protocollo di livello 2 definito in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="98ee2-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="98ee2-112">Il protocollo ARP viene usato per mappare l'indirizzo Ethernet (indirizzo MAC) con un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="98ee2-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="98ee2-113">La tabella ARP fornisce un mapping dell'indirizzo ipv4 e dell'indirizzo MAC per un particolare peering.</span><span class="sxs-lookup"><span data-stu-id="98ee2-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="98ee2-114">La tabella ARP del peering di un circuito ExpressRoute fornisce le informazioni seguenti per ogni interfaccia (primaria e secondaria):</span><span class="sxs-lookup"><span data-stu-id="98ee2-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="98ee2-115">Mapping dell'indirizzo IP dell'interfaccia del router locale all'indirizzo MAC</span><span class="sxs-lookup"><span data-stu-id="98ee2-115">Mapping of on-premises router interface ip address to the MAC address</span></span>
2. <span data-ttu-id="98ee2-116">Mapping dell'indirizzo IP dell'interfaccia del router di ExpressRoute all'indirizzo MAC</span><span class="sxs-lookup"><span data-stu-id="98ee2-116">Mapping of ExpressRoute router interface ip address to the MAC address</span></span>
3. <span data-ttu-id="98ee2-117">Età del mapping</span><span class="sxs-lookup"><span data-stu-id="98ee2-117">Age of the mapping</span></span>

<span data-ttu-id="98ee2-118">Le tabelle ARP consentono di convalidare la configurazione di livello 2 e risoluzione dei problemi di connettività di base di livello 2.</span><span class="sxs-lookup"><span data-stu-id="98ee2-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="98ee2-119">Tabella ARP di esempio:</span><span class="sxs-lookup"><span data-stu-id="98ee2-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="98ee2-120">La sezione seguente fornisce informazioni su come visualizzare le tabelle ARP visualizzate tramite i router perimetrali di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="98ee2-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="98ee2-121">Prerequisiti per l'apprendimento delle tabelle ARP</span><span class="sxs-lookup"><span data-stu-id="98ee2-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="98ee2-122">Prima di procedere, verificare che siano presenti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="98ee2-122">Ensure that you have the following before you progress further</span></span>

* <span data-ttu-id="98ee2-123">Un circuito ExpressRoute valido configurato con almeno un peer.</span><span class="sxs-lookup"><span data-stu-id="98ee2-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="98ee2-124">Il circuito deve essere completamente configurato dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="98ee2-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="98ee2-125">L'utente o il provider di connettività deve aver configurato almeno un peer (privato di Azure, pubblico di Azure e Microsoft) su questo circuito.</span><span class="sxs-lookup"><span data-stu-id="98ee2-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="98ee2-126">Gli intervalli degli indirizzi IP usati per la configurazione del peer (privato di Azure, pubblico di Azure e Microsoft).</span><span class="sxs-lookup"><span data-stu-id="98ee2-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="98ee2-127">Consultare gli esempi di assegnazione dell'indirizzo IP in [Requisiti per il routing di ExpressRoute](expressroute-routing.md) per ottenere informazioni sul mapping degli indirizzi IP verso le interfacce sul lato utente e sul lato ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="98ee2-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span></span> <span data-ttu-id="98ee2-128">È possibile ottenere informazioni sulla configurazione del peering consultando la [pagina sulla configurazione del peering di ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="98ee2-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="98ee2-129">Informazioni dal team di rete/provider di connettività sugli indirizzi MAC delle interfacce usate con questi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="98ee2-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="98ee2-130">È necessario disporre del modulo PowerShell più recente per Azure (versione 1.50 o successiva).</span><span class="sxs-lookup"><span data-stu-id="98ee2-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-the-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="98ee2-131">Ottenere tabelle ARP per il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98ee2-131">Getting the ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="98ee2-132">Questa sezione fornisce istruzioni su come visualizzare le tabelle ARP per il peering tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98ee2-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="98ee2-133">Prima di procedere all'elaborazione, l'utente o il provider di connettività devono aver configurato il peering.</span><span class="sxs-lookup"><span data-stu-id="98ee2-133">You or your connectivity provider must have configured the peering before progressing further.</span></span> <span data-ttu-id="98ee2-134">Ogni circuito ha due percorsi (primario e secondario).</span><span class="sxs-lookup"><span data-stu-id="98ee2-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="98ee2-135">È possibile controllare la tabella ARP di ogni percorso in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="98ee2-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="98ee2-136">Tabelle ARP per il peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="98ee2-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="98ee2-137">Il cmdlet seguente fornisce le tabelle ARP per il peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="98ee2-137">The following cmdlet provides the ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="98ee2-138">Di seguito è illustrato un esempio di output per uno dei percorsi</span><span class="sxs-lookup"><span data-stu-id="98ee2-138">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="98ee2-139">Tabelle ARP per il peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="98ee2-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="98ee2-140">Il cmdlet seguente fornisce le tabelle ARP per il peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="98ee2-140">The following cmdlet provides the ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="98ee2-141">Di seguito è illustrato un esempio di output per uno dei percorsi</span><span class="sxs-lookup"><span data-stu-id="98ee2-141">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="98ee2-142">Tabelle ARP per il peering di Microsoft</span><span class="sxs-lookup"><span data-stu-id="98ee2-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="98ee2-143">Il cmdlet seguente fornisce le tabelle ARP per il peering di Microsoft</span><span class="sxs-lookup"><span data-stu-id="98ee2-143">The following cmdlet provides the ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="98ee2-144">Di seguito è illustrato un esempio di output per uno dei percorsi</span><span class="sxs-lookup"><span data-stu-id="98ee2-144">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="98ee2-145">Procedura: Come usare queste informazioni</span><span class="sxs-lookup"><span data-stu-id="98ee2-145">How to use this information</span></span>
<span data-ttu-id="98ee2-146">La tabella ARP di un peer può essere usata per determinare la connettività e la configurazione di livello 2 valide.</span><span class="sxs-lookup"><span data-stu-id="98ee2-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="98ee2-147">Questa sezione offre una panoramica dell'aspetto delle tabelle ARP in scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="98ee2-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="98ee2-148">Tabella ARP quando un circuito è in stato operativo (stato previsto)</span><span class="sxs-lookup"><span data-stu-id="98ee2-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="98ee2-149">La tabella ARP conterrà una voce per il lato locale con un indirizzo IP e un indirizzo MAC valido e una voce simile per il lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98ee2-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span></span> 
* <span data-ttu-id="98ee2-150">L'ultimo ottetto dell'indirizzo IP locale sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="98ee2-150">The last octet of the on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="98ee2-151">L'ultimo ottetto dell'indirizzo IP Microsoft sarà sempre un numero pari.</span><span class="sxs-lookup"><span data-stu-id="98ee2-151">The last octet of the Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="98ee2-152">Lo stesso indirizzo MAC verrà visualizzato sul lato Microsoft per tutti i 3 peer (principale/secondario).</span><span class="sxs-lookup"><span data-stu-id="98ee2-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="98ee2-153">Tabella ARP quando il lato locale/provider di connettività presenta problemi</span><span class="sxs-lookup"><span data-stu-id="98ee2-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="98ee2-154">In caso di problemi a livello di provider di connettività o locale, è possibile che nella tabella ARP risulti inclusa una sola voce o che l'indirizzo MAC locale venga visualizzato incompleto.</span><span class="sxs-lookup"><span data-stu-id="98ee2-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="98ee2-155">Viene mostrato il mapping tra gli indirizzi MAC e IP usati sul lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98ee2-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="98ee2-156">oppure</span><span class="sxs-lookup"><span data-stu-id="98ee2-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="98ee2-157">Aprire una richiesta di supporto al provider di connettività per il debug di questi problemi.</span><span class="sxs-lookup"><span data-stu-id="98ee2-157">Open a support request with your connectivity provider to debug such issues.</span></span> <span data-ttu-id="98ee2-158">Se la tabella ARP non dispone di indirizzi IP delle interfacce associate agli indirizzi MAC, esaminare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="98ee2-158">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
> 
> 1. <span data-ttu-id="98ee2-159">Se il primo indirizzo IP delle /30 subnet assegnate per il collegamento tra il MSEE-PR e il MSEE viene usato nell'interfaccia di MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="98ee2-159">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="98ee2-160">Azure usa sempre il secondo indirizzo IP per MSEE.</span><span class="sxs-lookup"><span data-stu-id="98ee2-160">Azure always uses the second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="98ee2-161">Verificare se i tag VLAN del cliente (C-Tag) e del servizio (S-Tag) corrispondono nella coppia MSEE-PR e MSEE.</span><span class="sxs-lookup"><span data-stu-id="98ee2-161">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="98ee2-162">Tabella ARP quando il lato Microsoft presenta problemi</span><span class="sxs-lookup"><span data-stu-id="98ee2-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="98ee2-163">Se sono presenti problemi sul lato Microsoft, non verrà visualizzata la tabella ARP illustrata per il peering.</span><span class="sxs-lookup"><span data-stu-id="98ee2-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span> 
* <span data-ttu-id="98ee2-164">Aprire un ticket di assistenza al [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="98ee2-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="98ee2-165">Specificare che si è riscontrato un problema di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="98ee2-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="98ee2-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98ee2-166">Next Steps</span></span>
* <span data-ttu-id="98ee2-167">Convalidare le configurazioni di livello 3 per il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98ee2-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="98ee2-168">Ottenere un riepilogo del routing per determinare lo stato delle sessioni BGP</span><span class="sxs-lookup"><span data-stu-id="98ee2-168">Get route summary to determine the state of BGP sessions</span></span> 
  * <span data-ttu-id="98ee2-169">Ottenere la tabella del routing per stabilire i prefissi pubblicati in ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98ee2-169">Get route table to determine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="98ee2-170">Convalidare il trasferimento dei dati controllando i byte in ingresso/uscita</span><span class="sxs-lookup"><span data-stu-id="98ee2-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="98ee2-171">Aprire un ticket di assistenza al [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se continuano a verificarsi problemi.</span><span class="sxs-lookup"><span data-stu-id="98ee2-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

