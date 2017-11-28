---
title: aaaEnabling metriche di archiviazione nel portale di Azure hello | Documenti Microsoft
description: Come tooenable metriche di archiviazione per hello servizi Blob, coda, tabella e File
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
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="07c16-103">Abilitazione di Metriche di archiviazione di Azure e visualizzazione dei dati delle metriche</span><span class="sxs-lookup"><span data-stu-id="07c16-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="07c16-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="07c16-104">Overview</span></span>
<span data-ttu-id="07c16-105">Le metriche di archiviazione vengono abilitate per impostazione predefinita quando si crea un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="07c16-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="07c16-106">È possibile configurare il monitoraggio tramite hello [portale di Azure](https://portal.azure.com) o Windows PowerShell, o a livello di codice attraverso una delle librerie client di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="07c16-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="07c16-107">È possibile configurare un periodo di memorizzazione per i dati di metrica hello: questo periodo determina per quanto tempo archiviazione hello servizio mantiene le metriche hello e spese di hello spazio richiesto toostore li.</span><span class="sxs-lookup"><span data-stu-id="07c16-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="07c16-108">In genere, è consigliabile utilizzare un periodo di memorizzazione più breve per le metriche al minuto più metrica oraria a causa di hello significativo spazio richiesto per le metriche al minuto.</span><span class="sxs-lookup"><span data-stu-id="07c16-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="07c16-109">È consigliabile scegliere un periodo di memorizzazione in modo che si dispone di sufficiente tempo tooanalyze hello dati e download delle metriche che si desidera tookeep per l'analisi offline o creazione di report.</span><span class="sxs-lookup"><span data-stu-id="07c16-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="07c16-110">Tenere presente che verrà addebitato anche il download dei dati di metrica dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="07c16-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="07c16-111">Come metriche tooenable usando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="07c16-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="07c16-112">Seguire questi passaggi tooenable criteri di misurazione in hello [portale di Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="07c16-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="07c16-113">Passare tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="07c16-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="07c16-114">Selezionare **diagnostica** su hello **Menu** pannello</span><span class="sxs-lookup"><span data-stu-id="07c16-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="07c16-115">Verificare che **stato** è troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="07c16-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="07c16-116">Le metriche di hello selezionare per i servizi di hello desiderato toomonitor.</span><span class="sxs-lookup"><span data-stu-id="07c16-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="07c16-117">Specificare un tooindicate di criteri di conservazione dei dati di metrica e di log tooretain come long.</span><span class="sxs-lookup"><span data-stu-id="07c16-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="07c16-118">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="07c16-118">Select **Save**.</span></span>

