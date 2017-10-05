---
title: Caricamento di un sito Web Java personalizzato in Azure
description: In questa esercitazione viene illustrato come caricare un'applicazione web di Java personalizzata in Azure applicazione servizio Web Apps.
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
ms.openlocfilehash: 9c8f9ee7780859f7640ac82d6ebce85082170ad7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-custom-java-web-app-to-azure"></a><span data-ttu-id="c3cf6-103">Caricamento di un sito Web Java personalizzato in Azure</span><span class="sxs-lookup"><span data-stu-id="c3cf6-103">Upload a custom Java web app to Azure</span></span>
<span data-ttu-id="c3cf6-104">Questo argomento illustra come caricare un'app Web Java personalizzata nelle app Web del [servizio app di Azure] .</span><span class="sxs-lookup"><span data-stu-id="c3cf6-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span></span> <span data-ttu-id="c3cf6-105">Sono incluse informazioni applicabili a qualsiasi sito Web Java e vengono forniti alcuni esempi per specifiche applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="c3cf6-106">Si noti che Azure fornisce un mezzo per la creazione di applicazioni web Java utilizzando l'interfaccia utente di configurazione del portale di Azure e Azure Marketplace, come descritto in [creare un'applicazione web Java nel servizio App di Azure](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3cf6-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="c3cf6-107">Questa esercitazione è adatta per gli scenari in cui si preferisce non usare l'interfaccia di configurazione del Portale di Azure o il Marketplace di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="c3cf6-108">Linee guida per la configurazione</span><span class="sxs-lookup"><span data-stu-id="c3cf6-108">Configuration guidelines</span></span>
<span data-ttu-id="c3cf6-109">Di seguito sono descritte le impostazioni previste per i siti Web Java personalizzati in Azure.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-109">The following describes the settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="c3cf6-110">La porta HTTP utilizzata dal processo Java viene assegnata in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-110">The HTTP port used by the Java process is dynamically assigned.</span></span>  <span data-ttu-id="c3cf6-111">Il processo deve usare la porta indicata dalla variabile di ambiente `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="c3cf6-112">Tutte le porte di ascolto diverse dal listener HTTP devono essere disabilitate.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-112">All listen ports other than the single HTTP listener should be disabled.</span></span>  <span data-ttu-id="c3cf6-113">In Tomcat questo include le porte di arresto, HTTPS e AJP.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="c3cf6-114">Il contenitore deve essere configurato solo per il traffico IPv4.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-114">The container needs to be configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="c3cf6-115">Il comando **startup** per l'applicazione deve essere impostato nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-115">The **startup** command for the application needs to be set in the configuration.</span></span>
* <span data-ttu-id="c3cf6-116">Le applicazioni che richiedono directory con autorizzazioni di scrittura devono trovarsi nella directory del contenuto di App Web di Azure, ovvero **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="c3cf6-117">La variabile di ambiente `HOME` fa riferimento a D:\home.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-117">The environmental variable `HOME` refers to D:\home.</span></span>  

<span data-ttu-id="c3cf6-118">Le variabili di ambiente possono essere impostate come richiesto nel file web.config.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-118">You can set environment variables as required in the web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="c3cf6-119">Configurazione httpPlatform in web.config</span><span class="sxs-lookup"><span data-stu-id="c3cf6-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="c3cf6-120">Le informazioni riportate di seguito descrivono il formato **httpPlatform** all'interno di web.config.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-120">The following information describes the **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="c3cf6-121">**arguments** (impostazione predefinita "").</span><span class="sxs-lookup"><span data-stu-id="c3cf6-121">**arguments** (Default="").</span></span> <span data-ttu-id="c3cf6-122">argomenti per l'eseguibile o lo script specificato nell'impostazione **processPath**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-122">Arguments to the executable or script specified in the **processPath** setting.</span></span>

<span data-ttu-id="c3cf6-123">Esempi (con **processPath** incluso):</span><span class="sxs-lookup"><span data-stu-id="c3cf6-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="c3cf6-124">**processPath** : percorso dell'eseguibile o dello script che avvierà un processo in ascolto delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="c3cf6-125">Esempi:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="c3cf6-126">**rapidFailsPerMinute** (impostazione predefinita 10) numero di blocchi al minuto consentiti per il processo specificato in **processPath**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="c3cf6-127">Se questo limite viene superato, **HttpPlatformHandler** interromperà l'avvio del processo per il resto del minuto.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span></span>

<span data-ttu-id="c3cf6-128">**requestTimeout** (impostazione predefinita "00:02:00") Periodo di tempo per cui **HttpPlatformHandler** attende una risposta dal processo in ascolto su `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="c3cf6-129">**startupRetryCount** (impostazione predefinita = 10 secondi) numero di volte per cui **HttpPlatformHandler** tenterà di avviare il processo specificato in **processPath**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span></span> <span data-ttu-id="c3cf6-130">Per informazioni più dettagliate, vedere **startupTimeLimit**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="c3cf6-131">**startupTimeLimit** (impostazione predefinita = 10 secondi) tempo per cui **HttpPlatformHandler** attende che l'eseguibile/script avvii un processo in ascolto sulla porta.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span></span>  <span data-ttu-id="c3cf6-132">Se questo limite di tempo viene superato, **HttpPlatformHandler** terminerà il processo e tenterà di riavviarlo il numero di volte indicato da **startupRetryCount**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="c3cf6-133">**stdoutLogEnabled** (impostazione predefinita "true") se è impostato su true, **stdout** e **stderr** per il processo specificato nell'impostazione **processPath** verranno reindirizzati al file specificato in **stdoutLogFile** (vedere la sezione relativa a **stdoutLogFile**).</span><span class="sxs-lookup"><span data-stu-id="c3cf6-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="c3cf6-134">**stdoutLogFile** (impostazione predefinita "d:\home\LogFiles\httpPlatformStdout.log") percorso file assoluto per cui verranno registrati **stdout** e **stderr** dal processo specificato in **processPath**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="c3cf6-135">`%HTTP_PLATFORM_PORT%` è un segnaposto speciale che deve essere specificato come parte di **arguments** o dell'elenco **httpPlatform** **environmentVariables**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="c3cf6-136">Verranno sostituiti da una porta generata internamente da **HttpPlatformHandler** affinché il processo specificato in **processPath** possa restare in ascolto su questa porta.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="c3cf6-137">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="c3cf6-137">Deployment</span></span>
<span data-ttu-id="c3cf6-138">I siti Web basati su Java possono essere distribuiti facilmente con quasi tutti i metodi usati per le applicazioni Web basate su Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="c3cf6-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="c3cf6-139">FTP, Git e Kudu sono supportati come meccanismi di distribuzione, così come la funzionalità SCM integrata per i siti Web.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span></span> <span data-ttu-id="c3cf6-140">WebDeploy è supportato come protocollo ma non è adatto negli scenari di utilizzo che prevedono la distribuzione di un sito Web Java poiché Java non è sviluppato in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="c3cf6-141">Esempi di configurazione delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="c3cf6-141">Application configuration Examples</span></span>
<span data-ttu-id="c3cf6-142">Per le applicazioni seguenti vengono forniti un file web.config e la configurazione dell'applicazione come esempi per illustrare come abilitare l'applicazione Java nei siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="c3cf6-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="c3cf6-143">Tomcat</span></span>
<span data-ttu-id="c3cf6-144">Con Siti Web di Azure vengono fornite due varianti Tomcat, ma è comunque possibile caricare istanze specifiche del cliente.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span></span> <span data-ttu-id="c3cf6-145">Di seguito è riportato un esempio di installazione di Tomcat con una Java Virtual Machine (JVM) diversa.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default to %programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="c3cf6-146">Sul lato Tomcat è necessario apportare alcune modifiche alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-146">On the Tomcat side, there are a few configuration changes that need to be made.</span></span> <span data-ttu-id="c3cf6-147">È necessario modificare il file server.xml per impostare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-147">The server.xml needs to be edited to set:</span></span>

* <span data-ttu-id="c3cf6-148">Porta di arresto = -1</span><span class="sxs-lookup"><span data-stu-id="c3cf6-148">Shutdown port = -1</span></span>
* <span data-ttu-id="c3cf6-149">Porta connettore HTTP = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="c3cf6-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="c3cf6-150">Indirizzo connettore HTTP = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="c3cf6-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="c3cf6-151">Impostare come commento i connettori HTTPS e AJP</span><span class="sxs-lookup"><span data-stu-id="c3cf6-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="c3cf6-152">L'impostazione IPv4 può essere configurata anche nel file catalina.properties in cui è possibile aggiungere `java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="c3cf6-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="c3cf6-153">Chiamate Direct3d non sono supportate in applicazione servizio Web App.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="c3cf6-154">Per disabilitarle, aggiungere l'opzione Java seguente nel caso in cui l'applicazione esegua chiamate di tale tipo: `-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="c3cf6-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="c3cf6-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="c3cf6-155">Jetty</span></span>
<span data-ttu-id="c3cf6-156">Come nel caso di Tomcat, i clienti possono caricare istanze personalizzate per Jetty.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="c3cf6-157">Se viene eseguita l'installazione completa di Jetty, la configurazione sarà analoga alla seguente:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-157">In the case of running the full install of Jetty, the configuration would look like this:</span></span>

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

<span data-ttu-id="c3cf6-158">La configurazione Jetty deve essere modificata in start.ini per impostare `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="c3cf6-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="c3cf6-159">Springboot</span></span>
<span data-ttu-id="c3cf6-160">Per ottenere un’applicazione Springboot in esecuzione, è necessario caricare il file JAR o WAR e aggiungere il seguente file web.config.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span></span> <span data-ttu-id="c3cf6-161">Il file web.config viene inserito nella cartella wwwroot.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-161">The web.config file goes into the wwwroot folder.</span></span> <span data-ttu-id="c3cf6-162">Modificare gli argomenti in modo da puntare al file JAR, nell'esempio seguente il file con estensione JAR si trova anche nella cartella wwwroot.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="c3cf6-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="c3cf6-163">Hudson</span></span>
<span data-ttu-id="c3cf6-164">Nel test sono stati utilizzati il file WAR di Hudson 3.1.2 e l'istanza predefinita di Tomcat 7.0.50, senza utilizzare l'interfaccia utente per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span></span>  <span data-ttu-id="c3cf6-165">Poiché Hudson è uno strumento per la compilazione di software, è consigliabile installarlo su istanze dedicate nelle quali sia possibile impostare il flag **AlwaysOn** sul sito.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span></span>

1. <span data-ttu-id="c3cf6-166">Nella radice del sito Web di Azure, ad esempio **d:\home\site\wwwroot**, creare una directory **webapps**, se non è già presente, quindi inserire Hudson.war in **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="c3cf6-167">Scaricare apache maven 3.0.5 (compatibile con Hudson) e posizionarlo in **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="c3cf6-168">Creare il file web.config in **d:\home\site\wwwroot** e incollarvi il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span></span>
   
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
   
    <span data-ttu-id="c3cf6-169">A questo punto è possibile riavviare il sito Web per applicare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-169">At this point the web app can be restarted to take the changes.</span></span>  <span data-ttu-id="c3cf6-170">Connettersi a http://yourwebapp/hudson per avviare Hudson.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-170">Connect to http://yourwebapp/hudson to start Hudson.</span></span>
4. <span data-ttu-id="c3cf6-171">Al termine della configurazione automatica di Hudson, dovrebbe essere visualizzata la schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-171">After Hudson configures itself, you should see the following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="c3cf6-173">Accedere alla pagina di configurazione di Hudson: fare clic su **Manage Hudson** (Gestisci Hudson), quindi su **Configure System** (Configura sistema).</span><span class="sxs-lookup"><span data-stu-id="c3cf6-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="c3cf6-174">Configurare JDK come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-174">Configure the JDK as shown below:</span></span>
   
    ![Configurazione di Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="c3cf6-176">Configurare Maven come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-176">Configure Maven as shown below:</span></span>
   
    ![Configurazione di Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="c3cf6-178">Salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-178">Save the settings.</span></span> <span data-ttu-id="c3cf6-179">A questo punto Hudson dovrebbe essere configurato e pronto per l'uso.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="c3cf6-180">Per ulteriori informazioni su Hudson, vedere [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="c3cf6-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="c3cf6-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="c3cf6-181">Liferay</span></span>
<span data-ttu-id="c3cf6-182">Liferay è supportato in applicazione servizio Web App.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="c3cf6-183">Poiché Liferay può richiedere una quantità di memoria considerevole, è necessario eseguire il sito su un processo di lavoro dedicato di medie o grandi dimensioni, che sia in grado di fornire memoria sufficiente.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="c3cf6-184">Liferay richiede inoltre alcuni minuti per l'avvio.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-184">Liferay also takes several minutes to start up.</span></span> <span data-ttu-id="c3cf6-185">Per questa ragione è consigliabile impostare il sito su **Always On**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-185">For that reason, it is recommended that you set the web app to **Always On**.</span></span>  

<span data-ttu-id="c3cf6-186">Mediante Liferay 6.1.2 Community Edition GA3 in bundle con Tomcat sono stati modificati i file seguenti dopo il download di Liferay:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="c3cf6-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="c3cf6-187">**Server.xml**</span></span>

* <span data-ttu-id="c3cf6-188">Impostare la porta di arresto su -1.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-188">Change Shutdown port to -1.</span></span>
* <span data-ttu-id="c3cf6-189">Impostare il connettore HTTP su `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="c3cf6-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="c3cf6-190">Impostare come commento il connettore AJP.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-190">Comment out the AJP connector.</span></span>

<span data-ttu-id="c3cf6-191">Nella cartella **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** creare un file denominato **portal-ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="c3cf6-192">Il file deve contenere una riga, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-192">This file needs to contain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="c3cf6-193">Allo stesso livello di directory della cartella tomcat-7.0.40 creare un file denominato **web.config** con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="c3cf6-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span></span>

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

<span data-ttu-id="c3cf6-194">Nel blocco **httpPlatform**, la variabile **requestTimeout** è impostata su "00:10:00".</span><span class="sxs-lookup"><span data-stu-id="c3cf6-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span></span>  <span data-ttu-id="c3cf6-195">Questo valore può essere ridotto ma in questo caso è probabile che si verifichino errori di timeout durante il bootstrap di Liferay.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="c3cf6-196">Se il valore viene modificato, è necessario modificare anche **connectionTimeout** nel file server.xml di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="c3cf6-197">Si noti che nel file web.config riportato sopra la variabile di ambiente JRE_HOME è impostata in modo da fare riferimento alla versione di JDK a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span></span> <span data-ttu-id="c3cf6-198">La versione predefinita è a 32 bit, ma poiché Liferay può richiedere livelli elevati di memoria è consigliabile utilizzare il JDK a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span></span>

<span data-ttu-id="c3cf6-199">Dopo avere apportato le modifiche indicate, riavviare l'app Web che esegue Liferay, quindi aprire http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="c3cf6-200">Il portale Liferay è disponibile dalla radice del sito Web.</span><span class="sxs-lookup"><span data-stu-id="c3cf6-200">The Liferay portal is available from the web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c3cf6-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3cf6-201">Next steps</span></span>
<span data-ttu-id="c3cf6-202">Per ulteriori informazioni su Liferay, vedere [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="c3cf6-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="c3cf6-203">Per altre informazioni su Java, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="c3cf6-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[servizio app di Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
