---
title: 'Come tooconfigure routing (peering) per un circuito ExpressRoute: Azure: classico | Documenti Microsoft'
description: In questo articolo vengono illustrati i passaggi hello per la creazione e il provisioning di hello privato, pubblico e peering Microsoft di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornamento o eliminazione di peering per il circuito.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Creare e modificare il peering per un circuito ExpressRoute (versione classica)
> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-routing-cli.md)
> * [Video - Peering privato](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - Peering pubblico](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Peering Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-routing-classic.md)
> 

In questo articolo illustra toocreate passaggi hello e gestire la configurazione di routing per un circuito ExpressRoute con PowerShell e hello modello di distribuzione classica. passaggi di Hello riportati di seguito verranno inoltre Visualizza come stato hello toocheck, aggiornare, o eliminare e il deprovisioning di peering per un circuito ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Informazioni sui modelli di distribuzione di Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Prerequisiti di configurazione
* Sarà necessario hello versione hello cmdlet PowerShell di gestione del servizio di Azure (SM). Per altre informazioni, vedere [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview).  
* Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md) pagina hello [requisiti di routing](expressroute-routing.md) pagina e hello [flussi di lavoro](expressroute-workflows.md) pagina prima di iniziare la configurazione.
* È necessario avere un circuito ExpressRoute attivo. Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e circuito hello abilitato dal provider di connettività prima di procedere. Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato per l'utente toobe toorun in grado di hello cmdlet descritti di seguito.

> [!IMPORTANT]
> Queste istruzioni si applicano solo toocircuits creato con il provider di servizi che offre servizi di connettività di livello 2. Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IPVPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.
> 
> 

Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft). È possibile configurare i peering nell'ordine desiderato. Tuttavia, è necessario assicurarsi completare hello configurazione di ogni peer uno alla volta.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Accedi tooyour account Azure e selezionare una sottoscrizione
1. Aprire la console di PowerShell con diritti elevati e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

        Login-AzureRmAccount

2. Controllare le sottoscrizioni di hello per account hello.

        Get-AzureRmSubscription

3. Se si dispone di più di una sottoscrizione, selezionare una sottoscrizione di hello che si desidera toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Successivamente, utilizzare hello seguente cmdlet tooadd tooPowerShell la sottoscrizione di Azure per il modello di distribuzione classica hello.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Peering privato di Azure
In questa sezione vengono fornite istruzioni su come toocreate, ottenere, aggiornare ed eliminare hello Azure configurazione peering privata per un circuito ExpressRoute. 

### <a name="toocreate-azure-private-peering"></a>toocreate peering privato di Azure
1. **Importare il modulo di PowerShell hello per ExpressRoute.**
   
    È necessario importare i moduli di Azure ed ExpressRoute hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello. I moduli di Azure ed ExpressRoute hello tooimport di comandi seguenti di hello esecuzione nella sessione di PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Creare un circuito ExpressRoute.**
   
    Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e fare in modo fornito dal provider di connettività hello. Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, istruzioni hello riportato di seguito. 
3. **Controllare tooensure circuito ExpressRoute di hello che è disponibile.**
   
    È innanzitutto necessario archiviare toosee se hello circuito ExpressRoute è stato eseguito il provisioning e inoltre abilitato. Vedere l'esempio hello riportato di seguito.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Assicurarsi che il circuito hello viene illustrato come provisioning eseguito e abilitato. In caso contrario, utilizzare il tooget di provider di connettività del circuito toohello necessarie sullo stato di e.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurare peering privato di Azure per il circuito hello.**
   
    Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:
   
   * / 30 subnet per collegamento primario hello. Non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.
   * / 30 subnet per collegamento secondario hello. Non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.
   * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
   * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte. È possibile usare il numero AS privato per questo peering. Assicurarsi di non usare il numero 65515.
   * Hash MD5 se si sceglie toouse uno. **Facoltativo**.
     
    È possibile eseguire hello seguente tooconfigure cmdlet peering privato di Azure per il circuito.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100
     
    È possibile utilizzare i cmdlet di hello riportato di seguito se si sceglie toouse un hash MD5.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview dettagli di peering privato di Azure
È possibile ottenere i dettagli di configurazione mediante hello seguenti cmdlet

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>configurazione di peering privato Azure tooupdate
È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello cmdlet seguente. Nel seguente esempio hello hello ID VLAN del circuito hello viene aggiornato da too500 100.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete peering privato di Azure
È possibile rimuovere la configurazione di peering eseguendo hello cmdlet seguente.

