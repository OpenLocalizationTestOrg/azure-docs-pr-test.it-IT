---
title: Configurare Diagnostica di Azure per l'invio di dati ad Application Insights | Documentazione Microsoft
description: Aggiornare la configurazione pubblica di Diagnostica di Azure per inviare dati ad Application Insights
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
ms.openlocfilehash: 67dc2d5bbfa2012e4e098616edda593d023c4c1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="c22a5-103">Inviare i dati di diagnostica del servizio Cloud, della macchina virtuale o di Service Fabric ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="c22a5-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="c22a5-104">I servizi cloud, le macchine virtuali, il set di scalabilità di macchine virtuali e Service Fabric usano l'estensione Diagnostica di Azure per raccogliere i dati.</span><span class="sxs-lookup"><span data-stu-id="c22a5-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="c22a5-105">La diagnostica di Azure invia i dati alle tabelle di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c22a5-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="c22a5-106">Tuttavia, è possibile anche inviare pipe o un subset di dati ad altri percorsi con l'estensione Diagnostica di Azure 1.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="c22a5-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="c22a5-107">In questo articolo viene descritto come inviare i dati dall'estensione Diagnostica di Azure ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c22a5-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="c22a5-108">Descrizione della configurazione di Diagnostica</span><span class="sxs-lookup"><span data-stu-id="c22a5-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="c22a5-109">L'estensione Diagnostica di Azure 1.5 ha introdotto i sink, ovvero percorsi aggiuntivi a cui è possibile inviare i dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c22a5-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="c22a5-110">Esempio di configurazione di un sink per Application Insights:</span><span class="sxs-lookup"><span data-stu-id="c22a5-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="c22a5-111">L'attributo **Sink** *name* è un valore della stringa che identifica in modo univoco il sink.</span><span class="sxs-lookup"><span data-stu-id="c22a5-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="c22a5-112">L'elemento **ApplicationInsights** specifica la chiave di strumentazione della risorsa di Application Insights a cui verranno inviati i dati di Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="c22a5-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="c22a5-113">Se non si ha una risorsa di Application Insights, vedere [Creare una risorsa di Application Insights](../application-insights/app-insights-create-new-resource.md) per altre informazioni sulla creazione di una risorsa e l'acquisizione della chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="c22a5-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="c22a5-114">Se si sviluppa un servizio Cloud con Azure SDK 2.8 e versioni successive, questa chiave di strumentazione viene compilata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c22a5-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="c22a5-115">Il valore si basa sull'impostazione di configurazione del servizio **APPINSIGHTS_INSTRUMENTATIONKEY** quando si crea il pacchetto del progetto del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="c22a5-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="c22a5-116">Vedere [Usare Application Insights con Diagnostica di Azure per risolvere i problemi del servizio cloud](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="c22a5-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="c22a5-117">L'elemento **Channels** contiene uno o più elementi **Channel**.</span><span class="sxs-lookup"><span data-stu-id="c22a5-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="c22a5-118">L'attributo *name* fa riferimento in modo univoco a tale canale.</span><span class="sxs-lookup"><span data-stu-id="c22a5-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="c22a5-119">L'attributo *loglevel* consente di specificare il livello di log consentito dal canale.</span><span class="sxs-lookup"><span data-stu-id="c22a5-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="c22a5-120">I livelli di log disponibili, in base al livello di dettaglio delle informazioni, sono:</span><span class="sxs-lookup"><span data-stu-id="c22a5-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="c22a5-121">Dettagliato</span><span class="sxs-lookup"><span data-stu-id="c22a5-121">Verbose</span></span>
        - <span data-ttu-id="c22a5-122">Informazioni</span><span class="sxs-lookup"><span data-stu-id="c22a5-122">Information</span></span>
        - <span data-ttu-id="c22a5-123">Avviso</span><span class="sxs-lookup"><span data-stu-id="c22a5-123">Warning</span></span>
        - <span data-ttu-id="c22a5-124">Errore</span><span class="sxs-lookup"><span data-stu-id="c22a5-124">Error</span></span>
        - <span data-ttu-id="c22a5-125">Critico</span><span class="sxs-lookup"><span data-stu-id="c22a5-125">Critical</span></span>

