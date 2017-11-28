---
title: Usare l'archiviazione BLOB per IIS e l'archiviazione tabelle per gli eventi in Log Analytics di Azure| Documentazione Microsoft
description: "Log Analytics è in grado di leggere i log per i servizi di Azure che scrivono dati di diagnostica nell'archivio tabelle o log di IIS nell'archivio BLOB."
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
ms.openlocfilehash: 459ef90ca1d76bada6565bfefd7b4bd1086197d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="1fc11-103">Usare l'archiviazione BLOB di Azure per IIS e l'archiviazione tabelle di Azure per gli eventi con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1fc11-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="1fc11-104">Log Analytics è in grado di leggere i log per i servizi seguenti che scrivono dati di diagnostica nell'archivio tabelle o log di IIS nell'archivio BLOB:</span><span class="sxs-lookup"><span data-stu-id="1fc11-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="1fc11-105">Cluster di Service Fabric (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="1fc11-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="1fc11-106">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fc11-106">Virtual Machines</span></span>
* <span data-ttu-id="1fc11-107">Ruoli di lavoro/Web</span><span class="sxs-lookup"><span data-stu-id="1fc11-107">Web/Worker Roles</span></span>

<span data-ttu-id="1fc11-108">Affinché Log Analytics possa raccogliere i dati per tali risorse, è necessario abilitare la diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc11-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="1fc11-109">Dopo l'abilitazione della diagnostica, è possibile usare il Portale di Azure o PowerShell per configurare Log Analytics per la raccolta dei log.</span><span class="sxs-lookup"><span data-stu-id="1fc11-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="1fc11-110">Diagnostica di Azure è un'estensione di Azure che consente di raccogliere i dati di diagnostica da un ruolo di lavoro, da un ruolo Web o da una macchina virtuale in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc11-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="1fc11-111">I dati vengono memorizzati in un account di archiviazione di Azure e possono quindi essere raccolti da Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1fc11-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="1fc11-112">Per consentire a Log Analytics di raccogliere questi log di Diagnostica di Azure, è necessario che i log si trovino nelle posizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1fc11-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="1fc11-113">Tipo di log</span><span class="sxs-lookup"><span data-stu-id="1fc11-113">Log Type</span></span> | <span data-ttu-id="1fc11-114">Tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="1fc11-114">Resource Type</span></span> | <span data-ttu-id="1fc11-115">Località</span><span class="sxs-lookup"><span data-stu-id="1fc11-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fc11-116">Log di IIS</span><span class="sxs-lookup"><span data-stu-id="1fc11-116">IIS logs</span></span> |<span data-ttu-id="1fc11-117">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fc11-117">Virtual Machines</span></span> <br> <span data-ttu-id="1fc11-118">Ruoli Web</span><span class="sxs-lookup"><span data-stu-id="1fc11-118">Web roles</span></span> <br> <span data-ttu-id="1fc11-119">Ruoli di lavoro</span><span class="sxs-lookup"><span data-stu-id="1fc11-119">Worker roles</span></span> |<span data-ttu-id="1fc11-120">wad-iis-logfiles (archivio BLOB)</span><span class="sxs-lookup"><span data-stu-id="1fc11-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="1fc11-121">syslog</span><span class="sxs-lookup"><span data-stu-id="1fc11-121">Syslog</span></span> |<span data-ttu-id="1fc11-122">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fc11-122">Virtual Machines</span></span> |<span data-ttu-id="1fc11-123">LinuxsyslogVer2v0 (archivio tabelle)</span><span class="sxs-lookup"><span data-stu-id="1fc11-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="1fc11-124">Eventi operativi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="1fc11-125">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-125">Service Fabric nodes</span></span> |<span data-ttu-id="1fc11-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="1fc11-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="1fc11-127">Eventi di Reliable Actor di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="1fc11-128">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-128">Service Fabric nodes</span></span> |<span data-ttu-id="1fc11-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="1fc11-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="1fc11-130">Eventi di Reliable Service di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="1fc11-131">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-131">Service Fabric nodes</span></span> |<span data-ttu-id="1fc11-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="1fc11-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="1fc11-133">Registri eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="1fc11-133">Windows Event logs</span></span> |<span data-ttu-id="1fc11-134">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="1fc11-135">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fc11-135">Virtual Machines</span></span> <br> <span data-ttu-id="1fc11-136">Ruoli Web</span><span class="sxs-lookup"><span data-stu-id="1fc11-136">Web roles</span></span> <br> <span data-ttu-id="1fc11-137">Ruoli di lavoro</span><span class="sxs-lookup"><span data-stu-id="1fc11-137">Worker roles</span></span> |<span data-ttu-id="1fc11-138">WADWindowsEventLogsTable (archivio tabelle)</span><span class="sxs-lookup"><span data-stu-id="1fc11-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="1fc11-139">Log di Windows ETW</span><span class="sxs-lookup"><span data-stu-id="1fc11-139">Windows ETW logs</span></span> |<span data-ttu-id="1fc11-140">Nodi di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="1fc11-141">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fc11-141">Virtual Machines</span></span> <br> <span data-ttu-id="1fc11-142">Ruoli Web</span><span class="sxs-lookup"><span data-stu-id="1fc11-142">Web roles</span></span> <br> <span data-ttu-id="1fc11-143">Ruoli di lavoro</span><span class="sxs-lookup"><span data-stu-id="1fc11-143">Worker roles</span></span> |<span data-ttu-id="1fc11-144">WADETWEventTable (archivio tabelle)</span><span class="sxs-lookup"><span data-stu-id="1fc11-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="1fc11-145">I log IIS provenienti dai siti Web di Azure non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="1fc11-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="1fc11-146">Per le macchine virtuali è anche possibile installare l'[agente di Log Analytics](log-analytics-azure-vm-extension.md) nella macchina virtuale per abilitare la raccolta di informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="1fc11-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="1fc11-147">In questo modo è possibile analizzare i log IIS e i registri eventi, oltre che eseguire ulteriori analisi, tra cui il rilevamento delle modifiche alla configurazione, la valutazione degli aggiornamenti e la valutazione di SQL.</span><span class="sxs-lookup"><span data-stu-id="1fc11-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="1fc11-148">Abilitare la diagnostica di Azure in una macchina virtuale per la raccolta di log eventi e IIS</span><span class="sxs-lookup"><span data-stu-id="1fc11-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="1fc11-149">Usare la procedura seguente per abilitare la Diagnostica di Azure in una macchina virtuale per la raccolta di log di eventi e IIS tramite il portale di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc11-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="1fc11-150">Per abilitare la Diagnostica di Azure in una macchina virtuale con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1fc11-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="1fc11-151">Installare l'agente di macchine virtuali quando si crea una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fc11-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="1fc11-152">Se la macchina virtuale esiste già, verificare che l'agente di macchine virtuali sia già installato.</span><span class="sxs-lookup"><span data-stu-id="1fc11-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="1fc11-153">Nel portale di Azure passare alla macchina virtuale, selezionare **Configurazione facoltativa**, quindi **Diagnostica** e impostare lo **Stato** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="1fc11-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="1fc11-154">Al termine, nella VM risulta installata e in esecuzione l'estensione di Diagnostica di Azure,</span><span class="sxs-lookup"><span data-stu-id="1fc11-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="1fc11-155">che ha il compito di raccogliere i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="1fc11-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="1fc11-156">Abilitare il monitoraggio e configurare la registrazione degli eventi su una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="1fc11-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="1fc11-157">La diagnostica può essere abilitata a livello di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fc11-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="1fc11-158">Per abilitare la diagnostica e quindi configurare la registrazione degli eventi, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1fc11-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="1fc11-159">Selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fc11-159">Select the VM.</span></span>
   2. <span data-ttu-id="1fc11-160">Fare clic su **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="1fc11-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="1fc11-161">Fare clic su **Diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="1fc11-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="1fc11-162">Impostare lo **Stato** su **SÌ**.</span><span class="sxs-lookup"><span data-stu-id="1fc11-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="1fc11-163">Selezionare ogni log di diagnostica da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="1fc11-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="1fc11-164">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fc11-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="1fc11-165">Abilitare Diagnostica di Azure in un ruolo Web per la raccolta di eventi e log IIS</span><span class="sxs-lookup"><span data-stu-id="1fc11-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="1fc11-166">Consultare l'argomento su [come abilitare la diagnostica in un servizio cloud](../cloud-services/cloud-services-dotnet-diagnostics.md) per una procedura generale di abilitazione della Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc11-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="1fc11-167">Le istruzioni seguenti usano queste informazioni, personalizzandole per l'uso con Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1fc11-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="1fc11-168">Con Diagnostica di Azure abilitata:</span><span class="sxs-lookup"><span data-stu-id="1fc11-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="1fc11-169">Per impostazione predefinita, i log di IIS vengono archiviati e i dati dei log vengono trasferiti in base all'intervallo di trasferimento scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="1fc11-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="1fc11-170">Per impostazione predefinita, i registri eventi di Windows non vengono trasferiti.</span><span class="sxs-lookup"><span data-stu-id="1fc11-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="1fc11-171">Per abilitare la diagnostica</span><span class="sxs-lookup"><span data-stu-id="1fc11-171">To enable diagnostics</span></span>
