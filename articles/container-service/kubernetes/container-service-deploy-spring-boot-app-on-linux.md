---
title: aaaDeploy un'App Web di avvio molla su Linux nel servizio contenitore di Azure | Documenti Microsoft
description: In questa esercitazione viene tuttavia hello passaggi toodeploy un'applicazione di avvio molla come un'app web di Linux in Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="23e94-103">Distribuire un'applicazione di avvio molla su Linux in hello servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="23e94-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="23e94-104">Hello  **[Spring Framework]**  è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="23e94-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="23e94-105">Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.</span><span class="sxs-lookup"><span data-stu-id="23e94-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="23e94-106">**[Docker]**  è soluzioni open source che consente agli sviluppatori di automatizzare la distribuzione di hello, scalabilità e gestione delle applicazioni in esecuzione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="23e94-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="23e94-107">In questa esercitazione illustra tramite Docker toodevelop e distribuire un host di Linux Spring avvio applicazione tooa in hello [servizio contenitore di Azure (ACS)].</span><span class="sxs-lookup"><span data-stu-id="23e94-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23e94-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="23e94-108">Prerequisites</span></span>

<span data-ttu-id="23e94-109">In ordine toocomplete hello passaggi di questa esercitazione, è necessario hello toohave seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="23e94-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="23e94-110">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="23e94-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="23e94-111">Hello [Azure interfaccia della riga di comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="23e94-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="23e94-112">Un [Java Developer Kit (JDK)] aggiornato.</span><span class="sxs-lookup"><span data-stu-id="23e94-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="23e94-113">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="23e94-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="23e94-114">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="23e94-114">A [Git] client.</span></span>
* <span data-ttu-id="23e94-115">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="23e94-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="23e94-116">A causa di requisiti della virtualizzazione toohello di questa esercitazione, non è possibile seguire i passaggi di hello in questo articolo in una macchina virtuale; è necessario utilizzare un computer fisico con le funzionalità di virtualizzazione abilitate.</span><span class="sxs-lookup"><span data-stu-id="23e94-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="23e94-117">Creare hello avvio molla nell'applicazione web di Guida introduttiva di Docker</span><span class="sxs-lookup"><span data-stu-id="23e94-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="23e94-118">Hello passaggi seguenti consentono di eseguire passaggi di hello che sono necessari toocreate una semplice applicazione web di avvio molla ed eseguirne il test in locale.</span><span class="sxs-lookup"><span data-stu-id="23e94-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="23e94-119">Aprire un prompt dei comandi e creare toohold una directory locale dell'applicazione e spostarsi nella directory toothat; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="23e94-120">- o-</span><span class="sxs-lookup"><span data-stu-id="23e94-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="23e94-121">Hello clone [avvio molla su Docker Introduzione] progetto di esempio nella directory hello è stato creato; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="23e94-122">Cambiare il progetto completato toohello directory; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="23e94-123">Compilare i file JAR hello utilizzando Maven; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="23e94-124">Una volta hello web app è stata creata, cambiare directory toohello `target` directory in cui si trova il file JAR hello e avvia l'app web hello; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="23e94-125">Testare l'app web hello esplorando tooit localmente tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="23e94-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="23e94-126">Ad esempio, se dispone di curl disponibile e configurato hello Tomcat server toorun sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="23e94-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="23e94-127">Dovrebbe essere hello segue messaggio visualizzato: **Docker Hello World!**</span><span class="sxs-lookup"><span data-stu-id="23e94-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![Esplorare l'app di esempio in locale][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="23e94-129">Creare un toouse del Registro di sistema di Azure contenitore privato Docker Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="23e94-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="23e94-130">Hello passaggi seguenti consentono l'utilizzo di hello toocreate portale Azure del Registro di sistema un contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="23e94-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="23e94-131">Se si vuole toouse hello CLI di Azure anziché hello portale di Azure, seguire i passaggi di hello in [creare un registro di sistema contenitore Docker privata mediante hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="23e94-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="23e94-132">Sfoglia toohello [portale di Azure] ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="23e94-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="23e94-133">Dopo l'accesso account tooyour in hello portale di Azure, è possibile seguire i passaggi di hello in hello [creare un registro di sistema contenitore Docker privata tramite il portale di Azure hello] articolo, sono tratto in hello alla procedura seguente per hello efficienza di convenienza.</span><span class="sxs-lookup"><span data-stu-id="23e94-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="23e94-134">Fare clic sull'icona di menu hello per **+ nuovo**, quindi fare clic su **contenitori**, quindi fare clic su **Registro di sistema di Azure contenitore**.</span><span class="sxs-lookup"><span data-stu-id="23e94-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Creare un nuovo Registro contenitori di Azure][AR01]

1. <span data-ttu-id="23e94-136">Quando viene visualizzata la pagina informazioni hello per il modello del Registro di sistema di Azure contenitore hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="23e94-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Creare un nuovo Registro contenitori di Azure][AR02]

1. <span data-ttu-id="23e94-138">Quando hello **Registro di sistema contenitore crea** viene visualizzata la pagina, immettere il **del Registro di sistema** e **gruppo di risorse**, scegliere **abilitare** per Hello **utente Admin**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="23e94-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![Configurare le impostazioni del Registro contenitori di Azure][AR03]

1. <span data-ttu-id="23e94-140">Dopo aver creato il Registro di sistema del contenitore, passare tooyour contenitore del Registro di sistema hello portale di Azure e quindi fare clic su **chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="23e94-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="23e94-141">Prendere nota del nome utente di hello e una password per i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="23e94-141">Take note of hello username and password for hello next steps.</span></span>

   ![Chiavi di accesso al Registro contenitori di Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="23e94-143">Configurare le chiavi di accesso del Registro di sistema di Azure contenitore di Maven toouse</span><span class="sxs-lookup"><span data-stu-id="23e94-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="23e94-144">Passare toohello directory di configurazione per l'installazione di Maven e aprire hello *Settings* file con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="23e94-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="23e94-145">Aggiungere le impostazioni di accesso del Registro di sistema di Azure contenitore dalla sezione precedente di hello di questa esercitazione toohello `<servers>` insieme in hello *Settings* file; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="23e94-146">Passare a directory di progetto toohello completato per l'applicazione di avvio molla, (ad esempio: "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker / completamento*") e aprire hello *pom.xml* file con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="23e94-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="23e94-147">Hello aggiornamento `<properties>` insieme in hello *pom.xml* file con valore hello di server di accesso per il Registro di sistema contenitore di Azure dalla sezione precedente di hello di questa esercitazione; ad esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="23e94-148">Hello aggiornamento `<plugins>` insieme in hello *pom.xml* file in modo che hello `<plugin>` contiene hello server indirizzo e del Registro di sistema nome di accesso per il Registro di sistema contenitore di Azure dalla sezione precedente di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="23e94-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="23e94-149">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-149">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="23e94-150">Directory del progetto toohello completato per l'applicazione di avvio Spring passare ed eseguire seguito comando toorebuild hello applicazione hello e push hello contenitore tooyour del Registro di sistema di Azure contenitore:</span><span class="sxs-lookup"><span data-stu-id="23e94-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="23e94-151">Quando si effettua il push del tooAzure contenitore Docker, si potrebbe ricevere un messaggio di errore è simile tooone di hello seguente anche se è stato creato il contenitore Docker:</span><span class="sxs-lookup"><span data-stu-id="23e94-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="23e94-152">In questo caso, potrebbe essere necessario toosign in tooyour account Azure dalla riga di comando di Docker hello; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="23e94-153">È quindi possibile distribuire il contenitore dalla riga di comando hello; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="23e94-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="23e94-154">Creare un'app Web in Linux nel servizio app di Azure usando l'immagine del contenitore</span><span class="sxs-lookup"><span data-stu-id="23e94-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="23e94-155">Sfoglia toohello [portale di Azure] ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="23e94-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="23e94-156">Fare clic sull'icona di menu hello per **+ nuovo**, quindi fare clic su **Web e dispositivi mobili**, quindi fare clic su **App Web in Linux**.</span><span class="sxs-lookup"><span data-stu-id="23e94-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Creare una nuova app web nel portale di Azure hello][LX01]

1. <span data-ttu-id="23e94-158">Quando hello **App Web in Linux** viene visualizzata la pagina, immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="23e94-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="23e94-159">a.</span><span class="sxs-lookup"><span data-stu-id="23e94-159">a.</span></span> <span data-ttu-id="23e94-160">Immettere un nome univoco per hello **nome App**, ad esempio: "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="23e94-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="23e94-161">b.</span><span class="sxs-lookup"><span data-stu-id="23e94-161">b.</span></span> <span data-ttu-id="23e94-162">Scegliere il **sottoscrizione** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="23e94-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="23e94-163">c.</span><span class="sxs-lookup"><span data-stu-id="23e94-163">c.</span></span> <span data-ttu-id="23e94-164">Scegliere un oggetto esistente **gruppo di risorse**, oppure specificare un toocreate nome nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="23e94-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="23e94-165">d.</span><span class="sxs-lookup"><span data-stu-id="23e94-165">d.</span></span> <span data-ttu-id="23e94-166">Fare clic su **Configura contenitore** e immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="23e94-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="23e94-167">Scegliere **Registro di sistema privato**.</span><span class="sxs-lookup"><span data-stu-id="23e94-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="23e94-168">**Immagine e tag facoltativo**: specificare il nome del contenitore dai passaggi precedenti, ad esempio: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="23e94-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="23e94-169">**URL server**: specificare l'URL del registro dai passaggi precedenti, ad esempio: "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="23e94-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="23e94-170">**Nome utente di accesso** e **Password**: specificare le credenziali di accesso dalle **Chiavi di accesso** usate nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="23e94-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="23e94-171">e.</span><span class="sxs-lookup"><span data-stu-id="23e94-171">e.</span></span> <span data-ttu-id="23e94-172">Dopo aver immesso tutte hello sopra informazioni, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="23e94-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![Configurare le impostazioni dell'app Web][LX02]

1. <span data-ttu-id="23e94-174">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="23e94-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="23e94-175">Azure eseguirà automaticamente il mapping Internet richieste tooembedded Tomcat server in cui viene eseguito su porte standard di hello di 80 o 8080.</span><span class="sxs-lookup"><span data-stu-id="23e94-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="23e94-176">Tuttavia, se è stato configurato l'incorporato toorun server Tomcat su una porta personalizzata, è necessario tooadd un'app web tooyour variabile di ambiente che definisce la porta hello del server Tomcat incorporato.</span><span class="sxs-lookup"><span data-stu-id="23e94-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="23e94-177">toodo in tal caso, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="23e94-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="23e94-178">Sfoglia toohello [portale di Azure] ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="23e94-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="23e94-179">Fare clic sull'icona hello **servizi App**.</span><span class="sxs-lookup"><span data-stu-id="23e94-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="23e94-180">(Vedere il #1 immagine hello riportata di seguito).</span><span class="sxs-lookup"><span data-stu-id="23e94-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="23e94-181">Selezionare l'app web dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="23e94-181">Select your web app from hello list.</span></span> <span data-ttu-id="23e94-182">(Voce #2 dell'immagine hello riportata di seguito).</span><span class="sxs-lookup"><span data-stu-id="23e94-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="23e94-183">Fare clic su **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="23e94-183">Click **Application Settings**.</span></span> <span data-ttu-id="23e94-184">(Voce #3 dell'immagine di hello riportata di seguito).</span><span class="sxs-lookup"><span data-stu-id="23e94-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="23e94-185">In hello **impostazioni App** sezione, aggiungere una nuova variabile di ambiente denominata **porta** e immettere il numero di porta personalizzato per il valore di hello.</span><span class="sxs-lookup"><span data-stu-id="23e94-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="23e94-186">(Voce #4 dell'immagine di hello riportata di seguito).</span><span class="sxs-lookup"><span data-stu-id="23e94-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="23e94-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="23e94-187">Click **Save**.</span></span> <span data-ttu-id="23e94-188">(Voce #5 dell'immagine di hello riportata di seguito).</span><span class="sxs-lookup"><span data-stu-id="23e94-188">(Item #5 in hello image below.)</span></span>
>
> ![Salvataggio di un numero di porta personalizzato in hello portale di Azure][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="23e94-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23e94-190">Next steps</span></span>

<span data-ttu-id="23e94-191">Per ulteriori informazioni sull'utilizzo di applicazioni di avvio Spring in Azure, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="23e94-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="23e94-192">Distribuire un servizio App di Azure di toohello Spring avvio applicazione</span><span class="sxs-lookup"><span data-stu-id="23e94-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="23e94-193">Distribuire un'applicazione di avvio Spring in un Kubernetes Cluster in hello servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="23e94-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="23e94-194">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="23e94-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="23e94-195">Per ulteriori dettagli sull'hello Spring avvio nel progetto di esempio Docker, vedere [avvio molla su Docker Introduzione].</span><span class="sxs-lookup"><span data-stu-id="23e94-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="23e94-196">Per informazioni sulla Guida introduttiva a applicazioni Spring avvio, vedere hello **Initializr Spring** in https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="23e94-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="23e94-197">Per ulteriori informazioni sulle attività iniziali con la creazione di una semplice applicazione di avvio molla, vedere hello Spring Initializr in https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="23e94-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="23e94-198">Per altri esempi per la modalità toouse immagini Docker personalizzato con Azure, vedere [utilizzando un'immagine Docker personalizzata per l'App Web di Azure in Linux].</span><span class="sxs-lookup"><span data-stu-id="23e94-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure interfaccia della riga di comando (CLI)]: /cli/azure/overview
[servizio contenitore di Azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[portale di Azure]: https://portal.azure.com/
[creare un registro di sistema contenitore Docker privata tramite il portale di Azure hello]: /azure/container-registry/container-registry-get-started-portal
[utilizzando un'immagine Docker personalizzata per l'App Web di Azure in Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[avvio Spring]: http://projects.spring.io/spring-boot/
[avvio molla su Docker Introduzione]: https://github.com/spring-guides/gs-spring-boot-docker (Introduzione a Spring Boot in Docker)
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
