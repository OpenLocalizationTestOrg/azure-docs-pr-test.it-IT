---
title: aaaConfigure diagnostica Azure toosend dati tooApplication Insights | Documenti Microsoft
description: Aggiornare hello diagnostica Azure configurazione pubblica toosend dati tooApplication Insights.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="a3e87-103">Inviare i dati di diagnostica del servizio Cloud, macchine virtuali o Service Fabric tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="a3e87-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="a3e87-104">Servizi cloud, macchine virtuali, il set di scalabilità di macchine virtuali e Service Fabric utilizzano dati toocollect dell'estensione diagnostica di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a3e87-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="a3e87-105">Diagnostica di Azure invia dati tooAzure tabelle di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a3e87-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="a3e87-106">Tuttavia, è anche possibile tutti pipe o un subset di posizioni di tooother hello dati utilizzando l'estensione diagnostica Azure 1.5 o versioni successiva.</span><span class="sxs-lookup"><span data-stu-id="a3e87-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="a3e87-107">In questo articolo viene descritto come dati toosend hello tooApplication estensione diagnostica di Azure Insights.</span><span class="sxs-lookup"><span data-stu-id="a3e87-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="a3e87-108">Descrizione della configurazione di Diagnostica</span><span class="sxs-lookup"><span data-stu-id="a3e87-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="a3e87-109">sink di estensione 1.5 introdotto diagnostica Windows Azure Hello, che sono percorsi aggiuntivi in cui è possibile inviare i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="a3e87-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="a3e87-110">Esempio di configurazione di un sink per Application Insights:</span><span class="sxs-lookup"><span data-stu-id="a3e87-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="a3e87-111">Hello **Sink** *nome* attributo è un valore stringa che identifica in modo univoco il sink hello.</span><span class="sxs-lookup"><span data-stu-id="a3e87-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="a3e87-112">Hello **ApplicationInsights** elemento specifica la chiave di strumentazione di hello in cui verrà inviato i dati di diagnostica Azure hello risorsa di Application insights.</span><span class="sxs-lookup"><span data-stu-id="a3e87-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="a3e87-113">Se non si dispone di una risorsa di Application Insights esistente, vedere [creare una nuova risorsa di Application Insights](../application-insights/app-insights-create-new-resource.md) per ulteriori informazioni sulla creazione di una risorsa e ottenere la chiave di strumentazione hello.</span><span class="sxs-lookup"><span data-stu-id="a3e87-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="a3e87-114">Se si sviluppa un servizio Cloud con Azure SDK 2.8 e versioni successive, questa chiave di strumentazione viene compilata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a3e87-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="a3e87-115">il valore di Hello è basato su hello **APPINSIGHTS_INSTRUMENTATIONKEY** impostazione di configurazione del servizio al progetto di servizio Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a3e87-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="a3e87-116">Vedere [problemi di servizio Cloud di utilizzare Application Insights con diagnostica Azure tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="a3e87-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="a3e87-117">Hello **canali** elemento contiene uno o più **canale** elementi.</span><span class="sxs-lookup"><span data-stu-id="a3e87-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="a3e87-118">Hello *nome* attributo fa riferimento in modo univoco il canale toothat.</span><span class="sxs-lookup"><span data-stu-id="a3e87-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="a3e87-119">Hello *loglevel* consente di specificare a livello di registrazione hello che hello canale consente di attributo.</span><span class="sxs-lookup"><span data-stu-id="a3e87-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="a3e87-120">livelli di log disponibili Hello nell'ordine della maggior parte delle informazioni tooleast sono:</span><span class="sxs-lookup"><span data-stu-id="a3e87-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="a3e87-121">Dettagliato</span><span class="sxs-lookup"><span data-stu-id="a3e87-121">Verbose</span></span>
        - <span data-ttu-id="a3e87-122">Informazioni</span><span class="sxs-lookup"><span data-stu-id="a3e87-122">Information</span></span>
        - <span data-ttu-id="a3e87-123">Avviso</span><span class="sxs-lookup"><span data-stu-id="a3e87-123">Warning</span></span>
        - <span data-ttu-id="a3e87-124">Errore</span><span class="sxs-lookup"><span data-stu-id="a3e87-124">Error</span></span>
        - <span data-ttu-id="a3e87-125">Critico</span><span class="sxs-lookup"><span data-stu-id="a3e87-125">Critical</span></span>

