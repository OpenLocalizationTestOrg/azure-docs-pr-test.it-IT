---
title: Recupero di tabelle ARP - Resource Manager - Risoluzione dei problemi di Azure ExpressRoute | Documentazione Microsoft
description: Questa pagina vengono fornite istruzioni su hello recupero ARP tabelle per un circuito ExpressRoute
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
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="a910b-103">Recupero delle tabelle nel modello di distribuzione di gestione risorse di hello ARP</span><span class="sxs-lookup"><span data-stu-id="a910b-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a910b-104">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="a910b-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="a910b-105">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="a910b-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="a910b-106">In questo articolo illustra hello toolearn di passaggi hello che ARP tabelle per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a910b-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a910b-107">Questo documento è previsto toohelp la diagnosi e risoluzione dei problemi semplici.</span><span class="sxs-lookup"><span data-stu-id="a910b-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="a910b-108">Non è previsto toobe una sostituzione per il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a910b-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="a910b-109">È necessario aprire un ticket di supporto con [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) in caso di problema hello toosolve Impossibile utilizzando istruzioni hello descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="a910b-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="a910b-110">ARP (Address Resolution Protocol) e tabelle ARP</span><span class="sxs-lookup"><span data-stu-id="a910b-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="a910b-111">ARP (Address Resolution Protocol) è un protocollo di livello 2 definito in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="a910b-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="a910b-112">ARP è utilizzato toomap hello indirizzo Ethernet (indirizzo MAC) con un indirizzo ip.</span><span class="sxs-lookup"><span data-stu-id="a910b-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="a910b-113">la tabella ARP Hello fornisce un mapping di indirizzi ipv4 hello e un indirizzo MAC per un particolare peering.</span><span class="sxs-lookup"><span data-stu-id="a910b-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="a910b-114">la tabella ARP per un circuito ExpressRoute peering Hello fornisce hello le seguenti informazioni per ogni interfaccia (primario e secondario)</span><span class="sxs-lookup"><span data-stu-id="a910b-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="a910b-115">Mapping dell'indirizzo MAC locale router interfaccia ip indirizzo toohello</span><span class="sxs-lookup"><span data-stu-id="a910b-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="a910b-116">Mapping dell'indirizzo MAC ExpressRoute router interfaccia ip indirizzo toohello</span><span class="sxs-lookup"><span data-stu-id="a910b-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="a910b-117">Periodo di memorizzazione dei mapping hello</span><span class="sxs-lookup"><span data-stu-id="a910b-117">Age of hello mapping</span></span>

