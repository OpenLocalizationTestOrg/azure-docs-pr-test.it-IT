---
title: aaaStore e visualizza i dati di diagnostica in archiviazione di Azure | Documenti Microsoft
description: Trasferire i dati di diagnostica di Azure in un account di archiviazione di Azure e visualizzarli
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="4350e-103">Archiviare e visualizzare i dati di diagnostica nell'account di archiviazione Azure</span><span class="sxs-lookup"><span data-stu-id="4350e-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="4350e-104">Dati di diagnostica non vengono archiviati in modo permanente solo se vengono trasferiti toohello emulatore di archiviazione di Microsoft Azure o archiviazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4350e-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="4350e-105">Una volta trasferiti nella risorsa di archiviazione, sono disponibili diversi strumenti per visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="4350e-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="4350e-106">Specificare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4350e-106">Specify a storage account</span></span>
<span data-ttu-id="4350e-107">Specificare hello account di archiviazione che si desidera toouse nel file ServiceConfiguration. cscfg hello.</span><span class="sxs-lookup"><span data-stu-id="4350e-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="4350e-108">informazioni sull'account Hello è definiti come una stringa di connessione in un'impostazione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4350e-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="4350e-109">Hello riportato di seguito stringa di connessione predefinita hello creato per un nuovo progetto di servizio Cloud in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="4350e-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="4350e-110">È possibile modificare queste informazioni di account di tooprovide stringa di connessione per un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4350e-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="4350e-111">In base al tipo di dati di diagnostica che si desidera raccogliere hello diagnostica Azure Usa servizio Blob hello o del servizio tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="4350e-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="4350e-112">Hello nella tabella seguente mostra le origini dati hello che vengono rese persistenti e il relativo formato.</span><span class="sxs-lookup"><span data-stu-id="4350e-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="4350e-113">Origine dati</span><span class="sxs-lookup"><span data-stu-id="4350e-113">Data source</span></span> | <span data-ttu-id="4350e-114">Formato di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4350e-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="4350e-115">Log di Azure</span><span class="sxs-lookup"><span data-stu-id="4350e-115">Azure logs</span></span> |<span data-ttu-id="4350e-116">Tabella</span><span class="sxs-lookup"><span data-stu-id="4350e-116">Table</span></span> |
| <span data-ttu-id="4350e-117">Log di IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="4350e-117">IIS 7.0 logs</span></span> |<span data-ttu-id="4350e-118">BLOB</span><span class="sxs-lookup"><span data-stu-id="4350e-118">Blob</span></span> |
| <span data-ttu-id="4350e-119">Log dell'infrastruttura Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="4350e-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="4350e-120">Tabella</span><span class="sxs-lookup"><span data-stu-id="4350e-120">Table</span></span> |
| <span data-ttu-id="4350e-121">Log di analisi delle richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="4350e-121">Failed Request Trace logs</span></span> |<span data-ttu-id="4350e-122">BLOB</span><span class="sxs-lookup"><span data-stu-id="4350e-122">Blob</span></span> |
| <span data-ttu-id="4350e-123">Registri eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="4350e-123">Windows Event logs</span></span> |<span data-ttu-id="4350e-124">Tabella</span><span class="sxs-lookup"><span data-stu-id="4350e-124">Table</span></span> |
| <span data-ttu-id="4350e-125">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="4350e-125">Performance counters</span></span> |<span data-ttu-id="4350e-126">Tabella</span><span class="sxs-lookup"><span data-stu-id="4350e-126">Table</span></span> |
| <span data-ttu-id="4350e-127">Dump di arresto anomalo del sistema</span><span class="sxs-lookup"><span data-stu-id="4350e-127">Crash dumps</span></span> |<span data-ttu-id="4350e-128">BLOB</span><span class="sxs-lookup"><span data-stu-id="4350e-128">Blob</span></span> |
| <span data-ttu-id="4350e-129">Log degli errori personalizzati</span><span class="sxs-lookup"><span data-stu-id="4350e-129">Custom error logs</span></span> |<span data-ttu-id="4350e-130">BLOB</span><span class="sxs-lookup"><span data-stu-id="4350e-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="4350e-131">Trasferire i dati di diagnostica</span><span class="sxs-lookup"><span data-stu-id="4350e-131">Transfer diagnostic data</span></span>
<span data-ttu-id="4350e-132">Per SDK 2.5 e versioni successive, dati di diagnostica di hello richiesta tootransfer possono verificarsi tramite file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="4350e-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="4350e-133">È possibile trasferire dati di diagnostica a intervalli pianificati, come specificato nella configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4350e-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="4350e-134">Per SDK 2.4 e precedente è possibile richiedere dati di diagnostica hello tootransfer tramite file di configurazione hello anche a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="4350e-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="4350e-135">approccio a livello di codice Hello consente trasferimenti su richiesta toodo.</span><span class="sxs-lookup"><span data-stu-id="4350e-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4350e-136">Quando si trasferiscono dati di diagnostica tooan account di archiviazione di Azure, si devono sostenere i costi per le risorse di archiviazione hello che utilizza i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="4350e-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="4350e-137">Archiviare i dati di diagnostica</span><span class="sxs-lookup"><span data-stu-id="4350e-137">Store diagnostic data</span></span>
<span data-ttu-id="4350e-138">Dati di log vengono archiviati nell'archiviazione Blob o tabella con hello seguenti nomi:</span><span class="sxs-lookup"><span data-stu-id="4350e-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="4350e-139">**Tabelle**</span><span class="sxs-lookup"><span data-stu-id="4350e-139">**Tables**</span></span>

