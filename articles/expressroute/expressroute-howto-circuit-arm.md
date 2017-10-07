---
title: 'Creare e modificare un circuito ExpressRoute: PowerShell: Azure Resource Manager| Microsoft Docs'
description: In questo articolo viene descritto come toocreate, eseguire il provisioning, verificare, aggiornare, eliminare e il deprovisioning di un circuito ExpressRoute.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Creare e modificare un circuito ExpressRoute mediante PowerShell
> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-circuit-cli.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-circuit-classic.md)
>

In questo articolo viene descritto come toocreate Azure ExpressRoute circuito mediante PowerShell cmdlet e hello Azure Resource Manager modello di distribuzione. Mostra anche come lo stato di hello toocheck del circuito di hello, aggiornare o eliminare e deprovisioning.

## <a name="before-you-begin"></a>Prima di iniziare
* Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure. Per altre informazioni, vedere la [panoramica di Azure PowerShell](/powershell/azure/overview).
* Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.


## <a name="create-and-provision-an-expressroute-circuit"></a>Creare un circuito ExpressRoute ed eseguirne il provisioning
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Accedi tooyour account Azure e selezionare la sottoscrizione
toobegin della configurazione, accedi tooyour account Azure. Hello seguenti esempi toohelp che ci si connette, utilizzare:

```powershell
Login-AzureRmAccount
```

Controllare le sottoscrizioni di hello per hello account:

```powershell
Get-AzureRmSubscription
```

Selezionare hello sottoscrizione che si desidera toocreate circuiti ExpressRoute per:

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Ottenere l'elenco di hello di provider supportati, posizioni e delle larghezze di banda
Prima di creare un circuito ExpressRoute, è necessario l'elenco di hello del provider di connettività supportate, località e le opzioni di larghezza di banda.

cmdlet di PowerShell Hello **Get AzureRmExpressRouteServiceProvider** restituisce queste informazioni, che verranno usati nei passaggi successivi:

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Controllare toosee se viene elencato il provider di connettività. Prendere nota di hello le seguenti informazioni. che saranno necessarie durante la creazione del circuito.

* Nome
* PeeringLocations
* BandwidthsOffered

Si è ora pronto toocreate un circuito ExpressRoute.   

### <a name="3-create-an-expressroute-circuit"></a>3. Creare un circuito ExpressRoute
Se non si ha già un gruppo di risorse, è necessario crearne uno prima di creare il circuito ExpressRoute. È possibile farlo eseguendo hello comando seguente:

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


Hello di esempio seguente viene illustrato come un ExpressRoute a 200 Mbps toocreate circuit tramite Equinix Silicon Valley. Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta. di seguito Hello è un esempio di richiesta per una nuova chiave di servizio:

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Assicurarsi di specificare hello corretto dello SKU e famiglia di SKU:

* Il livello SKU determina se deve essere abilitato il componente aggiuntivo ExpressRoute Standard o Premium. È possibile specificare *Standard* tooget hello SKU standard o *Premium* per il componente aggiuntivo di hello premium.
* Famiglia di SKU determina tipo fatturazione hello. Specificare *Metereddata* per un piano dati a consumo e *Unlimiteddata* per un piano dati senza limiti. È possibile modificare il tipo fatturazione di hello da *Metereddata* troppo*Unlimiteddata*, ma è possibile modificare il tipo di hello da *Unlimiteddata* troppo*Metereddata* .

> [!IMPORTANT]
> Dal momento hello che viene eseguita una chiave del servizio verrà addebitato il circuito ExpressRoute. Assicurarsi di eseguire questa operazione quando il provider di connettività hello è circuito hello tooprovision pronto.
> 
> 

risposta Hello contiene una chiave del servizio hello. È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello comando seguente:

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Elencare tutti i circuiti ExpressRoute
tooget hello di un elenco di tutti i circuiti ExpressRoute creato, eseguire hello **Get AzureRmExpressRouteCircuit** comando:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

risposta Hello avrà un aspetto simile toohello esempio seguente:

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