<span data-ttu-id="07c16-119">Si noti che hello [portale di Azure](https://portal.azure.com) non attualmente consentono tooconfigure metrica al minuto nell'account di archiviazione; è necessario abilitare le metriche al minuto mediante PowerShell o a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="07c16-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="07c16-120">Come le metriche tooenable tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="07c16-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="07c16-121">È possibile usare PowerShell sulle metriche di archiviazione di tooconfigure computer locale nell'account di archiviazione usando le impostazioni correnti di hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello e hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello le impostazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="07c16-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="07c16-122">cmdlet di Hello che controllano metriche di archiviazione usano hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="07c16-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="07c16-123">I valori possibili di MetricsType sono Hour e Minute.</span><span class="sxs-lookup"><span data-stu-id="07c16-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="07c16-124">I valori possibili di ServiceType sono Blob, Queue e Table.</span><span class="sxs-lookup"><span data-stu-id="07c16-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="07c16-125">I valori possibili di MetricsLevel sono None, Service e ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="07c16-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="07c16-126">Ad esempio, hello seguente comando attiva le metriche per il servizio Blob hello nell'account di archiviazione predefinito con il periodo di memorizzazione hello impostare i giorni toofive minuto:</span><span class="sxs-lookup"><span data-stu-id="07c16-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="07c16-127">Hello seguente comando Recupera hello corrente oraria metriche livello e alla conservazione dei giorni per il servizio blob hello nell'account di archiviazione predefinito:</span><span class="sxs-lookup"><span data-stu-id="07c16-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="07c16-128">Per informazioni su come tooconfigure hello Azure PowerShell cmdlet toowork con la sottoscrizione di Azure e come tooselect hello spazio di archiviazione predefinito degli account toouse, vedere: [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07c16-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="07c16-129">Come tooenable metriche di archiviazione a livello di codice</span><span class="sxs-lookup"><span data-stu-id="07c16-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="07c16-130">Hello frammento di codice c# seguente viene illustrato come tooenable metrica e registrazione per il servizio Blob hello utilizzando hello libreria client di archiviazione per .NET:</span><span class="sxs-lookup"><span data-stu-id="07c16-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="07c16-131">Visualizzazione di Metriche di archiviazione</span><span class="sxs-lookup"><span data-stu-id="07c16-131">Viewing Storage metrics</span></span>
<span data-ttu-id="07c16-132">Dopo la configurazione dell'account di archiviazione, toomonitor metriche di archiviazione Analitica Analitica archiviazione registra le metriche hello in un set di tabelle note nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="07c16-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="07c16-133">È possibile configurare le metriche orarie tooview di grafici in hello [portale di Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="07c16-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="07c16-134">Passare l'account di archiviazione tooyour in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07c16-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="07c16-135">Selezionare **metriche** in hello **Menu** pannello hello del servizio il cui metriche desiderate tooview.</span><span class="sxs-lookup"><span data-stu-id="07c16-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="07c16-136">Selezionare **modifica** grafico hello desiderato tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="07c16-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="07c16-137">In hello **Modifica grafico** blade, seleziona hello **intervallo di tempo**, **tipo di grafico**e si desidera visualizzare nel grafico hello metriche di hello.</span><span class="sxs-lookup"><span data-stu-id="07c16-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="07c16-138">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="07c16-138">Select **OK**</span></span>

<span data-ttu-id="07c16-139">Se si desidera che le metriche hello toodownload per l'archiviazione a lungo termine o tooanalyze li in locale, è necessario:</span><span class="sxs-lookup"><span data-stu-id="07c16-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="07c16-140">Utilizzare uno strumento che è a conoscenza di queste tabelle e consentono di tooview e scaricarli.</span><span class="sxs-lookup"><span data-stu-id="07c16-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="07c16-141">Scrivere un tooread applicazione o script personalizzato e archiviare tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="07c16-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="07c16-142">Molti strumenti di esplorazione di archiviazione di terze parti sono a conoscenza di queste tabelle e consentono di tooview direttamente.</span><span class="sxs-lookup"><span data-stu-id="07c16-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="07c16-143">Vedere [Strumento client di Archiviazione di Azure](storage-explorers.md) per un elenco di strumenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="07c16-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="07c16-144">A partire dalla versione 0.8.0 di hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), è possibile visualizzare e scaricare le tabelle di metrica di hello analitica.</span><span class="sxs-lookup"><span data-stu-id="07c16-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="07c16-145">In analitica di hello tooaccess ordine tabelle a livello di codice, si noti che le tabelle analitica hello non vengono visualizzati se si elencano tutte le tabelle di hello nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="07c16-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="07c16-146">È possibile accedervi direttamente per nome o utilizzare hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) nei nomi di tabella di hello .NET client libreria tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="07c16-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="07c16-147">Metriche orarie</span><span class="sxs-lookup"><span data-stu-id="07c16-147">Hourly metrics</span></span>
* <span data-ttu-id="07c16-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="07c16-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="07c16-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="07c16-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="07c16-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="07c16-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="07c16-151">Metriche al minuto</span><span class="sxs-lookup"><span data-stu-id="07c16-151">Minute metrics</span></span>
* <span data-ttu-id="07c16-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="07c16-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="07c16-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="07c16-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="07c16-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="07c16-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="07c16-155">Capacità</span><span class="sxs-lookup"><span data-stu-id="07c16-155">Capacity</span></span>
* <span data-ttu-id="07c16-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="07c16-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="07c16-157">È possibile trovare i dettagli completi degli schemi di hello delle tabelle in [Schema di tabella delle metriche di archiviazione Analitica](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="07c16-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="07c16-158">le righe di esempio Hello riportato di seguito mostrano solo un subset di colonne hello disponibili, ma illustrano alcune importanti funzionalità della modalità di hello che metriche di archiviazione Salva le metriche:</span><span class="sxs-lookup"><span data-stu-id="07c16-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="07c16-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="07c16-159">PartitionKey</span></span> | <span data-ttu-id="07c16-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="07c16-160">RowKey</span></span> | <span data-ttu-id="07c16-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="07c16-161">Timestamp</span></span> | <span data-ttu-id="07c16-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="07c16-162">TotalRequests</span></span> | <span data-ttu-id="07c16-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="07c16-163">TotalBillableRequests</span></span> | <span data-ttu-id="07c16-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="07c16-164">TotalIngress</span></span> | <span data-ttu-id="07c16-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="07c16-165">TotalEgress</span></span> | <span data-ttu-id="07c16-166">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="07c16-166">Availability</span></span> | <span data-ttu-id="07c16-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="07c16-167">AverageE2ELatency</span></span> | <span data-ttu-id="07c16-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="07c16-168">AverageServerLatency</span></span> | <span data-ttu-id="07c16-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="07c16-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="07c16-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="07c16-170">20140522T1100</span></span> |<span data-ttu-id="07c16-171">user;All</span><span class="sxs-lookup"><span data-stu-id="07c16-171">user;All</span></span> |<span data-ttu-id="07c16-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="07c16-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="07c16-173">7</span><span class="sxs-lookup"><span data-stu-id="07c16-173">7</span></span> |<span data-ttu-id="07c16-174">7</span><span class="sxs-lookup"><span data-stu-id="07c16-174">7</span></span> |<span data-ttu-id="07c16-175">4003</span><span class="sxs-lookup"><span data-stu-id="07c16-175">4003</span></span> |<span data-ttu-id="07c16-176">46801</span><span class="sxs-lookup"><span data-stu-id="07c16-176">46801</span></span> |<span data-ttu-id="07c16-177">100</span><span class="sxs-lookup"><span data-stu-id="07c16-177">100</span></span> |<span data-ttu-id="07c16-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="07c16-178">104.4286</span></span> |<span data-ttu-id="07c16-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="07c16-179">6.857143</span></span> |<span data-ttu-id="07c16-180">100</span><span class="sxs-lookup"><span data-stu-id="07c16-180">100</span></span> |
| <span data-ttu-id="07c16-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="07c16-181">20140522T1100</span></span> |<span data-ttu-id="07c16-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="07c16-182">user;QueryEntities</span></span> |<span data-ttu-id="07c16-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="07c16-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="07c16-184">5</span><span class="sxs-lookup"><span data-stu-id="07c16-184">5</span></span> |<span data-ttu-id="07c16-185">5</span><span class="sxs-lookup"><span data-stu-id="07c16-185">5</span></span> |<span data-ttu-id="07c16-186">2694</span><span class="sxs-lookup"><span data-stu-id="07c16-186">2694</span></span> |<span data-ttu-id="07c16-187">45951</span><span class="sxs-lookup"><span data-stu-id="07c16-187">45951</span></span> |<span data-ttu-id="07c16-188">100</span><span class="sxs-lookup"><span data-stu-id="07c16-188">100</span></span> |<span data-ttu-id="07c16-189">143.8</span><span class="sxs-lookup"><span data-stu-id="07c16-189">143.8</span></span> |<span data-ttu-id="07c16-190">7.8</span><span class="sxs-lookup"><span data-stu-id="07c16-190">7.8</span></span> |<span data-ttu-id="07c16-191">100</span><span class="sxs-lookup"><span data-stu-id="07c16-191">100</span></span> |
| <span data-ttu-id="07c16-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="07c16-192">20140522T1100</span></span> |<span data-ttu-id="07c16-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="07c16-193">user;QueryEntity</span></span> |<span data-ttu-id="07c16-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="07c16-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="07c16-195">1</span><span class="sxs-lookup"><span data-stu-id="07c16-195">1</span></span> |<span data-ttu-id="07c16-196">1</span><span class="sxs-lookup"><span data-stu-id="07c16-196">1</span></span> |<span data-ttu-id="07c16-197">538</span><span class="sxs-lookup"><span data-stu-id="07c16-197">538</span></span> |<span data-ttu-id="07c16-198">633</span><span class="sxs-lookup"><span data-stu-id="07c16-198">633</span></span> |<span data-ttu-id="07c16-199">100</span><span class="sxs-lookup"><span data-stu-id="07c16-199">100</span></span> |<span data-ttu-id="07c16-200">3</span><span class="sxs-lookup"><span data-stu-id="07c16-200">3</span></span> |<span data-ttu-id="07c16-201">3</span><span class="sxs-lookup"><span data-stu-id="07c16-201">3</span></span> |<span data-ttu-id="07c16-202">100</span><span class="sxs-lookup"><span data-stu-id="07c16-202">100</span></span> |
| <span data-ttu-id="07c16-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="07c16-203">20140522T1100</span></span> |<span data-ttu-id="07c16-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="07c16-204">user;UpdateEntity</span></span> |<span data-ttu-id="07c16-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="07c16-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="07c16-206">1</span><span class="sxs-lookup"><span data-stu-id="07c16-206">1</span></span> |<span data-ttu-id="07c16-207">1</span><span class="sxs-lookup"><span data-stu-id="07c16-207">1</span></span> |<span data-ttu-id="07c16-208">771</span><span class="sxs-lookup"><span data-stu-id="07c16-208">771</span></span> |<span data-ttu-id="07c16-209">217</span><span class="sxs-lookup"><span data-stu-id="07c16-209">217</span></span> |<span data-ttu-id="07c16-210">100</span><span class="sxs-lookup"><span data-stu-id="07c16-210">100</span></span> |<span data-ttu-id="07c16-211">9</span><span class="sxs-lookup"><span data-stu-id="07c16-211">9</span></span> |<span data-ttu-id="07c16-212">6</span><span class="sxs-lookup"><span data-stu-id="07c16-212">6</span></span> |<span data-ttu-id="07c16-213">100</span><span class="sxs-lookup"><span data-stu-id="07c16-213">100</span></span> |

<span data-ttu-id="07c16-214">Nei dati di metrica al minuto in questo esempio, la chiave di partizione hello utilizza ora hello risoluzione minuti.</span><span class="sxs-lookup"><span data-stu-id="07c16-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="07c16-215">chiave di riga Hello identifica il tipo di hello di informazioni archiviate nella riga hello ed è composta da due tipi di informazioni, il tipo di accesso hello e il tipo di richiesta di hello:</span><span class="sxs-lookup"><span data-stu-id="07c16-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="07c16-216">il tipo di accesso di Hello è l'utente o sistema, in cui utente fa riferimento a servizio di archiviazione toohello richieste utente tooall e ci si riferisce toorequests effettuate da archiviazione Analitica.</span><span class="sxs-lookup"><span data-stu-id="07c16-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="07c16-217">tipo di richiesta Hello è tutte nel qual caso è una riga di riepilogo, oppure identifica hello API specifica, ad esempio QueryEntity o UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="07c16-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="07c16-218">dati di esempio Hello precedente che tutti hello Registra per un singolo minuto (a partire da 11:00 AM), in tal caso hello numerose richieste QueryEntities più hello numero di richieste QueryEntity più hello un numero di richieste UpdateEntity somma tooseven, che è hello totale mostrato in riga user: All Hello.</span><span class="sxs-lookup"><span data-stu-id="07c16-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="07c16-219">Analogamente, è possibile derivare hello end-to-end latenza media 104.4286 riga user: All hello calcolando ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="07c16-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="07c16-220">Avvisi delle metriche</span><span class="sxs-lookup"><span data-stu-id="07c16-220">Metrics alerts</span></span>
<span data-ttu-id="07c16-221">È consigliabile impostare degli avvisi nella hello [portale di Azure](https://portal.azure.com) in modo metriche di archiviazione di notificare automaticamente di importanti modifiche di comportamento hello dei servizi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="07c16-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="07c16-222">Se si utilizzano un toodownload strumento soluzioni di archiviazione dati di metrica in un formato delimitato, è possibile utilizzare dati di Microsoft Excel tooanalyze hello.</span><span class="sxs-lookup"><span data-stu-id="07c16-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="07c16-223">Vedere [Strumento client di Archiviazione di Azure](storage-explorers.md) per un elenco di strumenti di esplorazione di archiviazione disponibili.</span><span class="sxs-lookup"><span data-stu-id="07c16-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="07c16-224">È possibile configurare gli avvisi in hello **regole di avviso** accessibile nel pannello **monitoraggio** nel Pannello di hello Storage account dal menu.</span><span class="sxs-lookup"><span data-stu-id="07c16-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07c16-225">Potrebbe verificarsi un ritardo tra un evento di archiviazione e quando viene registrata in hello corrispondenti dati di metrica oraria o minuti.</span><span class="sxs-lookup"><span data-stu-id="07c16-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="07c16-226">In caso di hello della metrica al minuto, alcuni minuti di dati possono essere scritti in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="07c16-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="07c16-227">Ciò può comportare tootransactions dai minuti precedenti da aggregare in transazione hello per hello minuto corrente.</span><span class="sxs-lookup"><span data-stu-id="07c16-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="07c16-228">In questo caso, avviso hello servizio non disponga di tutti i dati di metriche disponibili per hello configurato un intervallo di avviso, con conseguente rischio di tooalerts attivazione in modo imprevisto.</span><span class="sxs-lookup"><span data-stu-id="07c16-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="07c16-229">Accesso ai dati di metrica a livello di codice</span><span class="sxs-lookup"><span data-stu-id="07c16-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="07c16-230">Hello seguito è riportato codice c# che accede metrica al minuto per un intervallo di minuti hello e Visualizza risultati hello in una finestra della console.</span><span class="sxs-lookup"><span data-stu-id="07c16-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="07c16-231">Usa hello libreria di archiviazione di Azure versione 4 che include hello classe CloudAnalyticsClient che semplifica l'accesso alle tabelle di metrica hello nel servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="07c16-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="07c16-232">Quali addebiti è necessario sostenere quando si abilitano le metriche di archiviazione?</span><span class="sxs-lookup"><span data-stu-id="07c16-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="07c16-233">Scrivere l'entità della tabella toocreate richieste per le metriche vengono addebitate con operazioni di archiviazione di Azure di hello tariffe standard applicabili tooall.</span><span class="sxs-lookup"><span data-stu-id="07c16-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="07c16-234">Sono fatturabili in base alle tariffe standard anche le richieste di lettura ed eliminazione da una data toometrics client.</span><span class="sxs-lookup"><span data-stu-id="07c16-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="07c16-235">Se è stato configurato un criterio di memorizzazione dati, non è necessario sostenere alcun addebito quando Archiviazione di Azure elimina i vecchi dati di metrica.</span><span class="sxs-lookup"><span data-stu-id="07c16-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="07c16-236">Tuttavia, se si eliminano dati analitica, l'account viene addebitato hello nelle operazioni di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="07c16-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="07c16-237">capacità di Hello utilizzata dalle tabelle di metrica hello è fatturabile: è possibile utilizzare hello seguente quantità di hello tooestimate di capacità usata per l'archiviazione dei dati di metrica:</span><span class="sxs-lookup"><span data-stu-id="07c16-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="07c16-238">Se ogni ora un servizio utilizza ogni API in ogni servizio, quindi circa 148KB di dati è ogni ora archiviati nelle tabelle di metrica di transazione hello se è stata abilitata servizio sia a livello dell'API di riepilogo.</span><span class="sxs-lookup"><span data-stu-id="07c16-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="07c16-239">Se ogni ora un servizio utilizza ogni API in ogni servizio, quindi circa 12KB di dati è ogni ora archiviati nelle tabelle di metrica di transazione hello se sono stati abilitati solo i livello di servizio riepilogo.</span><span class="sxs-lookup"><span data-stu-id="07c16-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="07c16-240">Hello tabella della capacità per i BLOB dispone di due righe aggiunte ogni giorno (purché l'utente ha scelto i log): questo implica che ogni giorno hello dimensioni della tabella aumentano da backup tooapproximately 300 byte.</span><span class="sxs-lookup"><span data-stu-id="07c16-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07c16-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07c16-241">Next steps</span></span>
[<span data-ttu-id="07c16-242">Abilitazione di Registrazione archiviazione e accesso ai dati di log</span><span class="sxs-lookup"><span data-stu-id="07c16-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
