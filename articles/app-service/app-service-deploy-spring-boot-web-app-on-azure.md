---
title: aaaDeploy toohello un'applicazione di avvio Spring servizio App di Azure | Documenti Microsoft
description: In questa esercitazione fornisce le istruzioni sviluppatori tramite hello passaggi toodeploy hello Spring avvio introduzione web app tooAzure servizio App.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="675bc-103">Distribuire un servizio App di Azure di toohello Spring avvio applicazione</span><span class="sxs-lookup"><span data-stu-id="675bc-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="675bc-104">Hello  **[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale e uno dei progetti comuni a più di hello che si basa sulla piattaforma [Avvio spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.</span><span class="sxs-lookup"><span data-stu-id="675bc-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="675bc-105">In questa esercitazione assiste l'utente tramite la creazione di app web di molla avvio introduzione esempio hello e la distribuzione troppo[Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="675bc-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="675bc-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="675bc-106">Prerequisites</span></span>

<span data-ttu-id="675bc-107">In ordine toocomplete hello passaggi di questa esercitazione, è necessario seguente hello toohave:</span><span class="sxs-lookup"><span data-stu-id="675bc-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="675bc-108">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="675bc-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="675bc-109">Un [Java Developer Kit (JDK)] aggiornato.</span><span class="sxs-lookup"><span data-stu-id="675bc-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="675bc-110">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="675bc-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="675bc-111">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="675bc-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="675bc-112">Creare app web Spring avvio introduzione hello</span><span class="sxs-lookup"><span data-stu-id="675bc-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="675bc-113">Hello passaggi seguenti verranno illustrati i passaggi di hello che sono necessari toocreate una semplice applicazione web di avvio molla ed eseguirne il test in locale.</span><span class="sxs-lookup"><span data-stu-id="675bc-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="675bc-114">Aprire un prompt dei comandi e creare toohold una directory locale dell'applicazione e spostarsi nella directory toothat; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="675bc-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="675bc-115">- o-</span><span class="sxs-lookup"><span data-stu-id="675bc-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="675bc-116">Hello clone [Spring avvio Introduzione] progetto di esempio nella directory hello appena creato; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="675bc-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="675bc-117">Cambiare il progetto completato toohello directory; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="675bc-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="675bc-118">Compilare i file JAR hello utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="675bc-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="675bc-119">Una volta hello web app è stata creata, modificare il file JAR di directory toohello e avviare l'app web hello; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="675bc-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="675bc-120">Testare l'app web hello esplorando toohttp://localhost:8080 mediante un web browser o utilizzare sintassi hello come hello di esempio seguente, se si dispone di curl disponibili:</span><span class="sxs-lookup"><span data-stu-id="675bc-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="675bc-121">Dovrebbe essere hello segue messaggio visualizzato: **Greetings da avvio Spring!**</span><span class="sxs-lookup"><span data-stu-id="675bc-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Esplora la app di esempio][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="675bc-123">Creare un'app web di Azure con Java</span><span class="sxs-lookup"><span data-stu-id="675bc-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="675bc-124">Hello alla procedura seguente verrà illustrata hello passaggi toocreate un'App Web di Azure, configurare le impostazioni di hello necessario per Java e configurare le credenziali FTP.</span><span class="sxs-lookup"><span data-stu-id="675bc-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="675bc-125">Sfoglia toohello [portale di Azure] ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="675bc-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="675bc-126">Dopo aver eseguito l'accesso al tuo account nel portale di Azure hello, fare clic sull'icona di menu hello per **servizi App**:</span><span class="sxs-lookup"><span data-stu-id="675bc-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Portale di Azure][AZ01]

1. <span data-ttu-id="675bc-128">Quando hello **servizi App** viene visualizzata la pagina, fare clic su **+ Aggiungi** toocreate un nuovo servizio App.</span><span class="sxs-lookup"><span data-stu-id="675bc-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![Creare un servizio app][AZ02]

1. <span data-ttu-id="675bc-130">Quando viene visualizzato l'elenco di hello di modelli di app web, fare clic sul collegamento hello per hello base App Web di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="675bc-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Modelli di app Web][AZ03]

1. <span data-ttu-id="675bc-132">Quando viene visualizzata la pagina informazioni hello per il modello di App Web hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="675bc-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![Crea app Web][AZ04]

1. <span data-ttu-id="675bc-134">Specificare un nome univoco per l'app Web, quindi specificare eventuali impostazioni aggiuntive e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="675bc-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Creare delle impostazioni app Web][AZ05]

1. <span data-ttu-id="675bc-136">Dopo aver creato l'app web, fare clic sull'icona di menu hello per **servizi App**, quindi fare clic su app web appena creato:</span><span class="sxs-lookup"><span data-stu-id="675bc-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Elenco delle app Web][AZ06]