È possibile recuperare queste informazioni in qualsiasi momento utilizzando hello `Get-AzureRmExpressRouteCircuit` cmdlet. Chiamata hello senza parametri, vengono elencati tutti i circuiti hello. La chiave del servizio sarà elencata nel hello *ServiceKey* campo:

```powershell
Get-AzureRmExpressRouteCircuit
```


risposta Hello avrà un aspetto simile toohello esempio seguente:

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello comando seguente:

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Inviare i provider di connettività di hello servizio tooyour chiave per il provisioning
*ServiceProviderProvisioningState* fornisce informazioni sullo stato corrente di hello di provisioning sul lato di provider di servizi di hello. Stato fornisce lo stato di hello in hello lato Microsoft. Per ulteriori informazioni sul provisioning stati circuito, vedere hello [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) articolo.

Quando si crea un nuovo circuito ExpressRoute, circuito hello sarà nel seguente stato hello:

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



circuito Hello cambierà toohello seguente lo stato quando il provider di connettività hello è in corso di hello di abilitarlo per l'utente:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Per è toobe in grado di toouse un circuito ExpressRoute, deve essere nel seguente stato hello:

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Controllare periodicamente hello stato della chiave circuito hello e hello
Controllo stato hello della chiave circuito hello e hello consente di sapere quando il circuito viene abilitato il provider. Dopo aver configurato il circuito hello, *ServiceProviderProvisioningState* viene visualizzato come *provisioning eseguito*, come illustrato nell'esempio seguente hello:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


risposta Hello avrà un aspetto simile toohello esempio seguente:

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

### <a name="7-create-your-routing-configuration"></a>7. Creare la configurazione di routing
Per istruzioni dettagliate, vedere hello [configurazione del routing circuito ExpressRoute](expressroute-howto-routing-arm.md) toocreate dell'articolo e modificare peering di circuito.

> [!IMPORTANT]
> Queste istruzioni si applicano solo toocircuits creati con i provider di servizi che offrono servizi di livello 2 di connettività. Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Collegare un circuito ExpressRoute di tooan rete virtuale
Successivamente, collegare un circuito ExpressRoute di tooyour rete virtuale. Hello utilizzare [collegamento virtuale reti circuiti tooExpressRoute](expressroute-howto-linkvnet-arm.md) articolo quando si lavora con modello di distribuzione di gestione risorse di hello.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Ottenere lo stato di hello di un circuito ExpressRoute
È possibile recuperare queste informazioni in qualsiasi momento utilizzando hello **Get AzureRmExpressRouteCircuit** cmdlet. Chiamata hello senza parametri, vengono elencati tutti i circuiti hello.

```powershell
Get-AzureRmExpressRouteCircuit
```


risposta di Hello sarà simile toohello esempio seguente:

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


È possibile ottenere informazioni su un circuito ExpressRoute specifico passando nome gruppo di risorse hello e il nome del circuito come una chiamata di toohello parametro:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


risposta Hello avrà un aspetto simile toohello esempio seguente:

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


È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello comando seguente:

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Modifica di un circuito ExpressRoute
È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.

È possibile eseguire hello seguenti senza tempi di inattività:

* Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.
* Aumento della larghezza di banda hello del circuito ExpressRoute fornito è la capacità disponibile sulla porta hello. Il downgrade della larghezza di banda hello di un circuito non è supportato. 
* Modificare hello piano dati a consumo tooUnlimited dati di controllo. Modifica hello misurazione piano da dati senza limiti tooMetered che dati non è supportata.
* È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).

