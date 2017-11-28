---
title: Archiviare e visualizzare dati di diagnostica in Archiviazione di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="074e0-103">Archiviare e visualizzare i dati di diagnostica nell'account di archiviazione Azure</span><span class="sxs-lookup"><span data-stu-id="074e0-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="074e0-104">I dati di diagnostica non vengono archiviati definitivamente a meno che non vengano trasferiti nell'Emulatore di archiviazione di Microsoft Azure o nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="074e0-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="074e0-105">Una volta trasferiti nella risorsa di archiviazione, sono disponibili diversi strumenti per visualizzarli.</span><span class="sxs-lookup"><span data-stu-id="074e0-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="074e0-106">Specificare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="074e0-106">Specify a storage account</span></span>
<span data-ttu-id="074e0-107">Specificare l'account di archiviazione da usare nel file ServiceConfiguration.cscfg.</span><span class="sxs-lookup"><span data-stu-id="074e0-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="074e0-108">Le informazioni account vengono definite come stringa di connessione in un'impostazione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="074e0-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="074e0-109">L'esempio seguente mostra la stringa di connessione predefinita creata per un nuovo progetto di servizio cloud in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="074e0-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="074e0-110">È possibile modificare questa stringa di connessione per poter specificare le informazioni per un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="074e0-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="074e0-111">A seconda del tipo di dati di diagnostica da raccogliere, Diagnostica di Azure usa il servizio BLOB o il servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="074e0-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="074e0-112">La tabella seguente mostra le origini dati persistenti e il relativo formato.</span><span class="sxs-lookup"><span data-stu-id="074e0-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="074e0-113">Origine dati</span><span class="sxs-lookup"><span data-stu-id="074e0-113">Data source</span></span> | <span data-ttu-id="074e0-114">Formato di archiviazione</span><span class="sxs-lookup"><span data-stu-id="074e0-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="074e0-115">Log di Azure</span><span class="sxs-lookup"><span data-stu-id="074e0-115">Azure logs</span></span> |<span data-ttu-id="074e0-116">Tabella</span><span class="sxs-lookup"><span data-stu-id="074e0-116">Table</span></span> |
| <span data-ttu-id="074e0-117">Log di IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="074e0-117">IIS 7.0 logs</span></span> |<span data-ttu-id="074e0-118">BLOB</span><span class="sxs-lookup"><span data-stu-id="074e0-118">Blob</span></span> |
| <span data-ttu-id="074e0-119">Log dell'infrastruttura Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="074e0-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="074e0-120">Tabella</span><span class="sxs-lookup"><span data-stu-id="074e0-120">Table</span></span> |
| <span data-ttu-id="074e0-121">Log di analisi delle richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="074e0-121">Failed Request Trace logs</span></span> |<span data-ttu-id="074e0-122">BLOB</span><span class="sxs-lookup"><span data-stu-id="074e0-122">Blob</span></span> |
| <span data-ttu-id="074e0-123">Registri eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="074e0-123">Windows Event logs</span></span> |<span data-ttu-id="074e0-124">Tabella</span><span class="sxs-lookup"><span data-stu-id="074e0-124">Table</span></span> |
| <span data-ttu-id="074e0-125">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="074e0-125">Performance counters</span></span> |<span data-ttu-id="074e0-126">Tabella</span><span class="sxs-lookup"><span data-stu-id="074e0-126">Table</span></span> |
| <span data-ttu-id="074e0-127">Dump di arresto anomalo del sistema</span><span class="sxs-lookup"><span data-stu-id="074e0-127">Crash dumps</span></span> |<span data-ttu-id="074e0-128">BLOB</span><span class="sxs-lookup"><span data-stu-id="074e0-128">Blob</span></span> |
| <span data-ttu-id="074e0-129">Log degli errori personalizzati</span><span class="sxs-lookup"><span data-stu-id="074e0-129">Custom error logs</span></span> |<span data-ttu-id="074e0-130">BLOB</span><span class="sxs-lookup"><span data-stu-id="074e0-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="074e0-131">Trasferire i dati di diagnostica</span><span class="sxs-lookup"><span data-stu-id="074e0-131">Transfer diagnostic data</span></span>
<span data-ttu-id="074e0-132">Per SDK 2.5 e versioni successive, la richiesta di trasferimento dei dati di diagnostica può verificarsi nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="074e0-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="074e0-133">È possibile trasferire i dati di diagnostica a intervalli pianificati, come specificato nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="074e0-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="074e0-134">Per SDK 2.4 e versioni precedenti, è possibile richiedere di trasferire i dati di diagnostica nel file di configurazione oltre che a livello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="074e0-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="074e0-135">L'approccio programmatico consente anche di eseguire trasferimenti su richiesta.</span><span class="sxs-lookup"><span data-stu-id="074e0-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="074e0-136">Quando si trasferiscono i dati di diagnostica in un account di archiviazione di Azure, si devono sostenere i costi per le risorse di archiviazione usate dai dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="074e0-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="074e0-137">Archiviare i dati di diagnostica</span><span class="sxs-lookup"><span data-stu-id="074e0-137">Store diagnostic data</span></span>
<span data-ttu-id="074e0-138">I dati dei log vengono archiviati nell'archivio BLOB o tabelle con i nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="074e0-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="074e0-139">**Tabelle**</span><span class="sxs-lookup"><span data-stu-id="074e0-139">**Tables**</span></span>

