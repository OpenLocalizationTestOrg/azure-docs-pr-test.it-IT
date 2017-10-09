---
title: 'Creare e modificare un circuito ExpressRoute: PowerShell: Azure classico| Microsoft Docs'
description: In questo articolo vengono illustrati i passaggi hello per la creazione e il provisioning di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornare, o eliminare, quindi eseguire il deprovisioning del circuito.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>Creare e modificare un circuito ExpressRoute mediante PowerShell (versione classica)
> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-circuit-cli.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-circuit-classic.md)
>

In questo articolo illustra hello passaggi toocreate un circuito ExpressRoute di Azure con modello di distribuzione classica hello e di cmdlet di PowerShell. Mostra anche come stato hello toocheck, aggiornare, o eliminare e il deprovisioning di un circuito ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**Informazioni sui modelli di distribuzione di Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Prima di iniziare
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>Passaggio 1. Rivedere i prerequisiti di hello e gli articoli del flusso di lavoro
Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>Passaggio 2. Installare le versioni più recenti di hello dei moduli di PowerShell di gestione del servizio di Azure (SM) hello
Seguire le istruzioni hello [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview) per istruzioni dettagliate su come tooconfigure i moduli di Azure PowerShell hello toouse computer.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>Passaggio 3. Accedi tooyour account Azure e selezionare una sottoscrizione
1. Aprire la console di PowerShell con diritti elevati e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

        Login-AzureRmAccount

2. Controllare le sottoscrizioni di hello per account hello.

        Get-AzureRmSubscription

3. Se si dispone di più di una sottoscrizione, selezionare una sottoscrizione di hello che si desidera toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Successivamente, utilizzare hello seguente cmdlet tooadd tooPowerShell la sottoscrizione di Azure per il modello di distribuzione classica hello.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Creare un circuito ExpressRoute ed eseguirne il provisioning
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>Passaggio 1. Importare i moduli di PowerShell hello per ExpressRoute
 Se non è già stato fatto, è necessario importare i moduli di Azure ed ExpressRoute hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello. Importare i moduli di hello da hello percorso in cui erano installati tooon nel computer locale. In base al metodo hello è utilizzato moduli hello tooinstall, percorso hello potrebbe essere diverso da hello esempio illustrato di seguito. Se necessario, modificare l'esempio hello.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>Passaggio 2. Ottenere l'elenco di hello di provider supportati, posizioni e delle larghezze di banda
Prima di creare un circuito ExpressRoute, è necessario l'elenco di hello del provider di connettività supportate, località e le opzioni di larghezza di banda.

cmdlet di PowerShell Hello `Get-AzureDedicatedCircuitServiceProvider` restituisce queste informazioni, che verranno usati nei passaggi successivi:

    Get-AzureDedicatedCircuitServiceProvider

Controllare toosee se viene elencato il provider di connettività. Prendere nota di hello perché sarà necessaria successivamente quando si crea un circuito le seguenti informazioni:

* Nome
* PeeringLocations
* BandwidthsOffered

Si è ora pronto toocreate un circuito ExpressRoute.         

### <a name="step-3-create-an-expressroute-circuit"></a>Passaggio 3. Creare un circuito ExpressRoute
Hello di esempio seguente viene illustrato come un ExpressRoute a 200 Mbps toocreate circuit tramite Equinix Silicon Valley. Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta.

> [!IMPORTANT]
> Dal momento hello che viene eseguita una chiave del servizio verrà addebitato il circuito ExpressRoute. Assicurarsi di eseguire questa operazione quando il provider di connettività hello è circuito hello tooprovision pronto.
> 
> 

di seguito Hello è un esempio di richiesta per una nuova chiave di servizio:

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

In alternativa, se si desidera toocreate un circuito ExpressRoute con il componente aggiuntivo premium hello, hello di utilizzare l'esempio seguente. Fare riferimento toohello [domande frequenti su ExpressRoute](expressroute-faqs.md) per ulteriori informazioni sul componente aggiuntivo di hello premium.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


risposta Hello conterrà la chiave di servizio hello. È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello:

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>Passaggio 4. Elenco di tutti i circuiti ExpressRoute hello
È possibile eseguire hello `Get-AzureDedicatedCircuit` comando hello di tooget un elenco di tutti i circuiti ExpressRoute creato:

    Get-AzureDedicatedCircuit

