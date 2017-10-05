---
title: Analisi di app Web Java con Azure Application Insights | Documentazione Microsoft
description: 'Application Performance Monitoring per app Web Java con Application Insights. '
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a75815885d7ccd7cd56db3da2f3f92cae78fe033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="ed5ac-103">Introduzione ad Application Insights in un progetto Web Java</span><span class="sxs-lookup"><span data-stu-id="ed5ac-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="ed5ac-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) è un servizio di analisi estendibile per gli sviluppatori Web che semplifica la comprensione delle prestazioni e dell'uso dell'applicazione live.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="ed5ac-105">È possibile usarlo per [rilevare e diagnosticare i problemi di prestazioni e le eccezioni](app-insights-detect-triage-diagnose.md) e per [scrivere il codice][api] per tenere traccia della attività degli utenti con l'app.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![dati di esempio](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="ed5ac-107">Application Insights supporta le app Java in esecuzione in Linux, Unix o Windows.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="ed5ac-108">Sono necessari:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-108">You need:</span></span>

* <span data-ttu-id="ed5ac-109">Oracle JRE 1.6 o versione successiva o isiZulu JRE 1.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="ed5ac-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="ed5ac-110">Una sottoscrizione a [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="ed5ac-111">*Se è disponibile un'App Web già attiva, è possibile seguire la procedura alternativa per [aggiungere l'SDK al server Web in fase di esecuzione](app-insights-java-live.md). Tale alternativa evita di ricompilare il codice, ma non si ottiene l'opzione per scrivere codice per tenere traccia delle attività dell'utente.*</span><span class="sxs-lookup"><span data-stu-id="ed5ac-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="ed5ac-112">1. Ottenere una chiave di strumentazione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="ed5ac-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="ed5ac-113">Accedere al [portale di Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ed5ac-114">Creare una risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-114">Create an Application Insights resource.</span></span> <span data-ttu-id="ed5ac-115">Impostare il tipo di applicazione nell'applicazione Web Java.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-115">Set the application type to Java web application.</span></span>

    ![Inserire un nome, scegliere l'app Web Java e fare clic su Crea](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="ed5ac-117">Ottenere la chiave di strumentazione della nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="ed5ac-118">Questa chiave dovrà a breve essere incollata nel progetto di codice.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-118">You'll need to paste this key into your code project shortly.</span></span>

    ![Nella panoramica della nuova risorsa, fare clic su Proprietà e copiare la chiave di strumentazione](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="ed5ac-120">2. Aggiungere SDK per Java di Application Insights al progetto</span><span class="sxs-lookup"><span data-stu-id="ed5ac-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="ed5ac-121">*Scegliere il modo più appropriato per il progetto.*</span><span class="sxs-lookup"><span data-stu-id="ed5ac-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="ed5ac-122">Se si usa Eclipse per creare un progetto Web dinamico o Maven:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="ed5ac-123">Usare il [plug-in di Application Insights SDK per Java][eclipse].</span><span class="sxs-lookup"><span data-stu-id="ed5ac-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="ed5ac-124">Se si usa Maven...</span><span class="sxs-lookup"><span data-stu-id="ed5ac-124">If you're using Maven...</span></span>
<span data-ttu-id="ed5ac-125">Se il progetto è già stato configurato per usare Maven per la compilazione, unire il codice seguente al file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="ed5ac-126">Aggiornare quindi le dipendenze progetto per fare in modo che i file binari vengano scaricati.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="ed5ac-127">*Errori di convalida checksum o compilazione?*</span><span class="sxs-lookup"><span data-stu-id="ed5ac-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="ed5ac-128">Provare a usare una versione specifica, ad esempio `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="ed5ac-129">La versione più recente è disponibile nelle [note sulla versione dell'SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) o negli [elementi Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="ed5ac-130">*È necessario eseguire l'aggiornamento a un nuovo SDK?*</span><span class="sxs-lookup"><span data-stu-id="ed5ac-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="ed5ac-131">Aggiornare le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="ed5ac-132">Se si usa Gradle...</span><span class="sxs-lookup"><span data-stu-id="ed5ac-132">If you're using Gradle...</span></span>
<span data-ttu-id="ed5ac-133">Se il progetto è già stato configurato per usare Gradle per la compilazione, unire il codice seguente al file build.gradle.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="ed5ac-134">Aggiornare quindi le dipendenze progetto per fare in modo che i file binari vengano scaricati.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="ed5ac-135">*Errori di convalida checksum o compilazione? Provare a usare una versione specifica, come* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="ed5ac-136">*La versione più recente è disponibile nelle [note sulla versione dell'SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="ed5ac-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="ed5ac-137">*Per eseguire l'aggiornamento a un nuovo SDK*</span><span class="sxs-lookup"><span data-stu-id="ed5ac-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="ed5ac-138">Aggiornare le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="ed5ac-139">In caso contrario...</span><span class="sxs-lookup"><span data-stu-id="ed5ac-139">Otherwise ...</span></span>
<span data-ttu-id="ed5ac-140">Aggiungere manualmente SDK:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="ed5ac-141">Scaricare [Application Insights SDK per Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="ed5ac-142">Estrarre i file binari dal file ZIP e aggiungerli al progetto.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="ed5ac-143">Domande...</span><span class="sxs-lookup"><span data-stu-id="ed5ac-143">Questions...</span></span>
* <span data-ttu-id="ed5ac-144">*Qual è la relazione tra i componenti `-core` e `-web` nel file ZIP?*</span><span class="sxs-lookup"><span data-stu-id="ed5ac-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="ed5ac-145">`applicationinsights-core` fornisce semplicemente l'API.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="ed5ac-146">Questo componente sarà sempre necessario.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-146">You always need this component.</span></span>
  * <span data-ttu-id="ed5ac-147">`applicationinsights-web` fornisce le metriche che consentono di tenere traccia del numero e dei tempi di risposta delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="ed5ac-148">Questo componente può essere omesso se non si vuole che questi dati di telemetria vengano raccolti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="ed5ac-149">Ad esempio se si preferisce scrivere dati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="ed5ac-150">*Per aggiornare il SDK, quando si pubblicano le modifiche*</span><span class="sxs-lookup"><span data-stu-id="ed5ac-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="ed5ac-151">Scaricare la versione più recente di [Application Insights SDK per Java](https://aka.ms/qqkaq6) e sostituire le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="ed5ac-152">Le modifiche sono descritte nelle [note sulla versione dell'SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="ed5ac-153">3. Aggiungere un file XML di Application Insights</span><span class="sxs-lookup"><span data-stu-id="ed5ac-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="ed5ac-154">Aggiungere ApplicationInsights.xml alla cartella resources del progetto oppure verificare che sia stato aggiunto al percorso della classe di distribuzione del progetto.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="ed5ac-155">Copiarvi il seguente file XML.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-155">Copy the following XML into it.</span></span>

<span data-ttu-id="ed5ac-156">Sostituire la chiave di strumentazione recuperata dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="ed5ac-157">La chiave di strumentazione viene inviata insieme a tutti gli elementi di dati di telemetria e indica ad Application Insights di visualizzarla nella risorsa.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="ed5ac-158">Il componente delle richieste HTTP è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="ed5ac-159">Invia automaticamente i dati di telemetria sulle richieste e tempi di risposta al portale.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="ed5ac-160">La correlazione di eventi è un'aggiunta al componente delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="ed5ac-161">Assegna un identificatore a ogni richiesta ricevuta dal server e lo aggiunge come proprietà a ogni elemento di telemetria, come proprietà "Operation.Id".</span><span class="sxs-lookup"><span data-stu-id="ed5ac-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="ed5ac-162">Consente di correlare i dati di telemetria associati a ogni richiesta impostando un filtro in [Ricerca diagnostica][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="ed5ac-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="ed5ac-163">La chiave di Application Insights può essere passata dinamicamente dal portale di Azure come proprietà di sistema (-DAPPLICATION_INSIGHTS_IKEY=ikey).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="ed5ac-164">Se non è presente una proprietà definita, viene verificata la presenza della variabile di ambiente (APPLICATION_INSIGHTS_IKEY) nelle impostazioni dell'app Azure.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="ed5ac-165">Se nessuna delle due proprietà è definita, viene usato il valore InstrumentationKey predefinito di ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="ed5ac-166">Questa sequenza consente di gestire dinamicamente valori InstrumentationKey diversi per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="ed5ac-167">Modi alternativi per impostare la chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="ed5ac-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="ed5ac-168">Application Insights SDK cerca la chiave nell'ordine seguente.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="ed5ac-169">Proprietà di sistema: -DAPPLICATION_INSIGHTS_IKEY=ikey</span><span class="sxs-lookup"><span data-stu-id="ed5ac-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="ed5ac-170">Variabile di ambiente: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="ed5ac-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="ed5ac-171">File di configurazione: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="ed5ac-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="ed5ac-172">È anche possibile eseguirne l' [impostazione nel codice](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="ed5ac-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="ed5ac-173">4. Aggiungere un filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="ed5ac-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="ed5ac-174">L'ultimo passaggio di configurazione consente al componente delle richieste HTTP di registrare ogni richiesta Web.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="ed5ac-175">Non necessario se si desidera l'API.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="ed5ac-176">Individuare e aprire il file web.xml nel progetto e unire il codice seguente al di sotto del nodo app-web, in cui sono configurati i filtri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="ed5ac-177">Per ottenere risultati più accurati, il filtro deve essere mappato prima di tutti gli altri filtri.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="ed5ac-178">Se si usa Spring Web MVC 3.1 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="ed5ac-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="ed5ac-179">Modificare questi elementi in *-servlet.xml per includere il pacchetto di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-179">Edit these elements in *-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="ed5ac-180">Se si usa Struts 2</span><span class="sxs-lookup"><span data-stu-id="ed5ac-180">If you're using Struts 2</span></span>
<span data-ttu-id="ed5ac-181">Aggiungere questa voce al file di configurazione Struts (in genere denominato struts.xml o struts-default.xml):</span><span class="sxs-lookup"><span data-stu-id="ed5ac-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="ed5ac-182">Se si dispone di intercettori definiti in uno stack predefinito, l'intercettore può semplicemente essere aggiunto a tale stack.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="ed5ac-183">5. Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="ed5ac-183">5. Run your application</span></span>
<span data-ttu-id="ed5ac-184">Eseguire l'applicazione in modalità debug nel computer di distribuzione oppure pubblicarla nel server.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="ed5ac-185">6. Visualizzare i dati di telemetria in Application Insights</span><span class="sxs-lookup"><span data-stu-id="ed5ac-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="ed5ac-186">Tornare alla risorsa di Application Insights nel [portale di Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="ed5ac-187">Nel pannello di panoramica vengono visualizzati i dati delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="ed5ac-188">Se non sono visualizzati, attendere alcuni secondi e quindi fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dati di esempio](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="ed5ac-190">[Altre informazioni sulle metriche.][metrics]</span><span class="sxs-lookup"><span data-stu-id="ed5ac-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="ed5ac-191">Fare clic su qualsiasi grafico per visualizzare metriche aggregate più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="ed5ac-192">Application Insights presuppone che il formato delle richieste HTTP per le applicazioni MVC sia `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="ed5ac-193">Ad esempio, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` e `GET Home/Product/sdf96vws` vengono raggruppati in `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="ed5ac-194">Questo raggruppamento consente aggregazioni significative delle richieste, come il numero di richieste e il tempo medio di esecuzione per le richieste.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="ed5ac-195">Dati dell'istanza</span><span class="sxs-lookup"><span data-stu-id="ed5ac-195">Instance data</span></span>
<span data-ttu-id="ed5ac-196">Fare clic su un tipo di richiesta specifico per visualizzare le singole istanze.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="ed5ac-197">In Application Insights vengono visualizzati due tipi di dati, ovvero i dati aggregati, archiviati e visualizzati come medie, conteggi e somme, e i dati di istanza, ovvero singoli report di richieste HTTP, eccezioni, visualizzazioni di pagina o eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="ed5ac-198">Quando si visualizzano le proprietà di una richiesta, è possibile visualizzare gli eventi di telemetria associati, ad esempio le richieste e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="ed5ac-199">Analytics: linguaggio di query avanzato</span><span class="sxs-lookup"><span data-stu-id="ed5ac-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="ed5ac-200">Quando si accumulano molti dati, è possibile eseguire query per aggregare i dati e per individuare istanze singole.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="ed5ac-201">[Analisi](app-insights-analytics.md) è uno strumento avanzato per ottenere informazioni sulle prestazioni e sull'utilizzo e ai fini della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Esempio di Analytics](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="ed5ac-203">7. Installare l'applicazione nel server</span><span class="sxs-lookup"><span data-stu-id="ed5ac-203">7. Install your app on the server</span></span>
<span data-ttu-id="ed5ac-204">A questo punto è possibile pubblicare l'applicazione nel server, permettere agli utenti di utilizzarla e visualizzare la telemetria mostrata nel portale.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="ed5ac-205">Verificare che il firewall consenta all'applicazione di inviare i dati di telemetria a queste porte:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="ed5ac-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="ed5ac-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="ed5ac-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="ed5ac-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="ed5ac-208">Se il traffico in uscita deve essere instradato attraverso un firewall, definire le proprietà di sistema `http.proxyHost` e `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="ed5ac-209">Nei server Windows installare:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="ed5ac-210">Microsoft Visual C++ Redistributable Package</span><span class="sxs-lookup"><span data-stu-id="ed5ac-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="ed5ac-211">Questo componente abilita i contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="ed5ac-212">Eccezioni e richieste non eseguite</span><span class="sxs-lookup"><span data-stu-id="ed5ac-212">Exceptions and request failures</span></span>
<span data-ttu-id="ed5ac-213">Vengono raccolte automaticamente le eccezioni non gestite:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-213">Unhandled exceptions are automatically collected:</span></span>

![Aprire Impostazioni e quindi Errori](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="ed5ac-215">Per raccogliere dati su altre eccezioni, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="ed5ac-216">[Inserire chiamate a trackException() nel codice][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="ed5ac-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="ed5ac-217">[Installare l'agente Java nel server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="ed5ac-218">È possibile specificare i metodi da controllare.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="ed5ac-219">Monitorare le chiamate al metodo e le dipendenze esterne</span><span class="sxs-lookup"><span data-stu-id="ed5ac-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="ed5ac-220">[Installare l'agente Java](app-insights-java-agent.md) per registrare i metodi interni specificati e le chiamate effettuate tramite JDBC, con i dati relativi alle durate.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="ed5ac-221">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="ed5ac-221">Performance counters</span></span>
<span data-ttu-id="ed5ac-222">Per visualizzare un intervallo di contatori delle prestazioni, aprire **Impostazioni** e quindi **Server**.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="ed5ac-223">Personalizzare la raccolta del contatore delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="ed5ac-223">Customize performance counter collection</span></span>
<span data-ttu-id="ed5ac-224">Per disabilitare la raccolta del set standard di contatori delle prestazioni, aggiungere il seguente codice al di sotto del nodo principale del file ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="ed5ac-225">Raccogliere dei contatori di prestazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ed5ac-225">Collect additional performance counters</span></span>
<span data-ttu-id="ed5ac-226">È possibile specificare altri contatori di prestazioni da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="ed5ac-227">Contatori JMX (esposti da Java Virtual Machine)</span><span class="sxs-lookup"><span data-stu-id="ed5ac-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="ed5ac-228">`displayName` : il nome visualizzato nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="ed5ac-229">`objectName` : il nome dell'oggetto JMX.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="ed5ac-230">`attribute` : l'attributo del nome dell'oggetto JMX da recuperare</span><span class="sxs-lookup"><span data-stu-id="ed5ac-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="ed5ac-231">`type` (facoltativo): il tipo di attributo dell'oggetto JMX:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="ed5ac-232">Impostazione predefinita: un tipo semplice come int o long.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="ed5ac-233">`composite`: i dati del contatore delle prestazioni sono nel formato 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="ed5ac-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="ed5ac-234">`tabular`: i dati del contatore delle prestazioni sono nel formato della riga di una tabella</span><span class="sxs-lookup"><span data-stu-id="ed5ac-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="ed5ac-235">Contatori delle prestazioni di Windows</span><span class="sxs-lookup"><span data-stu-id="ed5ac-235">Windows performance counters</span></span>
<span data-ttu-id="ed5ac-236">Ogni [contatore delle prestazioni Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) è un membro di una categoria (nello stesso modo in cui un campo è un membro di una classe).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="ed5ac-237">Le categorie possono essere globali o possono disporre di istanze numerate o denominate.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="ed5ac-238">displayName: il nome visualizzato nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="ed5ac-239">categoryName: la categoria del contatore delle prestazioni (oggetto prestazioni) a cui è associato questo contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="ed5ac-240">counterName: il nome del contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="ed5ac-241">instanceName: il nome dell'istanza di categoria del contatore delle prestazioni o una stringa vuota (""), se la categoria contiene una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="ed5ac-242">Se categoryName è il processo e il contatore delle prestazioni di cui raccogliere i dati proviene dal processo JVM corrente su cui è in esecuzione l'app, specificare `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="ed5ac-243">I contatori delle prestazioni sono visibili come metriche personalizzate in [Esplora metriche][metrics].</span><span class="sxs-lookup"><span data-stu-id="ed5ac-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="ed5ac-244">Contatori delle prestazioni Unix</span><span class="sxs-lookup"><span data-stu-id="ed5ac-244">Unix performance counters</span></span>
* <span data-ttu-id="ed5ac-245">[Installare collectd con il plug-in di Application Insights](app-insights-java-collectd.md) per ottenere una vasta gamma di dati di sistema e di rete.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="ed5ac-246">Ottenere i dati relativi a utenti e sessioni</span><span class="sxs-lookup"><span data-stu-id="ed5ac-246">Get user and session data</span></span>
<span data-ttu-id="ed5ac-247">I dati di telemetria vengono normalmente inviati dal server Web.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="ed5ac-248">Per un quadro completo a 360 gradi dell'applicazione, è però possibile aggiungere altre funzionalità di monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="ed5ac-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="ed5ac-249">[Aggiungere la telemetria alle pagine Web][usage] per monitorare le visualizzazioni pagina e le metriche utente.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="ed5ac-250">[Configurare i test Web][availability] in modo da assicurarsi che l'applicazione sia disponibile e reattiva.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="ed5ac-251">Acquisire le tracce dei log</span><span class="sxs-lookup"><span data-stu-id="ed5ac-251">Capture log traces</span></span>
<span data-ttu-id="ed5ac-252">È possibile usare Application Insights per analizzare approfonditamente log di Log4J, Logback o altri framework di registrazione.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="ed5ac-253">È possibile correlare i log con le richieste HTTP e altri dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="ed5ac-254">[Informazioni][javalogs].</span><span class="sxs-lookup"><span data-stu-id="ed5ac-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="ed5ac-255">Inviare i propri dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="ed5ac-255">Send your own telemetry</span></span>
<span data-ttu-id="ed5ac-256">Ora che è stato installato SDK, è possibile usare l'API per inviare i propri dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="ed5ac-257">Per informazioni sulle attività svolte dagli utenti con l'applicazione, [tenere traccia di eventi e metriche personalizzate][api].</span><span class="sxs-lookup"><span data-stu-id="ed5ac-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="ed5ac-258">Per facilitare la diagnosi dei problemi, [cercare eventi e log][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="ed5ac-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="ed5ac-259">Test Web di disponibilità</span><span class="sxs-lookup"><span data-stu-id="ed5ac-259">Availability web tests</span></span>
<span data-ttu-id="ed5ac-260">Application Insights può testare il sito Web a intervalli regolari per verificare che funzioni e risponda correttamente.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="ed5ac-261">[Per eseguire la configurazione][availability], fare clic su Test Web.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-261">[To set up][availability], click Web tests.</span></span>

![Fare clic su Test Web e quindi su Aggiungi test Web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="ed5ac-263">Se il sito è inattivo, si otterranno grafici dei tempi di risposta, nonché notifiche di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Esempio di test Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="ed5ac-265">[Altre informazioni sui test Web di disponibilità.][availability]</span><span class="sxs-lookup"><span data-stu-id="ed5ac-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="ed5ac-266">Domande?</span><span class="sxs-lookup"><span data-stu-id="ed5ac-266">Questions?</span></span> <span data-ttu-id="ed5ac-267">Problemi?</span><span class="sxs-lookup"><span data-stu-id="ed5ac-267">Problems?</span></span>
[<span data-ttu-id="ed5ac-268">Risoluzione dei problemi Java</span><span class="sxs-lookup"><span data-stu-id="ed5ac-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="ed5ac-269">Video</span><span class="sxs-lookup"><span data-stu-id="ed5ac-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="ed5ac-270">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed5ac-270">Next steps</span></span>
* [<span data-ttu-id="ed5ac-271">Monitorare chiamate alle dipendenze</span><span class="sxs-lookup"><span data-stu-id="ed5ac-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="ed5ac-272">Monitorare contatori delle prestazioni Unix</span><span class="sxs-lookup"><span data-stu-id="ed5ac-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="ed5ac-273">Aggiungere il [monitoraggio alle pagine Web](app-insights-javascript.md) per monitorare i tempi di caricamento delle pagine, le chiamate AJAX e le eccezioni del browser.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="ed5ac-274">Scrivere [dati di telemetria personalizzati](app-insights-api-custom-events-metrics.md) per tenere traccia dell'uso nel browser o nel server.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="ed5ac-275">Creare [dashboard](app-insights-dashboards.md) per riunire i grafici chiave per il monitoraggio del sistema.</span><span class="sxs-lookup"><span data-stu-id="ed5ac-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="ed5ac-276">Usare [Analytics](app-insights-analytics.md) per eseguire query avanzate sui dati di telemetria dall'app</span><span class="sxs-lookup"><span data-stu-id="ed5ac-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="ed5ac-277">Per altre informazioni, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="ed5ac-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
