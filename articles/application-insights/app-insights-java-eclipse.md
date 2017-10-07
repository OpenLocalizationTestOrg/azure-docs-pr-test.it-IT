---
title: aaaGet avviato con Application Insights di Azure con Java in Eclipse | Documenti Microsoft
description: Utilizzare hello prestazioni tooadd plug-in Eclipse e utilizzo di monitoraggio del sito Web Java tooyour con Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="3280a-103">Introduzione ad Application Insights con Java in Eclipse</span><span class="sxs-lookup"><span data-stu-id="3280a-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="3280a-104">Hello Application Insights SDK invia dati di telemetria dall'applicazione web Java, in modo che è possibile analizzare l'utilizzo e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3280a-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="3280a-105">plug-in per Application Insights Eclipse Hello installa automaticamente hello SDK nel progetto in modo che perdano la telemetria casella hello, oltre a un'API che è possibile utilizzare i dati di telemetria personalizzati toowrite.</span><span class="sxs-lookup"><span data-stu-id="3280a-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="3280a-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3280a-106">Prerequisites</span></span>
<span data-ttu-id="3280a-107">Attualmente hello plug-in funziona per i progetti Maven e i progetti Web dinamica in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3280a-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="3280a-108">([Progetto Java tipi tooother Aggiungi Application Insights][java].)</span><span class="sxs-lookup"><span data-stu-id="3280a-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="3280a-109">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3280a-109">You'll need:</span></span>