Per ulteriori informazioni su limiti e limitazioni, vedere toohello [domande frequenti su ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>componente aggiuntivo di tooenable hello ExpressRoute premium
È possibile abilitare il componente aggiuntivo di hello ExpressRoute premium per il circuito esistente utilizzando hello seguente frammento di PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

circuito Hello avranno ora le funzionalità dei componenti aggiuntivi di hello ExpressRoute premium abilitata. Verrà avviato fatturazione è per la funzionalità di componente aggiuntivo di hello premium come comando hello è stata eseguita correttamente.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>componente aggiuntivo di toodisable hello ExpressRoute premium
> [!IMPORTANT]
> Questa operazione può non riuscire se si utilizza le risorse che sono maggiori di ciò che è consentito per il circuito standard hello.
> 
> 

Si noti hello segue:

* Prima effettuare il downgrade da premium toostandard, è necessario verificare tale numero hello di reti virtuali collegate circuito toohello è inferiore a 10. In caso contrario, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.
* È necessario scollegare tutte le reti virtuali in altre aree geopolitiche. In caso contrario, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.
* La tabella di route deve includere meno di 4.000 route per il peering privato. Se le dimensioni di tabella di route sono maggiore di 4.000 route, sessione BGP hello Elimina e non verrà riabilitata fino a quando il numero di hello di prefissi annunciati scende sotto 4.000.

È possibile disabilitare componente aggiuntivo di hello ExpressRoute premium per il circuito esistente hello utilizzando hello cmdlet di PowerShell seguente:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>larghezza di banda circuito ExpressRoute hello tooupdate
Per le larghezze di banda supportate per il provider, controllare hello [domande frequenti su ExpressRoute](expressroute-faqs.md). È possibile scegliere qualsiasi dimensione maggiore della dimensione hello del circuito esistente.

> [!IMPORTANT]
> Potrebbe essere circuito ExpressRoute di hello toorecreate se ha capacità insufficiente sulla porta esistente hello. Se non è presente capacità aggiuntive disponibili in tale posizione non è possibile aggiornare il circuito hello.
>
> È possibile ridurre la larghezza di banda hello di un circuito ExpressRoute senza interruzioni. Il downgrade della larghezza di banda è necessario il circuito ExpressRoute toodeprovision hello e quindi ripetere il provisioning di un nuovo circuito ExpressRoute.
> 

Dopo aver stabilito quali dimensioni, è necessario, usare il circuito hello tooresize di comando seguente:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


Il circuito verrà ridimensionato sul lato Microsoft hello. È quindi necessario contattare le configurazioni di tooupdate provider di connettività nella loro toomatch lato questa modifica. Dopo aver apportato questa notifica, verrà avviato è fatturazione per l'opzione di hello aggiornato della larghezza di banda.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>toomove hello SKU da toounlimited a consumo
È possibile modificare hello SKU di un circuito ExpressRoute tramite hello seguente frammento di PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>classica di toohello toocontrol accesso e gli ambienti di gestione risorse
Rivedere le istruzioni di hello in [circuiti ExpressRoute spostare dal modello di distribuzione di gestione risorse toohello classico hello](expressroute-howto-move-arm.md).  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Deprovisioning ed eliminazione di un circuito ExpressRoute
Si noti hello segue:

* È necessario scollegare tutte le reti virtuali da hello circuito ExpressRoute. Se questa operazione non riesce, controllare toosee se sono configurate reti virtuali collegate toohello circuito.
* Se il provider del servizio di circuito ExpressRoute di hello lo stato di provisioning **Provisioning** o **provisioning eseguito** è necessario collaborare con il circuito di hello toodeprovision provider del servizio sul relativo lato. Si continuerà tooreserve risorse e a pagamento fino a quando il provider di servizi di hello completa deprovisioning circuito hello e invia una notifica di Microsoft.
* Se il provider di servizi di hello è deprovisioning circuito hello (provider di servizi di hello lo stato di provisioning è stato impostato troppo**non è stato eseguito il provisioning**) è possibile eliminare il circuito hello. Questa operazione arresterà la fatturazione per il circuito hello

È possibile eliminare il circuito ExpressRoute eseguendo hello comando seguente:

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato il circuito, verificare che hello seguenti:

* [Creare e modificare il routing per un circuito ExpressRoute](expressroute-howto-routing-arm.md)
* [Collegamento del circuito ExpressRoute di tooyour di rete virtuale](expressroute-howto-linkvnet-arm.md)