<span data-ttu-id="c22a5-126">Un canale agisce da filtro e consente di selezionare specifici livelli di log da inviare al sink di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c22a5-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="c22a5-127">Ad esempio, l'utente può raccogliere log dettagliati inviarli alla risorsa di archiviazione, ma inviare solo gli errori al sink.</span><span class="sxs-lookup"><span data-stu-id="c22a5-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="c22a5-128">Il grafico seguente illustra questa relazione.</span><span class="sxs-lookup"><span data-stu-id="c22a5-128">The following graphic shows this relationship.</span></span>

![Configurazione pubblica di Diagnostica](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="c22a5-130">Nel grafico seguente sono riepilogati i valori di configurazione e il relativo funzionamento.</span><span class="sxs-lookup"><span data-stu-id="c22a5-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="c22a5-131">È inoltre possibile includere più sink nella configurazione, a vari livelli della gerarchia.</span><span class="sxs-lookup"><span data-stu-id="c22a5-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="c22a5-132">Il sink specificato al livello superiore svolge la funzione di impostazione globale, mentre quello specificato al livello di singolo elemento agisce da override dell'impostazione globale.</span><span class="sxs-lookup"><span data-stu-id="c22a5-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Configurazione dei sink di diagnostica con Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="c22a5-134">Esempio di configurazione del sink completo</span><span class="sxs-lookup"><span data-stu-id="c22a5-134">Complete sink configuration example</span></span>
<span data-ttu-id="c22a5-135">Ecco un esempio completo del file di configurazione pubblico che</span><span class="sxs-lookup"><span data-stu-id="c22a5-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="c22a5-136">invia tutti gli errori ad Application Insights (specificato nel nodo **DiagnosticMonitorConfiguration**)</span><span class="sxs-lookup"><span data-stu-id="c22a5-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="c22a5-137">invia anche i registri di livello Verbose per i log dell'applicazione (specificato nel nodo **Log**).</span><span class="sxs-lookup"><span data-stu-id="c22a5-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
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
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
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
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
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
<span data-ttu-id="c22a5-138">Nella configurazione precedente, le righe riportate di seguito hanno i significati seguenti:</span><span class="sxs-lookup"><span data-stu-id="c22a5-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="c22a5-139">Inviare tutti i dati raccolti dalla diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="c22a5-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="c22a5-140">Inviare solo i log di errore al sink di Application Insights</span><span class="sxs-lookup"><span data-stu-id="c22a5-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="c22a5-141">Inviare i log Verbose dell'applicazione ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="c22a5-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="c22a5-142">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="c22a5-142">Limitations</span></span>

- <span data-ttu-id="c22a5-143">**Unico tipo di log Channels e non per i contatori delle prestazioni.**</span><span class="sxs-lookup"><span data-stu-id="c22a5-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="c22a5-144">Se si specifica un canale con un elemento contatore delle prestazioni, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="c22a5-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="c22a5-145">**Il livello di log per un canale non può superare il livello di log relativo a quanto raccolto da Diagnostica di Azure.**</span><span class="sxs-lookup"><span data-stu-id="c22a5-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="c22a5-146">Ad esempio, non è possibile raccogliere errori di log applicazioni nell'elemento Los e provare a inviare log Verbose al sink di Application Insight.</span><span class="sxs-lookup"><span data-stu-id="c22a5-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="c22a5-147">L'attributo *scheduledTransferLogLevelFilter* deve sempre raccogliere un numero di log pari o superiore al numero di log che si sta tentando di inviare a un sink.</span><span class="sxs-lookup"><span data-stu-id="c22a5-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="c22a5-148">**Non è possibile inviare ad Application Insights dati BLOB raccolti dall'estensione Diagnostica di Azure.**</span><span class="sxs-lookup"><span data-stu-id="c22a5-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="c22a5-149">Ad esempio qualsiasi elemento specificato nel nodo *Directories*.</span><span class="sxs-lookup"><span data-stu-id="c22a5-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="c22a5-150">Per i dump di arresto anomalo, il dump effettivo di arresto anomalo viene inviato all'archiviazione BLOB e ad Application Insights viene inviata solo una notifica che attesta la creazione del dump di arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="c22a5-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c22a5-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c22a5-151">Next Steps</span></span>
* <span data-ttu-id="c22a5-152">Informazioni su come [visualizzare le informazioni di diagnostica di Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c22a5-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="c22a5-153">Usare [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) per abilitare l'estensione di Diagnostica di Azure per un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c22a5-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="c22a5-154">Usare [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) per abilitare l'estensione di Diagnostica di Azure per un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c22a5-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
