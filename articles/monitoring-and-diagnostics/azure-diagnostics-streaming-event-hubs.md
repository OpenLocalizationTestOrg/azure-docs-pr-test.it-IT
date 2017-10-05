---
title: Trasmettere i dati di Diagnostica di Azure nel percorso critico con Hub eventi | Microsoft Docs
description: Configurazione di Diagnostica di Azure con Hub eventi end-to-end, tra cui indicazioni per scenari comuni.
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: 1c05bd6dc4c4d394aa043b9995de9c184e4f14c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="c387c-103">Trasmettere i dati di Diagnostica di Azure nel percorso critico tramite Hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="c387c-104">Diagnostica di Azure fornisce metodi flessibili per raccogliere le metriche e i log delle macchine virtuali (VM) di servizi cloud e trasferire i risultati in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c387c-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="c387c-105">A partire da marzo 2016 (SDK 2.9), è possibile eseguire inviare la diagnostica a origini dati completamente personalizzate e trasferire i dati del percorso critico in pochi secondi tramite [Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="c387c-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="c387c-106">Tipi di dati supportati:</span><span class="sxs-lookup"><span data-stu-id="c387c-106">Supported data types include:</span></span>

* <span data-ttu-id="c387c-107">Tracciamento degli eventi di Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="c387c-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="c387c-108">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c387c-108">Performance counters</span></span>
* <span data-ttu-id="c387c-109">Registri eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="c387c-109">Windows event logs</span></span>
* <span data-ttu-id="c387c-110">Log applicazioni</span><span class="sxs-lookup"><span data-stu-id="c387c-110">Application logs</span></span>
* <span data-ttu-id="c387c-111">Log dell'infrastruttura Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="c387c-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="c387c-112">Questo articolo illustra le modalità di configurazione di Diagnostica di Azure con Hub eventi dall'inizio alla fine.</span><span class="sxs-lookup"><span data-stu-id="c387c-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="c387c-113">Vengono inoltre fornite delle linee guida per gli scenari comuni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c387c-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="c387c-114">Come personalizzare le metriche e i log inviati a Hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="c387c-115">Come modificare le configurazioni in ciascun ambiente</span><span class="sxs-lookup"><span data-stu-id="c387c-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="c387c-116">Come visualizzare i dati di flusso di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="c387c-117">Come risolvere i problemi di connessione</span><span class="sxs-lookup"><span data-stu-id="c387c-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c387c-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c387c-118">Prerequisites</span></span>
<span data-ttu-id="c387c-119">La ricezione di dati di Diagnostica di Azure in Hub eventi è supportata in Servizi cloud, macchine virtuali, set di scalabilità di macchine virtuali e Service Fabric a partire da Azure SDK 2.9 e dalla versione corrispondente di Strumenti di Azure per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c387c-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="c387c-120">Estensione di Diagnostica Azure 1.6 ([SDK di Azure per .NET 2.9 o versione successiva](https://azure.microsoft.com/downloads/) ha questa destinazione per impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="c387c-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="c387c-121">Visual Studio 2013 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="c387c-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="c387c-122">Configurazioni esistenti di Diagnostica di Azure in un'applicazione usando un file *.wadcfgx* e uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c387c-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="c387c-123">Visual Studio: [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="c387c-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="c387c-124">Windows PowerShell: [Abilitare la diagnostica nei servizi Cloud di Azure tramite PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c387c-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="c387c-125">Provisioning dello spazio dei nomi dell'Hub eventi eseguito in base all'articolo [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="c387c-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="c387c-126">Collegare Diagnostica di Azure al sink dell'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="c387c-127">Per impostazione predefinita, Diagnostica di Azure invia sempre log e metriche a un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c387c-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="c387c-128">Un'applicazione può anche inviare dati agli Hub eventi aggiungendo una nuova sezione **Sinks** nell'elemento **PublicConfig** / **WadCfg** del file *.wadcfgx*.</span><span class="sxs-lookup"><span data-stu-id="c387c-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="c387c-129">In Visual Studio il file *.wadcfgx* viene archiviato nel percorso di destinazione seguente: **Progetto servizio cloud** > **Ruoli** > **(NomeRuolo)** > **file diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="c387c-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

<span data-ttu-id="c387c-130">In questo esempio l'URL dell'Hub eventi è impostato sullo spazio dei nomi completo dell'Hub eventi: spazio dei nomi di Hub eventi + "/" + nome Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c387c-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="c387c-131">L'URL dell'Hub eventi viene visualizzato nel [Portale di Azure](http://go.microsoft.com/fwlink/?LinkID=213885) sul dashboard di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c387c-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="c387c-132">Il nome del **Sink** può essere impostato su qualsiasi stringa valida, purché lo stesso valore venga usato in modo coerente in tutto il file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c387c-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="c387c-133">In questa sezione potrebbero esserci altri sink configurati, come ad esempio *applicationInsights* .</span><span class="sxs-lookup"><span data-stu-id="c387c-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="c387c-134">Diagnostica di Azure consente di definire uno o più sink, ammesso che ciascun sink venga dichiarato anche nella sezione **PrivateConfig** .</span><span class="sxs-lookup"><span data-stu-id="c387c-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="c387c-135">Il sink dell'Hub eventi deve essere dichiarato e definito anche nella sezione **PrivateConfig** del file di configurazione *.wadcfgx* .</span><span class="sxs-lookup"><span data-stu-id="c387c-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

<span data-ttu-id="c387c-136">Il valore `SharedAccessKeyName` deve corrispondere a una chiave di firma di accesso condiviso e ai criteri definiti nello spazio dei nomi di **Hub eventi** .</span><span class="sxs-lookup"><span data-stu-id="c387c-136">The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace.</span></span> <span data-ttu-id="c387c-137">Passare al dashboard Hub eventi nel [portale di Azure](https://manage.windowsazure.com), selezionare la scheda **Configura** e impostare un criterio denominato (ad esempio, "SendRule") che dispone delle autorizzazioni *di invio* .</span><span class="sxs-lookup"><span data-stu-id="c387c-137">Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="c387c-138">Anche il valore **StorageAccount** viene dichiarato in **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="c387c-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="c387c-139">Non è necessario modificare i valori se funzionano.</span><span class="sxs-lookup"><span data-stu-id="c387c-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="c387c-140">In questo esempio, i valori vengono lasciati vuoti, poiché verranno impostati da un asset downstream.</span><span class="sxs-lookup"><span data-stu-id="c387c-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="c387c-141">Ad esempio, il file di configurazione dell'ambiente *ServiceConfiguration.Cloud.cscfg* consente l'impostazione delle chiavi e dei nomi appropriati per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="c387c-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="c387c-142">La chiave di firma di accesso condiviso di Hub eventi è archiviata in testo normale nel file *.wadcfgx* .</span><span class="sxs-lookup"><span data-stu-id="c387c-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="c387c-143">Spesso questa chiave viene archiviata nel controllo del codice sorgente o risulta disponibile in un asset del server di compilazione, pertanto è necessario proteggerla in maniera appropriata.</span><span class="sxs-lookup"><span data-stu-id="c387c-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="c387c-144">Si consiglia di usare una chiave SAS con autorizzazioni *Send only* in modo che qualsiasi utente malintenzionato possa al massimo scrivere nell'Hub eventi, ma non ascoltarlo o gestirlo.</span><span class="sxs-lookup"><span data-stu-id="c387c-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="c387c-145">Configurare la Diagnostica di Azure per inviare log e metriche a Hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="c387c-146">Come illustrato in precedenza, tutti i dati di diagnostica predefiniti e personalizzati (ovvero metriche e log) vengono inviati automaticamente ad Archiviazione di Azure agli intervalli configurati.</span><span class="sxs-lookup"><span data-stu-id="c387c-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="c387c-147">Con Hub eventi (e qualsiasi sink aggiuntivo), è possibile specificare qualsiasi nodo radice o foglia nella gerarchia da inviare a Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c387c-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="c387c-148">Questi includono gli eventi ETW, i contatori delle prestazioni, i registri eventi di Windows e i registri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c387c-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="c387c-149">È importante valutare il numero di punti dati effettivi da trasferire all'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c387c-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="c387c-150">Di solito gli sviluppatori trasferiscono i dati del percorso critico a bassa latenza che devono essere utilizzati e interpretati rapidamente.</span><span class="sxs-lookup"><span data-stu-id="c387c-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="c387c-151">I sistemi che monitorano gli avvisi o le regole di scalabilità automatica sono degli esempi.</span><span class="sxs-lookup"><span data-stu-id="c387c-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="c387c-152">Uno sviluppatore può anche configurare un archivio di analisi o di ricerca alternativo; ad esempio, Analisi di flusso di Azure, ElasticSearch, un sistema di monitoraggio personalizzato o un sistema di monitoraggio preferito di terze parti.</span><span class="sxs-lookup"><span data-stu-id="c387c-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="c387c-153">Di seguito alcuni esempi di configurazioni.</span><span class="sxs-lookup"><span data-stu-id="c387c-153">The following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

<span data-ttu-id="c387c-154">Nell'esempio precedente poiché il sink viene applicato al nodo padre **PerformanceCounters** nella gerarchia, tutti i nodi figlio **PerformanceCounters** verranno inviati agli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c387c-154">In the above example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

<span data-ttu-id="c387c-155">Nell'esempio precedente il sink è applicato solo a tre contatori: **richieste in coda**, **richieste rifiutate** e **% tempo processore**.</span><span class="sxs-lookup"><span data-stu-id="c387c-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="c387c-156">Nell'esempio seguente viene illustrato come uno sviluppatore può limitare la quantità di dati inviati come metriche importanti che vengono usate per l'integrità del servizio.</span><span class="sxs-lookup"><span data-stu-id="c387c-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

<span data-ttu-id="c387c-157">In questo esempio, il sink viene applicato ai registri e filtrato solo per l'analisi a livello di errore.</span><span class="sxs-lookup"><span data-stu-id="c387c-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="c387c-158">Distribuire e aggiornare un'applicazione dei servizi cloud e della configurazione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="c387c-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="c387c-159">Visual Studio offre il modo più semplice per distribuire l'applicazione e la configurazione sink dell'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c387c-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="c387c-160">Per visualizzare e modificare il file, aprire il file *.wadcfgx* in Visual Studio, modificarlo e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="c387c-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="c387c-161">Il percorso è **Progetto servizio cloud** > **Ruoli** > **(NomeRuolo)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="c387c-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="c387c-162">A questo punto, tutte le operazioni di distribuzione e di aggiornamento delle distribuzioni in Visual Studio, Visual Studio Team System e tutti i comandi o script che si basano su MSBuild e usano la destinazione **/t:publish** includeranno il file *.wadcfgx* nel processo di creazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c387c-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="c387c-163">Le distribuzioni e gli aggiornamenti distribuiscono anche il file in Azure tramite l'appropriata estensione agente di Diagnostica di Azure nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c387c-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="c387c-164">Al termine della distribuzione dell'applicazione e della configurazione di Diagnostica di Azure, l'attività verrà visualizzata immediatamente nel dashboard dell'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c387c-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="c387c-165">Ciò indica che si è pronti per passare alla visualizzazione dei dati del percorso critico nel client listener o nello strumento di analisi scelto.</span><span class="sxs-lookup"><span data-stu-id="c387c-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="c387c-166">Nella figura seguente, il dashboard Hub eventi mostra l'invio integro dei dati di diagnostica all'Hub eventi a partire da un certo momento dopo le 23.00,</span><span class="sxs-lookup"><span data-stu-id="c387c-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="c387c-167">ossia quando l'applicazione è stata distribuita con una versione aggiornata del file *.wadcfgx* e il sink è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c387c-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="c387c-168">Quando si eseguono gli aggiornamenti del file di configurazione di Diagnostica di Azure (.wadcfgx), si consiglia di eseguire il push degli aggiornamenti per l'intera applicazione e la configurazione tramite la pubblicazione di Visual Studio o tramite script di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c387c-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="c387c-169">Visualizzare i dati del percorso critico</span><span class="sxs-lookup"><span data-stu-id="c387c-169">View hot-path data</span></span>
<span data-ttu-id="c387c-170">Come illustrato in precedenza, esistono molti casi d'uso per l'ascolto e l'elaborazione dei dati dell'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c387c-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="c387c-171">Un approccio semplice consiste nel creare una piccola applicazione console di verifica per l'ascolto dell'Hub eventi e per la stampa del flusso di output.</span><span class="sxs-lookup"><span data-stu-id="c387c-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="c387c-172">È possibile inserire il seguente codice (descritto dettagliatamente nell'articolo [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)) in un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="c387c-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="c387c-173">L'applicazione console deve includere il [pacchetto Event Processor Host NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="c387c-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="c387c-174">Sostituire i valori in parentesi tonde nella funzione **Main** con i valori per le proprie risorse.</span><span class="sxs-lookup"><span data-stu-id="c387c-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="c387c-175">Risoluzione dei problemi relativi ai sink dell'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="c387c-176">L'Hub eventi non visualizza le attività dell'evento in ingresso o in uscita come previsto.</span><span class="sxs-lookup"><span data-stu-id="c387c-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="c387c-177">Verificare che l'Hub eventi esegua correttamente il provisioning.</span><span class="sxs-lookup"><span data-stu-id="c387c-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="c387c-178">Tutte le informazioni di connessione nella sezione **PrivateConfig** del file *.wadcfgx* devono corrispondere ai valori della risorsa, come illustrato nel portale.</span><span class="sxs-lookup"><span data-stu-id="c387c-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="c387c-179">Assicurarsi di avere definito un criterio SAS ("SendRule" nell'esempio) nel portale e che sia stata concessa l'autorizzazione di *invio* .</span><span class="sxs-lookup"><span data-stu-id="c387c-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="c387c-180">Dopo un aggiornamento, l'Hub eventi non visualizza più le attività dell'evento in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="c387c-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="c387c-181">In primo luogo, assicurarsi che le informazioni di configurazione e dell'Hub eventi siano esatte, come spiegato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c387c-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="c387c-182">Capita che a volte **PrivateConfig** venga reimpostato in un aggiornamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c387c-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="c387c-183">La soluzione consigliata consiste nell'apportare tutte le modifiche nel file *.wadcfgx* del progetto e quindi eseguire il push di un aggiornamento completo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c387c-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="c387c-184">Se non è possibile, verificare che l'aggiornamento della diagnostica esegua il push della sezione **PrivateConfig** completa, che include la chiave SAS.</span><span class="sxs-lookup"><span data-stu-id="c387c-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="c387c-185">Ho provato a seguire i suggerimenti, ma l'Hub eventi continua a non funzionare.</span><span class="sxs-lookup"><span data-stu-id="c387c-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="c387c-186">Eseguire una ricerca nella tabella di Archiviazione di Azure contenente i registri e gli errori della Diagnostica di Azure: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="c387c-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="c387c-187">Una possibilità consiste nell'usare uno strumento come [Esplora archivi Azure](http://www.storageexplorer.com) per connettersi a questo account di archiviazione, visualizzare la tabella e aggiungere una query per il TimeStamp delle ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="c387c-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="c387c-188">È possibile utilizzare lo strumento per esportare un file .csv e aprirlo in un'applicazione come Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="c387c-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="c387c-189">Excel semplifica la ricerca di stringhe di presentazione come **EventHubs**per visualizzare l'errore segnalato.</span><span class="sxs-lookup"><span data-stu-id="c387c-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c387c-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c387c-190">Next steps</span></span>
<span data-ttu-id="c387c-191">• [Altre informazioni su Hub eventi](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="c387c-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="c387c-192">Appendice: completare l'esempio di file (.wadcfgx) della configurazione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="c387c-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="c387c-193">Il file *ServiceConfiguration.Cloud.cscfg* complementare per questo esempio si presenta come segue.</span><span class="sxs-lookup"><span data-stu-id="c387c-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="c387c-194">Le impostazioni basate su Json equivalenti per le macchine virtuali sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="c387c-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c387c-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c387c-195">Next steps</span></span>
<span data-ttu-id="c387c-196">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c387c-196">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="c387c-197">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c387c-198">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="c387c-199">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="c387c-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
