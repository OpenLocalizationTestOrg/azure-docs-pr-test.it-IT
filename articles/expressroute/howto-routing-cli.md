---
title: 'Come tooconfigure routing per un circuito ExpressRoute di Azure: CLI | Documenti Microsoft'
description: In questo articolo consente di creare ed eseguire il provisioning di hello privato, pubblico e peering Microsoft di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornamento o eliminazione di peering per il circuito.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Creare e modificare il routing per un circuito ExpressRoute con l'interfaccia della riga di comando

In questo articolo consente di creare e gestire la configurazione di routing per un circuito ExpressRoute nel modello di distribuzione di gestione risorse hello utilizzando CLI. È anche possibile controllare lo stato di hello, update o delete e deprovisioning peering per un circuito ExpressRoute. Se si desidera toouse toowork un metodo diverso con il circuito, selezionare un articolo da hello seguente elenco:

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

* Prima di iniziare, installare hello versione i comandi CLI hello (2.0 o versione successivo). Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli).
* Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flusso di lavoro](expressroute-workflows.md) pagine prima di iniziare la configurazione.
* È necessario avere un circuito ExpressRoute attivo. Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](howto-circuit-cli.md) e circuito hello abilitato dal provider di connettività prima di procedere. Hello circuito ExpressRoute deve essere in uno stato di provisioning e attivato per consentire i comandi di hello in grado di toorun toobe in questo articolo.

Queste istruzioni si applicano solo toocircuits creato con il provider di servizi che offre servizi di connettività di livello 2. Se si usa un provider di servizi che offre servizi gestiti di livello 3 (in genere una VPN IP, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.

Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft). È possibile configurare i peering nell'ordine desiderato. Tuttavia, è necessario assicurarsi completare hello configurazione di ogni peer uno alla volta.

## <a name="azure-private-peering"></a>Peering privato di Azure

In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione peering privata per un circuito ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate peering privato di Azure

1. Installare hello l'ultima versione di CLI di Azure. È necessario utilizzare una versione più recente di hello di hello Azure interfaccia della riga di comando (CLI). * hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.

  ```azurecli
  az login
  ```

  Selezionare la sottoscrizione di hello da circuito ExpressRoute toocreate

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Creare un circuito ExpressRoute. Seguire hello istruzioni toocreate un [circuito ExpressRoute](howto-circuit-cli.md) e fare in modo fornito dal provider di connettività hello.

  Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.
3. Controllare toomake di circuito ExpressRoute hello assicurarsi che sia stato eseguito il provisioning e inoltre abilitato. Utilizzare hello di esempio seguente:

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  risposta Hello è simile toohello esempio seguente:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configurare peering privato di Azure per il circuito hello. Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:

  * / 30 subnet per collegamento primario hello. subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.
  * / 30 subnet per collegamento secondario hello. subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.
  * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
  * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte. È possibile usare il numero AS privato per questo peering. Assicurarsi di non usare il numero 65515.
  * **Facoltativo:** un hash MD5 se si sceglie toouse uno.

  Utilizzare hello seguente esempio tooconfigure privata peering per il circuito di Azure:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Se si sceglie toouse un hash MD5, usare hello di esempio seguente:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview dettagli di peering privato di Azure

È possibile ottenere i dettagli di configurazione utilizzando hello di esempio seguente:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

Hello l'output è simile toohello seguente esempio:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>configurazione di peering privato Azure tooupdate

È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente. In questo esempio hello ID VLAN del circuito hello viene aggiornato da too500 100.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete peering privato di Azure

È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:

> [!WARNING]
> È necessario assicurarsi che tutte le reti virtuali vengono scollegate dal hello circuito ExpressRoute prima di eseguire questo esempio. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Peering pubblico di Azure

In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione di peering pubblico per un circuito ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate peering pubblico di Azure

