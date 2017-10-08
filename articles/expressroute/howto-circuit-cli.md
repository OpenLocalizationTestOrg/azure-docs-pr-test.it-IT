---
title: 'Creare e modificare un circuito Azure ExpressRoute: interfaccia della riga di comando | Microsoft Docs'
description: In questo articolo viene descritto come toocreate, eseguire il provisioning, verificare, aggiornare, eliminare e il deprovisioning di un circuito ExpressRoute tramite CLI.
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
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>Creare e modificare un circuito ExpressRoute tramite l'interfaccia della riga di comando


In questo articolo viene descritto come toocreate un circuito ExpressRoute di Azure tramite hello interfaccia della riga di comando (CLI). Mostra anche come stato hello toocheck, aggiornare, o eliminare e il deprovisioning di un circuito. Se si desidera toouse toowork un metodo diverso con circuiti ExpressRoute, è possibile selezionare l'articolo hello da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-circuit-cli.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>Prima di iniziare

* Prima di iniziare, installare hello versione i comandi CLI hello (2.0 o versione successivo). Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli) e [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).
* Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.

## <a name="create-and-provision-an-expressroute-circuit"></a>Creare un circuito ExpressRoute ed eseguirne il provisioning

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Accedi tooyour account Azure e selezionare la sottoscrizione

toobegin della configurazione, accedi tooyour account Azure. Hello seguenti esempi toohelp che ci si connette, utilizzare:

```azurecli
az login
```

Controllare le sottoscrizioni di hello per account hello.

```azurecli
az account list
```

Selezionare la sottoscrizione di hello per cui si desidera toocreate un circuito ExpressRoute.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Ottenere l'elenco di hello di provider supportati, posizioni e delle larghezze di banda

Prima di creare un circuito ExpressRoute, è necessario l'elenco di hello del provider di connettività supportate, località e le opzioni di larghezza di banda. Hello CLI comando 'az express route elenco-servizio-provider di rete' Restituisce queste informazioni, che verranno usati nei passaggi successivi:

```azurecli
az network express-route list-service-providers
```

risposta Hello è simile toohello esempio seguente:

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

Controllare hello risposta toosee se è elencato il provider di connettività. Prendere nota di hello informazioni, è necessario quando si crea un circuito di seguito:

* Nome
* PeeringLocations
* BandwidthsOffered

Si è ora pronto toocreate un circuito ExpressRoute.

### <a name="3-create-an-expressroute-circuit"></a>3. Creare un circuito ExpressRoute

> [!IMPORTANT]
> Il circuito ExpressRoute viene fatturato dall'istante hello che viene eseguita una chiave del servizio. Eseguire questa operazione quando il provider di connettività hello è circuito hello tooprovision pronto.
> 
> 

Se non si ha già un gruppo di risorse, è necessario crearne uno prima di creare il circuito ExpressRoute. È possibile creare un gruppo di risorse eseguendo hello comando seguente:

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

Hello di esempio seguente viene illustrato come un ExpressRoute a 200 Mbps toocreate circuit tramite Equinix Silicon Valley. Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta. 

Assicurarsi di specificare hello corretto dello SKU e famiglia di SKU:

* Il livello SKU determina se deve essere abilitato il componente aggiuntivo ExpressRoute Standard o Premium. È possibile specificare 'Standard' tooget hello SKU standard o 'Premium' per il componente aggiuntivo di hello premium.
* Famiglia di SKU determina tipo fatturazione hello. Specificare 'Metereddata' per un piano dati a consumo e 'Unlimiteddata' per un piano dati senza limiti. È possibile modificare il tipo fatturazione di hello da 'Metereddata 'too'Unlimiteddata', ma è possibile modificare il tipo di hello da too'Metereddata 'Unlimiteddata' '.


Il circuito ExpressRoute viene fatturato dall'istante hello che viene eseguita una chiave del servizio. Hello di esempio seguente è una richiesta per una nuova chiave di servizio:

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

