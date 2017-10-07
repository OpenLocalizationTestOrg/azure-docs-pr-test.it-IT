---
title: Recupero di tabelle ARP - Modello di distribuzione classica - Risoluzione dei problemi di Azure ExpressRoute | Documentazione Microsoft
description: Questa pagina vengono fornite istruzioni per il recupero hello ARP tabelle per un circuito ExpressRoute.
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
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="c49cc-103">Recupero delle tabelle nel modello di distribuzione classica hello ARP</span><span class="sxs-lookup"><span data-stu-id="c49cc-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c49cc-104">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="c49cc-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="c49cc-105">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="c49cc-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="c49cc-106">In questo articolo vengono illustrati i passaggi hello per il recupero delle tabelle di hello protocollo ARP (Address Resolution) per il circuito ExpressRoute di Azure.</span><span class="sxs-lookup"><span data-stu-id="c49cc-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c49cc-107">Questo documento è previsto toohelp la diagnosi e risoluzione dei problemi semplici.</span><span class="sxs-lookup"><span data-stu-id="c49cc-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="c49cc-108">Non è previsto toobe una sostituzione per il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c49cc-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="c49cc-109">Se è possibile risolvere il problema di hello utilizzando hello seguenti linee guida, aprire una richiesta di supporto con [Guida di Microsoft Azure e supporto](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="c49cc-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="c49cc-110">ARP (Address Resolution Protocol) e tabelle ARP</span><span class="sxs-lookup"><span data-stu-id="c49cc-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="c49cc-111">ARP è un protocollo di livello 2 che viene definito in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="c49cc-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="c49cc-112">ARP è toomap usato un indirizzo IP tooan di Ethernet indirizzo (MAC).</span><span class="sxs-lookup"><span data-stu-id="c49cc-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="c49cc-113">Una tabella ARP fornisce un mapping di indirizzi IPv4 hello e un indirizzo MAC per un particolare peering.</span><span class="sxs-lookup"><span data-stu-id="c49cc-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="c49cc-114">la tabella ARP per un circuito ExpressRoute peering Hello fornisce hello le seguenti informazioni per ogni interfaccia (primario e secondario):</span><span class="sxs-lookup"><span data-stu-id="c49cc-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="c49cc-115">Mapping di on-premise router interfaccia indirizzo tooa MAC indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="c49cc-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="c49cc-116">Mapping di ExpressRoute router interfaccia indirizzo tooa MAC indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="c49cc-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="c49cc-117">età Hello del mapping di hello</span><span class="sxs-lookup"><span data-stu-id="c49cc-117">hello age of hello mapping</span></span>