risposta di Hello sarà simile toohello esempio seguente:

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

È possibile recuperare queste informazioni in qualsiasi momento utilizzando hello `Get-AzureDedicatedCircuit` cmdlet. Effettuare hello chiamata senza parametri, vengono elencati tutti i circuiti hello. La chiave del servizio sarà elencata nel hello *ServiceKey* campo.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello:

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>Passaggio 5. Inviare i provider di connettività di hello servizio tooyour chiave per il provisioning
*ServiceProviderProvisioningState* fornisce informazioni sullo stato corrente di hello di provisioning sul lato di provider di servizi di hello. *Stato* fornisce lo stato di hello in hello lato Microsoft. Per ulteriori informazioni sul provisioning stati circuito, vedere hello [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) articolo.

Quando si crea un nuovo circuito ExpressRoute, circuito hello sarà nel seguente stato hello:

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


circuito Hello andrà toohello seguente lo stato quando il provider di connettività hello è in corso di hello di abilitarlo per l'utente:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Un circuito ExpressRoute deve essere nel seguente stato si toobe in grado di toouse hello è:

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>Passaggio 6. Controllare periodicamente hello stato della chiave circuito hello e hello
In questo modo è possibile sapere quando il provider ha abilitato il circuito. Dopo aver configurato il circuito hello, *ServiceProviderProvisioningState* verrà visualizzato come *provisioning eseguito* come illustrato nell'esempio seguente hello:

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>Passaggio 7. Creare la configurazione di routing
Fare riferimento toohello [configurazione del routing circuito ExpressRoute (creare e modificare il circuito peering)](expressroute-howto-routing-classic.md) per istruzioni dettagliate.

> [!IMPORTANT]
> Queste istruzioni si applicano solo toocircuits creati con i provider di servizi che offrono servizi di livello 2 di connettività. Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>Passaggio 8. Collegare un circuito ExpressRoute di tooan rete virtuale
Successivamente, collegare un circuito ExpressRoute di tooyour rete virtuale. Fare riferimento troppo[toovirtual reti i circuiti ExpressRoute collegamento](expressroute-howto-linkvnet-classic.md) per istruzioni dettagliate. Se è necessario toocreate una rete virtuale usando il modello di distribuzione classica hello per ExpressRoute, vedere [creare una rete virtuale per ExpressRoute](expressroute-howto-vnet-portal-classic.md).

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Ottenere lo stato di hello di un circuito ExpressRoute
È possibile recuperare queste informazioni in qualsiasi momento utilizzando hello `Get-AzureCircuit` cmdlet. Effettuare hello chiamata senza parametri, vengono elencati tutti i circuiti hello.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

È possibile ottenere informazioni su un circuito ExpressRoute specifico passando la chiave di servizio hello come una chiamata di toohello parametro.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello di esempio seguente:

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Modifica di un circuito ExpressRoute
È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.

È possibile eseguire hello seguenti senza tempi di inattività:

* Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.
* Aumento della larghezza di banda hello del circuito ExpressRoute fornito è la capacità disponibile sulla porta hello. Si noti che il downgrade della larghezza di banda hello di un circuito non è supportato. 
* Modificare hello piano dati a consumo tooUnlimited dati di controllo. Si noti tale piano del controllo modifica hello da dati senza limiti tooMetered che dati non è supportata.
* È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).

Fare riferimento toohello [domande frequenti su ExpressRoute](expressroute-faqs.md) per ulteriori informazioni su limiti e limitazioni.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>componente aggiuntivo di tooenable hello ExpressRoute premium
È possibile abilitare il componente aggiuntivo di hello ExpressRoute premium per il circuito esistente utilizzando hello seguente cmdlet di PowerShell:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

Il circuito avranno ora le funzionalità dei componenti aggiuntivi di hello ExpressRoute premium abilitata. Si noti che si inizierà fatturazione è per la funzionalità di componente aggiuntivo di hello premium come comando hello è stata eseguita correttamente.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>componente aggiuntivo di toodisable hello ExpressRoute premium
> [!IMPORTANT]
> Questa operazione può non riuscire se si utilizza le risorse che sono maggiori di ciò che è consentito per il circuito standard hello.
> 
> 

