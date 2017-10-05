---
title: 'Monitorare le prestazioni delle app Web in Linux: Azure | Documentazione Microsoft'
description: Monitoraggio esteso delle prestazioni delle applicazioni del sito Web Java con il plug-in CollectD per Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: 4ea917b068e0242bfb88d7357eca032607a43a3f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="3f365-103">collectd: metriche delle prestazioni Linux in Application Insights</span><span class="sxs-lookup"><span data-stu-id="3f365-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="3f365-104">Per esplorare le metriche delle prestazioni del sistema Linux in [Application Insights](app-insights-overview.md), installare [collectd](http://collectd.org/) insieme al rispettivo plug-in di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3f365-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="3f365-105">Questa soluzione open source raccoglie diverse che relative al sistema e alla rete.</span><span class="sxs-lookup"><span data-stu-id="3f365-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="3f365-106">In genere, si usa collectd se è già stato [instrumentato il servizio Web Java con Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="3f365-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="3f365-107">Fornisce una maggiore quantità di dati che consentono di migliorare le prestazioni dell'app o diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="3f365-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span></span> 

![Grafici di esempio](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="3f365-109">Ottenere la chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="3f365-109">Get your instrumentation key</span></span>
<span data-ttu-id="3f365-110">Nel [Portale di Microsoft Azure](https://portal.azure.com) aprire la risorsa [Application Insights](app-insights-overview.md) in cui devono essere visualizzati i dati.</span><span class="sxs-lookup"><span data-stu-id="3f365-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span></span> <span data-ttu-id="3f365-111">In alternativa, [creare una nuova risorsa](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3f365-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="3f365-112">Copiare la chiave di strumentazione, che identifica la risorsa.</span><span class="sxs-lookup"><span data-stu-id="3f365-112">Take a copy of the instrumentation key, which identifies the resource.</span></span>

![Visualizzare tutto, aprire la risorsa e quindi nell'elenco a discesa Informazioni di base selezionare e copiare la chiave di strumentazione](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-the-plug-in"></a><span data-ttu-id="3f365-114">Installare collectd e il plug-in</span><span class="sxs-lookup"><span data-stu-id="3f365-114">Install collectd and the plug-in</span></span>
<span data-ttu-id="3f365-115">Nei computer server Linux:</span><span class="sxs-lookup"><span data-stu-id="3f365-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="3f365-116">Installare [collectd](http://collectd.org/) versione 5.4.0 o successive.</span><span class="sxs-lookup"><span data-stu-id="3f365-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="3f365-117">Scaricare il [plug-in di scrittura collectd di Application Insights](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="3f365-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="3f365-118">Annotare il numero di versione.</span><span class="sxs-lookup"><span data-stu-id="3f365-118">Note the version number.</span></span>
3. <span data-ttu-id="3f365-119">Copiare il file JAR del plug-in in `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="3f365-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="3f365-120">Modificare `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="3f365-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="3f365-121">Assicurarsi che il [plug-in Java](https://collectd.org/wiki/index.php/Plugin:Java) sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="3f365-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="3f365-122">Aggiornare JVMArg per java.class.path in modo da includere il file JAR seguente.</span><span class="sxs-lookup"><span data-stu-id="3f365-122">Update the JVMArg for the java.class.path to include the following JAR.</span></span> <span data-ttu-id="3f365-123">Aggiornare il numero di versione in modo che corrisponda a quello scaricato:</span><span class="sxs-lookup"><span data-stu-id="3f365-123">Update the version number to match the one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="3f365-124">Aggiungere questo frammento di codice usando la chiave di strumentazione dalla risorsa:</span><span class="sxs-lookup"><span data-stu-id="3f365-124">Add this snippet, using the Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="3f365-125">Di seguito è riportata una parte di un file di configurazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="3f365-125">Here's part of a sample configuration file:</span></span>

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

<span data-ttu-id="3f365-126">Configurare altri [plug-in collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), che possono raccogliere diversi dati da origini diverse.</span><span class="sxs-lookup"><span data-stu-id="3f365-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="3f365-127">Riavviare collectd, come indicato nel rispettivo [manuale](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="3f365-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-the-data-in-application-insights"></a><span data-ttu-id="3f365-128">Visualizzare i dati in Application Insights</span><span class="sxs-lookup"><span data-stu-id="3f365-128">View the data in Application Insights</span></span>
<span data-ttu-id="3f365-129">Nella risorsa di Application Insights aprire [Esplora metriche e aggiungere grafici][metrics], selezionando le metriche da visualizzare dalla categoria personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3f365-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="3f365-130">Per impostazione predefinita, le metriche vengono aggregate per tutti i computer host da cui vengono raccolte le metriche.</span><span class="sxs-lookup"><span data-stu-id="3f365-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span></span> <span data-ttu-id="3f365-131">Per visualizzare le metriche dei singoli host, nel pannello di dettagli del grafico attivare l'opzione Raggruppamento e quindi scegliere di eseguire il raggruppamento in base a CollectD-Host.</span><span class="sxs-lookup"><span data-stu-id="3f365-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span></span>

## <a name="to-exclude-upload-of-specific-statistics"></a><span data-ttu-id="3f365-132">Per escludere il caricamento di statistiche specifiche</span><span class="sxs-lookup"><span data-stu-id="3f365-132">To exclude upload of specific statistics</span></span>
<span data-ttu-id="3f365-133">Per impostazione predefinita, il plug-in di Application Insights invia tutti i dati raccolti da tutti i plug-in di tipo 'read' di collectd.</span><span class="sxs-lookup"><span data-stu-id="3f365-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="3f365-134">Per escludere dati da plug-in specifici oppure origini dati specifiche:</span><span class="sxs-lookup"><span data-stu-id="3f365-134">To exclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="3f365-135">Modificare il file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3f365-135">Edit the configuration file.</span></span> 
* <span data-ttu-id="3f365-136">In `<Plugin ApplicationInsightsWriter>`aggiungere righe di direttive analoghe alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="3f365-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="3f365-137">Direttiva</span><span class="sxs-lookup"><span data-stu-id="3f365-137">Directive</span></span> | <span data-ttu-id="3f365-138">Effetto</span><span class="sxs-lookup"><span data-stu-id="3f365-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="3f365-139">Esclusione di tutti i dati raccolti dal plug-in `disk` .</span><span class="sxs-lookup"><span data-stu-id="3f365-139">Exclude all data collected by the `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="3f365-140">Esclusione delle origini denominate `read` e `write` dal plug-in `disk`.</span><span class="sxs-lookup"><span data-stu-id="3f365-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span></span> |

<span data-ttu-id="3f365-141">Separare le direttive con un valore NewLine.</span><span class="sxs-lookup"><span data-stu-id="3f365-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="3f365-142">Problemi?</span><span class="sxs-lookup"><span data-stu-id="3f365-142">Problems?</span></span>
<span data-ttu-id="3f365-143">*I dati non vengono visualizzati nel portale*</span><span class="sxs-lookup"><span data-stu-id="3f365-143">*I don't see data in the portal*</span></span>

* <span data-ttu-id="3f365-144">Aprire [Cerca][diagnostic] per verificare se gli eventi non elaborati sono stati ricevuti.</span><span class="sxs-lookup"><span data-stu-id="3f365-144">Open [Search][diagnostic] to see if the raw events have arrived.</span></span> <span data-ttu-id="3f365-145">In alcuni casi necessitano di più tempo per la visualizzazione in Esplora metriche.</span><span class="sxs-lookup"><span data-stu-id="3f365-145">Sometimes they take longer to appear in metrics explorer.</span></span>
* <span data-ttu-id="3f365-146">Potrebbe essere necessario [impostare le eccezioni del firewall per i dati in uscita](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="3f365-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="3f365-147">Abilitare la traccia nel plug-in di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3f365-147">Enable tracing in the Application Insights plugin.</span></span> <span data-ttu-id="3f365-148">Aggiungere questa riga in `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="3f365-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="3f365-149">Aprire un terminale e avviare collectd in modalità dettagliata, per visualizzare eventuali problemi segnalati:</span><span class="sxs-lookup"><span data-stu-id="3f365-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="3f365-150">Problema noto</span><span class="sxs-lookup"><span data-stu-id="3f365-150">Known issue</span></span>

<span data-ttu-id="3f365-151">Il plug-in di scrittura di Application Insights non è compatibile con alcuni plug-in di lettura.</span><span class="sxs-lookup"><span data-stu-id="3f365-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="3f365-152">Alcuni plug-in a volte inviano un errore "non un numero" quando il plug-in di Application Insights prevede un numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="3f365-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="3f365-153">Sintomo: Il log di collectd visualizza errori che includono "AI:... SyntaxError: N token non previsto".</span><span class="sxs-lookup"><span data-stu-id="3f365-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="3f365-154">Soluzione alternativa: escludere i dati raccolti dal plug-in di scrittura che causa il problema.</span><span class="sxs-lookup"><span data-stu-id="3f365-154">Workaround: Exclude data collected by the problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