* <span data-ttu-id="4350e-140">**WadLogsTable** - log scritto in codice utilizzando il listener di traccia hello.</span><span class="sxs-lookup"><span data-stu-id="4350e-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="4350e-141">**WADDiagnosticInfrastructureLogsTable** : monitor di diagnostica e modifiche di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4350e-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="4350e-142">**WADDirectoriesTable** : directory esegue il monitoraggio di tale monitor di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="4350e-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="4350e-143">Sono inclusi i log di IIS, i log delle richieste non riuscite di IIS e le directory personalizzate.</span><span class="sxs-lookup"><span data-stu-id="4350e-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="4350e-144">percorso Hello hello blob del file di log viene specificato nel campo Container hello e nome hello del blob hello nel campo RelativePath hello.</span><span class="sxs-lookup"><span data-stu-id="4350e-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="4350e-145">campo AbsolutePath Hello indica hello percorso e il nome del file hello esistente nella macchina virtuale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4350e-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="4350e-146">**WADPerformanceCountersTable** : contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="4350e-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="4350e-147">**WADWindowsEventLogsTable** : registri eventi di Windows.</span><span class="sxs-lookup"><span data-stu-id="4350e-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="4350e-148">**BLOB**</span><span class="sxs-lookup"><span data-stu-id="4350e-148">**Blobs**</span></span>

* <span data-ttu-id="4350e-149">**wad-control-container** – (solo per SDK 2.4 e precedenti) contiene file di configurazione XML hello che controlla hello diagnostica Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="4350e-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="4350e-150">**wad-iis-failedreqlogfiles** : contiene informazioni provenienti dai log delle richieste non riuscite di IIS.</span><span class="sxs-lookup"><span data-stu-id="4350e-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="4350e-151">**wad-iis-logfiles** : contiene informazioni sui log di IIS.</span><span class="sxs-lookup"><span data-stu-id="4350e-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="4350e-152">**"custom"** : contenitore personalizzato basato sulle directory monitorate da Monitoraggio diagnostica hello di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4350e-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="4350e-153">nome Hello di questo contenitore blob verrà specificato in WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="4350e-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="4350e-154">Dati di diagnostica tooview degli strumenti</span><span class="sxs-lookup"><span data-stu-id="4350e-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="4350e-155">Sono inoltre numerosi strumenti dati hello tooview disponibile dopo essere stato trasferito toostorage.</span><span class="sxs-lookup"><span data-stu-id="4350e-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="4350e-156">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4350e-156">For example:</span></span>

* <span data-ttu-id="4350e-157">Esplora server in Visual Studio - se è stato installato hello Azure Tools per Microsoft Visual Studio, è possibile utilizzare il nodo di archiviazione di Azure hello in Esplora Server tooview-blob e tabelle dati di sola lettura dagli account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4350e-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="4350e-158">È possibile visualizzare i dati dall'account dell'emulatore di archiviazione locale e anche dagli account di archiviazione creati per Azure.</span><span class="sxs-lookup"><span data-stu-id="4350e-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="4350e-159">Per altre informazioni, vedere [Esplorazione e gestione delle risorse di archiviazione con Esplora server](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="4350e-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="4350e-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'applicazione autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, OSX e Linux.</span><span class="sxs-lookup"><span data-stu-id="4350e-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="4350e-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) include Azure Diagnostics Manager che consente di tooview, scaricare e gestire dati di diagnostica hello raccolti dalle applicazioni hello in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="4350e-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4350e-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4350e-162">Next Steps</span></span>
[<span data-ttu-id="4350e-163">Tracciare il flusso di hello in un'applicazione di servizi Cloud con diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="4350e-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

