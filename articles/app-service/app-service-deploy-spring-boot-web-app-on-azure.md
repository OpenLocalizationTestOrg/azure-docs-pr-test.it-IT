---
title: Distribuire un'applicazione Spring Boot nel servizio app di Azure | Microsoft Docs
description: "Questa esercitazione fornirà agli sviluppatori i passaggi per distribuire l'app Web Introduzione a Spring Boot nel servizio app di Azure."
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
ms.openlocfilehash: 0c388862d927a1492745832225c686670c071f86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a><span data-ttu-id="6a957-103">Distribuire un'applicazione Spring Boot nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="6a957-103">Deploy a Spring Boot Application to the Azure App Service</span></span>

<span data-ttu-id="6a957-104">**[Spring Framework]** è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello enterprise; uno dei progetti più comuni che si basa su questa piattaforma è [Spring Boot], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.</span><span class="sxs-lookup"><span data-stu-id="6a957-104">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="6a957-105">In questa esercitazione verrà illustrata tuttavia la creazione di una app Web Introduzione a Spring Boot Guida di esempio e la sua distribuzione nel [servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="6a957-105">This tutorial will walk you though creating the sample Spring Boot Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6a957-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6a957-106">Prerequisites</span></span>

<span data-ttu-id="6a957-107">Per completare i passaggi di questa esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a957-107">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="6a957-108">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="6a957-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="6a957-109">Un [Java Developer Kit (JDK)] aggiornato.</span><span class="sxs-lookup"><span data-stu-id="6a957-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="6a957-110">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="6a957-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="6a957-111">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="6a957-111">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="6a957-112">Creare l'app Web Introduzione a Spring Boot</span><span class="sxs-lookup"><span data-stu-id="6a957-112">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="6a957-113">I passaggi seguenti illustrano i passaggi necessari per creare una semplice applicazione Web Spring Boot e testarla localmente.</span><span class="sxs-lookup"><span data-stu-id="6a957-113">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="6a957-114">Aprire un prompt dei comandi e creare una directory locale in cui contenere l'applicazione, quindi passare a tale directory. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a957-114">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="6a957-115">- o-</span><span class="sxs-lookup"><span data-stu-id="6a957-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="6a957-116">Clonare il progetto di esempio [Introduzione a Spring Boot ] nella directory appena creata, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a957-116">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="6a957-117">Passare alla directory del progetto completato. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a957-117">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="6a957-118">Compilare il file JAR usando Maven. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a957-118">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="6a957-119">Dopo aver creato l'app Web, passare alla directory del file JAR e avviare l'app Web. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a957-119">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="6a957-120">Testare l'app Web passando a http://localhost:8080 tramite un Web browser o usare una sintassi simile all'esempio seguente, se si hanno curl disponibili:</span><span class="sxs-lookup"><span data-stu-id="6a957-120">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="6a957-121">Si dovrebbe visualizzare il messaggio seguente: **Greetings from Spring Boot!** (Benvenuti in Spring Boot!)</span><span class="sxs-lookup"><span data-stu-id="6a957-121">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Esplora la app di esempio][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="6a957-123">Creare un'app web di Azure con Java</span><span class="sxs-lookup"><span data-stu-id="6a957-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="6a957-124">I passaggi seguenti illustrano la creazione di un'app Web di Azure, la configurazione delle impostazioni necessarie per Java e delle proprie credenziali FTP.</span><span class="sxs-lookup"><span data-stu-id="6a957-124">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="6a957-125">Aprire il [portale di Azure] ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="6a957-125">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="6a957-126">Dopo aver effettuato l'accesso all'account nel portale di Azure, fare clic sull'icona di menu per i **servizi App**:</span><span class="sxs-lookup"><span data-stu-id="6a957-126">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Portale di Azure][AZ01]

1. <span data-ttu-id="6a957-128">Quando la pagina **servizi App** viene visualizzata, fare clic su **+ Aggiungi** per creare un nuovo servizio App.</span><span class="sxs-lookup"><span data-stu-id="6a957-128">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Creare un servizio app][AZ02]

1. <span data-ttu-id="6a957-130">Quando viene visualizzato l'elenco di modelli di app Web, fare clic sul collegamento per l'applicazione Web Microsoft base.</span><span class="sxs-lookup"><span data-stu-id="6a957-130">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Modelli di app Web][AZ03]