risposta Hello contiene una chiave del servizio hello.

### <a name="4-list-all-expressroute-circuits"></a>4. Elencare tutti i circuiti ExpressRoute

tooget un elenco di tutti i circuiti ExpressRoute hello creato, eseguire il comando di 'list express route di rete az' hello. È possibile recuperare queste informazioni in qualsiasi momento usando questo comando. toolist tutti i circuiti, effettuare hello chiamata senza parametri.

```azurecli
az network express-route list
```

La chiave del servizio è elencata nella hello *ServiceKey* campo della risposta hello.

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

È possibile ottenere una descrizione dettagliata di tutti i parametri di hello comando hello utilizzando hello '-h' parametro.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Inviare i provider di connettività di hello servizio tooyour chiave per il provisioning

'ServiceProviderProvisioningState' vengono fornite informazioni sullo stato corrente di hello del provisioning sul lato di provider di servizi di hello. stato Hello fornisce lo stato di hello in hello lato Microsoft. Per ulteriori informazioni, vedere hello [articolo flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states).

Quando si crea un nuovo circuito ExpressRoute, hello circuito si trova in hello seguente stato:

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

circuito Hello modifica toohello seguente lo stato quando il provider di connettività hello è in corso di hello di abilitarlo per l'utente:

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

Per è toobe in grado di toouse un circuito ExpressRoute, deve essere nel seguente stato hello:

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Controllare periodicamente hello stato della chiave circuito hello e hello

Controllo stato hello della chiave circuito hello e hello consente di sapere quando il circuito viene abilitato il provider. Dopo aver configurato il circuito hello, 'ServiceProviderProvisioningState' viene visualizzato come "Provisioning eseguito", come illustrato nell'esempio seguente hello:

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. Creare la configurazione di routing

Per istruzioni dettagliate, vedere hello [configurazione del routing circuito ExpressRoute](howto-routing-cli.md) toocreate dell'articolo e modificare peering di circuito.

> [!IMPORTANT]
> Queste istruzioni si applicano solo toocircuits creati con i provider di servizi che offrono servizi di livello 2 di connettività. Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito una VPN IP, come MPLS), il provider di connettività configura e gestisce il routing per conto dell'utente.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Collegare un circuito ExpressRoute di tooan rete virtuale

Successivamente, collegare un circuito ExpressRoute di tooyour rete virtuale. Hello utilizzare [collegamento virtuale reti circuiti tooExpressRoute](howto-linkvnet-cli.md) articolo.

## <a name="modify"></a>Modifica di un circuito ExpressRoute

È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività. È possibile apportare hello dopo le modifiche senza tempi di inattività:

* Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.
* È possibile aumentare la larghezza di banda hello del circuito ExpressRoute purché vi sia la capacità disponibile sulla porta hello. Tuttavia, non è supportato il downgrade della larghezza di banda hello di un circuito. 
* È possibile modificare piano controllo hello da dati a consumo tooUnlimited dati. Tuttavia, la modifica hello misurazione piano da dati senza limiti tooMetered che dati non è supportata.
* È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).

Per ulteriori informazioni su limiti e limitazioni, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>componente aggiuntivo di tooenable hello ExpressRoute premium

È possibile abilitare il componente aggiuntivo di hello ExpressRoute premium per il circuito esistente utilizzando hello comando seguente:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

circuito Hello dispone ora di funzionalità aggiuntive di hello ExpressRoute premium abilitata. Per iniziare, si fatturazione per la funzionalità di componente aggiuntivo di hello premium come comando hello è stata eseguita correttamente.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>componente aggiuntivo di toodisable hello ExpressRoute premium

> [!IMPORTANT]
> Questa operazione può non riuscire se si utilizza le risorse che sono maggiori di ciò che è consentito per il circuito standard hello.
> 
> 

