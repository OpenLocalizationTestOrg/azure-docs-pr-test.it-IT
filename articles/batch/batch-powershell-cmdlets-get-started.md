---
title: aaaGet introduttiva a PowerShell per Azure Batch | Documenti Microsoft
description: "Toohello una rapida introduzione dei cmdlet di Azure PowerShell è possibile utilizzare le risorse di Batch toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>Gestire le risorse Batch con i cmdlet di PowerShell

Con i cmdlet PowerShell di Azure Batch hello, è possibile eseguire e script molti hello stesse attività svolgere con le API di Batch, hello hello portale di Azure e hello Azure interfaccia della riga di comando (CLI). Si tratta di un cmdlet toohello introduzione rapida è possibile usare toomanage gli account di Batch e lavorare con le risorse di Batch, ad esempio pool di processi e attività.

Per un elenco completo dei cmdlet di Batch e sintassi del cmdlet dettagliate, vedere hello [riferimento ai cmdlet di Azure Batch](/powershell/module/azurerm.batch/#batch).

Questo articolo si basa sui cmdlet di Azure PowerShell versione 3.0.0. È consigliabile aggiornare il Azure PowerShell spesso tootake vantaggio di servizio aggiornamenti e miglioramenti.

## <a name="prerequisites"></a>Prerequisiti
Eseguire hello dopo operazioni toouse Azure PowerShell toomanage le risorse di Batch.

* [Installare e configurare Azure PowerShell](/powershell/azure/overview)
* Eseguire hello **accesso AzureRmAccount** cmdlet tooconnect tooyour sottoscrizione (Buongiorno spedire i cmdlet di Azure Batch nel modulo di gestione risorse di Azure hello):
  
    `Login-AzureRmAccount`
* **Registrare con spazio dei nomi del provider di Batch hello**. Questa operazione è sufficiente eseguire toobe **una volta per ogni sottoscrizione**.
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>Gestire gli account e le chiavi Batch
### <a name="create-a-batch-account"></a>Creare un account Batch
**New-AzureRmBatchAccount** crea un account Batch in un gruppo di risorse specificato. Se si dispone già di un gruppo di risorse, crearne una eseguendo hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet. Specificare uno dei hello Azure aree in hello **percorso** parametro, ad esempio "Central US". ad esempio:

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

Quindi, creare un account Batch nel gruppo di risorse hello, specificando un nome per l'account di hello in <*account_name*> e il percorso di hello e nome del gruppo di risorse. Creazione di account di Batch hello può richiedere alcuni toocomplete ora. ad esempio:

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> account di Batch Hello nome deve essere univoco toohello area di Azure per il gruppo di risorse hello, essere compresa tra 3 e 24 caratteri e utilizzare solo lettere minuscole e numeri.
> 
> 

### <a name="get-account-access-keys"></a>Ottenere le chiavi di accesso all'account
**Get-AzureRmBatchAccountKeys** Mostra chiavi di accesso hello associate a un account Azure Batch. Ad esempio, eseguire hello seguenti chiavi tooget hello primaria e secondaria dell'account hello creato.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>Generare una nuova chiave di accesso
**New-AzureRmBatchAccountKey** genera una nuova chiave dell'account primaria o secondaria per un account Azure Batch. Ad esempio, toogenerate una nuova chiave primaria per l'account Batch, digitare:

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> toogenerate una nuova chiave secondaria, specificare "Secondario" per hello **KeyType** parametro. Hai chiavi primarie e secondarie hello tooregenerate separatamente.
> 
> 

### <a name="delete-a-batch-account"></a>Eliminare un account Batch
**Remove-AzureRmBatchAccount** elimina un account Batch. ad esempio:

    Remove-AzureRmBatchAccount -AccountName <account_name>

Quando richiesto, confermare l'account di hello tooremove. La rimozione di account può richiedere alcuni toocomplete ora.

## <a name="create-a-batchaccountcontext-object"></a>Creare un oggetto BatchAccountContext
utilizzando tooauthenticate hello i cmdlet di PowerShell Batch quando si crea e Gestisci pool di Batch, i processi, attività, e altre risorse, creare innanzitutto un toostore oggetto BatchAccountContext il nome dell'account e le chiavi:

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

Si passa l'oggetto di BatchAccountContext hello in cmdlet hello tale utilizzo **BatchContext** parametro.

> [!NOTE]
> Per impostazione predefinita, la chiave primaria dell'account hello viene utilizzata per l'autenticazione, ma è possibile selezionare esplicitamente toouse chiave hello modificando l'oggetto di BatchAccountContext **KeyInUse** proprietà: `$context.KeyInUse = "Secondary"`.
> 
> 

## <a name="create-and-modify-batch-resources"></a>Creare e modificare le risorse Batch
Utilizzare i cmdlet, ad esempio **New AzureBatchPool**, **New AzureBatchJob**, e **New AzureBatchTask** toocreate risorse in un account di Batch. Sono disponibili corrispondenti **Get -** e **Set -** proprietà hello tooupdate di cmdlet di risorse esistente, e **Remove -** cmdlet tooremove risorse con un account Batch.

Quando si utilizza molti di questi cmdlet, toopassing inoltre un oggetto BatchContext, è necessario toocreate o passare gli oggetti che contengono le impostazioni dettagliate risorse, come illustrato nell'esempio seguente hello. Vedere hello informazioni dettagliate della Guida per ciascun cmdlet per altri esempi.

### <a name="create-a-batch-pool"></a>Creare un pool di Batch
Durante la creazione o l'aggiornamento di un pool di Batch, si seleziona la configurazione di macchina virtuale hello o della configurazione del servizio cloud hello per hello del sistema operativo su hello nodi di calcolo (vedere [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md#pool)). Se si specifica la configurazione del servizio cloud hello, i nodi di calcolo si crea un'immagine con uno di hello [versioni del sistema operativo Guest Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases). Se si specifica la configurazione della macchina virtuale hello, è possibile specificare uno dei hello è supportato Linux o immagini di macchina virtuale di Windows hello elencato in [macchine virtuali di Azure Marketplace][vm_marketplace], o fornire un oggetto personalizzato immagine preparata.

Quando si esegue **New AzureBatchPool**, passare a impostazioni del sistema operativo hello in un oggetto PSCloudServiceConfiguration o PSVirtualMachineConfiguration. Ad esempio, hello cmdlet seguente crea un nuovo pool di Batch con nodi di calcolo piccole dimensioni nella configurazione del servizio cloud hello, viene creata un'immagine con hello del sistema operativo più recente della famiglia 3 (Windows Server 2012). In questo caso, hello **CloudServiceConfiguration** parametro specifica hello *$configuration* variabile come oggetto PSCloudServiceConfiguration hello. Hello **BatchContext** parametro specifica una variabile definita in precedenza *$context* come oggetto BatchAccountContext hello.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

numero di destinazione Hello dei nodi di calcolo nel nuovo pool di hello è determinato da una formula di scalabilità automatica. In questo caso, la formula hello è semplicemente **$TargetDedicated = 4**, che indica il numero di hello dei nodi di calcolo nel pool di hello è al massimo 4.

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>Query per pool, processi, attività e altri dettagli
Utilizzare i cmdlet, ad esempio **Get AzureBatchPool**, **Get AzureBatchJob**, e **Get AzureBatchTask** tooquery per le entità create con un account Batch.

### <a name="query-for-data"></a>Eseguire query per ottenere dati
Ad esempio, utilizzare **Get AzureBatchPools** toofind i pool. Per impostazione predefinita, questo esegue una query per tutti i pool con l'account, presupponendo che sia già archiviato l'oggetto BatchAccountContext hello in *$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>Usare un filtro OData
È possibile specificare un filtro OData utilizzando hello **filtro** toofind parametro hello solo oggetti di cui si è interessati. Ad esempio, è possibile trovare tutti i pool con nomi che iniziano con "myPool":

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

Questo metodo non è flessibile come l'uso di "Where-Object" in una pipeline locale. Tuttavia, query hello viene inviato toohello servizio Batch direttamente in modo che tutti i filtri avviene sul lato server hello, risparmiando larghezza di banda Internet.

### <a name="use-hello-id-parameter"></a>Utilizzare il parametro Id hello
Un filtro di OData tooan alternativo è hello toouse **Id** parametro. tooquery per un pool specifico con id "myPool":

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

Hello **Id** parametro supporta solo la ricerca full-id, non i caratteri jolly o i filtri di stile di OData.

### <a name="use-hello-maxcount-parameter"></a>Utilizzare il parametro MaxCount hello
Per impostazione predefinita, ogni cmdlet restituisce un massimo di 1000 oggetti. Se si raggiunge questo limite, ridefinire il filtro toobring nuovamente meno oggetti oppure impostare in modo esplicito un massimo di utilizzo hello **MaxCount** parametro. ad esempio:

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

limite superiore di hello tooremove, impostare **MaxCount** too0 o meno.

### <a name="use-hello-powershell-pipeline"></a>Utilizzare la pipeline di PowerShell hello
I cmdlet di batch possono sfruttare hello PowerShell pipeline toosend dei dati tra i cmdlet. Questa operazione ha lo stesso effetto dell'impostazione di un parametro, ma rende l'utilizzo con più entità hello.

Ad esempio, per trovare e visualizzare tutte le attività dell'account:

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

Per riavviare ogni nodo di calcolo in un pool:

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>Gestione dei pacchetti dell'applicazione
Pacchetti di applicazioni forniscono un modo semplificato toodeploy applicazioni toohello nodi nei pool di calcolo. Con i cmdlet di PowerShell Batch hello, è possibile caricare e gestire i pacchetti di applicazioni nell'account di Batch e distribuire i nodi toocompute di versioni di pacchetto.

**Creare** un'applicazione:

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

**Aggiungere** un pacchetto dell'applicazione:

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

Set hello **versione predefinita** per un'applicazione hello:

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

**Elencare** i pacchetti dell'applicazione

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

**Eliminare** un pacchetto dell'applicazione

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

**Eliminare** un'applicazione

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> È necessario eliminare tutte le versioni di pacchetto di applicazione di un'applicazione prima di eliminare un'applicazione hello. Se si tenta di toodelete un'applicazione che dispone attualmente di pacchetti di applicazioni, si riceverà un errore di 'Conflitto'.
> 
> 

### <a name="deploy-an-application-package"></a>Distribuire un pacchetto dell'applicazione
Quando si crea un pool è possibile specificare uno o più pacchetti dell'applicazione da distribuire. Quando si specifica un pacchetto in fase di creazione di pool, è il nodo tooeach distribuito come hello nodo join pool. I pacchetti vengono distribuiti anche quando un nodo viene riavviato o ne viene ricreata l'immagine.

Specificare hello `-ApplicationPackageReference` opzione quando si crea un pool toodeploy nodi di un pacchetto toohello del pool di applicazioni che si connettono pool hello. Creare innanzitutto un **PSApplicationPackageReference** dell'oggetto e configurarlo con hello Id pacchetto e la versione dell'applicazione si desidera toodeploy toohello pool nodi di calcolo:

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

A questo punto creare pool di hello e specificare l'oggetto di riferimento pacchetto hello hello argomento toohello `ApplicationPackageReferences` opzione:

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

È possibile trovare ulteriori informazioni sui pacchetti di applicazioni in [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).

> [!IMPORTANT]
> È necessario [collegare un account di archiviazione di Azure](#linked-storage-account-autostorage) tooyour Batch account toouse pacchetti di applicazioni.
> 
> 

### <a name="update-a-pools-application-packages"></a>Aggiornare i pacchetti dell’applicazione di un pool
applicazioni di hello tooupdate assegnate tooan pool esistente, creare innanzitutto un oggetto PSApplicationPackageReference con proprietà hello desiderato (Id pacchetto e la versione dell'applicazione):

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

Successivamente, ottenere il pool di hello dal Batch, cancellare tutti i pacchetti esistenti, aggiungere il nuovo riferimento al pacchetto e aggiornare il servizio Batch hello con le nuove impostazioni del pool di hello:

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

Ora è effettuato l'aggiornamento delle proprietà del pool di hello nel servizio Batch hello. tooactually distribuire hello nuovo pacchetto toocompute nodi di applicazioni nel pool di hello, tuttavia, è necessario riavviare o ricreare l'immagine di tali nodi. È possibile riavviare ogni nodo di un pool con questo comando:

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> È possibile distribuire più applicazione pacchetti toohello nodi di calcolo in un pool. Se si desidera troppo*aggiungere* un pacchetto di applicazioni non sostituisce i pacchetti hello attualmente distribuita, omettere hello `$pool.ApplicationPackageReferences.Clear()` riga precedente.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Per la sintassi dettagliata ed esempi dei cmdlet, vedere le [informazioni di riferimento sui cmdlet per Azure Batch](/powershell/module/azurerm.batch/#batch).
* Per ulteriori informazioni sulle applicazioni e pacchetti di applicazioni in Batch, vedere [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/