1. <span data-ttu-id="6a957-132">Quando la pagina delle informazioni per il modello di app Web viene visualizzata, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6a957-132">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Crea app Web][AZ04]

1. <span data-ttu-id="6a957-134">Specificare un nome univoco per l'app Web, quindi specificare eventuali impostazioni aggiuntive e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6a957-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Creare delle impostazioni app Web][AZ05]

1. <span data-ttu-id="6a957-136">Dopo aver creato un'app Web, fare clic sull'icona di menu **servizi App**, quindi fare clic sulla app Web appena creata:</span><span class="sxs-lookup"><span data-stu-id="6a957-136">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Elenco delle app Web][AZ06]

1. <span data-ttu-id="6a957-138">Quando viene visualizzata l'app web, specificare la versione di Java usando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6a957-138">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="6a957-139">a.</span><span class="sxs-lookup"><span data-stu-id="6a957-139">a.</span></span> <span data-ttu-id="6a957-140">Fare clic sulla voce di menu **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="6a957-140">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="6a957-141">b.</span><span class="sxs-lookup"><span data-stu-id="6a957-141">b.</span></span> <span data-ttu-id="6a957-142">Scegliere **Java 8** per la versione di Java.</span><span class="sxs-lookup"><span data-stu-id="6a957-142">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="6a957-143">c.</span><span class="sxs-lookup"><span data-stu-id="6a957-143">c.</span></span> <span data-ttu-id="6a957-144">Scegliere **Più recenti** per la versione di Java.</span><span class="sxs-lookup"><span data-stu-id="6a957-144">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="6a957-145">d.</span><span class="sxs-lookup"><span data-stu-id="6a957-145">d.</span></span> <span data-ttu-id="6a957-146">Scegliere **Newest Tomcat 8.5** [Tomcat 8.5 più recente] per il contenitore Web.</span><span class="sxs-lookup"><span data-stu-id="6a957-146">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="6a957-147">(Questo contenitore non verrà effettivamente usato; Azure userà il contenitore dall'app Spring Boot.)</span><span class="sxs-lookup"><span data-stu-id="6a957-147">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="6a957-148">e.</span><span class="sxs-lookup"><span data-stu-id="6a957-148">e.</span></span> <span data-ttu-id="6a957-149">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6a957-149">Click **Save**.</span></span>

   ![Impostazioni dell'applicazione][AZ07]

1. <span data-ttu-id="6a957-151">Specificare le credenziali di distribuzione FTP usando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6a957-151">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="6a957-152">a.</span><span class="sxs-lookup"><span data-stu-id="6a957-152">a.</span></span> <span data-ttu-id="6a957-153">Fare clic sulla voce di menu **Credenziali distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="6a957-153">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="6a957-154">b.</span><span class="sxs-lookup"><span data-stu-id="6a957-154">b.</span></span> <span data-ttu-id="6a957-155">Specificare il proprio nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="6a957-155">Specify your username and password.</span></span>

   <span data-ttu-id="6a957-156">c.</span><span class="sxs-lookup"><span data-stu-id="6a957-156">c.</span></span> <span data-ttu-id="6a957-157">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6a957-157">Click **Save**.</span></span>

   ![Specificare le credenziali di distribuzione][AZ08]

1. <span data-ttu-id="6a957-159">Recuperare le informazioni di connessione FTP usando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6a957-159">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="6a957-160">a.</span><span class="sxs-lookup"><span data-stu-id="6a957-160">a.</span></span> <span data-ttu-id="6a957-161">Fare clic sulla voce di menu **Credenziali distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="6a957-161">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="6a957-162">b.</span><span class="sxs-lookup"><span data-stu-id="6a957-162">b.</span></span> <span data-ttu-id="6a957-163">Copiare il nome utente FTP completo e l'URL e salvarli per la sezione successiva di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6a957-163">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![URL FTP e credenziali][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="6a957-165">Distribuire l'applicazione Web Spring Boot in Azure</span><span class="sxs-lookup"><span data-stu-id="6a957-165">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="6a957-166">La procedura seguente illustra i passaggi per distribuire l'app Web Spring Boot in Azure.</span><span class="sxs-lookup"><span data-stu-id="6a957-166">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="6a957-167">Aprire un editor di testo come Blocco note e incollare il testo seguente in un nuovo documento, quindi salvare il file come *web.config*:</span><span class="sxs-lookup"><span data-stu-id="6a957-167">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
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

1. <span data-ttu-id="6a957-168">Dopo aver salvato il file *web.config* nel sistema, effettuare la connessione all'app Web tramite FTP usando l'URL, il nome utente e la password della sezione precedente di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6a957-168">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="6a957-169">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a957-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="6a957-170">Modificare la directory remota nella cartella radice dell'app Web (ovvero */sito/wwwroot*), quindi copiare il file JAR dall'applicazione Spring Boot e il file *web.config* salvato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6a957-170">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="6a957-171">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a957-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="6a957-172">Dopo aver distribuito i file JAR e *web.config* nell'app Web, è necessario riavviare l'app Web tramite il portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="6a957-172">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="6a957-173">Testare l'app Web passando all'URL relativo tramite un browser Web o usare una sintassi simile all'esempio seguente, se si hanno curl disponibili:</span><span class="sxs-lookup"><span data-stu-id="6a957-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="6a957-174">Si dovrebbe visualizzare il messaggio seguente: **Greetings from Spring Boot!** (Benvenuti in Spring Boot!)</span><span class="sxs-lookup"><span data-stu-id="6a957-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Esplora la app di esempio][SB02]

## <a name="next-steps"></a><span data-ttu-id="6a957-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a957-176">Next steps</span></span>

<span data-ttu-id="6a957-177">Per altre informazioni sull'uso delle applicazioni Spring Boot in Azure, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a957-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="6a957-178">Distribuire un'applicazione Spring Boot in Linux nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6a957-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="6a957-179">Distribuire un'applicazione Spring Boot in un cluster Kubernetes nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6a957-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="6a957-180">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="6a957-180">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="6a957-181">Per altre informazioni sulla distribuzione di app Web in Azure tramite FTP, vedere [Distribuire l'app nel servizio app di Azure usando FTP/S].</span><span class="sxs-lookup"><span data-stu-id="6a957-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="6a957-182">Per altre informazioni sul progetto di esempio Spring Boot, vedere [Introduzione a Spring Boot ].</span><span class="sxs-lookup"><span data-stu-id="6a957-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="6a957-183">Per informazioni sulla Guida introduttiva con le proprie applicazioni Spring Boot, vedere **Spring Initializr** (Inizializzazione di SpringBoot) all'indirizzo https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="6a957-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="6a957-184">Per altre informazioni sulla configurazione delle impostazioni aggiuntive per l'app Web, vedere [Configurare app Web in Servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="6a957-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

<span data-ttu-id="6a957-185">[servizio app di Azure]: https://azure.microsoft.com/services/app-service/</span><span class="sxs-lookup"><span data-stu-id="6a957-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span></span>
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
<span data-ttu-id="6a957-186">[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="6a957-186">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="6a957-187">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="6a957-187">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="6a957-188">[Configurare app Web in Servizio app di Azure]: /azure/app-service-web/web-sites-configure</span><span class="sxs-lookup"><span data-stu-id="6a957-188">[Configure web apps in Azure App Service]: /azure/app-service-web/web-sites-configure</span></span>
<span data-ttu-id="6a957-189">[Distribuire l'app nel servizio app di Azure usando FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span><span class="sxs-lookup"><span data-stu-id="6a957-189">[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span></span>
<span data-ttu-id="6a957-190">[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="6a957-190">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="6a957-191">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="6a957-191">[Git]: https://github.com/</span></span>
<span data-ttu-id="6a957-192">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="6a957-192">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="6a957-193">[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="6a957-193">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="6a957-194">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="6a957-194">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="6a957-195">[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="6a957-195">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="6a957-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="6a957-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="6a957-197">[Introduzione a Spring Boot ]: https://github.com/spring-guides/gs-spring-boot</span><span class="sxs-lookup"><span data-stu-id="6a957-197">[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot</span></span>
<span data-ttu-id="6a957-198">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="6a957-198">[Spring Framework]: https://spring.io/</span></span>

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