<span data-ttu-id="c49cc-118">Le tabelle ARP consentono di convalidare la configurazione di livello 2 e la risoluzione dei problemi di connettività di base di livello 2.</span><span class="sxs-lookup"><span data-stu-id="c49cc-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="c49cc-119">Di seguito è riportato un esempio di tabella ARP:</span><span class="sxs-lookup"><span data-stu-id="c49cc-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="c49cc-120">Hello successiva sezione fornisce informazioni su come tooview hello tabelle ARP visualizzate da router perimetrali di hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c49cc-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="c49cc-121">Prerequisiti per l'utilizzo delle tabelle ARP</span><span class="sxs-lookup"><span data-stu-id="c49cc-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="c49cc-122">Assicurarsi di aver seguito hello prima di continuare:</span><span class="sxs-lookup"><span data-stu-id="c49cc-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="c49cc-123">Un circuito ExpressRoute valido configurato con almeno un peer.</span><span class="sxs-lookup"><span data-stu-id="c49cc-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="c49cc-124">circuito Hello deve essere completamente configurato dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="c49cc-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="c49cc-125">Utente (o il provider di servizi) necessario configurare almeno un peering di hello (Azure pubblico privato, Azure o Microsoft) su questo circuito.</span><span class="sxs-lookup"><span data-stu-id="c49cc-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="c49cc-126">Intervalli di indirizzi IP vengono utilizzati per la configurazione di peering di hello (Azure pubblico privato, Azure e Microsoft).</span><span class="sxs-lookup"><span data-stu-id="c49cc-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="c49cc-127">Esaminare esempi assegnazione di indirizzi IP hello in hello [nella pagina requisiti di routing ExpressRoute](expressroute-routing.md) tooget la comprensione di come gli indirizzi IP sono mappati toointerfaces il aise e sul lato di ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="c49cc-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="c49cc-128">È possibile ottenere informazioni sulla configurazione di peering hello esaminando hello [pagina Configurazione di peering ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c49cc-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="c49cc-129">Informazioni dal provider di team o la connettività di rete su indirizzi MAC hello delle interfacce hello utilizzati con questi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="c49cc-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="c49cc-130">modulo Windows PowerShell più recente Hello per Azure (versione 1,50 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="c49cc-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="c49cc-131">Le tabelle ARP per il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c49cc-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="c49cc-132">In questa sezione vengono fornite istruzioni su come tooview hello ARP tabelle per ogni tipo di peering con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c49cc-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="c49cc-133">Prima di continuare, l'utente o il provider di servizi deve tooconfigure hello peering.</span><span class="sxs-lookup"><span data-stu-id="c49cc-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="c49cc-134">Ogni circuito ha due percorsi (primario e secondario).</span><span class="sxs-lookup"><span data-stu-id="c49cc-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="c49cc-135">È possibile controllare la tabella ARP per ogni percorso hello in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="c49cc-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="c49cc-136">Tabelle ARP per il peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="c49cc-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="c49cc-137">Hello seguendo i cmdlet disponibili hello ARP tabelle per il peering privato di Azure:</span><span class="sxs-lookup"><span data-stu-id="c49cc-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="c49cc-138">Di seguito è l'output di esempio per uno dei percorsi di hello:</span><span class="sxs-lookup"><span data-stu-id="c49cc-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="c49cc-139">Tabelle ARP per il peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="c49cc-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="c49cc-140">Hello seguendo i cmdlet disponibili hello ARP tabelle per il peering pubblico di Azure:</span><span class="sxs-lookup"><span data-stu-id="c49cc-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="c49cc-141">Di seguito è l'output di esempio per uno dei percorsi di hello:</span><span class="sxs-lookup"><span data-stu-id="c49cc-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="c49cc-142">Di seguito è l'output di esempio per uno dei percorsi di hello:</span><span class="sxs-lookup"><span data-stu-id="c49cc-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="c49cc-143">Tabelle ARP per il peering di Microsoft</span><span class="sxs-lookup"><span data-stu-id="c49cc-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="c49cc-144">Hello seguente cmdlet fornisce hello ARP tabelle per il peering Microsoft:</span><span class="sxs-lookup"><span data-stu-id="c49cc-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="c49cc-145">Esempio di output è illustrato di seguito per uno dei percorsi di hello:</span><span class="sxs-lookup"><span data-stu-id="c49cc-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="c49cc-146">Come toouse queste informazioni</span><span class="sxs-lookup"><span data-stu-id="c49cc-146">How toouse this information</span></span>
<span data-ttu-id="c49cc-147">è possibile Hello tabella ARP di un peering connettività e la configurazione utilizzata toovalidate livello 2.</span><span class="sxs-lookup"><span data-stu-id="c49cc-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="c49cc-148">Questa sezione offre una panoramica dell'aspetto delle tabelle ARP in scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="c49cc-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="c49cc-149">La tabella ARP quando un circuito è in stato operativo (previsto)</span><span class="sxs-lookup"><span data-stu-id="c49cc-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="c49cc-150">una voce per il lato locale di hello con un indirizzo IP e MAC e una voce simile per hello lato Microsoft Hello tabella ARP.</span><span class="sxs-lookup"><span data-stu-id="c49cc-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="c49cc-151">l'ottetto ultimo Hello dell'indirizzo IP locale di hello è sempre un numero dispari.</span><span class="sxs-lookup"><span data-stu-id="c49cc-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="c49cc-152">ottetti di ultima Hello dell'indirizzo IP di Microsoft hello sono sempre un numero pari.</span><span class="sxs-lookup"><span data-stu-id="c49cc-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="c49cc-153">Hello stesso indirizzo MAC viene visualizzato sul lato di Microsoft per tutti i peering di tre (primario o secondario) hello.</span><span class="sxs-lookup"><span data-stu-id="c49cc-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="c49cc-154">Tabella ARP quando è locale o quando il lato di provider di connettività hello presenta problemi</span><span class="sxs-lookup"><span data-stu-id="c49cc-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="c49cc-155">Una sola voce viene visualizzata nella tabella ARP hello.</span><span class="sxs-lookup"><span data-stu-id="c49cc-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="c49cc-156">Mostra il mapping di hello tra l'indirizzo MAC hello e indirizzo IP di hello utilizzato sul lato Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="c49cc-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="c49cc-157">Se si riscontra un problema simile al seguente, aprire un supporto richiederla con il tooresolve di provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="c49cc-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="c49cc-158">Tabella ARP quando hello lato Microsoft presenta dei problemi</span><span class="sxs-lookup"><span data-stu-id="c49cc-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="c49cc-159">Non si noterà una tabella ARP visualizzata per il peering se sono presenti problemi in hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c49cc-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="c49cc-160">Aprire una richiesta di supporto con [Guida e supporto di Azure Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="c49cc-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="c49cc-161">Specificare che si è riscontrato un problema di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="c49cc-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c49cc-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c49cc-162">Next steps</span></span>
* <span data-ttu-id="c49cc-163">Convalidare le configurazioni di livello 3 per il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c49cc-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="c49cc-164">Ottenere uno stato di hello route toodetermine riepilogo di sessioni BGP.</span><span class="sxs-lookup"><span data-stu-id="c49cc-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="c49cc-165">Ottenere un toodetermine tabella di route che i prefissi sono annunciati attraverso ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c49cc-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="c49cc-166">Convalidare il trasferimento dei dati controllando i byte in ingresso e uscita.</span><span class="sxs-lookup"><span data-stu-id="c49cc-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="c49cc-167">Aprire una richiesta di supporto con [Guida e supporto di Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se continuano a verificarsi problemi.</span><span class="sxs-lookup"><span data-stu-id="c49cc-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

