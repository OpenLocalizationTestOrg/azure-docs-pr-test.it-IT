---
title: aaaUpload un tooAzure di app web Java personalizzate
description: Questa esercitazione viene illustrato come un linguaggio personalizzato tooupload web app tooAzure App del servizio Web App.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="3c54b-103">Caricare un tooAzure di app web Java personalizzate</span><span class="sxs-lookup"><span data-stu-id="3c54b-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="3c54b-104">Questo argomento viene illustrato come un linguaggio personalizzato tooupload app web troppo[Azure App Service] App Web.</span><span class="sxs-lookup"><span data-stu-id="3c54b-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="3c54b-105">Sono inoltre incluse informazioni che si applicano anche alcuni esempi per applicazioni specifiche o app web e sito Web Java tooany.</span><span class="sxs-lookup"><span data-stu-id="3c54b-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="3c54b-106">Si noti che Azure fornisce un mezzo per la creazione di applicazioni web Java utilizzando l'interfaccia utente di configurazione del portale di Azure hello e hello Azure Marketplace, come illustrato in [creare un'app web Java in Azure App Service](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3c54b-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="3c54b-107">In questa esercitazione è per gli scenari in cui non si desidera una configurazione del portale di Azure hello toouse dell'interfaccia utente o hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3c54b-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="3c54b-108">Linee guida per la configurazione</span><span class="sxs-lookup"><span data-stu-id="3c54b-108">Configuration guidelines</span></span>
<span data-ttu-id="3c54b-109">Hello di seguito è riportate le impostazioni di hello previste per l'App web Java personalizzate in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c54b-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="3c54b-110">porta HTTP Hello utilizzata da hello processo Java viene assegnata dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="3c54b-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="3c54b-111">il processo di Hello deve usare la porta hello dalla variabile di ambiente hello `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="3c54b-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="3c54b-112">Tutti porte in ascolto diverso listener HTTP singolo hello deve essere disabilitato.</span><span class="sxs-lookup"><span data-stu-id="3c54b-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="3c54b-113">In Tomcat, che include l'arresto di hello, HTTPS e AJP porte.</span><span class="sxs-lookup"><span data-stu-id="3c54b-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="3c54b-114">contenitore di Hello deve toobe configurato per il solo traffico IPv4.</span><span class="sxs-lookup"><span data-stu-id="3c54b-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="3c54b-115">Hello **avvio** comando per un'applicazione hello deve toobe impostato nella configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="3c54b-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="3c54b-116">Le applicazioni che richiedono directory con l'autorizzazione di scrittura devono toobe si trova nella directory del contenuto dell'applicazione web di Azure hello, che è **d:\home.**.</span><span class="sxs-lookup"><span data-stu-id="3c54b-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="3c54b-117">variabile di ambiente Hello `HOME` fa riferimento tooD:\home.</span><span class="sxs-lookup"><span data-stu-id="3c54b-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="3c54b-118">È possibile impostare le variabili di ambiente necessarie nel file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="3c54b-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="3c54b-119">Configurazione httpPlatform in web.config</span><span class="sxs-lookup"><span data-stu-id="3c54b-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="3c54b-120">Hello informazioni seguenti vengono descritte hello **httpplatform in** formato all'interno di Web. config.</span><span class="sxs-lookup"><span data-stu-id="3c54b-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="3c54b-121">**arguments** (impostazione predefinita "").</span><span class="sxs-lookup"><span data-stu-id="3c54b-121">**arguments** (Default="").</span></span> <span data-ttu-id="3c54b-122">Argomenti toohello eseguibile o script specificato nella hello **processPath** impostazione.</span><span class="sxs-lookup"><span data-stu-id="3c54b-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="3c54b-123">Esempi (con **processPath** incluso):</span><span class="sxs-lookup"><span data-stu-id="3c54b-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="3c54b-124">**processPath** -toohello percorso eseguibile o uno script che verrà avviato un processo in ascolto delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="3c54b-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="3c54b-125">Esempi:</span><span class="sxs-lookup"><span data-stu-id="3c54b-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="3c54b-126">**rapidFailsPerMinute** (impostazione predefinita 10) Numero di volte specificato nel processo di hello **processPath** è consentito toocrash al minuto.</span><span class="sxs-lookup"><span data-stu-id="3c54b-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="3c54b-127">Se questo limite viene superato, **HttpPlatformHandler** smetterà di avviare il processo di hello per il resto di hello di minuto hello.</span><span class="sxs-lookup"><span data-stu-id="3c54b-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="3c54b-128">**requestTimeout** (impostazione predefinita "00:02:00") Durata per cui **HttpPlatformHandler** rimarrà in attesa di una risposta dal processo hello in ascolto su `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="3c54b-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="3c54b-129">**startupRetryCount** (impostazione predefinita = 10 secondi) Numero di volte in cui **HttpPlatformHandler** tenterà il processo di hello toolaunch specificato **processPath**.</span><span class="sxs-lookup"><span data-stu-id="3c54b-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="3c54b-130">Per informazioni più dettagliate, vedere **startupTimeLimit**.</span><span class="sxs-lookup"><span data-stu-id="3c54b-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="3c54b-131">**startupTimeLimit** (impostazione predefinita = 10 secondi) Durata per cui **HttpPlatformHandler** rimarrà in attesa di hello eseguibile o script toostart un processo in ascolto sulla porta hello.</span><span class="sxs-lookup"><span data-stu-id="3c54b-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="3c54b-132">Se viene superato questo limite di tempo, **HttpPlatformHandler** verrà terminare il processo di hello e provare toolaunch nuovamente **startupRetryCount** volte.</span><span class="sxs-lookup"><span data-stu-id="3c54b-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="3c54b-133">**stdoutLogEnabled** (impostazione predefinita "true") Se true, **stdout** e **stderr** per processo hello specificato in hello **processPath** impostazione sarà reindirizzato toohello file specificato in  **stdoutLogFile** (vedere **stdoutLogFile** sezione).</span><span class="sxs-lookup"><span data-stu-id="3c54b-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="3c54b-134">**stdoutLogFile** (impostazione predefinita "d:\home\LogFiles\httpPlatformStdout.log") Percorso file assoluto per il quale **stdout** e **stderr** dal processo hello specificato in **processPath** verranno registrati.</span><span class="sxs-lookup"><span data-stu-id="3c54b-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="3c54b-135">`%HTTP_PLATFORM_PORT%`è un segnaposto speciale che deve toospecified o come parte di **argomenti** o come parte di hello **httpplatform in** **environmentVariables** elenco.</span><span class="sxs-lookup"><span data-stu-id="3c54b-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="3c54b-136">Questo verrà sostituito da una porta generata internamente da **HttpPlatformHandler** in modo che il processo di hello specificato dalla **processPath** può restare in ascolto su questa porta.</span><span class="sxs-lookup"><span data-stu-id="3c54b-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="3c54b-137">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="3c54b-137">Deployment</span></span>
<span data-ttu-id="3c54b-138">Le applicazioni web Java in base possono essere distribuite facilmente la maggior parte di hello che stesso indica che vengono utilizzata con le applicazioni web di hello basato su Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="3c54b-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="3c54b-139">FTP, Git e Kudu sono tutte supportate come meccanismo di distribuzione, come è hello funzionalità SCM integrata per le applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="3c54b-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="3c54b-140">WebDeploy è supportato come protocollo ma non è adatto negli scenari di utilizzo che prevedono la distribuzione di un sito Web Java poiché Java non è sviluppato in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c54b-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="3c54b-141">Esempi di configurazione delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="3c54b-141">Application configuration Examples</span></span>
<span data-ttu-id="3c54b-142">Per hello seguenti applicazioni, un file Web. config e hello configurazione dell'applicazione viene fornita come esempi tooshow come tooenable l'applicazione Java in App del servizio Web App.</span><span class="sxs-lookup"><span data-stu-id="3c54b-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="3c54b-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="3c54b-143">Tomcat</span></span>
<span data-ttu-id="3c54b-144">Esistono due varianti nel Tomcat che vengono fornite con l'App del servizio Web App, è comunque possibile tooupload istanze specifiche di clienti.</span><span class="sxs-lookup"><span data-stu-id="3c54b-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="3c54b-145">Di seguito è riportato un esempio di installazione di Tomcat con una Java Virtual Machine (JVM) diversa.</span><span class="sxs-lookup"><span data-stu-id="3c54b-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="3c54b-146">Hello lato Tomcat, esistono alcune modifiche di configurazione necessarie toobe apportate.</span><span class="sxs-lookup"><span data-stu-id="3c54b-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="3c54b-147">Hello server.xml deve tooset toobe modificato:</span><span class="sxs-lookup"><span data-stu-id="3c54b-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="3c54b-148">Porta di arresto = -1</span><span class="sxs-lookup"><span data-stu-id="3c54b-148">Shutdown port = -1</span></span>
* <span data-ttu-id="3c54b-149">Porta connettore HTTP = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="3c54b-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="3c54b-150">Indirizzo connettore HTTP = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="3c54b-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="3c54b-151">Impostare come commento i connettori HTTPS e AJP</span><span class="sxs-lookup"><span data-stu-id="3c54b-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="3c54b-152">Hello IPv4 può anche essere impostata nel file catalina hello in cui è possibile aggiungere`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="3c54b-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="3c54b-153">Chiamate Direct3d non sono supportate in applicazione servizio Web App.</span><span class="sxs-lookup"><span data-stu-id="3c54b-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="3c54b-154">toodisable, aggiungere hello seguente opzione Java deve applicazione effettuare tali chiamate:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="3c54b-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="3c54b-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="3c54b-155">Jetty</span></span>
<span data-ttu-id="3c54b-156">Come accade hello per Tomcat, i clienti possono caricare relative istanze per Jetty.</span><span class="sxs-lookup"><span data-stu-id="3c54b-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="3c54b-157">Nel caso di hello di in esecuzione hello eseguire l'installazione completa di Jetty, configurazione di hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3c54b-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="3c54b-158">configurazione di Jetty Hello deve toobe modificato in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="3c54b-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="3c54b-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="3c54b-159">Springboot</span></span>
<span data-ttu-id="3c54b-160">In ordine tooget un Springboot applicazione in esecuzione è necessario tooupload il file JAR o azioni di GUERRA e aggiunta hello seguenti il file Web. config.</span><span class="sxs-lookup"><span data-stu-id="3c54b-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="3c54b-161">file Web. config Hello inseriti nella cartella wwwroot hello.</span><span class="sxs-lookup"><span data-stu-id="3c54b-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="3c54b-162">In Web. config hello regolare file JAR di hello argomenti toopoint tooyour, hello seguenti il file JAR di esempio hello si trova nella cartella wwwroot di hello anche.</span><span class="sxs-lookup"><span data-stu-id="3c54b-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="3c54b-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="3c54b-163">Hudson</span></span>
<span data-ttu-id="3c54b-164">Test utilizzato hello war Hudson 3.1.2 e hello istanza Tomcat 7.0.50 predefinita ma senza l'utilizzo di operazioni tooset dell'interfaccia utente di hello.</span><span class="sxs-lookup"><span data-stu-id="3c54b-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="3c54b-165">Poiché Hudson è uno strumento di compilazione di software, è consigliato tooinstall sul dedicato istanze in cui hello **AlwaysOn** flag può essere impostato su hello web app.</span><span class="sxs-lookup"><span data-stu-id="3c54b-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="3c54b-166">Nella radice del sito Web di Azure, ad esempio **d:\home\site\wwwroot**, creare una directory **webapps**, se non è già presente, quindi inserire Hudson.war in **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="3c54b-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="3c54b-167">Scaricare apache maven 3.0.5 (compatibile con Hudson) e posizionarlo in **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="3c54b-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="3c54b-168">Creazione di Web. config in **d:\home\site\wwwroot** e Incolla hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="3c54b-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="3c54b-169">A questo punto hello web app può essere riavviato tootake hello modifiche.</span><span class="sxs-lookup"><span data-stu-id="3c54b-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="3c54b-170">Connettersi toohttp://yourwebapp/hudson toostart Hudson.</span><span class="sxs-lookup"><span data-stu-id="3c54b-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="3c54b-171">Al termine Hudson viene configurato, verrà visualizzato hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="3c54b-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="3c54b-173">Hello accesso pagina configuration di Hudson: fare clic su **gestire Hudson**, quindi fare clic su **Configura sistema**.</span><span class="sxs-lookup"><span data-stu-id="3c54b-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="3c54b-174">Configurare hello JDK, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3c54b-174">Configure hello JDK as shown below:</span></span>
   
    ![Configurazione di Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="3c54b-176">Configurare Maven come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3c54b-176">Configure Maven as shown below:</span></span>
   
    ![Configurazione di Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="3c54b-178">Salvare le impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="3c54b-178">Save hello settings.</span></span> <span data-ttu-id="3c54b-179">A questo punto Hudson dovrebbe essere configurato e pronto per l'uso.</span><span class="sxs-lookup"><span data-stu-id="3c54b-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="3c54b-180">Per ulteriori informazioni su Hudson, vedere [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="3c54b-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="3c54b-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="3c54b-181">Liferay</span></span>
<span data-ttu-id="3c54b-182">Liferay è supportato in applicazione servizio Web App.</span><span class="sxs-lookup"><span data-stu-id="3c54b-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="3c54b-183">Poiché Liferay possono richiedere notevole di memoria, l'app web hello deve toorun su un lavoro dedicato medio o grandi dimensioni, che può fornire memoria sufficiente.</span><span class="sxs-lookup"><span data-stu-id="3c54b-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="3c54b-184">Liferay anche richiede diversi minuti toostart.</span><span class="sxs-lookup"><span data-stu-id="3c54b-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="3c54b-185">Per questo motivo, è consigliabile impostare app web hello troppo**Always On**.</span><span class="sxs-lookup"><span data-stu-id="3c54b-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="3c54b-186">Usa Liferay 6.1.2 che Community Edition GA3 in bundle con Tomcat, hello seguenti file sono stati modificati dopo il download Liferay:</span><span class="sxs-lookup"><span data-stu-id="3c54b-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="3c54b-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="3c54b-187">**Server.xml**</span></span>

* <span data-ttu-id="3c54b-188">Modificare arresto porta troppo-1.</span><span class="sxs-lookup"><span data-stu-id="3c54b-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="3c54b-189">Modificare anche il connettore HTTP`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="3c54b-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="3c54b-190">Connettore AJP hello come commento.</span><span class="sxs-lookup"><span data-stu-id="3c54b-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="3c54b-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** cartella, creare un file denominato **portale ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="3c54b-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="3c54b-192">Questo file deve toocontain una riga, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3c54b-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="3c54b-193">Hello stesso livello di directory come cartella tomcat 7.0.40 hello, creare un file denominato **Web. config** con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="3c54b-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="3c54b-194">In hello **httpplatform in** blocco, hello **requestTimeout** è troppo "00: 10:00".</span><span class="sxs-lookup"><span data-stu-id="3c54b-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="3c54b-195">Quest'ultimo può essere ridotto ma si è probabilmente toosee alcuni errori di timeout durante il Liferay è l'avvio.</span><span class="sxs-lookup"><span data-stu-id="3c54b-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="3c54b-196">Se questo valore viene modificato, hello **connectionTimeout** in tomcat hello server.xml dovrebbe essere modificato.</span><span class="sxs-lookup"><span data-stu-id="3c54b-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="3c54b-197">Vale la pena notare che varariable di ambiente JRE_HOME hello è specificato in hello di sopra di Web. config toopoint toohello JDK a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="3c54b-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="3c54b-198">valore predefinito di Hello è a 32 bit, ma poiché Liferay potrebbe richiedono livelli elevati di memoria, è consigliabile toouse hello JDK a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="3c54b-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="3c54b-199">Dopo avere apportato le modifiche indicate, riavviare l'app Web che esegue Liferay, quindi aprire http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="3c54b-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="3c54b-200">portale Liferay Hello è disponibile dalla radice di app web hello.</span><span class="sxs-lookup"><span data-stu-id="3c54b-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3c54b-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c54b-201">Next steps</span></span>
<span data-ttu-id="3c54b-202">Per ulteriori informazioni su Liferay, vedere [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="3c54b-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="3c54b-203">Per altre informazioni su Java, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="3c54b-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
