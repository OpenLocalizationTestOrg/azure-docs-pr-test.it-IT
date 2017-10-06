---
title: aaaMove risorse di Azure toonew sottoscrizione o la risorsa gruppo | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure toomove risorse tooa nuovo gruppo di risorse o di sottoscrizione.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Gruppo di risorse di spostare risorse toonew o sottoscrizione
Questo argomento viene illustrato come toomove risorse tooeither una nuova sottoscrizione o una nuova risorsa gruppo hello stessa sottoscrizione. È possibile utilizzare il portale di hello, PowerShell, CLI di Azure o hello risorsa toomove API REST. operazioni di spostamento Hello in questo argomento sono disponibili tooyou senza assistenza dal supporto tecnico di Azure.

Quando lo spostamento delle risorse, sia il gruppo di origine hello e il gruppo di destinazione hello sono bloccate durante l'operazione di hello. Scrivere e le operazioni di eliminazione sono bloccati in gruppi di risorse hello fino al completamento di spostamento hello. Non è possibile aggiungere, aggiornare o eliminare le risorse in gruppi di risorse hello, ma questo non significa che vengono bloccate risorse hello, significa che questo blocco. Ad esempio, se si sposta un Server SQL e il relativo database tooa nuovo gruppo di risorse, un'applicazione che utilizza database hello non esperienze tempi di inattività. Può comunque leggere e scrivere toohello database.

È possibile modificare il percorso di hello della risorsa hello. Lo spostamento di una risorsa solo spostarlo tooa nuovo gruppo di risorse. nuovo gruppo di risorse Hello può avere un percorso diverso, ma che non modificare il percorso di hello della risorsa hello.

