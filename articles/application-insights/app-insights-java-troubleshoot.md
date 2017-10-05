---
title: Risoluzione dei problemi di Application Insights in un progetto Web Java
description: Guida per la risoluzione dei problemi - monitoraggio di app Java live con Application Insights.
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="396d3-103">Risoluzione dei problemi e domande e risposte relative ad Application Insights per Java</span><span class="sxs-lookup"><span data-stu-id="396d3-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="396d3-104">Domande o problemi relativi ad [Azure Application Insights in Java][java]?</span><span class="sxs-lookup"><span data-stu-id="396d3-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="396d3-105">Ecco alcuni suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="396d3-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="396d3-106">Errori di compilazione</span><span class="sxs-lookup"><span data-stu-id="396d3-106">Build errors</span></span>
<span data-ttu-id="396d3-107">**Quando si aggiunge Application Insights SDK in Eclipse tramite Maven o Gradle, vengono visualizzati errori di convalida relativi a compilazione o checksum.**</span><span class="sxs-lookup"><span data-stu-id="396d3-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="396d3-108">Se l'elemento di dipendenza <version> usa un criterio di ricerca con caratteri jolly, ad esempio (Maven) `<version>[1.0,)</version>` o (Gradle) `version:'1.0.+'`, provare a indicare una versione specifica, come `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="396d3-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="396d3-109">Vedere le [note sulla versione](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) per la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="396d3-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="396d3-110">Dati non presenti</span><span class="sxs-lookup"><span data-stu-id="396d3-110">No data</span></span>
<span data-ttu-id="396d3-111">**Dopo avere aggiunto Application Insights correttamente ed avere eseguito l'app, nel portale non vengono visualizzati dati.**</span><span class="sxs-lookup"><span data-stu-id="396d3-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="396d3-112">Attendere un minuto, quindi fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="396d3-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="396d3-113">I grafici si aggiornano autonomamente periodicamente, ma è anche possibile aggiornare manualmente.</span><span class="sxs-lookup"><span data-stu-id="396d3-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="396d3-114">L'intervallo di aggiornamento dipende dall'intervallo di tempo del grafico.</span><span class="sxs-lookup"><span data-stu-id="396d3-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="396d3-115">Verificare di disporre di una chiave di strumentazione definita nel file ApplicationInsights.xml (presente nella cartella resources del progetto).</span><span class="sxs-lookup"><span data-stu-id="396d3-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="396d3-116">Verificare che non vi siano nodi `<DisableTelemetry>true</DisableTelemetry>` nel file XML.</span><span class="sxs-lookup"><span data-stu-id="396d3-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="396d3-117">Nel firewall, potrebbe essere necessario aprire le porte TCP 80 e 443 per il traffico in uscita verso dc.services.visualstudio.com. Vedere l' [elenco completo delle eccezioni del firewall](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="396d3-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="396d3-118">Nella schermata iniziale di Microsoft Azure osservare la mappa dello stato dei servizi.</span><span class="sxs-lookup"><span data-stu-id="396d3-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="396d3-119">Se ci sono indicazioni di avviso, attendere che tornino alla normalità, quindi chiudere e riaprire il pannello dell'applicazione di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="396d3-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="396d3-120">Attivare la registrazione nella finestra della console IDE aggiungendo un elemento `<SDKLogger />` sotto il nodo radice nel file ApplicationInsights.xml (nella cartella resources del progetto) e verificare la presenza di voci con prefisso [Error].</span><span class="sxs-lookup"><span data-stu-id="396d3-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="396d3-121">Per verificare che Java SDK abbia caricato il file ApplicationInsights.xml corretto, esaminare i messaggi di output della console e cercare il messaggio "Configuration file has been successfully found".</span><span class="sxs-lookup"><span data-stu-id="396d3-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="396d3-122">Se il file di configurazione non è stato trovato, verificare i percorsi di ricerca di questo file nei messaggi di output e assicurarsi che il file ApplicationInsights.xml sia memorizzato in uno di tali percorsi.</span><span class="sxs-lookup"><span data-stu-id="396d3-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="396d3-123">In linea di massima, il file di configurazione può essere salvato accanto ai file JAR di Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="396d3-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="396d3-124">In Tomcat, ad esempio, questo percorso corrisponde alla cartella WEB-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="396d3-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="396d3-125">Non vengono più visualizzati i dati disponibili in precedenza</span><span class="sxs-lookup"><span data-stu-id="396d3-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="396d3-126">Controllare il [blog sullo stato](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="396d3-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="396d3-127">È stata raggiunta la quota mensile relativa ai punti dati?</span><span class="sxs-lookup"><span data-stu-id="396d3-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="396d3-128">Per saperlo, aprire Impostazioni/Quota e Prezzi. Se la quota è stata raggiunta, è possibile aggiornare il piano oppure pagare per disporre di ulteriore capacità.</span><span class="sxs-lookup"><span data-stu-id="396d3-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="396d3-129">Vedere lo [schema dei prezzi](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="396d3-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="396d3-130">Non sono presenti tutti i dati previsti</span><span class="sxs-lookup"><span data-stu-id="396d3-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="396d3-131">Aprire il pannello Quota + prezzi e verificare se il [campionamento](app-insights-sampling.md) è abilitato.</span><span class="sxs-lookup"><span data-stu-id="396d3-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="396d3-132">La trasmissione al 100% indica che il campionamento non è abilitato. È possibile impostare il servizio Application Insights in modo che vengano accettati soltanto i dati di telemetria provenienti dall'app.</span><span class="sxs-lookup"><span data-stu-id="396d3-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="396d3-133">Ciò permette di evitare il superamento della quota mensile.</span><span class="sxs-lookup"><span data-stu-id="396d3-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="396d3-134">Dati di utilizzo non presenti</span><span class="sxs-lookup"><span data-stu-id="396d3-134">No usage data</span></span>
<span data-ttu-id="396d3-135">**I dati relativi a richieste e tempi di risposta vengono visualizzati, ma non sono presenti dati relativi alla visualizzazione di pagine, ai browser o dati relativi agli utenti.**</span><span class="sxs-lookup"><span data-stu-id="396d3-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="396d3-136">L'app è stata correttamente configurata per inviare dati di telemetria dal server.</span><span class="sxs-lookup"><span data-stu-id="396d3-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="396d3-137">Il passaggio successivo consiste nel [configurare le pagine Web per inviare dati di telemetria dal Web browser][usage].</span><span class="sxs-lookup"><span data-stu-id="396d3-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="396d3-138">In alternativa, se il client è un'app in un [telefono o altro dispositivo][platforms], è possibile inviare i dati di telemetria da tali dispositivi.</span><span class="sxs-lookup"><span data-stu-id="396d3-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="396d3-139">Usare la chiave di strumentazione per impostare la telemetria sia sul client che sul server.</span><span class="sxs-lookup"><span data-stu-id="396d3-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="396d3-140">I dati verranno visualizzati nella stessa risorsa di Application Insights e sarà possibile correlare eventi dal client e dal server.</span><span class="sxs-lookup"><span data-stu-id="396d3-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="396d3-141">Disabilitazione della telemetria</span><span class="sxs-lookup"><span data-stu-id="396d3-141">Disabling telemetry</span></span>
<span data-ttu-id="396d3-142">**In che modo è possibile disabilitare la raccolta di dati di telemetria?**</span><span class="sxs-lookup"><span data-stu-id="396d3-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="396d3-143">Nel codice:</span><span class="sxs-lookup"><span data-stu-id="396d3-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="396d3-144">**Oppure**</span><span class="sxs-lookup"><span data-stu-id="396d3-144">**Or**</span></span> 

<span data-ttu-id="396d3-145">Aggiornare ApplicationInsights.xml (nella cartella resources del progetto).</span><span class="sxs-lookup"><span data-stu-id="396d3-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="396d3-146">Aggiungere la riga seguente sotto il nodo radice:</span><span class="sxs-lookup"><span data-stu-id="396d3-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="396d3-147">Usando il metodo XML, dopo la modifica di questo valore sarà necessario riavviare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="396d3-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="396d3-148">Modifica della destinazione</span><span class="sxs-lookup"><span data-stu-id="396d3-148">Changing the target</span></span>
<span data-ttu-id="396d3-149">**In che modo è possibile modificare la risorsa di Azure che riceve i dati del progetto?**</span><span class="sxs-lookup"><span data-stu-id="396d3-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="396d3-150">[Ottenere la chiave di strumentazione della nuova risorsa][java].</span><span class="sxs-lookup"><span data-stu-id="396d3-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="396d3-151">Se si è aggiunto Application Insights al progetto usando Azure Toolkit for Eclipse, fare clic con il pulsante destro del mouse sul progetto Web, selezionare **Azure**, **Configura Application Insights**, quindi modificare la chiave.</span><span class="sxs-lookup"><span data-stu-id="396d3-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="396d3-152">Oppure, aggiornare la chiave nel file ApplicationInsights.xml presente nella cartella resources del progetto.</span><span class="sxs-lookup"><span data-stu-id="396d3-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="396d3-153">Debug dei dati dall'SDK</span><span class="sxs-lookup"><span data-stu-id="396d3-153">Debug data from the SDK</span></span>

<span data-ttu-id="396d3-154">**Come ottenere informazioni sulle attività dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="396d3-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="396d3-155">Per ottenere altre informazioni su quello che accade nell'API, aggiungere `<SDKLogger/>` sotto il nodo radice del file di configurazione ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="396d3-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="396d3-156">È anche possibile impostare il logger perché fornisca un file di output:</span><span class="sxs-lookup"><span data-stu-id="396d3-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="396d3-157">I file si trovano in `%temp%\javasdklogs` o `java.io.tmpdir` nel caso di un server Tomcat.</span><span class="sxs-lookup"><span data-stu-id="396d3-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="396d3-158">Schermata iniziale di Azure</span><span class="sxs-lookup"><span data-stu-id="396d3-158">The Azure start screen</span></span>
<span data-ttu-id="396d3-159">**Guardando nel [portale di Azure](https://portal.azure.com). la mappa contiene informazioni sull'app?**</span><span class="sxs-lookup"><span data-stu-id="396d3-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="396d3-160">No, la mappa visualizza lo stato di integrità dei server Azure nelle varie parti del mondo.</span><span class="sxs-lookup"><span data-stu-id="396d3-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="396d3-161">*Dalla schermata iniziale (home) di Azure, in che modo è possibile trovare i dati relativi all'app?*</span><span class="sxs-lookup"><span data-stu-id="396d3-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="396d3-162">Supponendo che [l'app sia stata impostata per Application Insights][java], fare clic su Esplora, selezionare Application Insights, quindi selezionare la risorsa dell'app creata per l'app specifica.</span><span class="sxs-lookup"><span data-stu-id="396d3-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="396d3-163">Per raggiungere questa area più velocemente in futuro, è possibile aggiungere l'app alla schermata iniziale.</span><span class="sxs-lookup"><span data-stu-id="396d3-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="396d3-164">Server Intranet</span><span class="sxs-lookup"><span data-stu-id="396d3-164">Intranet servers</span></span>
<span data-ttu-id="396d3-165">**È possibile monitorare un server nella Intranet?**</span><span class="sxs-lookup"><span data-stu-id="396d3-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="396d3-166">Sì, purché il server possa inviare dati di telemetria al portale di Application Insights tramite la rete Internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="396d3-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="396d3-167">Nel firewall, potrebbe essere necessario aprire le porte TCP 80 e 443 per il traffico in uscita verso dc.services.visualstudio.com e f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="396d3-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="396d3-168">Conservazione dei dati</span><span class="sxs-lookup"><span data-stu-id="396d3-168">Data retention</span></span>
<span data-ttu-id="396d3-169">**Per quanto tempo vengono conservati i dati nel portale? Tale conservazione è sicura?**</span><span class="sxs-lookup"><span data-stu-id="396d3-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="396d3-170">Vedere [Conservazione dei dati e privacy][data].</span><span class="sxs-lookup"><span data-stu-id="396d3-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="396d3-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="396d3-171">Next steps</span></span>
<span data-ttu-id="396d3-172">**Application Insights è stato correttamente impostato per l'app server Java. Cos'altro è possibile fare?**</span><span class="sxs-lookup"><span data-stu-id="396d3-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="396d3-173">[Monitorare la disponibilità delle pagine Web][availability]</span><span class="sxs-lookup"><span data-stu-id="396d3-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="396d3-174">[Monitorare l'utilizzo delle pagine Web][usage]</span><span class="sxs-lookup"><span data-stu-id="396d3-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="396d3-175">[Tenere traccia dell'utilizzo delle app per dispositivi e diagnosticarne i problemi][platforms]</span><span class="sxs-lookup"><span data-stu-id="396d3-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="396d3-176">[Scrivere codice per tenere traccia dell'utilizzo dell'app][track]</span><span class="sxs-lookup"><span data-stu-id="396d3-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="396d3-177">[Acquisire i log di diagnostica][javalogs]</span><span class="sxs-lookup"><span data-stu-id="396d3-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="396d3-178">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="396d3-178">Get help</span></span>
* [<span data-ttu-id="396d3-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="396d3-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