> [!WARNING]
> È necessario assicurarsi che tutte le reti virtuali vengono scollegate dal hello circuito ExpressRoute prima di eseguire questo cmdlet. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Peering pubblico di Azure
In questa sezione vengono fornite istruzioni su come toocreate, ottenere, aggiornare ed eliminare hello Azure configurazione di peering pubblico per un circuito ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate peering pubblico di Azure
1. **Importare il modulo di PowerShell hello per ExpressRoute.**
   
    È necessario importare i moduli di Azure ed ExpressRoute hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello. I moduli di Azure ed ExpressRoute hello tooimport di comandi seguenti di hello esecuzione nella sessione di PowerShell hello. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Creare un circuito ExpressRoute**
   
    Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e fare in modo fornito dal provider di connettività hello. Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività pubblici di peering per l'utente di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, istruzioni hello riportato di seguito.
3. **Tooensure circuito ExpressRoute di controllo che è disponibile**
   
    È innanzitutto necessario archiviare toosee se hello circuito ExpressRoute è stato eseguito il provisioning e inoltre abilitato. Vedere l'esempio hello riportato di seguito.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Assicurarsi che il circuito hello viene illustrato come provisioning eseguito e abilitato. In caso contrario, utilizzare il tooget di provider di connettività del circuito toohello necessarie sullo stato di e.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurare peering pubblico di Azure per il circuito hello**
   
    Verificare di disporre di hello le seguenti informazioni prima di procedere ulteriormente.
   
   * / 30 subnet per collegamento primario hello. Deve essere un prefisso IPv4 pubblico valido.
   * / 30 subnet per collegamento secondario hello. Deve essere un prefisso IPv4 pubblico valido.
   * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
   * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte.
   * Hash MD5 se si sceglie toouse uno. **Facoltativo**.
     
    È possibile eseguire i seguenti cmdlet tooconfigure peering pubblico di Azure per il circuito hello
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200
     
    È possibile utilizzare i cmdlet di hello riportato di seguito se si sceglie toouse un hash MD5
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview dettagli di peering pubblico di Azure
È possibile ottenere i dettagli di configurazione mediante hello seguenti cmdlet

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>configurazione di peering pubblico Azure tooupdate
È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello seguenti cmdlet

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

ID VLAN del circuito hello Hello viene aggiornato da 200 too600 in hello sopra riportato.

### <a name="toodelete-azure-public-peering"></a>toodelete peering pubblico di Azure
È possibile rimuovere la configurazione di peering eseguendo i seguenti cmdlet hello

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Peering Microsoft
In questa sezione vengono fornite istruzioni su come toocreate, ottenere, aggiornare ed eliminare le configurazioni di peering Microsoft hello per un circuito ExpressRoute. 

### <a name="toocreate-microsoft-peering"></a>toocreate peering Microsoft
1. **Importare il modulo di PowerShell hello per ExpressRoute.**
   
    È necessario importare i moduli di Azure ed ExpressRoute hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello. I moduli di Azure ed ExpressRoute hello tooimport di comandi seguenti di hello esecuzione nella sessione di PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Creare un circuito ExpressRoute**
   
    Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e fare in modo fornito dal provider di connettività hello. Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, istruzioni hello riportato di seguito.
3. **Tooensure circuito ExpressRoute di controllo che è disponibile**
   
    È innanzitutto necessario archiviare toosee se hello circuito ExpressRoute è in stato di provisioning eseguito e abilitato.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Assicurarsi che il circuito hello viene illustrato come provisioning eseguito e abilitato. In caso contrario, utilizzare il tooget di provider di connettività del circuito toohello necessarie sullo stato di e.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurare Microsoft peering per il circuito hello**
   
    Assicurarsi di aver hello le seguenti informazioni prima di procedere.
   
   * / 30 subnet per collegamento primario hello. Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.
   * / 30 subnet per collegamento secondario hello. Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.
   * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
   * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte.
   * I prefissi annunciati: È necessario fornire un elenco di tutti i prefissi Prevedi tooadvertise sessione BGP hello. Sono accettati solo prefissi di indirizzi IP pubblici. Se si prevede un set di prefissi toosend, è possibile inviare un elenco separato da virgole. I prefissi devono essere registrati tooyou in un RIR / IRR.
   * Cliente ASN: Se si desidera annunciare prefissi che non sono registrato toohello peering sotto forma di numero, è possibile specificare hello come numero toowhich che sono registrati. **Facoltativo**.
   * Nome del Registro di sistema di routing: È possibile specificare hello RIR / IRR contro cui hello come numero e i prefissi sono registrati.
   * Hash MD5, se si sceglie toouse uno. **Facoltativo.**
     
    È possibile eseguire hello seguente pering Microsoft tooconfigure di cmdlet per il circuito
     
        New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>dettagli di peering Microsoft tooview
È possibile ottenere i dettagli di configurazione mediante hello cmdlet seguente.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>configurazione di peering Microsoft tooupdate
È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello cmdlet seguente.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete peering Microsoft
È possibile rimuovere la configurazione di peering eseguendo hello cmdlet seguente.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Passaggi successivi
Successivamente, [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-classic.md).

* Per ulteriori informazioni sui flussi di lavoro, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).
* Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)

