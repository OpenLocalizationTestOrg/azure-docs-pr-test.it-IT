---
title: analitica di app web aaaJava con Azure Application Insights | Documenti Microsoft
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
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="cfe09-103">Introduzione ad Application Insights in un progetto Web Java</span><span class="sxs-lookup"><span data-stu-id="cfe09-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="cfe09-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) è un servizio estendibile analitica per gli sviluppatori web che consentono di comprendano le prestazioni di hello e l'utilizzo dell'applicazione in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="cfe09-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="cfe09-105">Utilizzarlo troppo[rilevare e diagnosticare i problemi di prestazioni ed eccezioni](app-insights-detect-triage-diagnose.md), e [scrivere codice] [ api] tootrack degli utenti a cui eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="cfe09-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![dati di esempio](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="cfe09-107">Application Insights supporta le app Java in esecuzione in Linux, Unix o Windows.</span><span class="sxs-lookup"><span data-stu-id="cfe09-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="cfe09-108">Sono necessari:</span><span class="sxs-lookup"><span data-stu-id="cfe09-108">You need:</span></span>

* <span data-ttu-id="cfe09-109">Oracle JRE 1.6 o versione successiva o isiZulu JRE 1.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="cfe09-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="cfe09-110">Una sottoscrizione troppo[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="cfe09-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="cfe09-111">*Se si dispone di un'app web che è già in tempo reale, si può seguire la procedura alternativa hello troppo[aggiungere hello SDK in fase di esecuzione nel server web hello](app-insights-java-live.md). Tale alternativa consente di evitare la ricompilazione di codice hello, ma non si ottiene l'attività dell'utente tootrack toowrite codice hello opzione.*</span><span class="sxs-lookup"><span data-stu-id="cfe09-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="cfe09-112">1. Ottenere una chiave di strumentazione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="cfe09-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="cfe09-113">Accedi toohello [portale Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cfe09-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cfe09-114">Creare una risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cfe09-114">Create an Application Insights resource.</span></span> <span data-ttu-id="cfe09-115">Impostare hello tipo tooJava applicazione web.</span><span class="sxs-lookup"><span data-stu-id="cfe09-115">Set hello application type tooJava web application.</span></span>

    ![Inserire un nome, scegliere l'app Web Java e fare clic su Crea](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="cfe09-117">Trovare la chiave di strumentazione hello della nuova risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="cfe09-118">È necessario toopaste questa chiave nel progetto di codice a breve.</span><span class="sxs-lookup"><span data-stu-id="cfe09-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="cfe09-120">2. Aggiungere hello Application Insights SDK per il progetto tooyour Java</span><span class="sxs-lookup"><span data-stu-id="cfe09-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="cfe09-121">*Scegliere hello modalità appropriata per il progetto.*</span><span class="sxs-lookup"><span data-stu-id="cfe09-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="cfe09-122">Se si usa Eclipse toocreate un progetto Web dinamico o Maven...</span><span class="sxs-lookup"><span data-stu-id="cfe09-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="cfe09-123">Hello utilizzare [Application Insights SDK per Java plug-in][eclipse].</span><span class="sxs-lookup"><span data-stu-id="cfe09-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="cfe09-124">Se si usa Maven...</span><span class="sxs-lookup"><span data-stu-id="cfe09-124">If you're using Maven...</span></span>
<span data-ttu-id="cfe09-125">Se il progetto è già impostato toouse Maven per la compilazione, di tipo merge seguenti codice tooyour pom.xml file hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="cfe09-126">Quindi, file binari di hello tooget dipendenze progetto hello aggiornamento scaricato.</span><span class="sxs-lookup"><span data-stu-id="cfe09-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

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

* <span data-ttu-id="cfe09-127">*Errori di convalida checksum o compilazione?*</span><span class="sxs-lookup"><span data-stu-id="cfe09-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="cfe09-128">Provare a usare una versione specifica, ad esempio `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="cfe09-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="cfe09-129">È disponibile la versione più recente di hello in hello [note sulla versione di SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) o nel nostro [elementi Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="cfe09-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="cfe09-130">*Necessario tooupdate tooa nuovo SDK?*</span><span class="sxs-lookup"><span data-stu-id="cfe09-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="cfe09-131">Aggiornare le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="cfe09-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="cfe09-132">Se si usa Gradle...</span><span class="sxs-lookup"><span data-stu-id="cfe09-132">If you're using Gradle...</span></span>
<span data-ttu-id="cfe09-133">Se il progetto è già impostato toouse Gradle per la compilazione, unire hello seguenti file di codice tooyour gradle.</span><span class="sxs-lookup"><span data-stu-id="cfe09-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="cfe09-134">File binari di hello tooget dipendenze progetto hello aggiornamento scaricati.</span><span class="sxs-lookup"><span data-stu-id="cfe09-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="cfe09-135">*Errori di convalida checksum o compilazione? Provare a usare una versione specifica, come* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="cfe09-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="cfe09-136">*È disponibile la versione più recente di hello in hello [note sulla versione di SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="cfe09-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="cfe09-137">*tooupdate tooa nuovo SDK*</span><span class="sxs-lookup"><span data-stu-id="cfe09-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="cfe09-138">Aggiornare le dipendenze del progetto.</span><span class="sxs-lookup"><span data-stu-id="cfe09-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="cfe09-139">In caso contrario...</span><span class="sxs-lookup"><span data-stu-id="cfe09-139">Otherwise ...</span></span>
<span data-ttu-id="cfe09-140">Aggiungere manualmente hello SDK:</span><span class="sxs-lookup"><span data-stu-id="cfe09-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="cfe09-141">Scaricare hello [Application Insights SDK per Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="cfe09-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="cfe09-142">Estrarre i file binari hello da file zip hello e aggiungerli tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="cfe09-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="cfe09-143">Domande...</span><span class="sxs-lookup"><span data-stu-id="cfe09-143">Questions...</span></span>
* <span data-ttu-id="cfe09-144">*Qual è la relazione hello tra hello `-core` e `-web` componenti ZIP hello?*</span><span class="sxs-lookup"><span data-stu-id="cfe09-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="cfe09-145">`applicationinsights-core`consente che Hello bare API.</span><span class="sxs-lookup"><span data-stu-id="cfe09-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="cfe09-146">Questo componente sarà sempre necessario.</span><span class="sxs-lookup"><span data-stu-id="cfe09-146">You always need this component.</span></span>
  * <span data-ttu-id="cfe09-147">`applicationinsights-web` fornisce le metriche che consentono di tenere traccia del numero e dei tempi di risposta delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="cfe09-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="cfe09-148">Questo componente può essere omesso se non si vuole che questi dati di telemetria vengano raccolti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cfe09-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="cfe09-149">Ad esempio, se si desidera toowrite personalizzati.</span><span class="sxs-lookup"><span data-stu-id="cfe09-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="cfe09-150">*hello tooupdate SDK di quando si pubblicano le modifiche*</span><span class="sxs-lookup"><span data-stu-id="cfe09-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="cfe09-151">Download più recenti hello [Application Insights SDK per Java](https://aka.ms/qqkaq6) e sostituire hello quelle meno recenti.</span><span class="sxs-lookup"><span data-stu-id="cfe09-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="cfe09-152">Le modifiche sono descritte in hello [note sulla versione di SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="cfe09-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="cfe09-153">3. Aggiungere un file XML di Application Insights</span><span class="sxs-lookup"><span data-stu-id="cfe09-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="cfe09-154">Aggiungere una cartella di risorse toohello ApplicationInsights.xml nel progetto o assicurarsi che viene aggiunto un percorso di classe di distribuzione del progetto tooyour.</span><span class="sxs-lookup"><span data-stu-id="cfe09-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="cfe09-155">Copiare hello seguente XML al suo interno.</span><span class="sxs-lookup"><span data-stu-id="cfe09-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="cfe09-156">Sostituire con chiave di strumentazione hello recuperato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="cfe09-157">chiave di strumentazione Hello viene inviata insieme a tutti gli elementi di dati di telemetria e indica toodisplay Application Insights nella risorsa.</span><span class="sxs-lookup"><span data-stu-id="cfe09-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="cfe09-158">componente di richiesta HTTP Hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="cfe09-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="cfe09-159">Invia automaticamente i dati di telemetria sulle richieste e portale toohello tempi di risposta.</span><span class="sxs-lookup"><span data-stu-id="cfe09-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="cfe09-160">Correlazione di eventi è un componente di richiesta di aggiunta toohello HTTP.</span><span class="sxs-lookup"><span data-stu-id="cfe09-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="cfe09-161">Assegna una richiesta di tooeach identificatore ricevuta dal server hello e aggiunge questo identificatore come un elemento di dati di telemetria tooevery delle proprietà come proprietà hello 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="cfe09-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="cfe09-162">Consente di telemetria hello toocorrelate associata a ogni richiesta impostando un filtro [ricerca diagnostica][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="cfe09-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="cfe09-163">chiave di Application Insights Hello può essere passato in modo dinamico da hello portale di Azure come una proprietà di sistema (-DAPPLICATION_INSIGHTS_IKEY = your_ikey).</span><span class="sxs-lookup"><span data-stu-id="cfe09-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="cfe09-164">Se non è presente una proprietà definita, viene verificata la presenza della variabile di ambiente (APPLICATION_INSIGHTS_IKEY) nelle impostazioni dell'app Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe09-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="cfe09-165">Se entrambe le proprietà hello sono definite, viene usato il predefinito di hello manualmente InstrumentationKey da ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="cfe09-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="cfe09-166">Questa sequenza consente di toomanage InstrumentationKeys diversi per diversi ambienti in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="cfe09-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="cfe09-167">Chiave di strumentazione di metodi alternativi tooset hello</span><span class="sxs-lookup"><span data-stu-id="cfe09-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="cfe09-168">Application Insights SDK cerca i chiave hello in questo ordine:</span><span class="sxs-lookup"><span data-stu-id="cfe09-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="cfe09-169">Proprietà di sistema: -DAPPLICATION_INSIGHTS_IKEY=ikey</span><span class="sxs-lookup"><span data-stu-id="cfe09-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="cfe09-170">Variabile di ambiente: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="cfe09-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="cfe09-171">File di configurazione: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="cfe09-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="cfe09-172">È anche possibile eseguirne l' [impostazione nel codice](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="cfe09-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="cfe09-173">4. Aggiungere un filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="cfe09-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="cfe09-174">ultimo passaggio di configurazione Hello consente hello HTTP richiesta componente toolog ogni richiesta web.</span><span class="sxs-lookup"><span data-stu-id="cfe09-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="cfe09-175">(Non obbligatorio se si desidera hello bare API).</span><span class="sxs-lookup"><span data-stu-id="cfe09-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="cfe09-176">Individuare e aprire i file Web. XML hello nel progetto e hello merge seguente codice nel nodo di app web hello, dove sono stati configurati i filtri di applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfe09-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="cfe09-177">risultati più accurati tooget hello, filtro hello devono essere mappati prima tutti gli altri filtri.</span><span class="sxs-lookup"><span data-stu-id="cfe09-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="cfe09-178">Se si usa Spring Web MVC 3.1 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="cfe09-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="cfe09-179">Modificare questi elementi in *-pacchetto di Application Insights servlet.xml tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="cfe09-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="cfe09-180">Se si usa Struts 2</span><span class="sxs-lookup"><span data-stu-id="cfe09-180">If you're using Struts 2</span></span>
<span data-ttu-id="cfe09-181">Aggiungere questo file di configurazione di elementi toohello strutture (in genere denominata struts.xml o strutture default.xml):</span><span class="sxs-lookup"><span data-stu-id="cfe09-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="cfe09-182">(Se si dispone di intercettori definiti in uno stack predefinita, l'intercettore hello semplicemente aggiungere stack toothat.)</span><span class="sxs-lookup"><span data-stu-id="cfe09-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="cfe09-183">5. Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="cfe09-183">5. Run your application</span></span>
<span data-ttu-id="cfe09-184">Eseguirlo in modalità di debug nel computer di sviluppo oppure tooyour server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="cfe09-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="cfe09-185">6. Visualizzare i dati di telemetria in Application Insights</span><span class="sxs-lookup"><span data-stu-id="cfe09-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="cfe09-186">Restituzione della risorsa di Application Insights tooyour in [portale Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cfe09-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="cfe09-187">Dati di richieste HTTP vengono visualizzati nel pannello della panoramica hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="cfe09-188">Se non sono visualizzati, attendere alcuni secondi e quindi fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="cfe09-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dati di esempio](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="cfe09-190">[Altre informazioni sulle metriche.][metrics]</span><span class="sxs-lookup"><span data-stu-id="cfe09-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="cfe09-191">Click-through toosee qualsiasi grafico più dettagliate aggregate le metriche.</span><span class="sxs-lookup"><span data-stu-id="cfe09-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="cfe09-192">Application Insights si presuppone il formato di hello di richieste HTTP per le applicazioni MVC: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="cfe09-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="cfe09-193">Ad esempio, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` e `GET Home/Product/sdf96vws` vengono raggruppati in `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="cfe09-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="cfe09-194">Questo raggruppamento consente aggregazioni significative delle richieste, come il numero di richieste e il tempo medio di esecuzione per le richieste.</span><span class="sxs-lookup"><span data-stu-id="cfe09-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="cfe09-195">Dati dell'istanza</span><span class="sxs-lookup"><span data-stu-id="cfe09-195">Instance data</span></span>
<span data-ttu-id="cfe09-196">Fare clic su tramite una richiesta specifica digitare toosee singole istanze.</span><span class="sxs-lookup"><span data-stu-id="cfe09-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="cfe09-197">In Application Insights vengono visualizzati due tipi di dati, ovvero i dati aggregati, archiviati e visualizzati come medie, conteggi e somme, e i dati di istanza, ovvero singoli report di richieste HTTP, eccezioni, visualizzazioni di pagina o eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="cfe09-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="cfe09-198">Quando si visualizzano le proprietà di hello di una richiesta, è possibile visualizzare gli eventi di telemetria hello associati, ad esempio le richieste e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="cfe09-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="cfe09-199">Analytics: linguaggio di query avanzato</span><span class="sxs-lookup"><span data-stu-id="cfe09-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="cfe09-200">Come si accumulano più dati, è possibile eseguire query entrambi tooaggregate dati e toofind le singole istanze.</span><span class="sxs-lookup"><span data-stu-id="cfe09-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="cfe09-201">[Analisi](app-insights-analytics.md) è uno strumento avanzato per ottenere informazioni sulle prestazioni e sull'utilizzo e ai fini della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="cfe09-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Esempio di Analytics](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="cfe09-203">7. Installare l'applicazione nel server hello</span><span class="sxs-lookup"><span data-stu-id="cfe09-203">7. Install your app on hello server</span></span>
<span data-ttu-id="cfe09-204">Pubblicare il server toohello app, consentire alle persone che usano e guardare telemetria hello visualizzati nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="cfe09-205">Verificare che il firewall consenta le porte di telemetria toothese toosend l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="cfe09-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="cfe09-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="cfe09-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="cfe09-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="cfe09-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="cfe09-208">Se il traffico in uscita deve essere instradato attraverso un firewall, definire le proprietà di sistema `http.proxyHost` e `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="cfe09-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="cfe09-209">Nei server Windows installare:</span><span class="sxs-lookup"><span data-stu-id="cfe09-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="cfe09-210">Microsoft Visual C++ Redistributable Package</span><span class="sxs-lookup"><span data-stu-id="cfe09-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="cfe09-211">Questo componente abilita i contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cfe09-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="cfe09-212">Eccezioni e richieste non eseguite</span><span class="sxs-lookup"><span data-stu-id="cfe09-212">Exceptions and request failures</span></span>
<span data-ttu-id="cfe09-213">Vengono raccolte automaticamente le eccezioni non gestite:</span><span class="sxs-lookup"><span data-stu-id="cfe09-213">Unhandled exceptions are automatically collected:</span></span>

![Aprire Impostazioni e quindi Errori](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="cfe09-215">dati toocollect su altre eccezioni, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="cfe09-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="cfe09-216">[Inserire le chiamate nel codice tootrackException()][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="cfe09-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="cfe09-217">[Installare hello Java agente nel server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="cfe09-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="cfe09-218">Specificare i metodi di hello da toowatch.</span><span class="sxs-lookup"><span data-stu-id="cfe09-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="cfe09-219">Monitorare le chiamate al metodo e le dipendenze esterne</span><span class="sxs-lookup"><span data-stu-id="cfe09-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="cfe09-220">[Installare l'agente APM Java hello](app-insights-java-agent.md) toolog specificato metodi interni e le chiamate effettuate tramite JDBC, con dati di intervallo.</span><span class="sxs-lookup"><span data-stu-id="cfe09-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="cfe09-221">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="cfe09-221">Performance counters</span></span>
<span data-ttu-id="cfe09-222">Aprire **impostazioni**, **server**, toosee un intervallo di contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cfe09-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="cfe09-223">Personalizzare la raccolta del contatore delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="cfe09-223">Customize performance counter collection</span></span>
<span data-ttu-id="cfe09-224">toodisable raccolta di set di contatori delle prestazioni, standard di hello aggiungere hello seguente codice sotto il nodo radice hello del file ApplicationInsights.xml hello:</span><span class="sxs-lookup"><span data-stu-id="cfe09-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="cfe09-225">Raccogliere dei contatori di prestazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cfe09-225">Collect additional performance counters</span></span>
<span data-ttu-id="cfe09-226">È possibile specificare toobe i contatori delle prestazioni raccolti.</span><span class="sxs-lookup"><span data-stu-id="cfe09-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="cfe09-227">Contatori JMX (esposti da hello Java Virtual Machine)</span><span class="sxs-lookup"><span data-stu-id="cfe09-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="cfe09-228">`displayName`– nome hello visualizzato nel portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="cfe09-229">`objectName`– nome dell'oggetto JMX hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="cfe09-230">`attribute`: attributo hello di hello JMX oggetto nome toofetch</span><span class="sxs-lookup"><span data-stu-id="cfe09-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="cfe09-231">`type`(facoltativo): tipo di attributo dell'oggetto JMX hello:</span><span class="sxs-lookup"><span data-stu-id="cfe09-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="cfe09-232">Impostazione predefinita: un tipo semplice come int o long.</span><span class="sxs-lookup"><span data-stu-id="cfe09-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="cfe09-233">`composite`: i dati dei contatori delle prestazioni hello sono nel formato 'Attribute.Data' hello</span><span class="sxs-lookup"><span data-stu-id="cfe09-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="cfe09-234">`tabular`: i dati dei contatori delle prestazioni hello sono nel formato hello di una riga di tabella</span><span class="sxs-lookup"><span data-stu-id="cfe09-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="cfe09-235">Contatori delle prestazioni di Windows</span><span class="sxs-lookup"><span data-stu-id="cfe09-235">Windows performance counters</span></span>
<span data-ttu-id="cfe09-236">Ogni [contatore delle prestazioni Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) è un membro di una categoria (in hello allo stesso modo che un campo è un membro di una classe).</span><span class="sxs-lookup"><span data-stu-id="cfe09-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="cfe09-237">Le categorie possono essere globali o possono disporre di istanze numerate o denominate.</span><span class="sxs-lookup"><span data-stu-id="cfe09-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="cfe09-238">displayName: nome hello visualizzato nel portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="cfe09-239">categoryName: hello categoria contatori delle prestazioni (oggetto prestazioni) a cui è associato questo contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cfe09-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="cfe09-240">counterName – nome hello hello del contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cfe09-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="cfe09-241">instanceName-nome hello dell'istanza di categoria del contatore delle prestazioni hello o una stringa vuota (""), se la categoria hello contiene una sola istanza.</span><span class="sxs-lookup"><span data-stu-id="cfe09-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="cfe09-242">Se categoryName hello è processo e si desidera toocollect contatore delle prestazioni hello è dal processo JVM corrente hello in cui è in esecuzione l'app, specificare `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="cfe09-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="cfe09-243">I contatori delle prestazioni sono visibili come metriche personalizzate in [Esplora metriche][metrics].</span><span class="sxs-lookup"><span data-stu-id="cfe09-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="cfe09-244">Contatori delle prestazioni Unix</span><span class="sxs-lookup"><span data-stu-id="cfe09-244">Unix performance counters</span></span>
* <span data-ttu-id="cfe09-245">[Installare collectd con plug-in Application Insights hello](app-insights-java-collectd.md) tooget un'ampia gamma di dati di sistema e di rete.</span><span class="sxs-lookup"><span data-stu-id="cfe09-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="cfe09-246">Ottenere i dati relativi a utenti e sessioni</span><span class="sxs-lookup"><span data-stu-id="cfe09-246">Get user and session data</span></span>
<span data-ttu-id="cfe09-247">I dati di telemetria vengono normalmente inviati dal server Web.</span><span class="sxs-lookup"><span data-stu-id="cfe09-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="cfe09-248">Ora tooget hello 360 gradi di visualizzazione dell'applicazione, è possibile aggiungere più monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="cfe09-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="cfe09-249">[Aggiungere le pagine web di telemetria tooyour] [ usage] toomonitor pagina viste e le metriche di utente.</span><span class="sxs-lookup"><span data-stu-id="cfe09-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="cfe09-250">[Configurare i test web] [ availability] toomake che l'applicazione rimane in tempo reale e reattiva.</span><span class="sxs-lookup"><span data-stu-id="cfe09-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="cfe09-251">Acquisire le tracce dei log</span><span class="sxs-lookup"><span data-stu-id="cfe09-251">Capture log traces</span></span>
<span data-ttu-id="cfe09-252">È possibile utilizzare Application Insights tooslice e ripartiscono registri Log4J o Logback altri framework di registrazione.</span><span class="sxs-lookup"><span data-stu-id="cfe09-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="cfe09-253">È possibile correlare i registri di hello con richieste HTTP e altri dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="cfe09-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="cfe09-254">[Informazioni][javalogs].</span><span class="sxs-lookup"><span data-stu-id="cfe09-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="cfe09-255">Inviare i propri dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="cfe09-255">Send your own telemetry</span></span>
<span data-ttu-id="cfe09-256">Ora che è stato installato hello SDK, è possibile utilizzare hello API toosend propri dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="cfe09-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="cfe09-257">[Tenere traccia di eventi personalizzati e le metriche] [ api] toolearn gli utenti che eseguono l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cfe09-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="cfe09-258">[Ricerca di eventi e log] [ diagnostic] toohelp diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="cfe09-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="cfe09-259">Test Web di disponibilità</span><span class="sxs-lookup"><span data-stu-id="cfe09-259">Availability web tests</span></span>
<span data-ttu-id="cfe09-260">Application Insights è possibile testare il sito Web all'indirizzo toocheck a intervalli regolari che è attivo e risponde correttamente.</span><span class="sxs-lookup"><span data-stu-id="cfe09-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="cfe09-261">[tooset backup][availability], fare clic su test Web.</span><span class="sxs-lookup"><span data-stu-id="cfe09-261">[tooset up][availability], click Web tests.</span></span>

![Fare clic su Test Web e quindi su Aggiungi test Web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="cfe09-263">Se il sito è inattivo, si otterranno grafici dei tempi di risposta, nonché notifiche di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="cfe09-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Esempio di test Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="cfe09-265">[Altre informazioni sui test Web di disponibilità.][availability]</span><span class="sxs-lookup"><span data-stu-id="cfe09-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="cfe09-266">Domande?</span><span class="sxs-lookup"><span data-stu-id="cfe09-266">Questions?</span></span> <span data-ttu-id="cfe09-267">Problemi?</span><span class="sxs-lookup"><span data-stu-id="cfe09-267">Problems?</span></span>
[<span data-ttu-id="cfe09-268">Risoluzione dei problemi Java</span><span class="sxs-lookup"><span data-stu-id="cfe09-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="cfe09-269">Video</span><span class="sxs-lookup"><span data-stu-id="cfe09-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="cfe09-270">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cfe09-270">Next steps</span></span>
* [<span data-ttu-id="cfe09-271">Monitorare chiamate alle dipendenze</span><span class="sxs-lookup"><span data-stu-id="cfe09-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="cfe09-272">Monitorare contatori delle prestazioni Unix</span><span class="sxs-lookup"><span data-stu-id="cfe09-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="cfe09-273">Aggiungere [monitoraggio le pagine web tooyour](app-insights-javascript.md) tempi di caricamento pagina toomonitor, le chiamate AJAX, le eccezioni del browser.</span><span class="sxs-lookup"><span data-stu-id="cfe09-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="cfe09-274">Scrivere [telemetria personalizzata](app-insights-api-custom-events-metrics.md) tootrack utilizzo in hello browser o nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="cfe09-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="cfe09-275">Creare [dashboard](app-insights-dashboards.md) toobring grafici con chiave hello insieme per il monitoraggio del sistema.</span><span class="sxs-lookup"><span data-stu-id="cfe09-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="cfe09-276">Usare [Analytics](app-insights-analytics.md) per eseguire query avanzate sui dati di telemetria dall'app</span><span class="sxs-lookup"><span data-stu-id="cfe09-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="cfe09-277">Per altre informazioni, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="cfe09-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