<span data-ttu-id="a910b-118">Le tabelle ARP consentono di convalidare la configurazione di livello 2 e risoluzione dei problemi di connettività di base di livello 2.</span><span class="sxs-lookup"><span data-stu-id="a910b-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="a910b-119">Tabella ARP di esempio:</span><span class="sxs-lookup"><span data-stu-id="a910b-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="a910b-120">Hello seguente sezione vengono fornite informazioni su come visualizzare hello tabelle ARP rilevate da router perimetrali di hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a910b-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="a910b-121">Prerequisiti per l'apprendimento delle tabelle ARP</span><span class="sxs-lookup"><span data-stu-id="a910b-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="a910b-122">Assicurarsi di disporre di hello dopo prima di avviare lo stato di avanzamento ulteriormente</span><span class="sxs-lookup"><span data-stu-id="a910b-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="a910b-123">Un circuito ExpressRoute valido configurato con almeno un peer.</span><span class="sxs-lookup"><span data-stu-id="a910b-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="a910b-124">circuito Hello deve essere completamente configurato dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="a910b-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="a910b-125">Utente (o il provider di servizi) deve avere configurato almeno un del peering di hello (Azure pubblico privato, Azure e Microsoft) su questo circuito.</span><span class="sxs-lookup"><span data-stu-id="a910b-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="a910b-126">Intervalli di indirizzi IP utilizzati per la configurazione di peering di hello (Azure pubblico privato, Azure e Microsoft).</span><span class="sxs-lookup"><span data-stu-id="a910b-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="a910b-127">Esaminare esempi assegnazione di indirizzi ip hello in hello [nella pagina requisiti di routing ExpressRoute](expressroute-routing.md) tooget la comprensione di come gli indirizzi ip sono mappati toointerfaces hello lato ExpressRoute e il lato.</span><span class="sxs-lookup"><span data-stu-id="a910b-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="a910b-128">È possibile ottenere informazioni sulla configurazione di peering hello esaminando hello [pagina Configurazione di peering ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a910b-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="a910b-129">Le informazioni dal team di rete / provider di connettività su indirizzi MAC hello delle interfacce utilizzato con questi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="a910b-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="a910b-130">È necessario che il modulo PowerShell più recente di hello per Azure (versione più recente o 1,50).</span><span class="sxs-lookup"><span data-stu-id="a910b-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="a910b-131">Recupero delle tabelle hello ARP per il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a910b-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="a910b-132">Questa sezione vengono fornite istruzioni su come visualizzare hello tabelle ARP per peering tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a910b-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="a910b-133">Si o il provider di servizi deve essere configurata hello peering prima di addentrarsi ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="a910b-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="a910b-134">Ogni circuito ha due percorsi (primario e secondario).</span><span class="sxs-lookup"><span data-stu-id="a910b-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="a910b-135">È possibile controllare la tabella ARP per ogni percorso hello in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="a910b-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="a910b-136">Tabelle ARP per il peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="a910b-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="a910b-137">Hello seguente cmdlet fornisce hello ARP tabelle per il peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="a910b-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="a910b-138">Esempio di output è illustrato di seguito per uno dei percorsi di hello</span><span class="sxs-lookup"><span data-stu-id="a910b-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="a910b-139">Tabelle ARP per il peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="a910b-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="a910b-140">Hello seguente cmdlet fornisce hello ARP tabelle per peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="a910b-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="a910b-141">Esempio di output è illustrato di seguito per uno dei percorsi di hello</span><span class="sxs-lookup"><span data-stu-id="a910b-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="a910b-142">Tabelle ARP per il peering di Microsoft</span><span class="sxs-lookup"><span data-stu-id="a910b-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="a910b-143">Hello seguente cmdlet fornisce hello ARP tabelle per il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="a910b-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="a910b-144">Esempio di output è illustrato di seguito per uno dei percorsi di hello</span><span class="sxs-lookup"><span data-stu-id="a910b-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="a910b-145">Come toouse queste informazioni</span><span class="sxs-lookup"><span data-stu-id="a910b-145">How toouse this information</span></span>
<span data-ttu-id="a910b-146">Hello tabella ARP di un peering utilizzabile toodetermine convalidare la configurazione di livello 2 e connettività.</span><span class="sxs-lookup"><span data-stu-id="a910b-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="a910b-147">Questa sezione offre una panoramica dell'aspetto delle tabelle ARP in scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="a910b-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="a910b-148">Tabella ARP quando un circuito è in stato operativo (stato previsto)</span><span class="sxs-lookup"><span data-stu-id="a910b-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="a910b-149">la tabella ARP Hello avrà una voce per il lato locale di hello con un indirizzo IP valido e l'indirizzo MAC e una voce simile per hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a910b-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="a910b-150">l'ottetto ultimo Hello dell'indirizzo ip locale di hello sarà sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="a910b-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="a910b-151">ottetti di ultima Hello dell'indirizzo ip di Microsoft hello sarà sempre un numero pari.</span><span class="sxs-lookup"><span data-stu-id="a910b-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="a910b-152">Hello stesso indirizzo MAC verrà visualizzato nella hello lato Microsoft per tutti i peering di 3 (principale / secondaria).</span><span class="sxs-lookup"><span data-stu-id="a910b-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="a910b-153">Tabella ARP quando il lato locale/provider di connettività presenta problemi</span><span class="sxs-lookup"><span data-stu-id="a910b-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="a910b-154">Se si verificano problemi con hello in locale o provider di connettività, si può vedere entrambi una sola voce verrà visualizzato in hello ARP tabella hello locale indirizzo MAC o visualizzerà incompleti.</span><span class="sxs-lookup"><span data-stu-id="a910b-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="a910b-155">Verranno visualizzati i mapping hello tra hello indirizzo MAC e indirizzo IP utilizzato in hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a910b-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="a910b-156">oppure</span><span class="sxs-lookup"><span data-stu-id="a910b-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="a910b-157">Aprire una richiesta di supporto con il toodebug di provider di connettività a questi problemi.</span><span class="sxs-lookup"><span data-stu-id="a910b-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="a910b-158">Se la tabella ARP hello non dispone di indirizzi IP delle interfacce hello eseguire il mapping di indirizzi tooMAC, hello esaminare le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="a910b-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="a910b-159">Se hello primo indirizzo IP del subnet hello /30 assegnato per il collegamento hello tra hello MSEE PR e MSEE viene utilizzato nell'interfaccia hello del MSEE PR</span><span class="sxs-lookup"><span data-stu-id="a910b-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="a910b-160">Azure Usa sempre l'indirizzo IP secondo hello per MSEEs.</span><span class="sxs-lookup"><span data-stu-id="a910b-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="a910b-161">Verificare se cliente hello (C-Tag) e i tag VLAN servizio (S-Tag) corrispondano entrambi in coppia MSEE PR e MSEE.</span><span class="sxs-lookup"><span data-stu-id="a910b-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="a910b-162">Tabella ARP quando il lato Microsoft presenta problemi</span><span class="sxs-lookup"><span data-stu-id="a910b-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="a910b-163">Non si noterà una tabella ARP visualizzata per il peering se sono presenti problemi in hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a910b-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="a910b-164">Aprire un ticket di assistenza al [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="a910b-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="a910b-165">Specificare che si è riscontrato un problema di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="a910b-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a910b-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a910b-166">Next Steps</span></span>
* <span data-ttu-id="a910b-167">Convalidare le configurazioni di livello 3 per il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a910b-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="a910b-168">Ottenere lo stato di hello toodetermine riepilogo route di sessioni BGP</span><span class="sxs-lookup"><span data-stu-id="a910b-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="a910b-169">Ottenere toodetermine tabella di route che i prefissi sono annunciati attraverso ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a910b-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="a910b-170">Convalidare il trasferimento dei dati controllando i byte in ingresso/uscita</span><span class="sxs-lookup"><span data-stu-id="a910b-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="a910b-171">Aprire un ticket di assistenza al [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se continuano a verificarsi problemi.</span><span class="sxs-lookup"><span data-stu-id="a910b-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

