---
title: Introduzione ad Azure Application Insights con Java in Eclipse | Documentazione Microsoft
description: Usare il plug-in Eclipse per aggiungere il monitoraggio delle prestazioni e l'uso nel sito Web Java con Application Insights
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
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="1b5b5-103">Introduzione ad Application Insights con Java in Eclipse</span><span class="sxs-lookup"><span data-stu-id="1b5b5-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="1b5b5-104">SDK di Application Insights invia dati di telemetria dall'applicazione Web Java in modo da poter analizzare l'uso e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="1b5b5-105">Il plug-in Eclipse per Application Insights installa automaticamente SDK nel progetto in modo da ottenere i dati di telemetria predefiniti, oltre a un'API che è possibile usare per scrivere dati di telemetria personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="1b5b5-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1b5b5-106">Prerequisites</span></span>
<span data-ttu-id="1b5b5-107">Attualmente il plug-in funziona per progetti Mavern e progetti Dynamic Web in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="1b5b5-108">[Aggiungere Application Insights ad altri tipi di progetti Java][java].</span><span class="sxs-lookup"><span data-stu-id="1b5b5-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="1b5b5-109">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-109">You'll need:</span></span>

* <span data-ttu-id="1b5b5-110">Oracle JRE 1.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="1b5b5-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="1b5b5-111">Una sottoscrizione a [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="1b5b5-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="1b5b5-112">[Eclipse IDE per sviluppatori Java EE](http://www.eclipse.org/downloads/), Indigo o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="1b5b5-113">Windows 7 o versioni successive o Windows Server 2008 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="1b5b5-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="1b5b5-114">Installare SDK su Eclipse (una volta)</span><span class="sxs-lookup"><span data-stu-id="1b5b5-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="1b5b5-115">È sufficiente eseguire questa operazione una volta per ogni macchina.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="1b5b5-116">Con questo passaggio viene installato un toolkit che può quindi aggiungere SDK a ciascun progetto Web dinamico.Con questo passaggio viene installato un toolkit che può quindi aggiungere SDK a ciascun Dynamic Web Project.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="1b5b5-117">Dal menu Help di Eclipse scegliere Install New Software.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Guida in linea, Installa nuovo Software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="1b5b5-119">L'SDK è disponibile alla pagina http://dl.microsoft.com/eclipse in Azure Toolkit.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="1b5b5-120">Deselezionare l'opzione **Contatta tutti i siti di aggiornamento...**</span><span class="sxs-lookup"><span data-stu-id="1b5b5-120">Uncheck **Contact all update sites...**</span></span>

    ![Per Application Insights SDK deselezionare tutti i siti di aggiornamento Contatta tutti](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="1b5b5-122">Seguire i passaggi rimanenti per ogni progetto Java.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="1b5b5-123">Creare una risorsa di Application Insights in Azure</span><span class="sxs-lookup"><span data-stu-id="1b5b5-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="1b5b5-124">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5b5-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b5b5-125">Creare una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="1b5b5-126">Impostare il tipo di applicazione nell'applicazione Web Java.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-126">Set the application type to Java web application.</span></span>  

    ![Fare clic su + e scegliere Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="1b5b5-128">Ottenere la chiave di strumentazione della nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="1b5b5-129">Dopo poco sarà necessario incollarla in questo progetto del codice.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-129">You'll need to paste this into your code project shortly.</span></span>  

    ![Nella panoramica della nuova risorsa, fare clic su Proprietà e copiare la chiave di strumentazione](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="1b5b5-131">Aggiunta di Application Insights al progetto</span><span class="sxs-lookup"><span data-stu-id="1b5b5-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="1b5b5-132">Aggiungere Application Insights dal menu di scelta rapida del progetto Web Java.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![Nella panoramica della nuova risorsa, fare clic su Proprietà e copiare la chiave di strumentazione](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="1b5b5-134">Incollare la chiave di strumentazione recuperata dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![Nella panoramica della nuova risorsa, fare clic su Proprietà e copiare la chiave di strumentazione](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="1b5b5-136">La chiave viene inviata insieme a tutti gli elementi di dati di telemetria e indica ad Application Insights di visualizzarla nella risorsa.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="1b5b5-137">Eseguire l'applicazione e visualizzare le metriche</span><span class="sxs-lookup"><span data-stu-id="1b5b5-137">Run the application and see metrics</span></span>
<span data-ttu-id="1b5b5-138">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-138">Run your application.</span></span>

<span data-ttu-id="1b5b5-139">Tornare alla risorsa di Application Insights in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="1b5b5-140">Nel pannello Panoramica verranno visualizzati i dati delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="1b5b5-141">Se non sono visualizzati, attendere alcuni secondi e quindi fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="1b5b5-142">Risposta del server, conteggi delle richieste ed errori</span><span class="sxs-lookup"><span data-stu-id="1b5b5-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="1b5b5-143">Fare clic su qualsiasi grafico per visualizzare metriche più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-143">Click through any chart to see more detailed metrics.</span></span>

![Numero di richieste per nome](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="1b5b5-145">[Altre informazioni sulle metriche.][metrics]</span><span class="sxs-lookup"><span data-stu-id="1b5b5-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="1b5b5-146">E quando si visualizzano le proprietà di una richiesta, è possibile visualizzare gli eventi di telemetria associati, ad esempio le richieste e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![Tutte le tracce per questa richiesta](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="1b5b5-148">Telemetria sul lato client</span><span class="sxs-lookup"><span data-stu-id="1b5b5-148">Client-side telemetry</span></span>
<span data-ttu-id="1b5b5-149">Dal pannello Avvio rapido fare clic su Recupera codice per monitorare le pagine Web:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![Nel pannello di panoramica delle app, scegliere Avvio rapido, quindi ottenere il codice per monitorare le pagine Web.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="1b5b5-152">Inserire il frammento di codice nella parte iniziale dei file HTML.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="1b5b5-153">Visualizzare i dati lato client</span><span class="sxs-lookup"><span data-stu-id="1b5b5-153">View client-side data</span></span>
<span data-ttu-id="1b5b5-154">Aprire le pagine Web aggiornate e usarle.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="1b5b5-155">Attendere uno o due minuti, quindi tornare ad Application Insights e aprire il pannello Utilizzo.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="1b5b5-156">(Nel pannello Panoramica scorrere verso il basso e fare clic su Utilizzo.)</span><span class="sxs-lookup"><span data-stu-id="1b5b5-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="1b5b5-157">Le metriche di visualizzazioni pagine, utenti e sessioni verranno visualizzate nel pannello Utilizzo:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![Sessioni, utenti e visualizzazioni pagina](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="1b5b5-159">[Altre informazioni sulla configurazione della telemetria sul lato client.][usage]</span><span class="sxs-lookup"><span data-stu-id="1b5b5-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="1b5b5-160">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b5b5-160">Publish your application</span></span>
<span data-ttu-id="1b5b5-161">A questo punto è possibile pubblicare l'applicazione nel server, permettere agli utenti di utilizzarla e visualizzare la telemetria mostrata nel portale.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="1b5b5-162">Verificare che il firewall consenta all'applicazione di inviare i dati di telemetria a queste porte:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="1b5b5-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="1b5b5-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="1b5b5-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="1b5b5-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="1b5b5-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="1b5b5-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="1b5b5-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="1b5b5-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="1b5b5-167">Nei server Windows installare:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="1b5b5-168">Microsoft Visual C++ Redistributable Package</span><span class="sxs-lookup"><span data-stu-id="1b5b5-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="1b5b5-169">(Ciò abilita i contatori delle prestazioni).</span><span class="sxs-lookup"><span data-stu-id="1b5b5-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="1b5b5-170">Eccezioni e richieste non eseguite</span><span class="sxs-lookup"><span data-stu-id="1b5b5-170">Exceptions and request failures</span></span>
<span data-ttu-id="1b5b5-171">Vengono raccolte automaticamente le eccezioni non gestite:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="1b5b5-172">Per raccogliere dati su altre eccezioni, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="1b5b5-173">[Inserire chiamate a TrackException nel codice](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="1b5b5-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="1b5b5-174">[Installare l'agente Java sul server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="1b5b5-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="1b5b5-175">È possibile specificare i metodi da controllare.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="1b5b5-176">Monitorare le chiamate al metodo e le dipendenze esterne</span><span class="sxs-lookup"><span data-stu-id="1b5b5-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="1b5b5-177">[Installare l'agente Java](app-insights-java-agent.md) per registrare i metodi interni specificati e le chiamate effettuate tramite JDBC, con i dati relativi alle durate.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="1b5b5-178">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="1b5b5-178">Performance counters</span></span>
<span data-ttu-id="1b5b5-179">Nel pannello Panoramica scorrere verso il basso e fare clic sul riquadro **Server**.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="1b5b5-180">Verrà visualizzato un intervallo di contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-180">You'll see a range of performance counters.</span></span>

![Scorrere verso il basso fare clic sul riquadro Server](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="1b5b5-182">Personalizzare la raccolta del contatore delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="1b5b5-182">Customize performance counter collection</span></span>
<span data-ttu-id="1b5b5-183">Per disabilitare la raccolta del set standard di contatori delle prestazioni, aggiungere il seguente codice al di sotto del nodo principale del file ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="1b5b5-184">Raccogliere dei contatori di prestazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1b5b5-184">Collect additional performance counters</span></span>
<span data-ttu-id="1b5b5-185">È possibile specificare altri contatori di prestazioni da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="1b5b5-186">Contatori JMX (esposti da Java Virtual Machine)</span><span class="sxs-lookup"><span data-stu-id="1b5b5-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="1b5b5-187">`displayName` : il nome visualizzato nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="1b5b5-188">`objectName` : il nome dell'oggetto JMX.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="1b5b5-189">`attribute` : l'attributo del nome dell'oggetto JMX da recuperare</span><span class="sxs-lookup"><span data-stu-id="1b5b5-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="1b5b5-190">`type` (facoltativo): il tipo di attributo dell'oggetto JMX:</span><span class="sxs-lookup"><span data-stu-id="1b5b5-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="1b5b5-191">Impostazione predefinita: un tipo semplice come int o long.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="1b5b5-192">`composite`: i dati del contatore delle prestazioni sono nel formato 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="1b5b5-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="1b5b5-193">`tabular`: i dati del contatore delle prestazioni sono nel formato della riga di una tabella</span><span class="sxs-lookup"><span data-stu-id="1b5b5-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="1b5b5-194">Contatori delle prestazioni di Windows</span><span class="sxs-lookup"><span data-stu-id="1b5b5-194">Windows performance counters</span></span>
<span data-ttu-id="1b5b5-195">Ogni [contatore delle prestazioni Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) è un membro di una categoria (nello stesso modo in cui un campo è un membro di una classe).</span><span class="sxs-lookup"><span data-stu-id="1b5b5-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="1b5b5-196">Le categorie possono essere globali o possono disporre di istanze numerate o denominate.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="1b5b5-197">displayName: il nome visualizzato nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="1b5b5-198">categoryName: la categoria del contatore delle prestazioni (oggetto prestazioni) a cui è associato questo contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="1b5b5-199">counterName: il nome del contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="1b5b5-200">instanceName: il nome dell'istanza di categoria del contatore delle prestazioni o una stringa vuota (""), se la categoria contiene una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="1b5b5-201">Se categoryName è il processo e il contatore delle prestazioni di cui raccogliere i dati proviene dal processo JVM corrente su cui è in esecuzione l'app, specificare `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="1b5b5-202">I contatori delle prestazioni sono visibili come metriche personalizzate in [Esplora metriche][metrics].</span><span class="sxs-lookup"><span data-stu-id="1b5b5-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="1b5b5-203">Contatori delle prestazioni Unix</span><span class="sxs-lookup"><span data-stu-id="1b5b5-203">Unix performance counters</span></span>
* <span data-ttu-id="1b5b5-204">[Installare collectd con il plug-in di Application Insights](app-insights-java-collectd.md) per ottenere una vasta gamma di dati di sistema e di rete.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="1b5b5-205">Test Web di disponibilità</span><span class="sxs-lookup"><span data-stu-id="1b5b5-205">Availability web tests</span></span>
<span data-ttu-id="1b5b5-206">Application Insights può testare il sito Web a intervalli regolari per verificare che funzioni e risponda correttamente.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="1b5b5-207">[Per eseguire la configurazione][availability], scorrere verso il basso e fare clic su Disponibilità.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-207">[To set up][availability], scroll down to click Availability.</span></span>

![Scorrere verso il basso, fare clic su Disponibilità, quindi su Aggiungi test Web](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="1b5b5-209">Se il sito è inattivo, si otterranno grafici dei tempi di risposta, nonché notifiche di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Esempio di test Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="1b5b5-211">[Altre informazioni sui test Web di disponibilità.][availability]</span><span class="sxs-lookup"><span data-stu-id="1b5b5-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="1b5b5-212">Log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="1b5b5-212">Diagnostic logs</span></span>
<span data-ttu-id="1b5b5-213">Se si usa Logback o Log4J (v1.2 o v2.0) per la traccia, è possibile inviare automaticamente i log di traccia ad Application Insights dove è possibile esplorarli e eseguirvi ricerche.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="1b5b5-214">[Altre informazioni sui log di diagnostica][javalogs]</span><span class="sxs-lookup"><span data-stu-id="1b5b5-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="1b5b5-215">Telemetria personalizzata</span><span class="sxs-lookup"><span data-stu-id="1b5b5-215">Custom telemetry</span></span>
<span data-ttu-id="1b5b5-216">Inserire alcune righe di codice nell'applicazione Web Java per scoprire come viene usato dagli utenti o per agevolare la diagnosi dei problemi.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="1b5b5-217">È possibile inserire il codice sia nella pagina Web JavaScript che in Java lato server.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="1b5b5-218">[Informazioni sulla telemetria personalizzata][track]</span><span class="sxs-lookup"><span data-stu-id="1b5b5-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b5b5-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b5b5-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="1b5b5-220">Rilevare e diagnosticare i problemi</span><span class="sxs-lookup"><span data-stu-id="1b5b5-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="1b5b5-221">[Aggiungere dati di telemetria client Web][usage] per ottenere dati di telemetria delle prestazioni dal client Web.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="1b5b5-222">[Configurare i test Web][availability] in modo da assicurarsi che l'applicazione sia disponibile e reattiva.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="1b5b5-223">Per facilitare la diagnosi dei problemi, [cercare eventi e log][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="1b5b5-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="1b5b5-224">[Acquisire le tracce di Log4J o Logback][javalogs]</span><span class="sxs-lookup"><span data-stu-id="1b5b5-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="1b5b5-225">Tenere traccia dell'utilizzo</span><span class="sxs-lookup"><span data-stu-id="1b5b5-225">Track usage</span></span>
* <span data-ttu-id="1b5b5-226">[Aggiungere dati di telemetria client Web][usage] per monitorare le visualizzazioni pagina e le metriche utente di base.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="1b5b5-227">[Tenere traccia di eventi personalizzati e metriche](app-insights-web-track-usage.md) per altre informazioni sulle modalità di uso dell'applicazione, sul lato client e server.</span><span class="sxs-lookup"><span data-stu-id="1b5b5-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
