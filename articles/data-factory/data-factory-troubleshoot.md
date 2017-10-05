---
title: Risolvere i problemi di Data factory di Azure
description: Informazioni su come risolvere i problemi relativi all'uso di Data factory di Azure.
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
ms.openlocfilehash: 953a2703db7c8991f580a7c963d6cbd94265c213
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="ea297-103">Risolvere i problemi di Data factory</span><span class="sxs-lookup"><span data-stu-id="ea297-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="ea297-104">Questo articolo contiene suggerimenti per la risoluzione dei problemi correlati all'uso di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ea297-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="ea297-105">L'articolo non elenca tutti i problemi che si possono verificare usando il servizio, ma suggerisce come individuare e risolvere alcuni di essi.</span><span class="sxs-lookup"><span data-stu-id="ea297-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="ea297-106">Suggerimenti per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ea297-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="ea297-107">Errore: La sottoscrizione non è registrata per l'uso dello spazio dei nomi 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="ea297-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="ea297-108">Se viene visualizzato questo errore, il provider di risorse di Azure Data Factory non è stato registrato nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ea297-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="ea297-109">Eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea297-109">Do the following:</span></span>

1. <span data-ttu-id="ea297-110">Avviare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea297-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="ea297-111">Accedere al proprio account di Azure usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="ea297-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="ea297-112">Eseguire il comando seguente per registrare il provider di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ea297-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="ea297-113">Problema: errore di mancata autorizzazione quando si esegue un cmdlet di Data factory</span><span class="sxs-lookup"><span data-stu-id="ea297-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="ea297-114">È probabile che non si stia usando l'account o la sottoscrizione di Azure corretta con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea297-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="ea297-115">Usare i cmdlet seguenti per selezionare l'account e la sottoscrizione di Azure corretti per Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea297-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="ea297-116">Login-AzureRmAccount: usare l'ID utente e la password corretti</span><span class="sxs-lookup"><span data-stu-id="ea297-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="ea297-117">Get-AzureRmSubscription: visualizza tutte le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="ea297-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="ea297-118">Select-AzureRmSubscription &lt;nome della sottoscrizione&gt;: selezionare la sottoscrizione corretta.</span><span class="sxs-lookup"><span data-stu-id="ea297-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="ea297-119">Usare la stessa sottoscrizione selezionata per creare un Data Factory nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea297-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="ea297-120">Problema: impossibile avviare l'installazione rapida del Gateway di gestione dati dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ea297-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="ea297-121">L'installazione rapida del Gateway di gestione dati richiede Internet Explorer o un Web browser compatibile con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="ea297-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="ea297-122">Se non è possibile avviare l'installazione rapida, eseguire una di queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="ea297-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="ea297-123">Usare Internet Explorer o un Web browser compatibile con Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="ea297-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="ea297-124">Se si usa Chrome, accedere al [Chrome Web Store](https://chrome.google.com/webstore/), eseguire una ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni ClickOnce e installarla.</span><span class="sxs-lookup"><span data-stu-id="ea297-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="ea297-125">Seguire la stessa procedura per Firefox (installazione di un componente aggiuntivo).</span><span class="sxs-lookup"><span data-stu-id="ea297-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="ea297-126">Fare clic sul pulsante Apri menu sulla barra degli strumenti (tre righe orizzontali nell'angolo superiore destro), fare clic su Componenti aggiuntivi, eseguire una ricerca con la parola chiave "ClickOnce", scegliere una delle estensioni ClickOnce e installarla.</span><span class="sxs-lookup"><span data-stu-id="ea297-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="ea297-127">Usare il collegamento all' **installazione manuale** visualizzato sullo stesso pannello nel portale.</span><span class="sxs-lookup"><span data-stu-id="ea297-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="ea297-128">Adottare questo approccio per scaricare il file di installazione ed eseguirlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="ea297-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="ea297-129">Al termine dell'installazione viene visualizzata la finestra di configurazione di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="ea297-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="ea297-130">Copiare la **chiave** dalla schermata del portale e usarla in Gestione configurazione per registrare manualmente il gateway con il servizio.</span><span class="sxs-lookup"><span data-stu-id="ea297-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="ea297-131">Problema: impossibile connettersi all'istanza di SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="ea297-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="ea297-132">Avviare **Gestione configurazione di Gateway di gestione dati** nel computer gateway e usare la scheda **Risoluzione dei problemi** per testare la connessione a SQL Server dal computer gateway.</span><span class="sxs-lookup"><span data-stu-id="ea297-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="ea297-133">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="ea297-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="ea297-134">Problema: le sezioni di input rimangono nello stato Waiting</span><span class="sxs-lookup"><span data-stu-id="ea297-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="ea297-135">Le sezioni potrebbero essere **In attesa** per diversi motivi.</span><span class="sxs-lookup"><span data-stu-id="ea297-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="ea297-136">Uno dei motivi più comuni è che la proprietà **external** non è impostata su **true**.</span><span class="sxs-lookup"><span data-stu-id="ea297-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="ea297-137">Eventuali set di dati prodotti all'esterno dell'ambito di Azure Data Factory devono essere contrassegnati con la proprietà **external** .</span><span class="sxs-lookup"><span data-stu-id="ea297-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="ea297-138">Questa proprietà indica che i dati sono esterni e non sono supportati da alcuna pipeline nel Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ea297-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="ea297-139">Le sezioni di dati vengono contrassegnate con **Pronto** quando i dati sono disponibili nel rispettivo archivio.</span><span class="sxs-lookup"><span data-stu-id="ea297-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="ea297-140">Per l'uso della proprietà **external** , vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="ea297-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="ea297-141">È possibile specificare facoltativamente **externalData*** quando si imposta la proprietà external su true.</span><span class="sxs-lookup"><span data-stu-id="ea297-141">You can optionally specify **externalData*** when you set external to true.</span></span>

<span data-ttu-id="ea297-142">Per altre informazioni su questa proprietà, vedere [Set di dati in Azure Data Factory](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="ea297-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

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

<span data-ttu-id="ea297-143">Per risolvere l'errore, aggiungere la proprietà **external** e la sezione **externalData** facoltativa alla definizione JSON della tabella di input e ricreare la tabella.</span><span class="sxs-lookup"><span data-stu-id="ea297-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="ea297-144">Problema: l'operazione di copia ibrida non riesce</span><span class="sxs-lookup"><span data-stu-id="ea297-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="ea297-145">Per le procedure di risoluzione dei problemi relativi alla copia da e verso un archivio dati locale usando il gateway di gestione dati, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="ea297-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="ea297-146">Problema: non è possibile eseguire il provisioning di HDInsight su richiesta</span><span class="sxs-lookup"><span data-stu-id="ea297-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="ea297-147">Quando si usa un servizio collegato di tipo HDInsightOnDemand, è necessario specificare un linkedServiceName che punta a un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea297-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="ea297-148">Il servizio Data Factory usa questa risorsa di archiviazione per archiviare Questo account di archiviazione verrà usato per copiare i log e i file di supporto per il cluster HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ea297-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="ea297-149">In alcuni casi il provisioning di un cluster HDInsight su richiesta ha esito negativo con l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="ea297-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="ea297-150">Questo errore di solito indica che il percorso dell'account di archiviazione specificato nel linkedServiceName non si trova nella stessa posizione del data center in cui viene eseguito il provisioning di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea297-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="ea297-151">Esempio: se il Data Factory si trova negli Stati Uniti occidentali e l'archiviazione di Azure è negli Stati Uniti orientali, il provisioning su richiesta ha esito negativo negli Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="ea297-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="ea297-152">È anche disponibile una seconda proprietà JSON additionalLinkedServiceNames in cui è possibile specificare account di archiviazione aggiuntivi in HDInsight su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ea297-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="ea297-153">Gli account di archiviazione aggiuntivi collegati devono trovarsi nello stesso percorso del cluster HDInsight oppure avranno esito negativo, producendo lo stesso errore.</span><span class="sxs-lookup"><span data-stu-id="ea297-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="ea297-154">Problema: l'attività .NET personalizzata non riesce</span><span class="sxs-lookup"><span data-stu-id="ea297-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="ea297-155">Per una procedura dettagliata, vedere la sezione [Eseguire il debug della pipeline](data-factory-use-custom-activities.md#troubleshoot-failures) .</span><span class="sxs-lookup"><span data-stu-id="ea297-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="ea297-156">Usare il portale di Azure per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ea297-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="ea297-157">Uso dei pannelli del portale</span><span class="sxs-lookup"><span data-stu-id="ea297-157">Using portal blades</span></span>
<span data-ttu-id="ea297-158">Per una procedura dettagliata, vedere la sezione [Monitorare la pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="ea297-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="ea297-159">Uso dell'app di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="ea297-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="ea297-160">Per informazioni dettagliate, vedere [Monitorare e gestire le pipeline di Azure Data Factory con la nuova app di monitoraggio e gestione](data-factory-monitor-manage-app.md) .</span><span class="sxs-lookup"><span data-stu-id="ea297-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="ea297-161">Usare Azure PowerShell per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ea297-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="ea297-162">Usare Azure PowerShell per risolvere un errore</span><span class="sxs-lookup"><span data-stu-id="ea297-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="ea297-163">Per informazioni su come monitorare le pipeline di Data Factory con Azure PowerShell, vedere la sezione [Monitorare la pipeline](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="ea297-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

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