> [!NOTE]
> Questo articolo descrive la modalità dell'account offerte toomove risorse all'interno di Azure esistente. Se si desidera effettivamente toochange all'account Azure offerta (ad esempio, l'aggiornamento da toopre pagamento a consumo-pay) continuando toowork con le risorse esistenti, vedere [cambiare l'offerta di sottoscrizione di Azure tooanother](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Controllo prima di spostare le risorse
Esistono tooperform alcuni importanti passaggi prima di spostare una risorsa. La verifica di queste condizioni consente di evitare errori.

1. Hello le sottoscrizioni di origine e di destinazione devono esistere all'interno di hello stesso [tenant Azure Active Directory](../active-directory/active-directory-howto-tenant.md). toocheck che entrambe le sottoscrizioni sono hello stesso ID tenant, usare Azure PowerShell o CLI di Azure.

  Per Azure PowerShell usare:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Per l'interfaccia della riga di comando di Azure 2.0, usare:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Se hello tenant ID per le sottoscrizioni di origine e destinazione hello non sono hello stesso, è possibile tentare directory hello toochange per sottoscrizione hello. Tuttavia, questa opzione è disponibile tooService solo gli amministratori che ha eseguito l'accesso con un account Microsoft (non un account aziendale). modifica della directory di hello, accedi toohello tooattempt [portale classico](https://manage.windowsazure.com/)e selezionare **impostazioni**, selezionare la sottoscrizione hello. Se hello **modifica Directory** icona è disponibile, selezionarlo toochange hello associati di Azure Active Directory.

  ![modifica directory](./media/resource-group-move-resources/edit-directory.png)

  Se tale icona non è disponibile, è necessario contattare il supporto toomove hello risorse tooa nuovo tenant.

2. servizio Hello è necessario abilitare le risorse di toomove possibilità hello. In questo argomento sono elencati i servizi che consentono di spostare risorse e quelli che invece non lo permettono.
3. sottoscrizione di destinazione Hello deve essere registrati per il provider di risorse hello della risorsa hello viene spostato. Se non si riceve un errore che informa che hello **sottoscrizione non è registrata per un tipo di risorsa**. Questo problema possono verificarsi durante lo spostamento di una nuova sottoscrizione tooa di risorse, ma tale sottoscrizione non sia mai stato utilizzato con il tipo di risorsa. toolearn come toocheck hello lo stato della registrazione e registrare i provider di risorse, vedere [tipi e i provider di risorse](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>Quando il supporto toocall
È possibile spostare la maggior parte delle risorse tramite operazioni hello self-service illustrate in questo argomento. Utilizzare hello self-service delle operazioni:

* Spostare le risorse di Resource Manager.
* Spostare le risorse classiche in base toohello [limitazioni di distribuzione classica](#classic-deployment-limitations).

Chiamare il supporto quando è necessario:

* Spostare le risorse tooa nuovo account Azure (e tenant di Azure Active Directory).
* Spostare le risorse classiche ma problemi con limitazioni hello.

## <a name="services-that-enable-move"></a>Servizi che abilitano lo spostamento
Per il momento, servizi di hello che consentono lo spostamento tooboth un nuovo gruppo di risorse e la sottoscrizione sono:

* Gestione API
* App del servizio app (app Web): vedere [Limitazioni del servizio app](#app-service-limitations)
* Application Insights
* Automazione
* Batch
* Bing Mappe
* RETE CDN
* Servizi cloud: vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)
* Servizi cognitivi
* Content Moderator
* Data Catalog
* Data factory
* Analisi Data Lake
* Archivio Data Lake
* DNS
* Azure Cosmos DB
* Hub eventi
* Cluster HDInsight - vedere [Limitazioni di HDInsight](#hdinsight-limitations)
* Hub IoT
* Insieme di credenziali di chiave
* Servizi di bilanciamento del carico
* App per la logica
* Machine Learning
* Servizi multimediali
* Mobile Engagement
* Hub di notifica
* Operational Insights
* Operations Management
* Power BI
* Cache Redis
* Utilità di pianificazione
* Search
* Gestione server
* Bus di servizio
* Service Fabric
* Archiviazione
* Archiviazione (classica): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)
* Analisi di flusso: i processi di analisi di flusso non possono essere spostati durante l'esecuzione.
* Il server di Database SQL - hello database e server devono risiedere in hello stesso gruppo di risorse. Quando si sposta un server SQL, quindi, vengono spostati anche tutti i relativi database.
* Gestione traffico
* Macchine virtuali
* Macchine virtuali con certificato archiviato nell'insieme di credenziali chiave - toonew spostamento risorse del gruppo nella stessa sottoscrizione è abilitata, ma spostamento tra sottoscrizioni non è abilitato.
* Macchine virtuali (classiche): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)
* Set di scalabilità di macchine virtuali
* Reti virtuali: attualmente non è possibile spostare una rete virtuale con peering fino a quando non viene disabilitato il peering di rete virtuale. Una volta disabilitato, hello rete virtuale può essere spostato correttamente e hello peering di reti virtuali può essere abilitata. Inoltre, una rete virtuale non può essere spostato tooa altra sottoscrizione se hello rete virtuale contiene una qualsiasi subnet con collegamenti di navigazione delle risorse. Ad esempio, una subnet della rete virtuale ha un collegamento di navigazione delle risorse quando una risorsa redis Microsoft.Cache viene distribuita in questa subnet.
* Gateway VPN


## <a name="services-that-do-not-enable-move"></a>Servizi che non abilitano lo spostamento
servizi di Hello che attualmente non consentono di spostare una risorsa sono:

* AD Domain Services
* Servizio ibrido per l'integrità di AD
* gateway applicazione
* Set di disponibilità con macchine virtuali con Managed Disks
* Servizi BizTalk
* Servizio contenitore
* Express Route
* DevTest Labs - toonew spostamento risorse del gruppo nella stessa sottoscrizione sono abilitata, ma tra spostamento sottoscrizione non sono abilitata.
* Dynamics LCS
* Immagini create da Managed Disks
* Managed Disks
* Applicazioni gestite
* Insieme di credenziali di servizi di ripristino - anche eseguire hello servizi di ripristino non sposta hello calcolo, rete e archiviazione, le risorse associate all'insieme di credenziali, vedere [limitazioni di servizi di ripristino](#recovery-services-limitations).
* Sicurezza
* Snapshot creati da Managed Disks
* Gestione dispositivi StorSimple
* Macchine virtuali con Managed Disks
* Reti virtuali (classiche): vedere [Limitazioni della distribuzione classica](#classic-deployment-limitations)
* Impossibile spostare le macchine virtuali create da risorse Marketplace fra sottoscrizioni. È necessario toobe deprovisioning nella sottoscrizione corrente hello e distribuito di nuovo nella nuova sottoscrizione hello risorsa

## <a name="app-service-limitations"></a>Limitazioni del servizio app
Quando si usano le app del servizio app non è possibile spostare solo un piano di servizio app. le applicazioni di servizio App toomove, le opzioni disponibili sono:

* Spostare il piano di servizio App hello e tutte le altre risorse del servizio App in tale gruppo tooa nuova risorsa gruppo di risorse che non dispone di risorse del servizio App. Questo requisito significa che è necessario spostare anche hello risorse del servizio App che non sono associati al piano di servizio App hello.
* Sposta gruppo di risorse diverso tooa hello App, ma Mantieni tutti i piani di servizio App nel gruppo di risorse originale hello.

Hello servizio App non è necessario tooreside nel piano hello stesso gruppo di risorse applicazione hello per hello app toofunction correttamente.

Se ad esempio il gruppo di risorse contiene:

* **web-a** che è associata a **plan-a**
* **web-b** che è associata a **plan-b**

Le opzioni possibili sono:

* Spostare **web-a**, **plan-a**, **web-b** e **plan-b**
* Spostare **web-a** e **web-b**
* Spostare **web-a**
* Spostare **web-b**

Con tutte le altre combinazioni si lascerebbe dove si trova un tipo di risorsa che non può essere lasciato nella stessa posizione quando si sposta un piano di servizio app (qualsiasi tipo di risorsa del servizio app).

Se l'app web si trova in un gruppo di risorse diverso rispetto al relativo piano di servizio App, ma si desidera toomove entrambi tooa nuovo gruppo di risorse, è necessario eseguire spostamento hello in due passaggi. ad esempio:

* **web-a** si trova in **web-group**
* **plan-a** si trova in **plan-group**
* Si desidera **web-a** e **piano-a** tooreside in **gruppo combinati**

tooaccomplish questo spostamento, eseguire due operazioni di spostamento separato in hello seguente sequenza:

1. Spostare hello **web-a** troppo**piano gruppo**
2. Spostare **web-a** e **piano-a** troppo**gruppo combinati**.

È possibile spostare un certificato di servizio App tooa nuovo gruppo di risorse o di una sottoscrizione senza problemi. Tuttavia, se l'app web include un certificato SSL di acquistata esternamente e caricato toohello app, è necessario eliminare certificato hello prima dell'applicazione web di hello mobile. Ad esempio, è possibile eseguire hello alla procedura seguente:

1. Eliminare il certificato di hello caricata dall'app web hello
2. Spostare hello web app
3. Caricare hello certificato toohello web app

## <a name="recovery-services-limitations"></a>Limitazioni dei servizi di ripristino
Spostamento non è abilitato per l'archiviazione, rete, o risorse di calcolo utilizzato tooset ripristino di emergenza con Azure Site Recovery.

Ad esempio, si supponga di che aver configurato la replica di on-premise macchine tooa account di archiviazione (Storage1) e desidera toocome macchina hello protetto dopo il failover tooAzure come una macchina virtuale (VM1) è associata la rete virtuale tooa (rete1). Non è possibile spostare una di queste risorse Azure - Storage1, VM1, e - rete1 tra risorse gruppi all'interno di hello stessa sottoscrizione o per le sottoscrizioni.

## <a name="hdinsight-limitations"></a>Limitazioni di HDInsight

È possibile spostare HDInsight cluster tooa nuova sottoscrizione o un gruppo di risorse. Tuttavia, è possibile spostare tra hello sottoscrizioni rete cluster di HDInsight toohello collegato risorse (ad esempio una rete virtuale hello, scheda di rete o servizio di bilanciamento del carico). Inoltre, è possibile spostare il gruppo di risorse nuovo tooa una scheda di rete di macchina virtuale tooa collegato per il cluster hello.

Quando si sposta una nuova sottoscrizione tooa cluster HDInsight, spostare innanzitutto altre risorse (ad esempio account di archiviazione hello). Spostare quindi il cluster di HDInsight hello da se stesso.

## <a name="classic-deployment-limitations"></a>Limitazioni della distribuzione classica
salve le opzioni per lo spostamento delle risorse distribuite tramite il modello classico di hello differiscono a seconda se si desidera spostare le risorse di hello all'interno di una sottoscrizione o tooa nuova sottoscrizione.

### <a name="same-subscription"></a>Stessa sottoscrizione
Quando lo spostamento delle risorse dal gruppo di risorse di una risorsa gruppo tooanother all'interno di hello applicare stessa sottoscrizione, hello seguenti restrizioni:

* Le reti virtuali (classiche) non possono essere spostate.
* Macchine virtuali (classico) devono essere spostate con il servizio cloud hello.
* Servizio cloud può essere spostato solo quando si sposta hello include tutte le macchine virtuali.
* È possibile spostare un solo servizio cloud alla volta.
* È possibile spostare un solo account di archiviazione (classico) alla volta.
* Account di archiviazione (classico) non può essere spostato in hello stessa operazione con una macchina virtuale o un servizio cloud.

toomove le risorse classiche tooa nuovo gruppo di risorse interno hello stessa sottoscrizione, utilizzare le operazioni di spostamento standard hello tramite hello [portale](#use-portal), [Azure PowerShell](#use-powershell), [CLI di Azure](#use-azure-cli), o [API REST](#use-rest-api). Utilizzare hello stesse operazioni quando si utilizza per lo spostamento delle risorse di gestione risorse.

### <a name="new-subscription"></a>Nuova sottoscrizione
Quando si spostano nuova sottoscrizione di risorse tooa, si applica hello seguenti restrizioni:

* Tutte le risorse classiche nella sottoscrizione hello devono essere spostate in hello stessa operazione.
* sottoscrizione di destinazione Hello non deve contenere tutte le altre risorse classiche.
* spostamento Hello può essere richiesti solo tramite un'API REST separato per gli spostamenti classici. comandi di spostamento Hello standard di gestione delle risorse non funzionano quando sposta le risorse classiche tooa nuova sottoscrizione.

toomove le risorse classiche tooa nuova sottoscrizione, utilizzare hello le operazioni REST che rappresentano risorse tooclassic specifico. toouse REST, eseguire hello alla procedura seguente:

1. Verifica se la sottoscrizione di origine hello può partecipare a una sottoscrizione tra spostare. Utilizzare hello seguente operazione:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     Nel corpo della richiesta hello, includere:

  ```json
  {
    "role": "source"
  }
  ```

     risposta Hello per l'operazione di convalida hello è nel seguente formato hello:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Verifica se la sottoscrizione di destinazione hello può partecipare a una sottoscrizione tra spostare. Utilizzare hello seguente operazione:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     Nel corpo della richiesta hello, includere:

  ```json
  {
    "role": "target"
  }
  ```

     risposta Hello è nel stesso formato delle convalida della sottoscrizione di origine hello hello.
3. Se entrambe le sottoscrizioni superano la convalida, spostare tutte le risorse classiche dalla sottoscrizione di una sottoscrizione tooanother con hello seguente operazione:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    Nel corpo della richiesta hello, includere:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

può eseguire l'operazione di Hello per alcuni minuti.

## <a name="use-portal"></a>Usare il portale
risorse toomove, selezionare il gruppo di risorse hello contenente tali risorse, quindi hello **spostare** pulsante.

![Spostare le risorse](./media/resource-group-move-resources/select-move.png)

Selezionare se si sta spostando hello risorse tooa nuovo gruppo di risorse o una nuova sottoscrizione.

Selezionare toomove risorse hello e gruppo di risorse di destinazione hello. Confermare che è necessario tooupdate script per le risorse e selezionare **OK**. Se è stata selezionata nel passaggio precedente hello sull'icona di hello Modifica sottoscrizione, è necessario selezionare anche la sottoscrizione di destinazione hello.

![Selezione della destinazione](./media/resource-group-move-resources/select-destination.png)

In **notifiche**, vedrai che hello spostare l'operazione è in esecuzione.

![Visualizzare lo stato dello spostamento](./media/resource-group-move-resources/show-status.png)

Quando è stata completata, ricevono la notifica del risultato hello.

![Visualizzare il risultato dello spostamento](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>Usare PowerShell
esistente toomove gruppo di risorse tooanother risorse o una sottoscrizione, utilizzare hello `Move-AzureRmResource` comando.

Hello primo esempio viene illustrato come toomove una risorsa tooa nuovo gruppo di risorse.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Hello secondo esempio viene illustrato come toomove più risorse tooa nuovo gruppo di risorse.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa nuova sottoscrizione, includere un valore per hello `DestinationSubscriptionId` parametro.

Viene richiesto che si desidera hello toomove tooconfirm delle risorse specificate.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Usare l'interfaccia della riga di comando 2.0 di Azure
esistente toomove gruppo di risorse tooanother risorse o una sottoscrizione, utilizzare hello `az resource move` comando. Fornire hello ID risorsa delle toomove risorse hello. È possibile ottenere l'ID di risorsa con hello comando seguente:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Hello di esempio seguente viene illustrato come una risorsa di archiviazione toomove account tooa nuovo gruppo di risorse. In hello `--ids` parametro, fornire un elenco separato da spazi di toomove gli ID di risorsa hello.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

nuova sottoscrizione tooa toomove, fornire hello `--destination-subscription-id` parametro.

## <a name="use-azure-cli-10"></a>Usare l'interfaccia della riga di comando di Azure 1.0
esistente toomove gruppo di risorse tooanother risorse o una sottoscrizione, utilizzare hello `azure resource move` comando. Fornire hello ID risorsa delle toomove risorse hello. È possibile ottenere l'ID di risorsa con hello comando seguente:

```azurecli
azure resource list -g sourceGroup --json
```

Restituisce hello seguente formato:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

Hello di esempio seguente viene illustrato come una risorsa di archiviazione toomove account tooa nuovo gruppo di risorse. In hello `-i` parametro, fornire un elenco delimitato da virgole di toomove gli ID di risorsa hello.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

Viene richiesto che si desidera toomove hello tooconfirm risorsa specificata.

## <a name="use-rest-api"></a>Usare l'API REST
gruppo risorse tooanother toomove esistente risorse o sottoscrizione, eseguire:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

Nel corpo della richiesta hello, specificare gruppo di risorse di destinazione hello e toomove risorse hello. Per ulteriori informazioni sull'operazione di resto spostamento hello, vedere [lo spostamento di risorse](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Passaggi successivi
* toolearn sui cmdlet di PowerShell per gestire la sottoscrizione, vedere [tramite Azure PowerShell con Gestione risorse di](powershell-azure-resource-manager.md).
* toolearn sui comandi CLI di Azure per gestire la sottoscrizione, vedere [Using hello CLI di Azure con Gestione risorse di](xplat-cli-azure-resource-manager.md).
* toolearn sulle funzionalità del portale per gestire la sottoscrizione, vedere [utilizzando le risorse di Azure toomanage portale hello](resource-group-portal.md).
* toolearn sull'applicazione di una risorsa tooyour organizzazione logica, vedere [tramite tag tooorganize le risorse](resource-group-using-tags.md).
