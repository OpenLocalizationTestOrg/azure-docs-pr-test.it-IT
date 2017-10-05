---
title: Abilitazione delle metriche di archiviazione nel Portale di Azure | Microsoft Docs
description: Come abilitare le metriche di archiviazione per i servizi BLOB, di accodamento, di tabelle e file
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: 2906f808482d0b990e3ddd31ef5368e9fdd9f646
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="1c495-103">Abilitazione di Metriche di archiviazione di Azure e visualizzazione dei dati delle metriche</span><span class="sxs-lookup"><span data-stu-id="1c495-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="1c495-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1c495-104">Overview</span></span>
<span data-ttu-id="1c495-105">Le metriche di archiviazione vengono abilitate per impostazione predefinita quando si crea un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="1c495-106">È possibile configurare il monitoraggio tramite il [portale di Azure](https://portal.azure.com) o Windows PowerShell o a livello di codice con una delle librerie del client di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-106">You can configure monitoring via the [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of the storage client libraries.</span></span>

<span data-ttu-id="1c495-107">È possibile configurare un periodo di memorizzazione per i dati delle metriche: questo periodo determina per quanto tempo il servizio di archiviazione mantiene le metriche e addebita all'utente lo spazio necessario per archiviarle.</span><span class="sxs-lookup"><span data-stu-id="1c495-107">You can configure a retention period for the metrics data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="1c495-108">In genere, è consigliabile usare un periodo di memorizzazione per le metriche al minuto più breve che per le metriche orarie, a causa dello spazio supplementare significativo necessario per le metriche al minuto.</span><span class="sxs-lookup"><span data-stu-id="1c495-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="1c495-109">È consigliabile scegliere un periodo di memorizzazione tale da avere tempo sufficiente per analizzare i dati e scaricare le metriche da mantenere per l'analisi non in linea o la creazione di report.</span><span class="sxs-lookup"><span data-stu-id="1c495-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="1c495-110">Tenere presente che verrà addebitato anche il download dei dati di metrica dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-metrics-using-the-azure-portal"></a><span data-ttu-id="1c495-111">Come abilitare le metriche usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1c495-111">How to enable metrics using the Azure portal</span></span>
<span data-ttu-id="1c495-112">Seguire questi passaggi per abilitare le metriche nel [portale di Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="1c495-112">Follow these steps to enable metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="1c495-113">Passare all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-113">Navigate to your storage account.</span></span>
1. <span data-ttu-id="1c495-114">Selezionare **Diagnostica** nel pannello **Menu**</span><span class="sxs-lookup"><span data-stu-id="1c495-114">Select **Diagnostics** on the **Menu** blade</span></span>
1. <span data-ttu-id="1c495-115">Assicurarsi che **Stato** sia impostato su **On**.</span><span class="sxs-lookup"><span data-stu-id="1c495-115">Ensure that **Status** is set to **On**.</span></span>
1. <span data-ttu-id="1c495-116">Selezionare le metriche per i servizi che si desidera monitorare.</span><span class="sxs-lookup"><span data-stu-id="1c495-116">Select the metrics for the services you wish to monitor.</span></span>
1. <span data-ttu-id="1c495-117">Specificare un criterio di conservazione per indicare per quanto tempo conservare le metriche e dati di log.</span><span class="sxs-lookup"><span data-stu-id="1c495-117">Specify a retention policy to indicate how long to retain metrics and log data.</span></span>
1. <span data-ttu-id="1c495-118">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1c495-118">Select **Save**.</span></span>

<span data-ttu-id="1c495-119">Il [portale di Azure](https://portal.azure.com) non consente attualmente di configurare le metriche al minuto nell'account di archiviazione; è necessario abilitare le metriche al minuto usando PowerShell o a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="1c495-119">Note that the [Azure portal](https://portal.azure.com) does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-metrics-using-powershell"></a><span data-ttu-id="1c495-120">Come abilitare le metriche usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c495-120">How to enable metrics using PowerShell</span></span>
<span data-ttu-id="1c495-121">È possibile usare PowerShell nel computer locale per configurare Metriche di archiviazione nell'account di archiviazione usando il cmdlet di Azure PowerShell Get-AzureStorageServiceMetricsProperty per recuperare le impostazioni correnti e il cmdlet Set-AzureStorageServiceMetricsProperty per modificare le impostazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="1c495-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="1c495-122">I cmdlet che controllano Metriche di archiviazione usano i seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="1c495-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="1c495-123">I valori possibili di MetricsType sono Hour e Minute.</span><span class="sxs-lookup"><span data-stu-id="1c495-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="1c495-124">I valori possibili di ServiceType sono Blob, Queue e Table.</span><span class="sxs-lookup"><span data-stu-id="1c495-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="1c495-125">I valori possibili di MetricsLevel sono None, Service e ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="1c495-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="1c495-126">Ad esempio, il seguente comando attiva le metriche al minuto per il servizio BLOB nell'account di archiviazione predefinito con il periodo di memorizzazione impostato su cinque giorni:</span><span class="sxs-lookup"><span data-stu-id="1c495-126">For example, the following command switches on minute metrics for the Blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="1c495-127">Il seguente comando recupera il livello delle metriche orarie corrente e i giorni di memorizzazione per il servizio BLOB nell'account di archiviazione predefinito:</span><span class="sxs-lookup"><span data-stu-id="1c495-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="1c495-128">Per informazioni su come configurare i cmdlet di Azure PowerShell per usare la sottoscrizione di Azure e su come selezionare l'account di archiviazione predefinito da utilizzare, vedere: [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1c495-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="1c495-129">Come abilitare Metriche di archiviazione a livello di codice</span><span class="sxs-lookup"><span data-stu-id="1c495-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="1c495-130">Il frammento C# seguente illustra come abilitare le metriche e la registrazione per il servizio BLOB con la libreria del client di archiviazione per .NET:</span><span class="sxs-lookup"><span data-stu-id="1c495-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="1c495-131">Visualizzazione di Metriche di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1c495-131">Viewing Storage metrics</span></span>
<span data-ttu-id="1c495-132">Una volta configurate le metriche dell’analisi di archiviazione per monitorare l'account di archiviazione, l’analisi di archiviazione registra le metriche in un set di tabelle note nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-132">After you configure Storage Analytics metrics to monitor your storage account, Storage Analytics records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="1c495-133">È possibile configurare i grafici per visualizzare le metriche orarie nel [portale di Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="1c495-133">You can configure charts to view hourly metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="1c495-134">Passare all'account di archiviazione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c495-134">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="1c495-135">Selezionare **Metriche** nel pannello **Menu** per il servizio di cui visualizzare le metriche.</span><span class="sxs-lookup"><span data-stu-id="1c495-135">Select **Metrics** in the **Menu** blade for the service whose metrics you want to view.</span></span>
1. <span data-ttu-id="1c495-136">Selezionare **Modifica** del grafico che si vuole configurare.</span><span class="sxs-lookup"><span data-stu-id="1c495-136">Select **Edit** on the chart you want to configure.</span></span>
1. <span data-ttu-id="1c495-137">Nel pannello **Modifica grafico** selezionare l'**intervallo di tempo**, il **tipo di grafico** e le metriche da visualizzare nel grafico.</span><span class="sxs-lookup"><span data-stu-id="1c495-137">In the **Edit Chart** blade, select the **Time Range**, **Chart type**, and the metrics you want displayed in the chart.</span></span>
1. <span data-ttu-id="1c495-138">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c495-138">Select **OK**</span></span>

<span data-ttu-id="1c495-139">Se si vogliono scaricare le metriche per l'archiviazione a lungo termine o per analizzare le metriche in locale, è necessario:</span><span class="sxs-lookup"><span data-stu-id="1c495-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to:</span></span>

* <span data-ttu-id="1c495-140">Usare uno strumento che riconosca queste tabelle e consenta di visualizzarle e scaricarle.</span><span class="sxs-lookup"><span data-stu-id="1c495-140">Use a tool that is aware of these tables and will allow you to view and download them.</span></span>
* <span data-ttu-id="1c495-141">Scrivere un'applicazione personalizzata o script per leggere e archiviare le tabelle.</span><span class="sxs-lookup"><span data-stu-id="1c495-141">Write a custom application or script to read and store the tables.</span></span>

<span data-ttu-id="1c495-142">Molti strumenti di esplorazione dell'archivio di terze parti sono compatibili con queste tabelle e consentono di visualizzarle direttamente.</span><span class="sxs-lookup"><span data-stu-id="1c495-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly.</span></span>
<span data-ttu-id="1c495-143">Vedere [Strumento client di Archiviazione di Azure](storage-explorers.md) per un elenco di strumenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="1c495-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="1c495-144">A partire dalla versione 0.8.0 di [Microsoft Azure Storage Explorer](http://storageexplorer.com/) (Esplora archivi di Microsoft Azure), è possibile visualizzare e scaricare le tabelle della metrica di analisi.</span><span class="sxs-lookup"><span data-stu-id="1c495-144">Starting with version 0.8.0 of the [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download the analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="1c495-145">Per accedere alle tabelle di analisi a livello di codice, si noti che non vengono visualizzate se si elencano tutte le tabelle presenti nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-145">In order to access the analytics tables programmatically, do note that the analytics tables do not appear if you list all the tables in your storage account.</span></span> <span data-ttu-id="1c495-146">È possibile accedervi direttamente con il nome o usare l' [APICloudAnalyticsClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) nella libreria client .NET per eseguire query sui nomi delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="1c495-146">You can either access them directly by name, or use the [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in the .NET client library to query the table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="1c495-147">Metriche orarie</span><span class="sxs-lookup"><span data-stu-id="1c495-147">Hourly metrics</span></span>
* <span data-ttu-id="1c495-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="1c495-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="1c495-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="1c495-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="1c495-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="1c495-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="1c495-151">Metriche al minuto</span><span class="sxs-lookup"><span data-stu-id="1c495-151">Minute metrics</span></span>
* <span data-ttu-id="1c495-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="1c495-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="1c495-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="1c495-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="1c495-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="1c495-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="1c495-155">Capacità</span><span class="sxs-lookup"><span data-stu-id="1c495-155">Capacity</span></span>
* <span data-ttu-id="1c495-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="1c495-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="1c495-157">È possibile trovare i dettagli completi degli schemi di queste tabelle in [Schema di tabella della metrica di Analisi di archiviazione](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c495-157">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="1c495-158">Le righe di esempio riportate di seguito mostrano solo un subset delle colonne disponibili, ma illustrano alcune importanti funzionalità relative al modo in cui Metriche di archiviazione salva queste metriche:</span><span class="sxs-lookup"><span data-stu-id="1c495-158">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="1c495-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="1c495-159">PartitionKey</span></span> | <span data-ttu-id="1c495-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="1c495-160">RowKey</span></span> | <span data-ttu-id="1c495-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="1c495-161">Timestamp</span></span> | <span data-ttu-id="1c495-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="1c495-162">TotalRequests</span></span> | <span data-ttu-id="1c495-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="1c495-163">TotalBillableRequests</span></span> | <span data-ttu-id="1c495-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="1c495-164">TotalIngress</span></span> | <span data-ttu-id="1c495-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="1c495-165">TotalEgress</span></span> | <span data-ttu-id="1c495-166">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="1c495-166">Availability</span></span> | <span data-ttu-id="1c495-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="1c495-167">AverageE2ELatency</span></span> | <span data-ttu-id="1c495-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="1c495-168">AverageServerLatency</span></span> | <span data-ttu-id="1c495-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="1c495-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1c495-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="1c495-170">20140522T1100</span></span> |<span data-ttu-id="1c495-171">user;All</span><span class="sxs-lookup"><span data-stu-id="1c495-171">user;All</span></span> |<span data-ttu-id="1c495-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="1c495-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="1c495-173">7</span><span class="sxs-lookup"><span data-stu-id="1c495-173">7</span></span> |<span data-ttu-id="1c495-174">7</span><span class="sxs-lookup"><span data-stu-id="1c495-174">7</span></span> |<span data-ttu-id="1c495-175">4003</span><span class="sxs-lookup"><span data-stu-id="1c495-175">4003</span></span> |<span data-ttu-id="1c495-176">46801</span><span class="sxs-lookup"><span data-stu-id="1c495-176">46801</span></span> |<span data-ttu-id="1c495-177">100</span><span class="sxs-lookup"><span data-stu-id="1c495-177">100</span></span> |<span data-ttu-id="1c495-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="1c495-178">104.4286</span></span> |<span data-ttu-id="1c495-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="1c495-179">6.857143</span></span> |<span data-ttu-id="1c495-180">100</span><span class="sxs-lookup"><span data-stu-id="1c495-180">100</span></span> |
| <span data-ttu-id="1c495-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="1c495-181">20140522T1100</span></span> |<span data-ttu-id="1c495-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="1c495-182">user;QueryEntities</span></span> |<span data-ttu-id="1c495-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="1c495-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="1c495-184">5</span><span class="sxs-lookup"><span data-stu-id="1c495-184">5</span></span> |<span data-ttu-id="1c495-185">5</span><span class="sxs-lookup"><span data-stu-id="1c495-185">5</span></span> |<span data-ttu-id="1c495-186">2694</span><span class="sxs-lookup"><span data-stu-id="1c495-186">2694</span></span> |<span data-ttu-id="1c495-187">45951</span><span class="sxs-lookup"><span data-stu-id="1c495-187">45951</span></span> |<span data-ttu-id="1c495-188">100</span><span class="sxs-lookup"><span data-stu-id="1c495-188">100</span></span> |<span data-ttu-id="1c495-189">143.8</span><span class="sxs-lookup"><span data-stu-id="1c495-189">143.8</span></span> |<span data-ttu-id="1c495-190">7.8</span><span class="sxs-lookup"><span data-stu-id="1c495-190">7.8</span></span> |<span data-ttu-id="1c495-191">100</span><span class="sxs-lookup"><span data-stu-id="1c495-191">100</span></span> |
| <span data-ttu-id="1c495-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="1c495-192">20140522T1100</span></span> |<span data-ttu-id="1c495-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="1c495-193">user;QueryEntity</span></span> |<span data-ttu-id="1c495-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="1c495-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="1c495-195">1</span><span class="sxs-lookup"><span data-stu-id="1c495-195">1</span></span> |<span data-ttu-id="1c495-196">1</span><span class="sxs-lookup"><span data-stu-id="1c495-196">1</span></span> |<span data-ttu-id="1c495-197">538</span><span class="sxs-lookup"><span data-stu-id="1c495-197">538</span></span> |<span data-ttu-id="1c495-198">633</span><span class="sxs-lookup"><span data-stu-id="1c495-198">633</span></span> |<span data-ttu-id="1c495-199">100</span><span class="sxs-lookup"><span data-stu-id="1c495-199">100</span></span> |<span data-ttu-id="1c495-200">3</span><span class="sxs-lookup"><span data-stu-id="1c495-200">3</span></span> |<span data-ttu-id="1c495-201">3</span><span class="sxs-lookup"><span data-stu-id="1c495-201">3</span></span> |<span data-ttu-id="1c495-202">100</span><span class="sxs-lookup"><span data-stu-id="1c495-202">100</span></span> |
| <span data-ttu-id="1c495-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="1c495-203">20140522T1100</span></span> |<span data-ttu-id="1c495-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="1c495-204">user;UpdateEntity</span></span> |<span data-ttu-id="1c495-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="1c495-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="1c495-206">1</span><span class="sxs-lookup"><span data-stu-id="1c495-206">1</span></span> |<span data-ttu-id="1c495-207">1</span><span class="sxs-lookup"><span data-stu-id="1c495-207">1</span></span> |<span data-ttu-id="1c495-208">771</span><span class="sxs-lookup"><span data-stu-id="1c495-208">771</span></span> |<span data-ttu-id="1c495-209">217</span><span class="sxs-lookup"><span data-stu-id="1c495-209">217</span></span> |<span data-ttu-id="1c495-210">100</span><span class="sxs-lookup"><span data-stu-id="1c495-210">100</span></span> |<span data-ttu-id="1c495-211">9</span><span class="sxs-lookup"><span data-stu-id="1c495-211">9</span></span> |<span data-ttu-id="1c495-212">6</span><span class="sxs-lookup"><span data-stu-id="1c495-212">6</span></span> |<span data-ttu-id="1c495-213">100</span><span class="sxs-lookup"><span data-stu-id="1c495-213">100</span></span> |

<span data-ttu-id="1c495-214">Nei dati delle metriche al minuto di questo esempio, la chiave di partizione usa la risoluzione ora al minuto.</span><span class="sxs-lookup"><span data-stu-id="1c495-214">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="1c495-215">La chiave di riga identifica il tipo di informazioni archiviate nella riga ed è composta da due informazioni, il tipo di accesso e il tipo di richiesta:</span><span class="sxs-lookup"><span data-stu-id="1c495-215">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="1c495-216">Il tipo di accesso è user o system, laddove user si riferisce a tutte le richieste utente al servizio di archiviazione e system si riferisce alle richieste effettuate da Analisi archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-216">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="1c495-217">Il tipo di richiesta può essere all, e in questo caso si tratta di una riga di riepilogo, o identificare l'API specifica, ad esempio QueryEntity o UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="1c495-217">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="1c495-218">I dati di esempio sopra riportati mostrano tutti i record per un solo minuto (a partire dalle 11.00). La somma del numero di richieste QueryEntities, del numero di richieste QueryEntity e del numero di richieste UpdateEntity è sette, che corrisponde al totale visualizzato nella riga user:All.</span><span class="sxs-lookup"><span data-stu-id="1c495-218">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="1c495-219">Analogamente, è possibile ricavare la latenza end-to-end media 104,4286 nella riga user:All calcolando ((143,8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="1c495-219">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="1c495-220">Avvisi delle metriche</span><span class="sxs-lookup"><span data-stu-id="1c495-220">Metrics alerts</span></span>
<span data-ttu-id="1c495-221">È consigliabile impostare gli avvisi nel [portale di Azure](https://portal.azure.com) in modo che le metriche di archiviazione possano notificare automaticamente eventuali importanti modifiche nel comportamento dei servizi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-221">You should consider setting up alerts in the [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in the behavior of your storage services.</span></span> <span data-ttu-id="1c495-222">Se si usa uno strumento di esplorazione di archiviazione per scaricare i dati di metrica in un formato delimitato, è possibile usare Microsoft Excel per analizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="1c495-222">If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="1c495-223">Vedere [Strumento client di Archiviazione di Azure](storage-explorers.md) per un elenco di strumenti di esplorazione di archiviazione disponibili.</span><span class="sxs-lookup"><span data-stu-id="1c495-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="1c495-224">È possibile configurare gli avvisi nel pannello **Regole di avviso**, accessibile da **Monitoraggio** nel pannello dei menu dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-224">You can configure alerts in the **Alert rules** blade, accessible under **Monitoring** in the Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c495-225">Potrebbe verificarsi un ritardo tra un evento di archiviazione e la memorizzazione dei relativi dati di metrica oraria o al minuto.</span><span class="sxs-lookup"><span data-stu-id="1c495-225">There may be a delay between a storage event and when the corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="1c495-226">In caso di metriche al minuto, è possibile che vengano scritti contemporaneamente diversi dati.</span><span class="sxs-lookup"><span data-stu-id="1c495-226">In the case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="1c495-227">Ciò può comportare l'aggregazione di transazioni dai minuti precedenti nella transazione per il minuto corrente.</span><span class="sxs-lookup"><span data-stu-id="1c495-227">This can lead to transactions from earlier minutes being aggregated into the transaction for the current minute.</span></span> <span data-ttu-id="1c495-228">In questo caso il servizio avvisi potrebbe non avere tutti i dati di metrica a disposizione per l'intervallo di avviso configurato, il che potrebbe determinare l'attivazione imprevista degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="1c495-228">When this happens, the alert service may not have all available metrics data for the configured alert interval, which may lead to alerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="1c495-229">Accesso ai dati di metrica a livello di codice</span><span class="sxs-lookup"><span data-stu-id="1c495-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="1c495-230">Nell'elenco riportato di seguito viene illustrato il codice C# che consente l'accesso alle metriche al minuto per un intervallo di minuti. Vengono inoltre visualizzati i risultati in una finestra della console.</span><span class="sxs-lookup"><span data-stu-id="1c495-230">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="1c495-231">Viene utilizzata la libreria di archiviazione di Azure versione 4 che include la classe CloudAnalyticsClient, in grado di semplificare l'accesso alle tabelle di metrica nell'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-231">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="1c495-232">Quali addebiti è necessario sostenere quando si abilitano le metriche di archiviazione?</span><span class="sxs-lookup"><span data-stu-id="1c495-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="1c495-233">Le richieste di scrittura per creare entità di tabella per le metriche vengono addebitate alle tariffe standard applicabili a tutte le operazioni di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c495-233">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="1c495-234">Anche le richieste di lettura ed eliminazione da parte di un client relative ai dati di metrica sono fatturabili alle tariffe standard.</span><span class="sxs-lookup"><span data-stu-id="1c495-234">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="1c495-235">Se è stato configurato un criterio di memorizzazione dati, non è necessario sostenere alcun addebito quando Archiviazione di Azure elimina i vecchi dati di metrica.</span><span class="sxs-lookup"><span data-stu-id="1c495-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="1c495-236">Tuttavia, se si eliminano dati di analisi, all'account vengono addebitate le operazioni di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="1c495-236">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="1c495-237">Anche la capacità usata dalle tabelle di metrica è fatturabile: è possibile usare le seguenti informazioni per calcolare la quantità di capacità usata per l'archiviazione dei dati di metrica:</span><span class="sxs-lookup"><span data-stu-id="1c495-237">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="1c495-238">Se ogni ora un servizio utilizza tutte le API presenti in ciascun servizio, ogni ora circa 148 KB di dati vengono archiviati nelle tabelle delle transazioni metriche, se è stato abilitato il riepilogo a livello di servizio e di API.</span><span class="sxs-lookup"><span data-stu-id="1c495-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="1c495-239">Se ogni ora un servizio utilizza tutte le API presenti in ciascun servizio, ogni ora circa 12 KB di dati vengono archiviati nelle tabelle delle transazioni metriche, se è stato abilitato solo il riepilogo a livello di servizio.</span><span class="sxs-lookup"><span data-stu-id="1c495-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="1c495-240">La tabella di capacità per i BLOB contiene due righe aggiunte ogni giorno (se l'utente ha optato per i log): di conseguenza, ogni giorno la dimensione della tabella aumenta di circa 300 byte.</span><span class="sxs-lookup"><span data-stu-id="1c495-240">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c495-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c495-241">Next steps</span></span>
[<span data-ttu-id="1c495-242">Abilitazione di Registrazione archiviazione e accesso ai dati di log</span><span class="sxs-lookup"><span data-stu-id="1c495-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
