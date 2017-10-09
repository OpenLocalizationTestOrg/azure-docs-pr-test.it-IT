---
title: archiviazione di blob aaaUse per IIS e la tabella di archiviazione per gli eventi in Azure Log Analitica | Documenti Microsoft
description: "Log Analitica può leggere i log di hello per servizi di Azure che scrivere di archiviazione di diagnostica tootable o scrittura tooblob archiviazione dei log IIS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="7de3d-103">Usare l'archiviazione BLOB di Azure per IIS e l'archiviazione tabelle di Azure per gli eventi con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7de3d-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="7de3d-104">Log Analitica può leggere i log di hello per i seguenti servizi di archiviazione o IIS log scritto tooblob archiviazione scrivere diagnostica tootable hello:</span><span class="sxs-lookup"><span data-stu-id="7de3d-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="7de3d-105">Cluster di Service Fabric (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="7de3d-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="7de3d-106">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7de3d-106">Virtual Machines</span></span>
* <span data-ttu-id="7de3d-107">Ruoli di lavoro/Web</span><span class="sxs-lookup"><span data-stu-id="7de3d-107">Web/Worker Roles</span></span>

<span data-ttu-id="7de3d-108">Affinché Log Analytics possa raccogliere i dati per tali risorse, è necessario abilitare la diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="7de3d-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="7de3d-109">Quando è abilitata la diagnostica, è possibile usare hello portale di Azure o PowerShell configurare Log Analitica toocollect hello registri.</span><span class="sxs-lookup"><span data-stu-id="7de3d-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="7de3d-110">Diagnostica di Azure è un'estensione di Azure che permette toocollect i dati di diagnostica da un ruolo di lavoro, un ruolo web o una macchina virtuale in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="7de3d-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="7de3d-111">dati di Hello vengono archiviati in un account di archiviazione di Azure e possono quindi essere raccolti da Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="7de3d-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="7de3d-112">Per Log Analitica toocollect questi registri di diagnostica di Azure, hello log devono trovarsi in hello posizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7de3d-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="7de3d-113">Tipo di log</span><span class="sxs-lookup"><span data-stu-id="7de3d-113">Log Type</span></span> | <span data-ttu-id="7de3d-114">Tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="7de3d-114">Resource Type</span></span> | <span data-ttu-id="7de3d-115">Località</span><span class="sxs-lookup"><span data-stu-id="7de3d-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7de3d-116">Log di IIS</span><span class="sxs-lookup"><span data-stu-id="7de3d-116">IIS logs</span></span> |<span data-ttu-id="7de3d-117">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7de3d-117">Virtual Machines</span></span> <br> <span data-ttu-id="7de3d-118">Ruoli Web</span><span class="sxs-lookup"><span data-stu-id="7de3d-118">Web roles</span></span> <br> <span data-ttu-id="7de3d-119">Ruoli di lavoro</span><span class="sxs-lookup"><span data-stu-id="7de3d-119">Worker roles</span></span> |<span data-ttu-id="7de3d-120">wad-iis-logfiles (archivio BLOB)</span><span class="sxs-lookup"><span data-stu-id="7de3d-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="7de3d-121">syslog</span><span class="sxs-lookup"><span data-stu-id="7de3d-121">Syslog</span></span> |<span data-ttu-id="7de3d-122">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7de3d-122">Virtual Machines</span></span> |<span data-ttu-id="7de3d-123">LinuxsyslogVer2v0 (archivio tabelle)</span><span class="sxs-lookup"><span data-stu-id="7de3d-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="7de3d-124">Eventi operativi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="7de3d-125">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-125">Service Fabric nodes</span></span> |<span data-ttu-id="7de3d-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="7de3d-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="7de3d-127">Eventi di Reliable Actor di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="7de3d-128">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-128">Service Fabric nodes</span></span> |<span data-ttu-id="7de3d-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="7de3d-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="7de3d-130">Eventi di Reliable Service di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="7de3d-131">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-131">Service Fabric nodes</span></span> |<span data-ttu-id="7de3d-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="7de3d-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="7de3d-133">Registri eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="7de3d-133">Windows Event logs</span></span> |<span data-ttu-id="7de3d-134">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="7de3d-135">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7de3d-135">Virtual Machines</span></span> <br> <span data-ttu-id="7de3d-136">Ruoli Web</span><span class="sxs-lookup"><span data-stu-id="7de3d-136">Web roles</span></span> <br> <span data-ttu-id="7de3d-137">Ruoli di lavoro</span><span class="sxs-lookup"><span data-stu-id="7de3d-137">Worker roles</span></span> |<span data-ttu-id="7de3d-138">WADWindowsEventLogsTable (archivio tabelle)</span><span class="sxs-lookup"><span data-stu-id="7de3d-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="7de3d-139">Log di Windows ETW</span><span class="sxs-lookup"><span data-stu-id="7de3d-139">Windows ETW logs</span></span> |<span data-ttu-id="7de3d-140">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="7de3d-141">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7de3d-141">Virtual Machines</span></span> <br> <span data-ttu-id="7de3d-142">Ruoli Web</span><span class="sxs-lookup"><span data-stu-id="7de3d-142">Web roles</span></span> <br> <span data-ttu-id="7de3d-143">Ruoli di lavoro</span><span class="sxs-lookup"><span data-stu-id="7de3d-143">Worker roles</span></span> |<span data-ttu-id="7de3d-144">WADETWEventTable (archivio tabelle)</span><span class="sxs-lookup"><span data-stu-id="7de3d-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="7de3d-145">I log IIS provenienti dai siti Web di Azure non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="7de3d-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="7de3d-146">Per le macchine virtuali, è possibile hello installazione hello [agente Log Analitica](log-analytics-azure-vm-extension.md) in informazioni aggiuntive dettagliate tooenable macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7de3d-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="7de3d-147">Inoltre i registri eventi e registri di IIS in grado di tooanalyze toobeing è possibile eseguire ulteriori analisi, tra cui il rilevamento delle modifiche di configurazione, valutazione di SQL e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="7de3d-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="7de3d-148">Abilitare la diagnostica di Azure in una macchina virtuale per la raccolta di log eventi e IIS</span><span class="sxs-lookup"><span data-stu-id="7de3d-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="7de3d-149">Hello utilizzare seguendo procedure tooenable diagnostica di Azure in una macchina virtuale per il log eventi e IIS tramite il portale di Microsoft Azure hello insieme.</span><span class="sxs-lookup"><span data-stu-id="7de3d-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="7de3d-150">tooenable diagnostica di Azure in una macchina virtuale con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7de3d-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="7de3d-151">Installare l'agente VM hello quando si crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7de3d-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="7de3d-152">Se esiste già una macchina virtuale hello, verificare che hello che agente VM è già installato.</span><span class="sxs-lookup"><span data-stu-id="7de3d-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="7de3d-153">In hello portale di Azure, passare una macchina virtuale toohello, selezionare **configurazione facoltativa**, quindi **diagnostica** e impostare **stato** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="7de3d-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="7de3d-154">Al termine, hello VM ha estensione di diagnostica Azure hello installato e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7de3d-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="7de3d-155">che ha il compito di raccogliere i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="7de3d-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="7de3d-156">Abilitare il monitoraggio e configurare la registrazione degli eventi su una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="7de3d-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="7de3d-157">È possibile abilitare la diagnostica in hello livello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7de3d-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="7de3d-158">diagnostica tooenable e quindi configurare la registrazione degli eventi, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7de3d-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="7de3d-159">Selezionare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7de3d-159">Select hello VM.</span></span>
   2. <span data-ttu-id="7de3d-160">Fare clic su **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="7de3d-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="7de3d-161">Fare clic su **Diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="7de3d-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="7de3d-162">Set hello **stato** troppo**ON**.</span><span class="sxs-lookup"><span data-stu-id="7de3d-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="7de3d-163">Selezionare ogni log di diagnostica che si desidera toocollect.</span><span class="sxs-lookup"><span data-stu-id="7de3d-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="7de3d-164">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7de3d-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="7de3d-165">Abilitare Diagnostica di Azure in un ruolo Web per la raccolta di eventi e log IIS</span><span class="sxs-lookup"><span data-stu-id="7de3d-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="7de3d-166">Fare riferimento troppo[come tooEnable diagnostica in un servizio Cloud](../cloud-services/cloud-services-dotnet-diagnostics.md) per i passaggi generali per l'abilitazione della diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="7de3d-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="7de3d-167">istruzioni di Hello seguenti usare queste informazioni e personalizzarlo per l'utilizzo con Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="7de3d-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="7de3d-168">Con Diagnostica di Azure abilitata:</span><span class="sxs-lookup"><span data-stu-id="7de3d-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="7de3d-169">I log IIS vengono archiviati per impostazione predefinita, i dati di log trasferiti nell'intervallo di trasferimento scheduledTransferPeriod hello.</span><span class="sxs-lookup"><span data-stu-id="7de3d-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="7de3d-170">Per impostazione predefinita, i registri eventi di Windows non vengono trasferiti.</span><span class="sxs-lookup"><span data-stu-id="7de3d-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="7de3d-171">diagnostica tooenable</span><span class="sxs-lookup"><span data-stu-id="7de3d-171">tooenable diagnostics</span></span>
<span data-ttu-id="7de3d-172">tooenable registri eventi di Windows o toochange hello scheduledTransferPeriod, configurare la diagnostica di Azure utilizzando hello file di configurazione XML (Diagnostics. wadcfg), come illustrato nella [passaggio 4: creare il file di configurazione di diagnostica e installare hello estensione](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="7de3d-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="7de3d-173">Hello file di configurazione di esempio seguente raccoglie i log di IIS e tutti gli eventi dall'applicazione hello e registri di sistema:</span><span class="sxs-lookup"><span data-stu-id="7de3d-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="7de3d-174">Assicurarsi che ConfigurationSettings specifichi un account di archiviazione, come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="7de3d-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="7de3d-175">Hello **AccountName** e **AccountKey** i valori sono disponibili in hello portale Azure nel dashboard dell'account di archiviazione hello, in Gestisci chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="7de3d-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="7de3d-176">protocollo Hello hello stringa di connessione deve essere **https**.</span><span class="sxs-lookup"><span data-stu-id="7de3d-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="7de3d-177">Dopo aver applicata la configurazione di diagnostica aggiornati hello tooyour cloud service e sta scrivendo tooAzure diagnostica archiviazione, sarà necessario tooconfigure pronto Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="7de3d-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="7de3d-178">Utilizzare i log di Azure toocollect portale hello da archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7de3d-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="7de3d-179">È possibile usare il log hello toocollect di hello tooconfigure portale Azure Log Analitica per hello seguenti servizi di Azure:</span><span class="sxs-lookup"><span data-stu-id="7de3d-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="7de3d-180">Cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7de3d-180">Service Fabric clusters</span></span>
* <span data-ttu-id="7de3d-181">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7de3d-181">Virtual Machines</span></span>
* <span data-ttu-id="7de3d-182">Ruoli di lavoro/Web</span><span class="sxs-lookup"><span data-stu-id="7de3d-182">Web/Worker Roles</span></span>

<span data-ttu-id="7de3d-183">Nel portale di Azure hello, passare l'area di lavoro Log Analitica tooyour ed eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="7de3d-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="7de3d-184">Fare clic su *Log account di archiviazione*</span><span class="sxs-lookup"><span data-stu-id="7de3d-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="7de3d-185">Fare clic su hello *Aggiungi* attività</span><span class="sxs-lookup"><span data-stu-id="7de3d-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="7de3d-186">Selezionare l'account di archiviazione hello che contiene i log di diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="7de3d-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="7de3d-187">L'account di archiviazione può essere di tipo classico oppure un account di archiviazione di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7de3d-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="7de3d-188">Selezionare il tipo di dati desiderato nei registri toocollect hello</span><span class="sxs-lookup"><span data-stu-id="7de3d-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="7de3d-189">opzioni di Hello sono registri IIS Eventi; Syslog (Linux); Log ETW; Eventi dell'infrastruttura del servizio</span><span class="sxs-lookup"><span data-stu-id="7de3d-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="7de3d-190">valore Hello di origine viene popolato automaticamente in base hello tipo di dati e non possono essere modificati</span><span class="sxs-lookup"><span data-stu-id="7de3d-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="7de3d-191">Fare clic su OK toosave hello configurazione</span><span class="sxs-lookup"><span data-stu-id="7de3d-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="7de3d-192">Ripetere i passaggi da 2 a 6 per i tipi di dati e gli account di ulteriore spazio di archiviazione che si desidera toocollect Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="7de3d-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="7de3d-193">In circa 30 minuti, si è in grado di toosee dati dall'account di archiviazione hello in Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="7de3d-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="7de3d-194">Viene visualizzata solo i dati scritti toostorage dopo la configurazione di hello viene applicata.</span><span class="sxs-lookup"><span data-stu-id="7de3d-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="7de3d-195">Log Analitica leggere dati preesistenti hello dall'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="7de3d-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="7de3d-196">portale Hello non convalidare tale hello origine esista nell'account di archiviazione hello o se sono scritti nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="7de3d-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="7de3d-197">Abilitare la diagnostica di Azure in una macchina virtuale per la raccolta di log eventi e log IIS tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="7de3d-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="7de3d-198">Hello di utilizzare i passaggi [tooindex Analitica Log di configurazione di diagnostica di Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread da diagnostica di Azure che viene scritti tootable archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7de3d-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="7de3d-199">Utilizzo di PowerShell di Azure è possibile specificare più precisamente hello gli eventi scritti tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7de3d-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="7de3d-200">Per altre informazioni, vedere [Abilitare la diagnostica nelle macchine virtuali di Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7de3d-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="7de3d-201">È possibile abilitare e aggiornare diagnostica Windows Azure utilizzando lo script di PowerShell seguente hello.</span><span class="sxs-lookup"><span data-stu-id="7de3d-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="7de3d-202">È possibile usare questo script anche con una configurazione della registrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="7de3d-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="7de3d-203">Modificare l'account di archiviazione di hello script tooset hello, nome del servizio e il nome di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7de3d-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="7de3d-204">script di Hello Usa i cmdlet per le macchine virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="7de3d-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="7de3d-205">Esaminare hello seguente script di esempio, copiarlo, modificarlo se necessario, salvare l'esempio hello come file script di PowerShell e quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="7de3d-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="7de3d-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7de3d-206">Next steps</span></span>
* <span data-ttu-id="7de3d-207">[Raccogliere i log e le metriche per i servizi di Azure](log-analytics-azure-storage.md) per i servizi supportati di Azure.</span><span class="sxs-lookup"><span data-stu-id="7de3d-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="7de3d-208">[Abilitare soluzioni](log-analytics-add-solutions.md) tooprovide comprendere dati hello.</span><span class="sxs-lookup"><span data-stu-id="7de3d-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="7de3d-209">[Utilizzare le query di ricerca](log-analytics-log-searches.md) dati hello tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="7de3d-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
