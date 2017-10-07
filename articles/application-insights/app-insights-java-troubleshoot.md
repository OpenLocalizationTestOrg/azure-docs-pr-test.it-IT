---
title: aaaTroubleshoot Application Insights in un progetto web Java
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
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="a0c99-103">Risoluzione dei problemi e domande e risposte relative ad Application Insights per Java</span><span class="sxs-lookup"><span data-stu-id="a0c99-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="a0c99-104">Domande o problemi relativi ad [Azure Application Insights in Java][java]?</span><span class="sxs-lookup"><span data-stu-id="a0c99-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="a0c99-105">Ecco alcuni suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="a0c99-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="a0c99-106">Errori di compilazione</span><span class="sxs-lookup"><span data-stu-id="a0c99-106">Build errors</span></span>
<span data-ttu-id="a0c99-107">**In Eclipse, durante l'aggiunta di hello Application Insights SDK tramite Maven o Gradle, ottenere gli errori di convalida di checksum o di compilazione.**</span><span class="sxs-lookup"><span data-stu-id="a0c99-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="a0c99-108">Se hello dipendenza <version> elemento viene usato un modello con caratteri jolly (ad esempio (Maven) `<version>[1.0,)</version>` (Gradle) o `version:'1.0.+'`), provare a specificare invece una versione specifica come `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="a0c99-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="a0c99-109">Vedere hello [note sulla versione](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) per la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="a0c99-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="a0c99-110">Dati non presenti</span><span class="sxs-lookup"><span data-stu-id="a0c99-110">No data</span></span>
<span data-ttu-id="a0c99-111">**È stato aggiunto correttamente Application Insights ed è stata eseguita l'applicazione, ma non ho potuto osservare i dati nel portale di hello.**</span><span class="sxs-lookup"><span data-stu-id="a0c99-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="a0c99-112">Attendere un minuto, quindi fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="a0c99-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="a0c99-113">grafici di Hello Aggiorna periodicamente se stessi, ma è anche possibile aggiornare manualmente.</span><span class="sxs-lookup"><span data-stu-id="a0c99-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="a0c99-114">intervallo di aggiornamento Hello dipende dall'intervallo di tempo hello del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="a0c99-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="a0c99-115">Verificare di disporre di una chiave di strumentazione definita nel file ApplicationInsights.xml hello (nella cartella delle risorse hello del progetto)</span><span class="sxs-lookup"><span data-stu-id="a0c99-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="a0c99-116">Verificare che sia presente alcun `<DisableTelemetry>true</DisableTelemetry>` nodo nel file xml di hello.</span><span class="sxs-lookup"><span data-stu-id="a0c99-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="a0c99-117">Nel firewall, potrebbe essere tooopen le porte TCP 80 e 443 per toodc.services.visualstudio.com il traffico in uscita. Vedere hello [elenco completo delle eccezioni del firewall](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="a0c99-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="a0c99-118">In Microsoft Azure hello avviare discussioni ed esaminare mappa lo stato del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a0c99-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="a0c99-119">Se sono presenti alcune indicazioni relative all'avviso, attendere hanno restituito tooOK e quindi chiudere e riaprire il pannello di applicazioni di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a0c99-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="a0c99-120">Attivare la registrazione di finestra della console toohello IDE, aggiungendo un `<SDKLogger />` elemento sotto il nodo radice hello nel file ApplicationInsights.xml hello (nella cartella delle risorse hello del progetto) e cercare voci preceduti da [errore].</span><span class="sxs-lookup"><span data-stu-id="a0c99-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="a0c99-121">Verificare che tale hello corretto ApplicationInsights.xml file è stato caricato correttamente da hello SDK per Java, esaminando i messaggi di output della console hello per un'istruzione "file di configurazione è stato trovato".</span><span class="sxs-lookup"><span data-stu-id="a0c99-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="a0c99-122">Se non viene trovato il file di configurazione di hello, hello toosee di messaggi di output in cui viene cercato il file di configurazione di hello per verificare e assicurarsi che tale hello che applicationinsights.XML si trova in uno di questi percorsi di ricerca.</span><span class="sxs-lookup"><span data-stu-id="a0c99-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="a0c99-123">Come regola generale, è possibile inserire il file di configurazione hello quasi file JAR di hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="a0c99-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="a0c99-124">Ad esempio: in Tomcat, ciò significa hello cartella WEB-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="a0c99-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="a0c99-125">Utilizzato toosee dati, ma è stato arrestato</span><span class="sxs-lookup"><span data-stu-id="a0c99-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="a0c99-126">Controllare hello [stato blog](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="a0c99-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="a0c99-127">È stata raggiunta la quota mensile relativa ai punti dati?</span><span class="sxs-lookup"><span data-stu-id="a0c99-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="a0c99-128">Aprire impostazioni/quote e prezzi toofind out. Se la quota è stata raggiunta, è possibile aggiornare il piano oppure pagare per disporre di ulteriore capacità.</span><span class="sxs-lookup"><span data-stu-id="a0c99-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="a0c99-129">Vedere hello [prezzi schema](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="a0c99-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="a0c99-130">Non ho tutti i dati di hello che consapevole previsto</span><span class="sxs-lookup"><span data-stu-id="a0c99-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="a0c99-131">Aprire hello quote e prezzi blade e controllare se [campionamento](app-insights-sampling.md) è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a0c99-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="a0c99-132">(trasmissione 100% significa che il campionamento non è nell'operazione). Hello servizio Application Insights può essere set tooaccept solo una frazione di telemetria hello in arrivo dall'app.</span><span class="sxs-lookup"><span data-stu-id="a0c99-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="a0c99-133">Ciò permette di evitare il superamento della quota mensile.</span><span class="sxs-lookup"><span data-stu-id="a0c99-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="a0c99-134">Dati di utilizzo non presenti</span><span class="sxs-lookup"><span data-stu-id="a0c99-134">No usage data</span></span>
<span data-ttu-id="a0c99-135">**I dati relativi a richieste e tempi di risposta vengono visualizzati, ma non sono presenti dati relativi alla visualizzazione di pagine, ai browser o dati relativi agli utenti.**</span><span class="sxs-lookup"><span data-stu-id="a0c99-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="a0c99-136">I dati di telemetria toosend app è stato configurato dal server hello.</span><span class="sxs-lookup"><span data-stu-id="a0c99-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="a0c99-137">Dopo il passaggio successivo è troppo[impostare dati di telemetria toosend pagine web da browser hello][usage].</span><span class="sxs-lookup"><span data-stu-id="a0c99-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="a0c99-138">In alternativa, se il client è un'app in un [telefono o altro dispositivo][platforms], è possibile inviare i dati di telemetria da tali dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a0c99-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="a0c99-139">Utilizzare hello stesso tooset chiave di strumentazione di telemetria del client e server.</span><span class="sxs-lookup"><span data-stu-id="a0c99-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="a0c99-140">dati Hello verranno visualizzata nella stessa risorsa di Application Insights hello e sarà in grado di toocorrelate eventi dal client e server.</span><span class="sxs-lookup"><span data-stu-id="a0c99-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="a0c99-141">Disabilitazione della telemetria</span><span class="sxs-lookup"><span data-stu-id="a0c99-141">Disabling telemetry</span></span>
<span data-ttu-id="a0c99-142">**In che modo è possibile disabilitare la raccolta di dati di telemetria?**</span><span class="sxs-lookup"><span data-stu-id="a0c99-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="a0c99-143">Nel codice:</span><span class="sxs-lookup"><span data-stu-id="a0c99-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="a0c99-144">**Oppure**</span><span class="sxs-lookup"><span data-stu-id="a0c99-144">**Or**</span></span> 

<span data-ttu-id="a0c99-145">Aggiornare ApplicationInsights.xml (nella cartella delle risorse hello del progetto).</span><span class="sxs-lookup"><span data-stu-id="a0c99-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="a0c99-146">Aggiungere il seguente hello nel nodo radice hello:</span><span class="sxs-lookup"><span data-stu-id="a0c99-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="a0c99-147">Metodo XML hello è un'applicazione hello toorestart quando si modifica il valore di hello.</span><span class="sxs-lookup"><span data-stu-id="a0c99-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="a0c99-148">Modifica della destinazione di hello</span><span class="sxs-lookup"><span data-stu-id="a0c99-148">Changing hello target</span></span>
<span data-ttu-id="a0c99-149">**In che modo è possibile modificare la risorsa di Azure che riceve i dati del progetto?**</span><span class="sxs-lookup"><span data-stu-id="a0c99-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="a0c99-150">[Ottenere la chiave di strumentazione hello della nuova risorsa hello.][java]</span><span class="sxs-lookup"><span data-stu-id="a0c99-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="a0c99-151">Se è stato aggiunto il progetto di tooyour Application Insights usando hello Azure Toolkit per Eclipse, fare clic con il pulsante destro del progetto web, selezionare **Azure**, **Configura Application Insights**e modificare la chiave hello.</span><span class="sxs-lookup"><span data-stu-id="a0c99-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="a0c99-152">In caso contrario, aggiornare la chiave hello ApplicationInsights.xml nella cartella risorse hello nel progetto.</span><span class="sxs-lookup"><span data-stu-id="a0c99-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="a0c99-153">Debug dei dati da hello SDK</span><span class="sxs-lookup"><span data-stu-id="a0c99-153">Debug data from hello SDK</span></span>

<span data-ttu-id="a0c99-154">**Come è possibile scoprire quali hello esegue SDK?**</span><span class="sxs-lookup"><span data-stu-id="a0c99-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="a0c99-155">aggiungere ulteriori informazioni su cosa avviene nel hello API, tooget `<SDKLogger/>` sotto il nodo radice hello hello ApplicationInsights.xml del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a0c99-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="a0c99-156">È anche possibile indicare file tooa toooutput del logger di hello:</span><span class="sxs-lookup"><span data-stu-id="a0c99-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="a0c99-157">file Hello sono reperibile nella `%temp%\javasdklogs` o `java.io.tmpdir` in caso di server Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a0c99-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="a0c99-158">schermata di avvio Azure Hello</span><span class="sxs-lookup"><span data-stu-id="a0c99-158">hello Azure start screen</span></span>
<span data-ttu-id="a0c99-159">**Osservando [hello Azure portal](https://portal.azure.com). Mappa hello indica un elemento mia applicazione?**</span><span class="sxs-lookup"><span data-stu-id="a0c99-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="a0c99-160">No, Mostra stato hello del server Azure tutto il mondo hello.</span><span class="sxs-lookup"><span data-stu-id="a0c99-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="a0c99-161">*Dalla scheda Azure inizio hello (schermata iniziale), come è possibile individuare dati mia applicazione?*</span><span class="sxs-lookup"><span data-stu-id="a0c99-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="a0c99-162">Presupponendo che sia [impostare l'app per Application Insights][java], fare clic su Sfoglia, selezionare Application Insights e selezionare hello app risorsa creata per l'app.</span><span class="sxs-lookup"><span data-stu-id="a0c99-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="a0c99-163">tooget non esiste più velocemente in futuro, è possibile aggiungere la scheda avvio toohello di app.</span><span class="sxs-lookup"><span data-stu-id="a0c99-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="a0c99-164">Server Intranet</span><span class="sxs-lookup"><span data-stu-id="a0c99-164">Intranet servers</span></span>
<span data-ttu-id="a0c99-165">**È possibile monitorare un server nella Intranet?**</span><span class="sxs-lookup"><span data-stu-id="a0c99-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="a0c99-166">Sì, purché il server può inviare portale Application Insights toohello di telemetria tramite hello rete internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="a0c99-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="a0c99-167">Nel firewall, potrebbe essere tooopen le porte TCP 80 e 443 per toodc.services.visualstudio.com il traffico in uscita e f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="a0c99-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="a0c99-168">Conservazione dei dati</span><span class="sxs-lookup"><span data-stu-id="a0c99-168">Data retention</span></span>
<span data-ttu-id="a0c99-169">**Quanto tempo i dati verranno mantenuti nel portale di hello? Tale conservazione è sicura?**</span><span class="sxs-lookup"><span data-stu-id="a0c99-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="a0c99-170">Vedere [Conservazione dei dati e privacy][data].</span><span class="sxs-lookup"><span data-stu-id="a0c99-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0c99-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0c99-171">Next steps</span></span>
<span data-ttu-id="a0c99-172">**Application Insights è stato correttamente impostato per l'app server Java. Cos'altro è possibile fare?**</span><span class="sxs-lookup"><span data-stu-id="a0c99-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="a0c99-173">[Monitorare la disponibilità delle pagine Web][availability]</span><span class="sxs-lookup"><span data-stu-id="a0c99-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="a0c99-174">[Monitorare l'utilizzo delle pagine Web][usage]</span><span class="sxs-lookup"><span data-stu-id="a0c99-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="a0c99-175">[Tenere traccia dell'utilizzo delle app per dispositivi e diagnosticarne i problemi][platforms]</span><span class="sxs-lookup"><span data-stu-id="a0c99-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="a0c99-176">[Scrivere tootrack utilizzo del codice dell'app][track]</span><span class="sxs-lookup"><span data-stu-id="a0c99-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="a0c99-177">[Acquisire i log di diagnostica][javalogs]</span><span class="sxs-lookup"><span data-stu-id="a0c99-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="a0c99-178">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="a0c99-178">Get help</span></span>
* [<span data-ttu-id="a0c99-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="a0c99-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