1. Installare hello l'ultima versione di CLI di Azure. È necessario utilizzare una versione più recente di hello di hello Azure interfaccia della riga di comando (CLI). * hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.

  ```azurecli
  az login
  ```

  Selezionare la sottoscrizione di hello per cui si desidera circuito ExpressRoute toocreate.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Creare un circuito ExpressRoute.  Seguire hello istruzioni toocreate un [circuito ExpressRoute](howto-circuit-cli.md) e fare in modo fornito dal provider di connettività hello.

  Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di connettività di abilitare il peering privato di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.
3. Controllare hello ExpressRoute circuito tooensure che sia stato eseguito il provisioning e inoltre abilitato. Utilizzare hello di esempio seguente:

  ```azurecli
  az network express-route list
  ```

  risposta Hello è simile toohello esempio seguente:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configurare peering pubblico di Azure per il circuito hello. Assicurarsi di avere le seguenti informazioni prima di continuare ulteriormente hello.

  * / 30 subnet per collegamento primario hello. Deve essere un prefisso IPv4 pubblico valido.
  * / 30 subnet per collegamento secondario hello. Deve essere un prefisso IPv4 pubblico valido.
  * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
  * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte.
  * **Facoltativo:** un hash MD5 se si sceglie toouse uno.

  Eseguire hello seguente esempio tooconfigure pubblici di peering per il circuito di Azure:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Se si sceglie toouse un hash MD5, usare hello di esempio seguente:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.

### <a name="tooview-azure-public-peering-details"></a>tooview dettagli di peering pubblico di Azure

È possibile ottenere i dettagli di configurazione mediante hello di esempio seguente:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

Hello l'output è simile toohello seguente esempio:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>configurazione di peering pubblico Azure tooupdate

È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente. In questo esempio hello ID VLAN del circuito hello viene aggiornato da too600 200.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete peering pubblico di Azure

È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Peering Microsoft

In questa sezione consente di creare, ottenere, aggiornare ed eliminare le configurazioni di peering Microsoft hello per un circuito ExpressRoute.

> [!IMPORTANT]
> Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite hello peering Microsoft, anche se non sono definiti i filtri di route. Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito. Per altre informazioni, vedere [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurare un filtro di route per il peering Microsoft).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate peering Microsoft

1. Installare hello l'ultima versione di CLI di Azure. Utilizzare hello più recente di hello Azure interfaccia della riga di comando (CLI). * hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.

  ```azurecli
  az login
  ```

  Selezionare la sottoscrizione di hello per cui si desidera circuito ExpressRoute toocreate.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Creare un circuito ExpressRoute. Seguire hello istruzioni toocreate un [circuito ExpressRoute](howto-circuit-cli.md) e fare in modo fornito dal provider di connettività hello.

  Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure. In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello. Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.

3. Controllare toomake di circuito ExpressRoute hello assicurarsi che sia stato eseguito il provisioning e inoltre abilitato. Utilizzare hello di esempio seguente:

  ```azurecli
  az network express-route list
  ```

  risposta Hello è simile toohello esempio seguente:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
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

   Eseguire hello seguendo l'esempio tooconfigure peering Microsoft per il circuito:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>dettagli di peering Microsoft tooget

È possibile ottenere i dettagli di configurazione utilizzando hello di esempio seguente:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

Hello l'output è simile toohello seguente esempio:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configurazione di peering Microsoft tooupdate

È possibile aggiornare qualsiasi parte della configurazione di hello. Hello annunciati prefissi del circuito hello in corso l'aggiornamento da too124.1.0.0/24 123.1.0.0/24 nel seguente esempio hello:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete peering Microsoft

È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Passaggi successivi

Passaggio successivo, [collegare un circuito ExpressRoute di tooan rete virtuale](howto-linkvnet-cli.md).

* Per ulteriori informazioni sui flussi di lavoro ExpressRoute, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).
* Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)
* Per ulteriori informazioni sull’uso delle reti virtuali, vedere [Panoramica sulla rete virtuale](../virtual-network/virtual-networks-overview.md).