---
title: dati di diagnostica di Azure nel percorso di frequente hello tramite hub di eventi aaaStreaming | Documenti Microsoft
description: Configurazione della diagnostica Azure con gli hub di eventi di fine tooend, incluse indicazioni per gli scenari comuni.
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
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="a33cc-103">Flusso di dati di diagnostica di Azure nel percorso critico hello tramite gli hub di eventi</span><span class="sxs-lookup"><span data-stu-id="a33cc-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="a33cc-104">Diagnostica di Azure fornisce metodi flessibili toocollect metriche e i log da cloud services le macchine virtuali (VM) e trasferire risultati tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a33cc-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="a33cc-105">A partire da hello marzo 2016 (2.9 SDK) di tempo, è possibile inviare diagnostica toocustom origini dati e trasferire i dati di percorso ricorrente in secondi tramite [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="a33cc-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="a33cc-106">Tipi di dati supportati:</span><span class="sxs-lookup"><span data-stu-id="a33cc-106">Supported data types include:</span></span>

* <span data-ttu-id="a33cc-107">Tracciamento degli eventi di Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="a33cc-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="a33cc-108">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="a33cc-108">Performance counters</span></span>
* <span data-ttu-id="a33cc-109">Registri eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="a33cc-109">Windows event logs</span></span>
* <span data-ttu-id="a33cc-110">Log applicazioni</span><span class="sxs-lookup"><span data-stu-id="a33cc-110">Application logs</span></span>
* <span data-ttu-id="a33cc-111">Log dell'infrastruttura Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="a33cc-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="a33cc-112">Questo articolo illustra come tooconfigure diagnostica di Azure con gli hub di eventi da terminare tooend.</span><span class="sxs-lookup"><span data-stu-id="a33cc-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="a33cc-113">Vengono inoltre fornite istruzioni relative hello scenari comuni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a33cc-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="a33cc-114">Modalità di registrazione toocustomize hello e le metriche che vengano inviate tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="a33cc-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="a33cc-115">Come le configurazioni di toochange in ogni ambiente</span><span class="sxs-lookup"><span data-stu-id="a33cc-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="a33cc-116">Hub di eventi tooview come flusso di dati</span><span class="sxs-lookup"><span data-stu-id="a33cc-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="a33cc-117">Come tootroubleshoot hello connessione</span><span class="sxs-lookup"><span data-stu-id="a33cc-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="a33cc-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a33cc-118">Prerequisites</span></span>
<span data-ttu-id="a33cc-119">Dati dell'evento hub receieving da diagnostica di Azure sono supportati in servizi Cloud, macchine virtuali, il set di scalabilità di macchine virtuali e Service Fabric a partire da Azure SDK 2.9 hello e hello corrispondente di strumenti di Azure per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a33cc-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="a33cc-120">Estensione di Diagnostica Azure 1.6 ([SDK di Azure per .NET 2.9 o versione successiva](https://azure.microsoft.com/downloads/) ha questa destinazione per impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="a33cc-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="a33cc-121">Visual Studio 2013 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a33cc-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="a33cc-122">Le configurazioni esistenti di diagnostica di Azure in un'applicazione utilizzando un *wadcfgx* file e uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="a33cc-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="a33cc-123">Visual Studio: [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="a33cc-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="a33cc-124">Windows PowerShell: [Abilitare la diagnostica nei servizi Cloud di Azure tramite PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a33cc-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="a33cc-125">Spazio dei nomi degli hub di eventi il provisioning per ogni articolo hello [Introduzione agli hub di eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="a33cc-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="a33cc-126">La connessione di diagnostica Azure tooEvent hub sink</span><span class="sxs-lookup"><span data-stu-id="a33cc-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="a33cc-127">Per impostazione predefinita, diagnostica Azure invia sempre i log e le metriche tooan account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a33cc-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="a33cc-128">Un'applicazione può inoltre inviare dati tooEvent hub aggiungendo un nuovo **sink** sezione hello **PublicConfig** / **WadCfg** elemento di hello *wadcfgx* file.</span><span class="sxs-lookup"><span data-stu-id="a33cc-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="a33cc-129">In Visual Studio, hello *wadcfgx* file viene archiviato nel seguente percorso hello: **progetto servizio Cloud** > **ruoli** > **( RoleName)** > **wadcfgx** file.</span><span class="sxs-lookup"><span data-stu-id="a33cc-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="a33cc-130">In questo esempio, hub eventi hello è impostato l'URL toohello completamente qualificato dello spazio dei nomi dell'hub eventi hello: spazio dei nomi di hub eventi + "/" + nome hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a33cc-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="a33cc-131">hub di eventi Hello URL viene visualizzato in hello [portale di Azure](http://go.microsoft.com/fwlink/?LinkID=213885) nel dashboard di hello hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a33cc-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="a33cc-132">Hello **Sink** nome può essere impostato tooany di stringa valida, purché hello stesso valore viene utilizzato in modo coerente in tutto il file di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a33cc-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="a33cc-133">In questa sezione potrebbero esserci altri sink configurati, come ad esempio *applicationInsights* .</span><span class="sxs-lookup"><span data-stu-id="a33cc-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="a33cc-134">Diagnostica di Azure consente di specificare uno o più sink toobe definite se ogni sink viene dichiarato in hello **PrivateConfig** sezione.</span><span class="sxs-lookup"><span data-stu-id="a33cc-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="a33cc-135">Hello hub eventi sink deve inoltre essere dichiarati e definiti in hello **PrivateConfig** sezione di hello *wadcfgx* file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a33cc-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="a33cc-136">Hello `SharedAccessKeyName` valore deve corrispondere a una chiave di firma di accesso condiviso (SAS) e i criteri che sono stato definito in hello **hub eventi** dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="a33cc-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="a33cc-137">Esplorare il dashboard di hub eventi toohello in hello [portale di Azure](https://manage.windowsazure.com), fare clic su hello **configura** scheda e impostare un criterio denominato (ad esempio, "SendRule") che ha *inviare* autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a33cc-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="a33cc-138">Hello **StorageAccount** viene dichiarato **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="a33cc-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="a33cc-139">Non è necessario toochange valori qui se sono coinvolti.</span><span class="sxs-lookup"><span data-stu-id="a33cc-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="a33cc-140">In questo esempio, si lascia valori hello vuoto, ovvero un segno che un asset downstream verrà impostati valori hello.</span><span class="sxs-lookup"><span data-stu-id="a33cc-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="a33cc-141">Ad esempio, hello *ServiceConfiguration* file di configurazione Ambiente Imposta nomi appropriati ambiente hello e le chiavi.</span><span class="sxs-lookup"><span data-stu-id="a33cc-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="a33cc-142">chiave di firma di accesso condiviso hub eventi Hello viene archiviata in testo normale nel hello *wadcfgx* file.</span><span class="sxs-lookup"><span data-stu-id="a33cc-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="a33cc-143">Spesso, questa chiave viene archiviata nel controllo del codice toosource o è disponibile come una risorsa nel server di compilazione, pertanto deve essere protetto come appropriato.</span><span class="sxs-lookup"><span data-stu-id="a33cc-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="a33cc-144">È consigliabile usare una chiave SAS con *solo invio* autorizzazioni in modo che un utente malintenzionato può scrivere toohello hub eventi, ma non ascolto tooit o gestirlo.</span><span class="sxs-lookup"><span data-stu-id="a33cc-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="a33cc-145">Configurare diagnostica Azure toosend metriche e log tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="a33cc-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="a33cc-146">Come descritto in precedenza, tutti i dati di diagnostica personalizzata e le impostazione predefinita, vale a dire, metriche e i log, viene inviato automaticamente tooAzure archiviazione intervalli hello configurato.</span><span class="sxs-lookup"><span data-stu-id="a33cc-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="a33cc-147">Con gli hub di eventi e qualsiasi sink aggiuntive, è possibile specificare qualsiasi nodo radice o foglia in toobe gerarchia hello inviati toohello hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="a33cc-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="a33cc-148">Questi includono gli eventi ETW, i contatori delle prestazioni, i registri eventi di Windows e i registri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a33cc-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="a33cc-149">È importante tooconsider quanti punti dati devono effettivamente essere trasferiti tooEvent hub.</span><span class="sxs-lookup"><span data-stu-id="a33cc-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="a33cc-150">Di solito gli sviluppatori trasferiscono i dati del percorso critico a bassa latenza che devono essere utilizzati e interpretati rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a33cc-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="a33cc-151">I sistemi che monitorano gli avvisi o le regole di scalabilità automatica sono degli esempi.</span><span class="sxs-lookup"><span data-stu-id="a33cc-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="a33cc-152">Uno sviluppatore può anche configurare un archivio di analisi o di ricerca alternativo; ad esempio, Analisi di flusso di Azure, ElasticSearch, un sistema di monitoraggio personalizzato o un sistema di monitoraggio preferito di terze parti.</span><span class="sxs-lookup"><span data-stu-id="a33cc-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="a33cc-153">Hello seguito sono riportate alcune configurazioni di esempio.</span><span class="sxs-lookup"><span data-stu-id="a33cc-153">hello following are some example configurations.</span></span>

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

<span data-ttu-id="a33cc-154">In hello sopra riportato, sink hello è applicato toohello padre **PerformanceCounters** nodo nella gerarchia di hello, ovvero tutti elementi figlio **PerformanceCounters** verrà inviato tooEvent hub.</span><span class="sxs-lookup"><span data-stu-id="a33cc-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

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

<span data-ttu-id="a33cc-155">Nell'esempio precedente hello sink hello è applicato tooonly tre contatori: **richieste in coda**, **richieste rifiutate**, e **% tempo processore**.</span><span class="sxs-lookup"><span data-stu-id="a33cc-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="a33cc-156">Hello esempio seguente viene illustrato come uno sviluppatore può limitare quantità hello di dati inviato toobe hello metriche più importanti utilizzati per l'integrità del servizio.</span><span class="sxs-lookup"><span data-stu-id="a33cc-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="a33cc-157">In questo esempio, il sink hello è toologs applicato ed è tooerror filtrato solo livello traccia.</span><span class="sxs-lookup"><span data-stu-id="a33cc-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="a33cc-158">Distribuire e aggiornare un'applicazione dei servizi cloud e della configurazione della diagnostica</span><span class="sxs-lookup"><span data-stu-id="a33cc-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="a33cc-159">Visual Studio fornisce più semplice percorso toodeploy hello un'applicazione hello e configurazione di hub eventi sink.</span><span class="sxs-lookup"><span data-stu-id="a33cc-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="a33cc-160">file di hello tooview e modifica, aprirlo hello *wadcfgx* file in Visual Studio, modificarlo e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="a33cc-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="a33cc-161">percorso Hello è **progetto servizio Cloud** > **ruoli** > **(RoleName)** > **wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="a33cc-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="a33cc-162">A questo punto, tutti distribuzione e aggiornamento delle azioni in Visual Studio, Visual Studio Team System e tutti i comandi o script che si basano su MSBuild e utilizzano hello **/t: pubblicare** destinazione include hello *wadcfgx*  nel processo di creazione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="a33cc-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="a33cc-163">Inoltre, le distribuzioni e aggiornamenti è possibile distribuire tooAzure file hello usando hello appropriato agente l'estensione diagnostica Azure in macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a33cc-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="a33cc-164">Dopo aver distribuito l'applicazione hello e configurazione di diagnostica di Azure, verrà visualizzata immediatamente l'attività nel dashboard di hello dell'hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="a33cc-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="a33cc-165">Ciò indica che si è pronti toomove sui dati di percorso a caldo hello tooviewing hello listener client o l'analisi dello strumento di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="a33cc-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="a33cc-166">Nella seguente illustrazione di hello, il dashboard di hub eventi hello Mostra integro l'invio di diagnostica dati toohello evento hub avvio un po' dopo 11 PM.</span><span class="sxs-lookup"><span data-stu-id="a33cc-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="a33cc-167">Ovvero quando è stata distribuita un'applicazione hello con una versione aggiornata *wadcfgx* file e hello sink è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="a33cc-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="a33cc-168">Quando si apporta file di configurazione degli aggiornamenti toohello diagnostica Azure (con estensione wadcfgx), è consigliabile push hello aggiornamenti toohello intera applicazione, nonché configurazione hello tramite la pubblicazione in Visual Studio, o uno script di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a33cc-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="a33cc-169">Visualizzare i dati del percorso critico</span><span class="sxs-lookup"><span data-stu-id="a33cc-169">View hot-path data</span></span>
<span data-ttu-id="a33cc-170">Come descritto in precedenza, sono disponibili molti casi di utilizzo per l'ascolto tooand l'elaborazione dei dati di hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a33cc-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="a33cc-171">Un approccio semplice è un hub eventi del test di piccole dimensioni console applicazione toolisten toohello toocreate e flusso di output di stampa hello.</span><span class="sxs-lookup"><span data-stu-id="a33cc-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="a33cc-172">È possibile inserire hello seguente di codice, è illustrato più dettagliatamente nella [Introduzione agli hub di eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="a33cc-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="a33cc-173">Si noti che un'applicazione console hello deve includere hello [pacchetto NuGet Host processore di eventi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="a33cc-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="a33cc-174">Tenere presente i valori hello tooreplace tra parentesi quadre in hello **Main** funzione con valori per le risorse.</span><span class="sxs-lookup"><span data-stu-id="a33cc-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

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

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="a33cc-175">Risoluzione dei problemi relativi ai sink dell'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a33cc-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="a33cc-176">hub di eventi Hello non mostra l'attività dell'evento in ingresso o in uscita come previsto.</span><span class="sxs-lookup"><span data-stu-id="a33cc-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="a33cc-177">Verificare che l'Hub eventi esegua correttamente il provisioning.</span><span class="sxs-lookup"><span data-stu-id="a33cc-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="a33cc-178">Tutte le informazioni di connessione in hello **PrivateConfig** sezione *wadcfgx* devono corrispondere ai valori hello della risorsa come illustrato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="a33cc-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="a33cc-179">Assicurarsi di disporre di un criterio definito ("SendRule" nell'esempio hello) nel portale di hello e che *inviare* viene concessa l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="a33cc-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="a33cc-180">Dopo un aggiornamento, hub eventi hello non mostra più EventActivity in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="a33cc-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="a33cc-181">Innanzitutto, assicurarsi che tale hub eventi hello e le informazioni di configurazione siano corretta, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a33cc-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="a33cc-182">In alcuni casi hello **PrivateConfig** viene reimpostato in un aggiornamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a33cc-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="a33cc-183">Hello consiglia di correggere tutte le modifiche troppo toomake*wadcfgx* in hello progetto e quindi inviare un aggiornamento completo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a33cc-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="a33cc-184">In caso contrario, assicurarsi che gli aggiornamenti di diagnostica hello inserisce completa **PrivateConfig** che include una chiave SAS hello.</span><span class="sxs-lookup"><span data-stu-id="a33cc-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="a33cc-185">Si è tentato di suggerimenti hello e hub eventi hello ancora non funziona.</span><span class="sxs-lookup"><span data-stu-id="a33cc-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="a33cc-186">Provare a cercare nella tabella di archiviazione di Azure hello che contiene gli errori e log di diagnostica di Azure stesso: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="a33cc-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="a33cc-187">Un'opzione è toouse uno strumento, ad esempio [Azure Storage Explorer](http://www.storageexplorer.com) account di archiviazione toothis tooconnect, visualizzare in questa tabella e aggiungere una query per i TimeStamp in hello ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="a33cc-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="a33cc-188">È possibile utilizzare lo strumento di hello tooexport un file CSV e aprirlo in un'applicazione, ad esempio Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="a33cc-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="a33cc-189">Excel rende facile toosearch per le stringhe di carta telefonica, ad esempio **EventHubs**, toosee indica l'errore viene segnalato.</span><span class="sxs-lookup"><span data-stu-id="a33cc-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a33cc-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a33cc-190">Next steps</span></span>
<span data-ttu-id="a33cc-191">• [Altre informazioni su Hub eventi](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="a33cc-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="a33cc-192">Appendice: completare l'esempio di file (.wadcfgx) della configurazione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="a33cc-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="a33cc-193">Hello complementare *ServiceConfiguration* per questo esempio è simile a hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="a33cc-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

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

<span data-ttu-id="a33cc-194">Le impostazioni basate su Json equivalenti per le macchine virtuali sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="a33cc-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="a33cc-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a33cc-195">Next steps</span></span>
<span data-ttu-id="a33cc-196">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="a33cc-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="a33cc-197">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a33cc-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a33cc-198">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="a33cc-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="a33cc-199">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a33cc-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
