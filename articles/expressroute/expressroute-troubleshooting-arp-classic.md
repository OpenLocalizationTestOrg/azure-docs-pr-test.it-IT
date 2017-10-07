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
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>Recupero delle tabelle nel modello di distribuzione classica hello ARP
> [!div class="op_single_selector"]
> * [PowerShell - Gestione risorse](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Classico](expressroute-troubleshooting-arp-classic.md)
> 
> 

In questo articolo vengono illustrati i passaggi hello per il recupero delle tabelle di hello protocollo ARP (Address Resolution) per il circuito ExpressRoute di Azure.

> [!IMPORTANT]
> Questo documento è previsto toohelp la diagnosi e risoluzione dei problemi semplici. Non è previsto toobe una sostituzione per il supporto tecnico Microsoft. Se è possibile risolvere il problema di hello utilizzando hello seguenti linee guida, aprire una richiesta di supporto con [Guida di Microsoft Azure e supporto](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>ARP (Address Resolution Protocol) e tabelle ARP
ARP è un protocollo di livello 2 che viene definito in [RFC 826](https://tools.ietf.org/html/rfc826). ARP è toomap usato un indirizzo IP tooan di Ethernet indirizzo (MAC).

Una tabella ARP fornisce un mapping di indirizzi IPv4 hello e un indirizzo MAC per un particolare peering. la tabella ARP per un circuito ExpressRoute peering Hello fornisce hello le seguenti informazioni per ogni interfaccia (primario e secondario):

1. Mapping di on-premise router interfaccia indirizzo tooa MAC indirizzo IP
2. Mapping di ExpressRoute router interfaccia indirizzo tooa MAC indirizzo IP
3. età Hello del mapping di hello

Le tabelle ARP consentono di convalidare la configurazione di livello 2 e la risoluzione dei problemi di connettività di base di livello 2.

Di seguito è riportato un esempio di tabella ARP:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Hello successiva sezione fornisce informazioni su come tooview hello tabelle ARP visualizzate da router perimetrali di hello ExpressRoute.

## <a name="prerequisites-for-using-arp-tables"></a>Prerequisiti per l'utilizzo delle tabelle ARP
Assicurarsi di aver seguito hello prima di continuare:

* Un circuito ExpressRoute valido configurato con almeno un peer. circuito Hello deve essere completamente configurato dal provider di connettività hello. Utente (o il provider di servizi) necessario configurare almeno un peering di hello (Azure pubblico privato, Azure o Microsoft) su questo circuito.
* Intervalli di indirizzi IP vengono utilizzati per la configurazione di peering di hello (Azure pubblico privato, Azure e Microsoft). Esaminare esempi assegnazione di indirizzi IP hello in hello [nella pagina requisiti di routing ExpressRoute](expressroute-routing.md) tooget la comprensione di come gli indirizzi IP sono mappati toointerfaces il aise e sul lato di ExpressRoute hello. È possibile ottenere informazioni sulla configurazione di peering hello esaminando hello [pagina Configurazione di peering ExpressRoute](expressroute-howto-routing-classic.md).
* Informazioni dal provider di team o la connettività di rete su indirizzi MAC hello delle interfacce hello utilizzati con questi indirizzi IP.
* modulo Windows PowerShell più recente Hello per Azure (versione 1,50 o versione successiva).

## <a name="arp-tables-for-your-expressroute-circuit"></a>Le tabelle ARP per il circuito ExpressRoute
In questa sezione vengono fornite istruzioni su come tooview hello ARP tabelle per ogni tipo di peering con PowerShell. Prima di continuare, l'utente o il provider di servizi deve tooconfigure hello peering. Ogni circuito ha due percorsi (primario e secondario). È possibile controllare la tabella ARP per ogni percorso hello in modo indipendente.

### <a name="arp-tables-for-azure-private-peering"></a>Tabelle ARP per il peering privato di Azure
Hello seguendo i cmdlet disponibili hello ARP tabelle per il peering privato di Azure:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

Di seguito è l'output di esempio per uno dei percorsi di hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tabelle ARP per il peering pubblico di Azure
Hello seguendo i cmdlet disponibili hello ARP tabelle per il peering pubblico di Azure:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

Di seguito è l'output di esempio per uno dei percorsi di hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Di seguito è l'output di esempio per uno dei percorsi di hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tabelle ARP per il peering di Microsoft
Hello seguente cmdlet fornisce hello ARP tabelle per il peering Microsoft:

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


Esempio di output è illustrato di seguito per uno dei percorsi di hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Come toouse queste informazioni
è possibile Hello tabella ARP di un peering connettività e la configurazione utilizzata toovalidate livello 2. Questa sezione offre una panoramica dell'aspetto delle tabelle ARP in scenari diversi.

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>La tabella ARP quando un circuito è in stato operativo (previsto)
* una voce per il lato locale di hello con un indirizzo IP e MAC e una voce simile per hello lato Microsoft Hello tabella ARP.
* l'ottetto ultimo Hello dell'indirizzo IP locale di hello è sempre un numero dispari.
* ottetti di ultima Hello dell'indirizzo IP di Microsoft hello sono sempre un numero pari.
* Hello stesso indirizzo MAC viene visualizzato sul lato di Microsoft per tutti i peering di tre (primario o secondario) hello.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>Tabella ARP quando è locale o quando il lato di provider di connettività hello presenta problemi
 Una sola voce viene visualizzata nella tabella ARP hello. Mostra il mapping di hello tra l'indirizzo MAC hello e indirizzo IP di hello utilizzato sul lato Microsoft hello.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> Se si riscontra un problema simile al seguente, aprire un supporto richiederla con il tooresolve di provider di connettività.
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>Tabella ARP quando hello lato Microsoft presenta dei problemi
* Non si noterà una tabella ARP visualizzata per il peering se sono presenti problemi in hello lato Microsoft.
* Aprire una richiesta di supporto con [Guida e supporto di Azure Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Specificare che si è riscontrato un problema di connettività di livello 2.

## <a name="next-steps"></a>Passaggi successivi
* Convalidare le configurazioni di livello 3 per il circuito ExpressRoute
  * Ottenere uno stato di hello route toodetermine riepilogo di sessioni BGP.
  * Ottenere un toodetermine tabella di route che i prefissi sono annunciati attraverso ExpressRoute.
* Convalidare il trasferimento dei dati controllando i byte in ingresso e uscita.
* Aprire una richiesta di supporto con [Guida e supporto di Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se continuano a verificarsi problemi.

