---
title: problemi di Azure Data Factory aaaTroubleshoot
description: Informazioni su come tootroubleshoot problemi con Data Factory di Azure.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="9a6a7-103">Risolvere i problemi di Data factory</span><span class="sxs-lookup"><span data-stu-id="9a6a7-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="9a6a7-104">Questo articolo contiene suggerimenti per la risoluzione dei problemi correlati all'uso di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="9a6a7-105">In questo articolo non sono elencati tutti i possibili problemi di hello quando si utilizza servizio hello, ma comprende alcuni problemi e suggerimenti sulla risoluzione dei problemi generali.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="9a6a7-106">Suggerimenti per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9a6a7-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="9a6a7-107">Errore: hello sottoscrizione non è registrato toouse dello spazio dei nomi 'Microsoft. DataFactory'</span><span class="sxs-lookup"><span data-stu-id="9a6a7-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="9a6a7-108">Se si riceve questo errore, provider di risorse hello Azure Data Factory non è stato registrato nel computer.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="9a6a7-109">Hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9a6a7-109">Do hello following:</span></span>

1. <span data-ttu-id="9a6a7-110">Avviare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="9a6a7-111">Accedi tooyour account Azure tramite hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="9a6a7-112">Eseguire i seguenti provider di Azure Data Factory di comandi tooregister hello hello.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="9a6a7-113">Problema: errore di mancata autorizzazione quando si esegue un cmdlet di Data factory</span><span class="sxs-lookup"><span data-stu-id="9a6a7-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="9a6a7-114">Probabilmente non utilizza destra hello account Azure o una sottoscrizione con hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="9a6a7-115">Utilizzare hello cmdlet tooselect hello destra toouse di account e la sottoscrizione Azure con hello Azure PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="9a6a7-116">Account di accesso-AzureRmAccount - ID utente di utilizzare hello e una password</span><span class="sxs-lookup"><span data-stu-id="9a6a7-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="9a6a7-117">Get-AzureRmSubscription - Visualizza tutte le sottoscrizioni per account hello di hello.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="9a6a7-118">Selezionare AzureRmSubscription &lt;nome sottoscrizione&gt; -selezionare hello destra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="9a6a7-119">Utilizzare hello stesso che si utilizza una data factory toocreate su hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="9a6a7-120">Problema: Non toolaunch installazione di Express Data Management Gateway dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9a6a7-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="9a6a7-121">installazione di Express Hello per Gateway di gestione dati hello richiede Internet Explorer o un browser compatibile Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="9a6a7-122">Se l'installazione di Express hello ha esito negativo toostart, effettuare uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="9a6a7-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="9a6a7-123">Usare Internet Explorer o un Web browser compatibile con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="9a6a7-124">Se si utilizza Chrome, andare toohello [archivio web Chrome](https://chrome.google.com/webstore/), eseguire la ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni di ClickOnce hello e installarlo.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="9a6a7-125">Hello stesso per Firefox (Installa componente aggiuntivo).</span><span class="sxs-lookup"><span data-stu-id="9a6a7-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="9a6a7-126">Fare clic sul pulsante Apri Menu sulla barra degli strumenti hello (tre linee orizzontali nell'angolo superiore destro hello), fare clic su componenti aggiuntivi, eseguire la ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni di ClickOnce hello e installarlo.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="9a6a7-127">Hello utilizzare **l'installazione manuale** collegamento visualizzato in hello stesso pannello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="9a6a7-128">Utilizzare questo file di installazione toodownload approccio ed eseguirlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="9a6a7-129">Dopo l'installazione di hello ha esito positivo, vengono visualizzati la finestra di dialogo di configurazione di Gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="9a6a7-130">Hello copia **chiave** dalla schermata di portale hello e utilizzare in hello configuration manager toomanually registrare gateway hello hello servizio.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="9a6a7-131">Problema: Non tooconnect tooon locale SQL Server</span><span class="sxs-lookup"><span data-stu-id="9a6a7-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="9a6a7-132">Avviare **Gestione configurazione di Gateway di gestione di dati** hello computer gateway e utilizzare hello **Troubleshooting** scheda tootest hello connessione tooSQL Server dal computer del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="9a6a7-133">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="9a6a7-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="9a6a7-134">Problema: le sezioni di input rimangono nello stato Waiting</span><span class="sxs-lookup"><span data-stu-id="9a6a7-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="9a6a7-135">le sezioni Hello potrebbe essere in **in attesa** dello stato a causa di motivi toovarious.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="9a6a7-136">Uno dei motivi comuni hello è tale hello **esterno** non è impostata troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="9a6a7-137">Qualsiasi set di dati che è l'ambito di prodotti hello all'esterno di Azure Data Factory deve essere contrassegnato con **esterno** proprietà.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="9a6a7-138">Questa proprietà indica che i dati di hello esterni e non è supportato da qualsiasi pipeline all'interno di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="9a6a7-139">le sezioni di dati Hello sono contrassegnate come **pronto** quando dati hello sono disponibili nell'archivio rispettivi hello.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="9a6a7-140">Vedere l'esempio per l'utilizzo di hello di hello seguente hello **esterno** proprietà.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="9a6a7-141">È possibile specificare facoltativamente **externalData*** quando si imposta tootrue esterno.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="9a6a7-142">Per altre informazioni su questa proprietà, vedere [Set di dati in Azure Data Factory](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="9a6a7-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="9a6a7-143">tooresolve hello errore, aggiungere hello **esterno** proprietà e hello facoltativo **externalData** sezione Definizione JSON toohello della tabella di input hello e ricreare la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="9a6a7-144">Problema: l'operazione di copia ibrida non riesce</span><span class="sxs-lookup"><span data-stu-id="9a6a7-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="9a6a7-145">Vedere [risolvere i problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) per passaggi tootroubleshoot problemi con la copia da e verso un dati locali archiviano utilizzando hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="9a6a7-146">Problema: non è possibile eseguire il provisioning di HDInsight su richiesta</span><span class="sxs-lookup"><span data-stu-id="9a6a7-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="9a6a7-147">Quando si utilizza un servizio collegato di tipo HDInsightOnDemand, è necessario toospecify un linkedServiceName che punta tooan archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="9a6a7-148">Servizio Data Factory viene utilizzata questa archiviazione toostore registri e i file di supporto per il cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="9a6a7-149">In alcuni casi il provisioning di un cluster di HDInsight su richiesta non riesce con hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="9a6a7-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="9a6a7-150">Questo errore indica generalmente che il percorso di hello hello dell'account di archiviazione specificato in linkedServiceName hello non hello posizione in cui avviene il provisioning di HDInsight hello stesso data center.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="9a6a7-151">Esempio: se la data factory negli Stati Uniti occidentali e hello archiviazione di Azure in Stati Uniti orientali, hello su richiesta ha esito negativo provisioning negli Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="9a6a7-152">È anche disponibile una seconda proprietà JSON additionalLinkedServiceNames in cui è possibile specificare account di archiviazione aggiuntivi in HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="9a6a7-153">Tali account di archiviazione collegato aggiuntivi hello stessa località del cluster HDInsight hello o ha esito negativo con hello deve essere lo stesso errore.</span><span class="sxs-lookup"><span data-stu-id="9a6a7-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="9a6a7-154">Problema: l'attività .NET personalizzata non riesce</span><span class="sxs-lookup"><span data-stu-id="9a6a7-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="9a6a7-155">Per una procedura dettagliata, vedere la sezione [Eseguire il debug della pipeline](data-factory-use-custom-activities.md#troubleshoot-failures) .</span><span class="sxs-lookup"><span data-stu-id="9a6a7-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="9a6a7-156">Utilizzare tootroubleshoot portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9a6a7-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="9a6a7-157">Uso dei pannelli del portale</span><span class="sxs-lookup"><span data-stu-id="9a6a7-157">Using portal blades</span></span>
<span data-ttu-id="9a6a7-158">Per una procedura dettagliata, vedere la sezione [Monitorare la pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="9a6a7-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="9a6a7-159">Uso dell'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="9a6a7-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="9a6a7-160">Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md) .</span><span class="sxs-lookup"><span data-stu-id="9a6a7-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="9a6a7-161">Usare Azure PowerShell tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="9a6a7-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="9a6a7-162">Usare Azure PowerShell tootroubleshoot un errore</span><span class="sxs-lookup"><span data-stu-id="9a6a7-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="9a6a7-163">Per informazioni su come monitorare le pipeline di Data Factory con Azure PowerShell, vedere la sezione [Monitorare la pipeline](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="9a6a7-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