Prima di disabilitare i componenti aggiuntivi di hello ExpressRoute premium, comprendere hello seguenti criteri:

* Prima effettuare il downgrade da premium toostandard, assicurarsi di disporre di meno di 10 reti virtuali collegate toohello circuito. Se sono più di 10, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.
* È necessario scollegare tutte le reti virtuali in altre aree geopolitiche. Se non si scollegano tutte le reti virtuali, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.
* La tabella di route deve includere meno di 4.000 route per il peering privato. Se le dimensioni di tabella di route sono maggiore di 4.000 route, sessione BGP hello Elimina. non verrà riabilitata sessione Hello fino a quando il numero di hello di prefissi annunciati è inferiore a 4.000.

È possibile disabilitare componente aggiuntivo di hello ExpressRoute premium per il circuito esistente hello utilizzando hello di esempio seguente:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>larghezza di banda circuito ExpressRoute hello tooupdate

Per le opzioni di larghezza di banda hello è supportato per il provider, controllare hello [domande frequenti su ExpressRoute](expressroute-faqs.md). È possibile scegliere qualsiasi dimensione maggiore della dimensione hello del circuito esistente.

> [!IMPORTANT]
> Se sulla porta esistente hello capacità insufficiente, è possibile circuito ExpressRoute di toorecreate hello. Se non è presente capacità aggiuntive disponibili in tale posizione non è possibile aggiornare il circuito hello.
>
> È possibile ridurre la larghezza di banda hello di un circuito ExpressRoute senza interruzioni. Il downgrade della larghezza di banda richiede si toodeprovision hello circuito ExpressRoute e quindi ripetere il provisioning di un nuovo circuito ExpressRoute.
>

Dopo aver stabilito dimensioni hello che è necessario, utilizzare il circuito hello tooresize di comando seguente:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

Il circuito viene ridimensionato sul lato Microsoft hello. Successivamente, è necessario contattare le configurazioni di tooupdate provider di connettività nella loro toomatch lato questa modifica. Dopo aver apportato questa notifica, iniziamo è fatturazione per l'opzione di hello aggiornato della larghezza di banda.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>toomove hello SKU da toounlimited a consumo

È possibile modificare hello SKU di un circuito ExpressRoute tramite hello di esempio seguente:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>classica di toohello toocontrol accesso e gli ambienti di gestione risorse

Rivedere le istruzioni di hello in [circuiti ExpressRoute spostare dal modello di distribuzione di gestione risorse toohello classico hello](expressroute-howto-move-arm.md).

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Deprovisioning ed eliminazione di un circuito ExpressRoute

toodeprovision ed eliminare un circuito ExpressRoute, assicurarsi di comprendere hello seguenti criteri:

* È necessario scollegare tutte le reti virtuali da hello circuito ExpressRoute. Se questa operazione non riesce, controllare toosee se sono configurate reti virtuali collegate toohello circuito.
* Se il provider del servizio di circuito ExpressRoute di hello lo stato di provisioning **Provisioning** o **provisioning eseguito**, è necessario collaborare con il circuito di hello toodeprovision provider del servizio sul relativo lato. Abbiamo continuare tooreserve risorse e fatturate fino a quando il provider di servizi di hello completa deprovisioning circuito hello e invia una notifica di Microsoft.
* È possibile eliminare il circuito hello se il provider di servizi di hello è deprovisioning circuito hello. Quando viene effettuato il deprovisioning un circuito, il provider di servizi hello lo stato di provisioning è stato impostato troppo**non è stato eseguito il provisioning**. Viene arrestata la fatturazione per il circuito hello.

È possibile eliminare il circuito ExpressRoute eseguendo hello comando seguente:

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato il circuito, assicurarsi che hello quanto segue:

* [Creare e modificare il routing per un circuito ExpressRoute](howto-routing-cli.md)
* [Collegamento del circuito ExpressRoute di tooyour di rete virtuale](howto-linkvnet-cli.md)