<span data-ttu-id="a3e87-126">Un canale consente tooselect log specifici livelli toosend toohello destinazione sink e funziona come un filtro.</span><span class="sxs-lookup"><span data-stu-id="a3e87-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="a3e87-127">Ad esempio, si potrebbe raccogliere log dettagliati e inviarli toostorage, ma solo sink toohello di errori di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="a3e87-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="a3e87-128">Hello nella figura seguente viene illustrata questa relazione.</span><span class="sxs-lookup"><span data-stu-id="a3e87-128">hello following graphic shows this relationship.</span></span>

![Configurazione pubblica di Diagnostica](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="a3e87-130">Hello elemento grafico seguente sono riepilogati i valori di configurazione hello e sul relativo funzionamento.</span><span class="sxs-lookup"><span data-stu-id="a3e87-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="a3e87-131">È possibile includere più sink nella configurazione di hello a diversi livelli nella gerarchia di hello.</span><span class="sxs-lookup"><span data-stu-id="a3e87-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="a3e87-132">sink di Hello al primo livello hello funge da un'impostazione globale e hello uno specificata nella hello singoli elemento funziona come un'impostazione globale toothat di sostituzione.</span><span class="sxs-lookup"><span data-stu-id="a3e87-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Configurazione dei sink di diagnostica con Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="a3e87-134">Esempio di configurazione del sink completo</span><span class="sxs-lookup"><span data-stu-id="a3e87-134">Complete sink configuration example</span></span>
<span data-ttu-id="a3e87-135">Ecco un esempio completo della configurazione pubblica hello file</span><span class="sxs-lookup"><span data-stu-id="a3e87-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="a3e87-136">Invia tutti gli errori Insights tooApplication (specificato hello **DiagnosticMonitorConfiguration** nodo)</span><span class="sxs-lookup"><span data-stu-id="a3e87-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="a3e87-137">Invia anche i log dettagliati di livello per i registri applicazione hello (specificato hello **registri** nodo).</span><span class="sxs-lookup"><span data-stu-id="a3e87-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
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
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="a3e87-138">Nella configurazione precedente hello, hello seguendo le linee è hello seguenti significati:</span><span class="sxs-lookup"><span data-stu-id="a3e87-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="a3e87-139">Invia tutti i dati di hello raccolti dalla diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="a3e87-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="a3e87-140">Invia solo i registri toohello Application Insights il sink di errore</span><span class="sxs-lookup"><span data-stu-id="a3e87-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="a3e87-141">Trasmissione dettagliata applicazione registra tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="a3e87-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="a3e87-142">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="a3e87-142">Limitations</span></span>

- <span data-ttu-id="a3e87-143">**Unico tipo di log Channels e non per i contatori delle prestazioni.**</span><span class="sxs-lookup"><span data-stu-id="a3e87-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="a3e87-144">Se si specifica un canale con un elemento contatore delle prestazioni, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="a3e87-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="a3e87-145">**livello di log Hello di un canale non può superare il livello di log hello di ciò che sono stati raccolti dalla diagnostica di Azure.**</span><span class="sxs-lookup"><span data-stu-id="a3e87-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="a3e87-146">Ad esempio, non è possibile raccogliere gli errori di registro dell'applicazione nell'elemento registri hello si cerca toosend log dettagliati toohello Application Insights sink.</span><span class="sxs-lookup"><span data-stu-id="a3e87-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="a3e87-147">Hello *scheduledTransferLogLevelFilter* attributo necessario raccogliere sempre uguale o più log di hello registra si sta tentando di toosend tooa sink.</span><span class="sxs-lookup"><span data-stu-id="a3e87-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="a3e87-148">**Non è possibile inviare dati blob raccolti da tooApplication estensione diagnostica di Azure Insights.**</span><span class="sxs-lookup"><span data-stu-id="a3e87-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="a3e87-149">Ad esempio, un valore specificato in hello *directory* nodo.</span><span class="sxs-lookup"><span data-stu-id="a3e87-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="a3e87-150">Per i dump di arresto anomalo dump di arresto anomalo del sistema effettivo hello viene inviato archiviazione tooblob e solo una notifica che hello dump di arresto anomalo del sistema è stata generata viene inviato tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="a3e87-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3e87-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3e87-151">Next Steps</span></span>
* <span data-ttu-id="a3e87-152">Informazioni su come troppo[visualizzare le informazioni di diagnostica di Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a3e87-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="a3e87-153">Utilizzare [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello estensione diagnostica di Azure per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a3e87-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="a3e87-154">Utilizzare [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello estensione diagnostica di Azure per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="a3e87-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