<span data-ttu-id="1fc11-172">Per abilitare i registri eventi di Windows o per modificare scheduledTransferPeriod, configurare Diagnostica di Azure con il file di configurazione XML (diagnostics.wadcfg), come mostrato in [Passaggio 4: Creare il file di configurazione della diagnostica e installare l'estensione](../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1fc11-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="1fc11-173">Il file di configurazione di esempio seguente raccoglie i log IIS e tutti gli eventi dai log di applicazione e sistema:</span><span class="sxs-lookup"><span data-stu-id="1fc11-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
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

<span data-ttu-id="1fc11-174">Assicurarsi che ConfigurationSettings specifichi un account di archiviazione, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1fc11-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="1fc11-175">I valori **AccountName** e **AccountKey** sono disponibili nel dashboard dell'account di archiviazione del portale di Azure in Gestisci chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="1fc11-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="1fc11-176">Il protocollo per la stringa di connessione deve essere **https**.</span><span class="sxs-lookup"><span data-stu-id="1fc11-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="1fc11-177">Dopo che la configurazione della diagnostica aggiornata è stata applicata al servizio cloud e ha iniziato a scrivere la diagnostica in Archiviazione di Azure, è possibile configurare Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1fc11-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="1fc11-178">Usare il portale di Azure per raccogliere log da Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1fc11-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="1fc11-179">È possibile usare il portale di Azure per configurare Log Analytics per raccogliere i log per i servizi di Azure seguenti:</span><span class="sxs-lookup"><span data-stu-id="1fc11-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="1fc11-180">Cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1fc11-180">Service Fabric clusters</span></span>
* <span data-ttu-id="1fc11-181">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1fc11-181">Virtual Machines</span></span>
* <span data-ttu-id="1fc11-182">Ruoli di lavoro/Web</span><span class="sxs-lookup"><span data-stu-id="1fc11-182">Web/Worker Roles</span></span>

<span data-ttu-id="1fc11-183">Nel portale di Azure passare all'area di lavoro di Log Analytics ed eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="1fc11-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="1fc11-184">Fare clic su *Log account di archiviazione*</span><span class="sxs-lookup"><span data-stu-id="1fc11-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="1fc11-185">Fare clic sull'attività *Aggiungi*</span><span class="sxs-lookup"><span data-stu-id="1fc11-185">Click the *Add* task</span></span>
3. <span data-ttu-id="1fc11-186">Selezionare l'account di archiviazione che contiene i log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="1fc11-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="1fc11-187">L'account di archiviazione può essere di tipo classico oppure un account di archiviazione di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1fc11-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="1fc11-188">Selezionare il tipo di dati per cui si vogliono raccogliere i log</span><span class="sxs-lookup"><span data-stu-id="1fc11-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="1fc11-189">È possibile scegliere tra log IIS, log eventi, SysLog (Linux), log ETW ed eventi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1fc11-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="1fc11-190">Il valore per l'origine viene compilato automaticamente in base al tipo di dati e non può essere modificato</span><span class="sxs-lookup"><span data-stu-id="1fc11-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="1fc11-191">Fare clic su OK per salvare la configurazione</span><span class="sxs-lookup"><span data-stu-id="1fc11-191">Click OK to save the configuration</span></span>

<span data-ttu-id="1fc11-192">Ripetere i passaggi da 2 a 6 per account di archiviazione aggiuntivi e tipi di dati che devono essere raccolti da Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1fc11-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="1fc11-193">Nel giro di 30 minuti circa è possibile visualizzare i dati dell'account di archiviazione in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1fc11-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="1fc11-194">Verranno visualizzati solo i dati scritti nell'archivio dopo l'applicazione della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1fc11-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="1fc11-195">Log Analytics non legge i dati preesistenti dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1fc11-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="1fc11-196">Il portale non conferma l'esistenza dell'origine nell'account di archiviazione e non verifica se vengono scritti nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="1fc11-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="1fc11-197">Abilitare la diagnostica di Azure in una macchina virtuale per la raccolta di log eventi e log IIS tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fc11-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="1fc11-198">Usare la procedura [Configurazione di Log Analytics per indicizzare Diagnostica di Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) per leggere tramite PowerShell i dati di Diagnostica di Azure scritti nell'archiviazione tabelle.</span><span class="sxs-lookup"><span data-stu-id="1fc11-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="1fc11-199">Con Azure PowerShell è possibile specificare in modo più preciso gli eventi che vengono scritti nell'Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc11-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="1fc11-200">Per altre informazioni, vedere [Abilitare la diagnostica nelle macchine virtuali di Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1fc11-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="1fc11-201">È possibile abilitare e aggiornare la Diagnostica di Azure con il seguente script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1fc11-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="1fc11-202">È possibile usare questo script anche con una configurazione della registrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1fc11-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="1fc11-203">Modificare lo script per impostare l'account di archiviazione, il nome del servizio e il nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fc11-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="1fc11-204">Lo script usa i cmdlet per le macchine virtuali di tipo classico.</span><span class="sxs-lookup"><span data-stu-id="1fc11-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="1fc11-205">Esaminare il seguente script di esempio, copiarlo, modificarlo se necessario, salvare l'esempio come file script di PowerShell e quindi eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="1fc11-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

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
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="1fc11-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1fc11-206">Next steps</span></span>
* <span data-ttu-id="1fc11-207">[Raccogliere i log e le metriche per i servizi di Azure](log-analytics-azure-storage.md) per i servizi supportati di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc11-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="1fc11-208">[Abilitare soluzioni](log-analytics-add-solutions.md) per fornire informazioni dettagliate sui dati.</span><span class="sxs-lookup"><span data-stu-id="1fc11-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="1fc11-209">[Usare query di ricerca](log-analytics-log-searches.md) per analizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="1fc11-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