#### <a name="considerations"></a>Considerazioni

* È necessario assicurarsi che il numero di hello del circuito toohello collegato reti virtuali è inferiore a 10 prima effettuare il downgrade da premium toostandard. Se non si esegue questa operazione, la richiesta di aggiornamento avrà esito negativo e sarà tariffe fatturati hello.
* È necessario scollegare tutte le reti virtuali in altre aree geopolitiche. Se non si esegue questa operazione, la richiesta di aggiornamento avrà esito negativo e sarà tariffe fatturati hello.
* La tabella di route deve includere meno di 4.000 route per il peering privato. Se le dimensioni di tabella di route sono maggiore di 4.000 route, sessione BGP hello verrà eliminato e non verrà riabilitata fino a quando il numero di hello di prefissi annunciati scende sotto 4.000.

#### <a name="disable-hello-premium-add-on"></a>Disabilitare il componente aggiuntivo di hello premium
È possibile disabilitare il componente aggiuntivo di hello ExpressRoute premium per il circuito esistente utilizzando hello cmdlet di PowerShell seguente:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>larghezza di banda circuito ExpressRoute hello tooupdate
Controllare hello [domande frequenti su ExpressRoute](expressroute-faqs.md) per le opzioni della larghezza di banda per il provider è supportato. È possibile scegliere qualsiasi dimensione è maggiore della dimensione hello del circuito esistente, purché (in cui viene creato il circuito) la porta fisica hello consente.

> [!IMPORTANT]
> Potrebbe essere circuito ExpressRoute di hello toorecreate se ha capacità insufficiente sulla porta esistente hello. Se non è presente capacità aggiuntive disponibili in tale posizione non è possibile aggiornare il circuito hello.
>
> È possibile ridurre la larghezza di banda hello di un circuito ExpressRoute senza interruzioni. Il downgrade della larghezza di banda è necessario il circuito ExpressRoute toodeprovision hello e quindi ripetere il provisioning di un nuovo circuito ExpressRoute.
> 
> 

#### <a name="resize-a-circuit"></a>Ridimensionare un circuito

Dopo aver stabilito quali dimensioni, è necessario, è possibile utilizzare il circuito hello tooresize di comando seguente:

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Il circuito verrà sono stato ridimensionato sul lato Microsoft hello. È necessario contattare le configurazioni di tooupdate provider di connettività nella loro toomatch lato questa modifica. Si noti che si inizierà di fatturazione per hello aggiornato opzione larghezza di banda da questo punto.

Se viene visualizzato il seguente errore durante l'aumento della larghezza di banda circuito hello hello, significa non esiste alcuna larghezza di banda sufficiente a sinistra sulla porta di hello fisico in cui è stato creato il circuito esistente. Si crea un nuovo circuito delle dimensioni di hello che è necessario includere toodelete questo circuito. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Deprovisioning ed eliminazione di un circuito ExpressRoute

### <a name="considerations"></a>Considerazioni

* È necessario scollegare tutte le reti virtuali da hello circuito ExpressRoute per toosucceed questa operazione. Controllare toosee se si dispone di alcuna rete virtuale che sono collegati circuito toohello se questa operazione ha esito negativo.
* Se il provider del servizio di circuito ExpressRoute di hello lo stato di provisioning **Provisioning** o **provisioning eseguito** è necessario collaborare con il circuito di hello toodeprovision provider del servizio sul relativo lato. Si continuerà tooreserve risorse e a pagamento fino a quando il provider di servizi di hello completa deprovisioning circuito hello e invia una notifica di Microsoft.
* Se il provider di servizi di hello è deprovisioning circuito hello (provider di servizi di hello lo stato di provisioning è stato impostato troppo**non è stato eseguito il provisioning**) è possibile eliminare il circuito hello. Questa operazione arresterà la fatturazione per il circuito hello.

#### <a name="delete-a-circuit"></a>Eliminare un circuito

È possibile eliminare il circuito ExpressRoute eseguendo hello comando seguente:

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il circuito, verificare che hello seguenti:

* [Creare e modificare il routing per un circuito ExpressRoute](expressroute-howto-routing-classic.md)
* [Collegamento del circuito ExpressRoute di tooyour di rete virtuale](expressroute-howto-linkvnet-classic.md)

