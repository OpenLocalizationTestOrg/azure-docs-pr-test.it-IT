---
title: 'Come tooconfigure routing (peering) per un circuito ExpressRoute: Gestione risorse: PowerShell: Azure | Documenti Microsoft'
description: In questo articolo vengono illustrati i passaggi hello per la creazione e il provisioning di hello privato, pubblico e peering Microsoft di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornamento o eliminazione di peering per il circuito.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>Creare e modificare il peering per un circuito ExpressRoute usando PowerShell

In questo articolo consente di creare e gestire la configurazione di routing per un circuito ExpressRoute nel modello di distribuzione di gestione risorse hello tramite PowerShell. È anche possibile controllare lo stato di hello, update o delete e deprovisioning peering per un circuito ExpressRoute. Se si desidera toouse toowork un metodo diverso con il circuito, selezionare un articolo da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-routing-cli.md)
> * [Video - Peering privato](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - Peering pubblico](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Peering Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Prerequisiti di configurazione

* Sarà necessario hello versione hello cmdlet PowerShell di gestione risorse di Azure. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). 
* Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md) pagina hello [requisiti di routing](expressroute-routing.md) pagina e hello [flussi di lavoro](expressroute-workflows.md) pagina prima di iniziare la configurazione.
* È necessario avere un circuito ExpressRoute attivo. Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e circuito hello abilitato dal provider di connettività prima di procedere. Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato per l'utente toobe toorun in grado di hello cmdlet in questo articolo.

Queste istruzioni si applicano solo toocircuits creato con il provider di servizi che offre servizi di connettività di livello 2. Se si usa un provider di servizi che offre servizi gestiti di livello 3 (in genere una VPN IP, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.

> [!IMPORTANT]
> È attualmente non inviano annunci peering configurato dai provider di servizi tramite il portale di Gestione servizi hello. L'abilitazione di questa funzionalità sarà presto disponibile. Rivolgersi al provider di servizi prima di configurare peering BGP.
> 
> 

Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft). È possibile configurare i peering nell'ordine desiderato. Tuttavia, è necessario assicurarsi completare hello configurazione di ogni peer uno alla volta. 

## <a name="azure-private-peering"></a>Peering privato di Azure

In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione peering privata per un circuito ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate peering privato di Azure