* <span data-ttu-id="3280a-110">Oracle JRE 1.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="3280a-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="3280a-111">Una sottoscrizione troppo[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="3280a-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="3280a-112">[Eclipse IDE per sviluppatori Java EE](http://www.eclipse.org/downloads/), Indigo o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3280a-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="3280a-113">Windows 7 o versioni successive o Windows Server 2008 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="3280a-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="3280a-114">Installare SDK hello in Eclipse (una volta)</span><span class="sxs-lookup"><span data-stu-id="3280a-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="3280a-115">È sufficiente toodo questo una volta per ogni computer.</span><span class="sxs-lookup"><span data-stu-id="3280a-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="3280a-116">Questo passaggio vengono installati un toolkit che può quindi aggiungere hello SDK tooeach progetto Web dinamico.</span><span class="sxs-lookup"><span data-stu-id="3280a-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="3280a-117">Dal menu Help di Eclipse scegliere Install New Software.</span><span class="sxs-lookup"><span data-stu-id="3280a-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Guida in linea, Installa nuovo Software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="3280a-119">Hello SDK è http://dl.microsoft.com/eclipse, in Azure Toolkit.</span><span class="sxs-lookup"><span data-stu-id="3280a-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="3280a-120">Deselezionare l'opzione **Contatta tutti i siti di aggiornamento...**</span><span class="sxs-lookup"><span data-stu-id="3280a-120">Uncheck **Contact all update sites...**</span></span>

    ![Per Application Insights SDK deselezionare tutti i siti di aggiornamento Contatta tutti](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="3280a-122">Seguire i rimanenti passaggi per ogni progetto Java hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="3280a-123">Creare una risorsa di Application Insights in Azure</span><span class="sxs-lookup"><span data-stu-id="3280a-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="3280a-124">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3280a-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3280a-125">Creare una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3280a-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="3280a-126">Impostare hello tipo tooJava applicazione web.</span><span class="sxs-lookup"><span data-stu-id="3280a-126">Set hello application type tooJava web application.</span></span>  

    ![Fare clic su + e scegliere Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="3280a-128">Trovare la chiave di strumentazione hello della nuova risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="3280a-129">È necessario toopaste nel progetto di codice a breve.</span><span class="sxs-lookup"><span data-stu-id="3280a-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="3280a-131">Aggiungere il progetto tooyour Application Insights</span><span class="sxs-lookup"><span data-stu-id="3280a-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="3280a-132">Aggiungi Application Insights dal menu di scelta rapida hello del progetto web Java.</span><span class="sxs-lookup"><span data-stu-id="3280a-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="3280a-134">Incollare una chiave di strumentazione hello recuperato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="3280a-136">chiave Hello viene inviata insieme a tutti gli elementi di dati di telemetria e indica toodisplay Application Insights nella risorsa.</span><span class="sxs-lookup"><span data-stu-id="3280a-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="3280a-137">Eseguire un'applicazione hello e visualizzare le metriche</span><span class="sxs-lookup"><span data-stu-id="3280a-137">Run hello application and see metrics</span></span>
<span data-ttu-id="3280a-138">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3280a-138">Run your application.</span></span>

<span data-ttu-id="3280a-139">Restituisce la risorsa di Application Insights tooyour in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3280a-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="3280a-140">Dati di richieste HTTP verranno visualizzati nel pannello della panoramica hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="3280a-141">Se non sono visualizzati, attendere alcuni secondi e quindi fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="3280a-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="3280a-142">Risposta del server, conteggi delle richieste ed errori</span><span class="sxs-lookup"><span data-stu-id="3280a-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="3280a-143">Fare clic su tramite qualsiasi toosee grafico le metriche dettagliate.</span><span class="sxs-lookup"><span data-stu-id="3280a-143">Click through any chart toosee more detailed metrics.</span></span>

![Numero di richieste per nome](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="3280a-145">[Altre informazioni sulle metriche.][metrics]</span><span class="sxs-lookup"><span data-stu-id="3280a-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="3280a-146">E, quando si visualizzano le proprietà di hello di una richiesta, è possibile visualizzare gli eventi di telemetria hello associati, ad esempio le richieste e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="3280a-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![Tutte le tracce per questa richiesta](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="3280a-148">Telemetria sul lato client</span><span class="sxs-lookup"><span data-stu-id="3280a-148">Client-side telemetry</span></span>
<span data-ttu-id="3280a-149">Pannello avvio rapido di hello, fare clic su Get codice toomonitor le pagine web:</span><span class="sxs-lookup"><span data-stu-id="3280a-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![Nel pannello della panoramica app, scegliere l'avvio rapido, ottenere codice toomonitor le pagine web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="3280a-152">Inserire il frammento di codice hello in head hello dei file HTML.</span><span class="sxs-lookup"><span data-stu-id="3280a-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="3280a-153">Visualizzare i dati lato client</span><span class="sxs-lookup"><span data-stu-id="3280a-153">View client-side data</span></span>
<span data-ttu-id="3280a-154">Aprire le pagine Web aggiornate e usarle.</span><span class="sxs-lookup"><span data-stu-id="3280a-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="3280a-155">Attendere qualche minuto, quindi tornare tooApplication approfondimenti e blade utilizzo hello aperto.</span><span class="sxs-lookup"><span data-stu-id="3280a-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="3280a-156">(Dal pannello della panoramica hello, scorrere verso il basso e fare clic su utilizzo)</span><span class="sxs-lookup"><span data-stu-id="3280a-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="3280a-157">Le metriche di visualizzazione, utente e della sessione di pagina verranno visualizzate nel Pannello di utilizzo di hello:</span><span class="sxs-lookup"><span data-stu-id="3280a-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![Sessioni, utenti e visualizzazioni pagina](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="3280a-159">[Altre informazioni sulla configurazione della telemetria sul lato client.][usage]</span><span class="sxs-lookup"><span data-stu-id="3280a-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="3280a-160">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="3280a-160">Publish your application</span></span>
<span data-ttu-id="3280a-161">Pubblicare il server toohello app, consentire alle persone che usano e guardare telemetria hello visualizzati nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="3280a-162">Verificare che il firewall consenta le porte di telemetria toothese toosend l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="3280a-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="3280a-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="3280a-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="3280a-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="3280a-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="3280a-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="3280a-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="3280a-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="3280a-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="3280a-167">Nei server Windows installare:</span><span class="sxs-lookup"><span data-stu-id="3280a-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="3280a-168">Microsoft Visual C++ Redistributable Package</span><span class="sxs-lookup"><span data-stu-id="3280a-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="3280a-169">(Ciò abilita i contatori delle prestazioni).</span><span class="sxs-lookup"><span data-stu-id="3280a-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="3280a-170">Eccezioni e richieste non eseguite</span><span class="sxs-lookup"><span data-stu-id="3280a-170">Exceptions and request failures</span></span>
<span data-ttu-id="3280a-171">Vengono raccolte automaticamente le eccezioni non gestite:</span><span class="sxs-lookup"><span data-stu-id="3280a-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="3280a-172">dati toocollect su altre eccezioni, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="3280a-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="3280a-173">[Inserire le chiamate nel codice tooTrackException](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="3280a-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="3280a-174">[Installare hello Java agente nel server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="3280a-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="3280a-175">Specificare i metodi di hello da toowatch.</span><span class="sxs-lookup"><span data-stu-id="3280a-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="3280a-176">Monitorare le chiamate al metodo e le dipendenze esterne</span><span class="sxs-lookup"><span data-stu-id="3280a-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="3280a-177">[Installare l'agente APM Java hello](app-insights-java-agent.md) toolog specificato metodi interni e le chiamate effettuate tramite JDBC, con dati di intervallo.</span><span class="sxs-lookup"><span data-stu-id="3280a-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="3280a-178">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="3280a-178">Performance counters</span></span>
<span data-ttu-id="3280a-179">Nel pannello della panoramica, scorrere verso il basso e fare clic su hello **server** riquadro.</span><span class="sxs-lookup"><span data-stu-id="3280a-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="3280a-180">Verrà visualizzato un intervallo di contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3280a-180">You'll see a range of performance counters.</span></span>

![Scorrere verso il basso riquadro server di hello tooclick](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="3280a-182">Personalizzare la raccolta del contatore delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="3280a-182">Customize performance counter collection</span></span>
<span data-ttu-id="3280a-183">toodisable raccolta di set di contatori delle prestazioni, standard di hello aggiungere hello seguente codice sotto il nodo radice hello del file ApplicationInsights.xml hello:</span><span class="sxs-lookup"><span data-stu-id="3280a-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="3280a-184">Raccogliere dei contatori di prestazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3280a-184">Collect additional performance counters</span></span>
<span data-ttu-id="3280a-185">È possibile specificare toobe i contatori delle prestazioni raccolti.</span><span class="sxs-lookup"><span data-stu-id="3280a-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="3280a-186">Contatori JMX (esposti da hello Java Virtual Machine)</span><span class="sxs-lookup"><span data-stu-id="3280a-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="3280a-187">`displayName`– nome hello visualizzato nel portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="3280a-188">`objectName`– nome dell'oggetto JMX hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="3280a-189">`attribute`: attributo hello di hello JMX oggetto nome toofetch</span><span class="sxs-lookup"><span data-stu-id="3280a-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="3280a-190">`type`(facoltativo): tipo di attributo dell'oggetto JMX hello:</span><span class="sxs-lookup"><span data-stu-id="3280a-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="3280a-191">Impostazione predefinita: un tipo semplice come int o long.</span><span class="sxs-lookup"><span data-stu-id="3280a-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="3280a-192">`composite`: i dati dei contatori delle prestazioni hello sono nel formato 'Attribute.Data' hello</span><span class="sxs-lookup"><span data-stu-id="3280a-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="3280a-193">`tabular`: i dati dei contatori delle prestazioni hello sono nel formato hello di una riga di tabella</span><span class="sxs-lookup"><span data-stu-id="3280a-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="3280a-194">Contatori delle prestazioni di Windows</span><span class="sxs-lookup"><span data-stu-id="3280a-194">Windows performance counters</span></span>
<span data-ttu-id="3280a-195">Ogni [contatore delle prestazioni Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) è un membro di una categoria (in hello allo stesso modo che un campo è un membro di una classe).</span><span class="sxs-lookup"><span data-stu-id="3280a-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="3280a-196">Le categorie possono essere globali o possono disporre di istanze numerate o denominate.</span><span class="sxs-lookup"><span data-stu-id="3280a-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="3280a-197">displayName: nome hello visualizzato nel portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="3280a-198">categoryName: hello categoria contatori delle prestazioni (oggetto prestazioni) a cui è associato questo contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3280a-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="3280a-199">counterName – nome hello hello del contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="3280a-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="3280a-200">instanceName-nome hello dell'istanza di categoria del contatore delle prestazioni hello o una stringa vuota (""), se la categoria hello contiene una sola istanza.</span><span class="sxs-lookup"><span data-stu-id="3280a-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="3280a-201">Se categoryName hello è processo e si desidera toocollect contatore delle prestazioni hello è dal processo JVM corrente hello in cui è in esecuzione l'app, specificare `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="3280a-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="3280a-202">I contatori delle prestazioni sono visibili come metriche personalizzate in [Esplora metriche][metrics].</span><span class="sxs-lookup"><span data-stu-id="3280a-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="3280a-203">Contatori delle prestazioni Unix</span><span class="sxs-lookup"><span data-stu-id="3280a-203">Unix performance counters</span></span>
* <span data-ttu-id="3280a-204">[Installare collectd con plug-in Application Insights hello](app-insights-java-collectd.md) tooget un'ampia gamma di dati di sistema e di rete.</span><span class="sxs-lookup"><span data-stu-id="3280a-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="3280a-205">Test Web di disponibilità</span><span class="sxs-lookup"><span data-stu-id="3280a-205">Availability web tests</span></span>
<span data-ttu-id="3280a-206">Application Insights è possibile testare il sito Web all'indirizzo toocheck a intervalli regolari che è attivo e risponde correttamente.</span><span class="sxs-lookup"><span data-stu-id="3280a-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="3280a-207">[tooset backup][availability], scorrere verso il basso tooclick disponibilità.</span><span class="sxs-lookup"><span data-stu-id="3280a-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![Scorrere verso il basso, fare clic su Disponibilità, quindi su Aggiungi test Web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="3280a-209">Se il sito è inattivo, si otterranno grafici dei tempi di risposta, nonché notifiche di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="3280a-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Esempio di test Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="3280a-211">[Altre informazioni sui test Web di disponibilità.][availability]</span><span class="sxs-lookup"><span data-stu-id="3280a-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="3280a-212">Log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="3280a-212">Diagnostic logs</span></span>
<span data-ttu-id="3280a-213">Se si usa Log4J o Logback (versione 1.2 o 2.0) per la traccia, è possibile utilizzare i log di traccia inviati automaticamente tooApplication informazioni dettagliate in cui è possibile esplorare e ricerche.</span><span class="sxs-lookup"><span data-stu-id="3280a-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="3280a-214">[Altre informazioni sui log di diagnostica][javalogs]</span><span class="sxs-lookup"><span data-stu-id="3280a-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="3280a-215">Telemetria personalizzata</span><span class="sxs-lookup"><span data-stu-id="3280a-215">Custom telemetry</span></span>
<span data-ttu-id="3280a-216">Inserire alcune righe di codice nel toofind di applicazione web Java le operazioni con gli utenti o toohelp diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="3280a-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="3280a-217">Nella pagina web JavaScript e Java di hello sul lato server, è possibile inserire codice.</span><span class="sxs-lookup"><span data-stu-id="3280a-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="3280a-218">[Informazioni sulla telemetria personalizzata][track]</span><span class="sxs-lookup"><span data-stu-id="3280a-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3280a-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3280a-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="3280a-220">Rilevare e diagnosticare i problemi</span><span class="sxs-lookup"><span data-stu-id="3280a-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="3280a-221">[Aggiungi telemetria di client web] [ usage] telemetria relativi alle prestazioni tooget dal client web hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="3280a-222">[Configurare i test web] [ availability] toomake che l'applicazione rimane in tempo reale e reattiva.</span><span class="sxs-lookup"><span data-stu-id="3280a-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="3280a-223">[Ricerca di eventi e log] [ diagnostic] toohelp diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="3280a-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="3280a-224">[Acquisire le tracce di Log4J o Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="3280a-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="3280a-225">Tenere traccia dell'utilizzo</span><span class="sxs-lookup"><span data-stu-id="3280a-225">Track usage</span></span>
* <span data-ttu-id="3280a-226">[Aggiungi telemetria di client web] [ usage] toomonitor pagina viste e le metriche di utente di base.</span><span class="sxs-lookup"><span data-stu-id="3280a-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="3280a-227">[Tenere traccia di eventi personalizzati e le metriche](app-insights-web-track-usage.md) toolearn sulle modalità di utilizzo dell'applicazione, sia nel client hello e nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="3280a-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
