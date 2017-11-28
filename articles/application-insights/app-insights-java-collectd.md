---
title: prestazioni dell'applicazione web Java su Linux - Azure aaaMonitor | Documenti Microsoft
description: Estendere l'applicazione monitoraggio delle prestazioni del sito Web Java con hello CollectD plug-in per Application Insights.
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
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="a1f06-103">collectd: metriche delle prestazioni Linux in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a1f06-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="a1f06-104">tooexplore le metriche delle prestazioni di sistema di Linux in [Application Insights](app-insights-overview.md), installare [collectd](http://collectd.org/), insieme con il plug-in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a1f06-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="a1f06-105">Questa soluzione open source raccoglie diverse che relative al sistema e alla rete.</span><span class="sxs-lookup"><span data-stu-id="a1f06-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="a1f06-106">In genere, si usa collectd se è già stato [instrumentato il servizio Web Java con Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="a1f06-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="a1f06-107">Consente di definire ulteriori dati toohelp si tooenhance le prestazioni dell'app o diagnosticare problemi.</span><span class="sxs-lookup"><span data-stu-id="a1f06-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![Grafici di esempio](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="a1f06-109">Ottenere la chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="a1f06-109">Get your instrumentation key</span></span>
<span data-ttu-id="a1f06-110">In hello [portale Microsoft Azure](https://portal.azure.com)aprire hello [Application Insights](app-insights-overview.md) risorsa in cui si desidera tooappear dati hello.</span><span class="sxs-lookup"><span data-stu-id="a1f06-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="a1f06-111">In alternativa, [creare una nuova risorsa](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a1f06-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="a1f06-112">Eseguire una copia della chiave di strumentazione hello, che identifica una risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="a1f06-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![Sfoglia tutto, aprire la risorsa e quindi nell'elenco a discesa Essentials hello, selezionare e copiare hello chiave di strumentazione](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="a1f06-114">Installare collectd e hello plug-in</span><span class="sxs-lookup"><span data-stu-id="a1f06-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="a1f06-115">Nei computer server Linux:</span><span class="sxs-lookup"><span data-stu-id="a1f06-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="a1f06-116">Installare [collectd](http://collectd.org/) versione 5.4.0 o successive.</span><span class="sxs-lookup"><span data-stu-id="a1f06-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="a1f06-117">Scaricare hello [plug-in Application Insights collectd writer](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="a1f06-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="a1f06-118">Si noti il numero di versione di hello.</span><span class="sxs-lookup"><span data-stu-id="a1f06-118">Note hello version number.</span></span>
3. <span data-ttu-id="a1f06-119">Copiare i plug-in di hello JAR in `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="a1f06-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="a1f06-120">Modificare `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="a1f06-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="a1f06-121">Verificare che [hello plug-in Java](https://collectd.org/wiki/index.php/Plugin:Java) è abilitata.</span><span class="sxs-lookup"><span data-stu-id="a1f06-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="a1f06-122">Aggiornare hello JVMArg per hello di tooinclude java.class.path hello JAR seguenti.</span><span class="sxs-lookup"><span data-stu-id="a1f06-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="a1f06-123">Aggiornare hello versione numero toomatch hello che uno è stato scaricato:</span><span class="sxs-lookup"><span data-stu-id="a1f06-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="a1f06-124">Aggiungere questo frammento di codice, con chiave di strumentazione di hello dalla risorsa:</span><span class="sxs-lookup"><span data-stu-id="a1f06-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="a1f06-125">Di seguito è riportata una parte di un file di configurazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="a1f06-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="a1f06-126">Configurare altri [plug-in collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), che possono raccogliere diversi dati da origini diverse.</span><span class="sxs-lookup"><span data-stu-id="a1f06-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="a1f06-127">Riavviare in base tooits collectd [manuale](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="a1f06-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="a1f06-128">Visualizzare i dati di hello in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a1f06-128">View hello data in Application Insights</span></span>
<span data-ttu-id="a1f06-129">Nella risorsa di Application Insights, aprire [Esplora metriche e aggiungere grafici][metrics], selezione metriche hello da toosee dalla categoria personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="a1f06-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="a1f06-130">Per impostazione predefinita, le metriche hello vengono aggregate in tutti i computer host da cui sono state raccolte le metriche di hello.</span><span class="sxs-lookup"><span data-stu-id="a1f06-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="a1f06-131">le metriche di hello tooview per ogni host, nel pannello dettagli grafico di hello, attivare il raggruppamento e quindi scegliere toogroup CollectD host.</span><span class="sxs-lookup"><span data-stu-id="a1f06-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="a1f06-132">caricamento di tooexclude di statistiche specifiche</span><span class="sxs-lookup"><span data-stu-id="a1f06-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="a1f06-133">Per impostazione predefinita, i plug-in Application Insights hello invia tutti i dati di hello raccolti da tutti hello abilitato collectd 'read' plug-in.</span><span class="sxs-lookup"><span data-stu-id="a1f06-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="a1f06-134">tooexclude dati da origini dati o i plug-in specifici:</span><span class="sxs-lookup"><span data-stu-id="a1f06-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="a1f06-135">Modificare il file di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a1f06-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="a1f06-136">In `<Plugin ApplicationInsightsWriter>`aggiungere righe di direttive analoghe alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="a1f06-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="a1f06-137">Direttiva</span><span class="sxs-lookup"><span data-stu-id="a1f06-137">Directive</span></span> | <span data-ttu-id="a1f06-138">Effetto</span><span class="sxs-lookup"><span data-stu-id="a1f06-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="a1f06-139">Escludere tutti i dati raccolti da hello `disk` plug-in</span><span class="sxs-lookup"><span data-stu-id="a1f06-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="a1f06-140">Esclusione di origini di hello denominate `read` e `write` da hello `disk` plug-in.</span><span class="sxs-lookup"><span data-stu-id="a1f06-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="a1f06-141">Separare le direttive con un valore NewLine.</span><span class="sxs-lookup"><span data-stu-id="a1f06-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="a1f06-142">Problemi?</span><span class="sxs-lookup"><span data-stu-id="a1f06-142">Problems?</span></span>
<span data-ttu-id="a1f06-143">*Non è possibile visualizzare dati nel portale di hello*</span><span class="sxs-lookup"><span data-stu-id="a1f06-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="a1f06-144">Aprire [ricerca] [ diagnostic] toosee se sono arrivato eventi non elaborati hello.</span><span class="sxs-lookup"><span data-stu-id="a1f06-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="a1f06-145">In alcuni casi hanno più tooappear in Esplora metriche.</span><span class="sxs-lookup"><span data-stu-id="a1f06-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="a1f06-146">Potrebbe essere troppo[impostare le eccezioni del firewall per i dati in uscita](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="a1f06-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="a1f06-147">Abilitare la traccia nel plug-in Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="a1f06-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="a1f06-148">Aggiungere questa riga in `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="a1f06-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="a1f06-149">Aprire un terminale e avviare collectd in modalità dettagliata, toosee eventuali problemi che sta inviando report:</span><span class="sxs-lookup"><span data-stu-id="a1f06-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="a1f06-150">Problema noto</span><span class="sxs-lookup"><span data-stu-id="a1f06-150">Known issue</span></span>

<span data-ttu-id="a1f06-151">Hello Application Insights scrivere plug-in non è compatibile con alcuni plug-in lettura.</span><span class="sxs-lookup"><span data-stu-id="a1f06-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="a1f06-152">Alcuni plug-in di trasmissione talvolta "NaN" a cui i plug-in Application Insights hello prevede un numero a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="a1f06-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="a1f06-153">Sintomo: log collectd hello Mostra gli errori che includono "AI:... SyntaxError: N token non previsto".</span><span class="sxs-lookup"><span data-stu-id="a1f06-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="a1f06-154">Soluzione alternativa: Escludere i dati raccolti dai plug-in di hello problema scrittura.</span><span class="sxs-lookup"><span data-stu-id="a1f06-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