1. Importare il modulo di PowerShell hello per ExpressRoute.

  È necessario installare una versione più recente installer PowerShell hello da [PowerShell Gallery](http://www.powershellgallery.com/) e importare i moduli di gestione risorse di Azure hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello. È necessario toorun PowerShell come amministratore.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  Importare tutti i moduli AzureRM.* hello all'interno di hello noto l'intervallo di versioni semantico.

  ```powershell
  Import-AzureRM
  ```

  È anche possibile importare un modulo select all'interno di hello noto intervallo versione semantica.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Eseguire l'accesso tooyour account.

  ```powershell
  Login-AzureRmAccount
  ```

  Selezionare una sottoscrizione hello da circuito ExpressRoute toocreate.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Creare un circuito ExpressRoute.

  Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo fornito dal provider di connettività hello.

  Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.
3. Controllare toomake di circuito ExpressRoute hello assicurarsi che sia stato eseguito il provisioning e inoltre abilitato. Utilizzare hello di esempio seguente:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  risposta Hello è simile toohello esempio seguente:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configurare peering privato di Azure per il circuito hello. Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:

  * / 30 subnet per collegamento primario hello. subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.
  * / 30 subnet per collegamento secondario hello. subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.
  * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
  * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte. È possibile usare il numero AS privato per questo peering. Assicurarsi di non usare il numero 65515.
  * **Facoltativo:** un hash MD5 se si sceglie toouse uno.

  Utilizzare hello seguente esempio tooconfigure privata peering per il circuito di Azure:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Se si sceglie toouse un hash MD5, usare hello di esempio seguente:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview dettagli di peering privato di Azure

È possibile ottenere i dettagli di configurazione utilizzando hello di esempio seguente:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>configurazione di peering privato Azure tooupdate

È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente. In questo esempio hello ID VLAN del circuito hello viene aggiornato da too500 100.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>toodelete peering privato di Azure

È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:

> [!WARNING]
> È necessario assicurarsi che tutte le reti virtuali vengono scollegate dal hello circuito ExpressRoute prima di eseguire questo esempio. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Peering pubblico di Azure

In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione di peering pubblico per un circuito ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate peering pubblico di Azure

1. Importare il modulo di PowerShell hello per ExpressRoute.

  È necessario installare una versione più recente installer PowerShell hello da [PowerShell Gallery](http://www.powershellgallery.com/) e importare i moduli di gestione risorse di Azure hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello. È necessario toorun PowerShell come amministratore.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  Importare tutti i moduli AzureRM.* hello all'interno di hello noto l'intervallo di versioni semantico.

  ```powershell
  Import-AzureRM
  ```

  È anche possibile importare un modulo select all'interno di hello noto intervallo versione semantica.

  ```powershell
  Import-Module AzureRM.Network
```

  Eseguire l'accesso tooyour account.

  ```powershell
  Login-AzureRmAccount
  ```

  Selezionare una sottoscrizione hello da circuito ExpressRoute toocreate.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Creare un circuito ExpressRoute.

  Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo fornito dal provider di connettività hello.

  Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.
3. Controllare hello ExpressRoute circuito tooensure che sia stato eseguito il provisioning e inoltre abilitato. Utilizzare hello di esempio seguente:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  risposta Hello è simile toohello esempio seguente:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configurare peering pubblico di Azure per il circuito hello. Assicurarsi di avere le seguenti informazioni prima di continuare ulteriormente hello.

  * / 30 subnet per collegamento primario hello. Deve essere un prefisso IPv4 pubblico valido.
  * / 30 subnet per collegamento secondario hello. Deve essere un prefisso IPv4 pubblico valido.
  * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
  * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte.
  * **Facoltativo:** un hash MD5 se si sceglie toouse uno.

  Eseguire hello seguente esempio tooconfigure pubblici di peering per il circuito di Azure

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Se si sceglie toouse un hash MD5, usare hello di esempio seguente:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview dettagli di peering pubblico di Azure

È possibile ottenere i dettagli di configurazione mediante hello seguente cmdlet:

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>configurazione di peering pubblico Azure tooupdate

È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente. In questo esempio hello ID VLAN del circuito hello viene aggiornato da too600 200.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>toodelete peering pubblico di Azure

È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Peering Microsoft

In questa sezione consente di creare, ottenere, aggiornare ed eliminare le configurazioni di peering Microsoft hello per un circuito ExpressRoute.

> [!IMPORTANT]
> Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite hello peering Microsoft, anche se non sono definiti i filtri di route. Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito. Per altre informazioni, vedere [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurare un filtro di route per il peering Microsoft).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate peering Microsoft

1. Importare il modulo di PowerShell hello per ExpressRoute.

  È necessario installare una versione più recente installer PowerShell hello da [PowerShell Gallery](http://www.powershellgallery.com/) e importare i moduli di gestione risorse di Azure hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello. È necessario toorun PowerShell come amministratore.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  Importare tutti i moduli AzureRM.* hello all'interno di hello noto l'intervallo di versioni semantico.

  ```powershell
  Import-AzureRM
  ```

  È anche possibile importare un modulo select all'interno di hello noto intervallo versione semantica.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Eseguire l'accesso tooyour account.

  ```powershell
  Login-AzureRmAccount
  ```

  Selezionare una sottoscrizione hello da circuito ExpressRoute toocreate.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Creare un circuito ExpressRoute.

  Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo fornito dal provider di connettività hello.

  Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.
3. Controllare toomake di circuito ExpressRoute hello assicurarsi che sia stato eseguito il provisioning e inoltre abilitato. Utilizzare hello di esempio seguente:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  risposta Hello è simile toohello esempio seguente:

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configurare Microsoft peering per il circuito hello. Assicurarsi di aver hello le seguenti informazioni prima di procedere.

  * / 30 subnet per collegamento primario hello. Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.
  * / 30 subnet per collegamento secondario hello. Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.
  * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
  * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte.
  * I prefissi annunciati: È necessario fornire un elenco di tutti i prefissi Prevedi tooadvertise sessione BGP hello. Sono accettati solo prefissi di indirizzi IP pubblici. Se si prevede un set di prefissi toosend, è possibile inviare un elenco delimitato da virgole. I prefissi devono essere registrati tooyou in un RIR / IRR.
  * **Facoltativo:** cliente ASN: nel caso di annunci con prefissi non registrato toohello peering sotto forma di numero, è possibile specificare hello come numero toowhich sono registrati.
  * Nome del Registro di sistema di routing: È possibile specificare hello RIR / IRR contro cui hello come numero e i prefissi sono registrati.
  * **Facoltativo:** un hash MD5 se si sceglie toouse uno.

   Utilizzare hello seguendo l'esempio tooconfigure peering Microsoft per il circuito:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>dettagli di peering Microsoft tooget

È possibile ottenere i dettagli di configurazione mediante hello di esempio seguente:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configurazione di peering Microsoft tooupdate

È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente:

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>toodelete peering Microsoft

È possibile rimuovere la configurazione di peering eseguendo hello seguente cmdlet:

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>Passaggi successivi

Passaggio successivo, [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-arm.md).

* Per ulteriori informazioni sui flussi di lavoro ExpressRoute, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).
* Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)
* Per ulteriori informazioni sull’uso delle reti virtuali, vedere [Panoramica sulla rete virtuale](../virtual-network/virtual-networks-overview.md).