* <span data-ttu-id="074e0-140">**WadLogsTable** : log scritti nel codice con il listener di traccia.</span><span class="sxs-lookup"><span data-stu-id="074e0-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="074e0-141">**WADDiagnosticInfrastructureLogsTable** : monitor di diagnostica e modifiche di configurazione.</span><span class="sxs-lookup"><span data-stu-id="074e0-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="074e0-142">**WADDirectoriesTable** : directory monitorate dal monitor di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="074e0-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="074e0-143">Sono inclusi i log di IIS, i log delle richieste non riuscite di IIS e le directory personalizzate.</span><span class="sxs-lookup"><span data-stu-id="074e0-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="074e0-144">La posizione del file di log dei BLOB è specificata nel campo Container e il nome del BLOB si trova nel campo RelativePath.</span><span class="sxs-lookup"><span data-stu-id="074e0-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="074e0-145">Il campo AbsolutePath indica la posizione e il nome del file esistente nella macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="074e0-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="074e0-146">**WADPerformanceCountersTable** : contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="074e0-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="074e0-147">**WADWindowsEventLogsTable** : registri eventi di Windows.</span><span class="sxs-lookup"><span data-stu-id="074e0-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="074e0-148">**BLOB**</span><span class="sxs-lookup"><span data-stu-id="074e0-148">**Blobs**</span></span>

* <span data-ttu-id="074e0-149">**wad-control-container** : (solo per SDK 2.4 e versioni precedenti) contiene i file di configurazione XML che controllano Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="074e0-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="074e0-150">**wad-iis-failedreqlogfiles** : contiene informazioni provenienti dai log delle richieste non riuscite di IIS.</span><span class="sxs-lookup"><span data-stu-id="074e0-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="074e0-151">**wad-iis-logfiles** : contiene informazioni sui log di IIS.</span><span class="sxs-lookup"><span data-stu-id="074e0-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="074e0-152">**"custom"** : contenitore personalizzato basato sulle directory di configurazione monitorate dal monitor di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="074e0-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="074e0-153">Il nome di questo contenitore BLOB verrà specificato in WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="074e0-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="074e0-154">Strumenti per visualizzare i dati di diagnostica</span><span class="sxs-lookup"><span data-stu-id="074e0-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="074e0-155">Sono disponibili diversi strumenti per visualizzare i dati una volta trasferiti nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="074e0-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="074e0-156">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="074e0-156">For example:</span></span>

* <span data-ttu-id="074e0-157">Esplora server in Visual Studio: se sono stati installati gli Strumenti di Azure per Microsoft Visual Studio, è possibile usare il nodo Archiviazione di Azure in Esplora server per visualizzare i dati di tabelle e BLOB di sola lettura dagli account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="074e0-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="074e0-158">È possibile visualizzare i dati dall'account dell'emulatore di archiviazione locale e anche dagli account di archiviazione creati per Azure.</span><span class="sxs-lookup"><span data-stu-id="074e0-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="074e0-159">Per altre informazioni, vedere [Esplorazione e gestione delle risorse di archiviazione con Esplora server](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="074e0-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="074e0-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma che consente di usare facilmente dati di Archiviazione di Azure in Windows, OSX e Linux.</span><span class="sxs-lookup"><span data-stu-id="074e0-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="074e0-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) include Azure Diagnostics Manager che consente di visualizzare, scaricare e gestire i dati di diagnostica raccolti dalle applicazioni in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="074e0-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="074e0-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="074e0-162">Next Steps</span></span>
[<span data-ttu-id="074e0-163">Tracciare il flusso in un'applicazione di Servizi cloud con Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="074e0-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

