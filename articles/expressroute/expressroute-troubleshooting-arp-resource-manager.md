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
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>Recupero delle tabelle nel modello di distribuzione di gestione risorse di hello ARP
> [!div class="op_single_selector"]
> * [PowerShell - Gestione risorse](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Classico](expressroute-troubleshooting-arp-classic.md)
> 
> 

In questo articolo illustra hello toolearn di passaggi hello che ARP tabelle per il circuito ExpressRoute. 

> [!IMPORTANT]
> Questo documento è previsto toohelp la diagnosi e risoluzione dei problemi semplici. Non è previsto toobe una sostituzione per il supporto tecnico Microsoft. È necessario aprire un ticket di supporto con [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) in caso di problema hello toosolve Impossibile utilizzando istruzioni hello descritto di seguito.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>ARP (Address Resolution Protocol) e tabelle ARP
ARP (Address Resolution Protocol) è un protocollo di livello 2 definito in [RFC 826](https://tools.ietf.org/html/rfc826). ARP è utilizzato toomap hello indirizzo Ethernet (indirizzo MAC) con un indirizzo ip.

la tabella ARP Hello fornisce un mapping di indirizzi ipv4 hello e un indirizzo MAC per un particolare peering. la tabella ARP per un circuito ExpressRoute peering Hello fornisce hello le seguenti informazioni per ogni interfaccia (primario e secondario)

1. Mapping dell'indirizzo MAC locale router interfaccia ip indirizzo toohello
2. Mapping dell'indirizzo MAC ExpressRoute router interfaccia ip indirizzo toohello
3. Periodo di memorizzazione dei mapping hello

Le tabelle ARP consentono di convalidare la configurazione di livello 2 e risoluzione dei problemi di connettività di base di livello 2. 

Tabella ARP di esempio: 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


Hello seguente sezione vengono fornite informazioni su come visualizzare hello tabelle ARP rilevate da router perimetrali di hello ExpressRoute. 

## <a name="prerequisites-for-learning-arp-tables"></a>Prerequisiti per l'apprendimento delle tabelle ARP
Assicurarsi di disporre di hello dopo prima di avviare lo stato di avanzamento ulteriormente

* Un circuito ExpressRoute valido configurato con almeno un peer. circuito Hello deve essere completamente configurato dal provider di connettività hello. Utente (o il provider di servizi) deve avere configurato almeno un del peering di hello (Azure pubblico privato, Azure e Microsoft) su questo circuito.
* Intervalli di indirizzi IP utilizzati per la configurazione di peering di hello (Azure pubblico privato, Azure e Microsoft). Esaminare esempi assegnazione di indirizzi ip hello in hello [nella pagina requisiti di routing ExpressRoute](expressroute-routing.md) tooget la comprensione di come gli indirizzi ip sono mappati toointerfaces hello lato ExpressRoute e il lato. È possibile ottenere informazioni sulla configurazione di peering hello esaminando hello [pagina Configurazione di peering ExpressRoute](expressroute-howto-routing-arm.md).
* Le informazioni dal team di rete / provider di connettività su indirizzi MAC hello delle interfacce utilizzato con questi indirizzi IP.
* È necessario che il modulo PowerShell più recente di hello per Azure (versione più recente o 1,50).

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>Recupero delle tabelle hello ARP per il circuito ExpressRoute
Questa sezione vengono fornite istruzioni su come visualizzare hello tabelle ARP per peering tramite PowerShell. Si o il provider di servizi deve essere configurata hello peering prima di addentrarsi ulteriormente. Ogni circuito ha due percorsi (primario e secondario). È possibile controllare la tabella ARP per ogni percorso hello in modo indipendente.

### <a name="arp-tables-for-azure-private-peering"></a>Tabelle ARP per il peering privato di Azure
Hello seguente cmdlet fornisce hello ARP tabelle per il peering privato di Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Esempio di output è illustrato di seguito per uno dei percorsi di hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tabelle ARP per il peering pubblico di Azure
Hello seguente cmdlet fornisce hello ARP tabelle per peering pubblico di Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Esempio di output è illustrato di seguito per uno dei percorsi di hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tabelle ARP per il peering di Microsoft
Hello seguente cmdlet fornisce hello ARP tabelle per il peering Microsoft

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Esempio di output è illustrato di seguito per uno dei percorsi di hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Come toouse queste informazioni
Hello tabella ARP di un peering utilizzabile toodetermine convalidare la configurazione di livello 2 e connettività. Questa sezione offre una panoramica dell'aspetto delle tabelle ARP in scenari diversi.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>Tabella ARP quando un circuito è in stato operativo (stato previsto)
* la tabella ARP Hello avrà una voce per il lato locale di hello con un indirizzo IP valido e l'indirizzo MAC e una voce simile per hello lato Microsoft. 
* l'ottetto ultimo Hello dell'indirizzo ip locale di hello sarà sempre un numero dispari.
* ottetti di ultima Hello dell'indirizzo ip di Microsoft hello sarà sempre un numero pari.
* Hello stesso indirizzo MAC verrà visualizzato nella hello lato Microsoft per tutti i peering di 3 (principale / secondaria). 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>Tabella ARP quando il lato locale/provider di connettività presenta problemi
Se si verificano problemi con hello in locale o provider di connettività, si può vedere entrambi una sola voce verrà visualizzato in hello ARP tabella hello locale indirizzo MAC o visualizzerà incompleti. Verranno visualizzati i mapping hello tra hello indirizzo MAC e indirizzo IP utilizzato in hello lato Microsoft. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

oppure
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Aprire una richiesta di supporto con il toodebug di provider di connettività a questi problemi. Se la tabella ARP hello non dispone di indirizzi IP delle interfacce hello eseguire il mapping di indirizzi tooMAC, hello esaminare le seguenti informazioni:
> 
> 1. Se hello primo indirizzo IP del subnet hello /30 assegnato per il collegamento hello tra hello MSEE PR e MSEE viene utilizzato nell'interfaccia hello del MSEE PR Azure Usa sempre l'indirizzo IP secondo hello per MSEEs.
> 2. Verificare se cliente hello (C-Tag) e i tag VLAN servizio (S-Tag) corrispondano entrambi in coppia MSEE PR e MSEE.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>Tabella ARP quando il lato Microsoft presenta problemi
* Non si noterà una tabella ARP visualizzata per il peering se sono presenti problemi in hello lato Microsoft. 
* Aprire un ticket di assistenza al [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Specificare che si è riscontrato un problema di connettività di livello 2. 

## <a name="next-steps"></a>Passaggi successivi
* Convalidare le configurazioni di livello 3 per il circuito ExpressRoute
  * Ottenere lo stato di hello toodetermine riepilogo route di sessioni BGP 
  * Ottenere toodetermine tabella di route che i prefissi sono annunciati attraverso ExpressRoute
* Convalidare il trasferimento dei dati controllando i byte in ingresso/uscita
* Aprire un ticket di assistenza al [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se continuano a verificarsi problemi.