1. <span data-ttu-id="675bc-138">Quando viene visualizzata l'app web, è possibile specificare la versione di Java hello utilizzando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="675bc-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="675bc-139">a.</span><span class="sxs-lookup"><span data-stu-id="675bc-139">a.</span></span> <span data-ttu-id="675bc-140">Fare clic su hello **le impostazioni dell'applicazione** voce di menu.</span><span class="sxs-lookup"><span data-stu-id="675bc-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="675bc-141">b.</span><span class="sxs-lookup"><span data-stu-id="675bc-141">b.</span></span> <span data-ttu-id="675bc-142">Scegliere **Java 8** per la versione di Java hello.</span><span class="sxs-lookup"><span data-stu-id="675bc-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="675bc-143">c.</span><span class="sxs-lookup"><span data-stu-id="675bc-143">c.</span></span> <span data-ttu-id="675bc-144">Scegliere **più recente** per versione di hello secondaria Java.</span><span class="sxs-lookup"><span data-stu-id="675bc-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="675bc-145">d.</span><span class="sxs-lookup"><span data-stu-id="675bc-145">d.</span></span> <span data-ttu-id="675bc-146">Scegliere **più recenti Tomcat 8.5** per contenitore web hello.</span><span class="sxs-lookup"><span data-stu-id="675bc-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="675bc-147">(Questo contenitore non verrà effettivamente utilizzato; Azure userà il contenitore di hello dall'applicazione di avvio molla.)</span><span class="sxs-lookup"><span data-stu-id="675bc-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="675bc-148">e.</span><span class="sxs-lookup"><span data-stu-id="675bc-148">e.</span></span> <span data-ttu-id="675bc-149">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="675bc-149">Click **Save**.</span></span>

   ![Impostazioni dell'applicazione][AZ07]

1. <span data-ttu-id="675bc-151">Specificare le credenziali di distribuzione FTP utilizzando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="675bc-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="675bc-152">a.</span><span class="sxs-lookup"><span data-stu-id="675bc-152">a.</span></span> <span data-ttu-id="675bc-153">Fare clic su hello **le credenziali di distribuzione** voce di menu.</span><span class="sxs-lookup"><span data-stu-id="675bc-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="675bc-154">b.</span><span class="sxs-lookup"><span data-stu-id="675bc-154">b.</span></span> <span data-ttu-id="675bc-155">Specificare il proprio nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="675bc-155">Specify your username and password.</span></span>

   <span data-ttu-id="675bc-156">c.</span><span class="sxs-lookup"><span data-stu-id="675bc-156">c.</span></span> <span data-ttu-id="675bc-157">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="675bc-157">Click **Save**.</span></span>

   ![Specificare le credenziali di distribuzione][AZ08]

1. <span data-ttu-id="675bc-159">Recuperare le informazioni di connessione FTP tramite hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="675bc-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="675bc-160">a.</span><span class="sxs-lookup"><span data-stu-id="675bc-160">a.</span></span> <span data-ttu-id="675bc-161">Fare clic su hello **le credenziali di distribuzione** voce di menu.</span><span class="sxs-lookup"><span data-stu-id="675bc-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="675bc-162">b.</span><span class="sxs-lookup"><span data-stu-id="675bc-162">b.</span></span> <span data-ttu-id="675bc-163">Copiare il nome utente FTP completo e l'URL e salvate per la sezione successiva di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="675bc-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![URL FTP e credenziali][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="675bc-165">Distribuire il tooAzure app web di avvio della primavera</span><span class="sxs-lookup"><span data-stu-id="675bc-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="675bc-166">Hello passaggi verrà illustrati hello passaggi toodeploy tooAzure di app web la molla avvio.</span><span class="sxs-lookup"><span data-stu-id="675bc-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="675bc-167">Aprire un editor di testo come blocco note di Windows e incollare hello dopo il testo in un nuovo documento, quindi salvare il file hello come *Web. config*:</span><span class="sxs-lookup"><span data-stu-id="675bc-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="675bc-168">Dopo aver salvato hello *Web. config* del file system tooyour, connettere tooyour app web tramite FTP utilizzando URL hello, username e password da hello precedente sezione di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="675bc-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="675bc-169">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="675bc-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="675bc-170">Cartella radice dell'app web modifica hello directory remota toohello (ovvero */sito/wwwroot*), quindi copiare il file JAR hello dall'applicazione di avvio molla e hello *Web. config* precedenti.</span><span class="sxs-lookup"><span data-stu-id="675bc-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="675bc-171">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="675bc-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="675bc-172">Dopo aver distribuito il file JAR e *Web. config* file tooyour web app, è necessario toorestart app web utilizzando hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="675bc-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="675bc-173">Testare app web hello passando l'URL dell'app web tooyour mediante un web browser, o utilizzare sintassi hello come hello di esempio seguente, se si dispone di curl disponibili:</span><span class="sxs-lookup"><span data-stu-id="675bc-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="675bc-174">Dovrebbe essere hello segue messaggio visualizzato: **Greetings da avvio Spring!**</span><span class="sxs-lookup"><span data-stu-id="675bc-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Esplora la app di esempio][SB02]

## <a name="next-steps"></a><span data-ttu-id="675bc-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="675bc-176">Next steps</span></span>

<span data-ttu-id="675bc-177">Per ulteriori informazioni sull'utilizzo di applicazioni di avvio Spring in Azure, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="675bc-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="675bc-178">Distribuire un'applicazione di avvio Spring in Linux in hello servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="675bc-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="675bc-179">Distribuire un'applicazione di avvio Spring in un Kubernetes Cluster in hello servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="675bc-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="675bc-180">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="675bc-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="675bc-181">Per ulteriori informazioni su depoying web App tooAzure tramite FTP, vedere [distribuire il servizio App utilizzando FTP/S di tooAzure app].</span><span class="sxs-lookup"><span data-stu-id="675bc-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="675bc-182">Per ulteriori informazioni sul progetto di esempio hello Spring avvio, vedere [Spring avvio Introduzione].</span><span class="sxs-lookup"><span data-stu-id="675bc-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="675bc-183">Per informazioni sulla Guida introduttiva a applicazioni Spring avvio, vedere hello **Initializr Spring** in https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="675bc-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="675bc-184">Per altre informazioni sulla configurazione delle impostazioni aggiuntive per l'app Web, vedere [Configurare app Web in Servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="675bc-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[portale di Azure]: https://portal.azure.com/
[Configurare app Web in Servizio app di Azure]: /azure/app-service-web/web-sites-configure
[distribuire il servizio App utilizzando FTP/S di tooAzure app]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Avvio spring]: http://projects.spring.io/spring-boot/
[Spring avvio Introduzione]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
