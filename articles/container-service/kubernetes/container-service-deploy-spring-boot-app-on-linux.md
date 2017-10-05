---
title: Distribuire un'app Web Spring Boot su Linux nel servizio contenitore di Azure | Microsoft Docs
description: Questa esercitazione illustra in modo dettagliato la procedura per la distribuzione di un'applicazione Spring Boot come app Web Linux in Microsoft Azure.
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
ms.openlocfilehash: 5f0b470bd46cfeaf00b3092dbe9db507ed50f622
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="16941-103">Distribuire un'applicazione Spring Boot in Linux nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="16941-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="16941-104">**[Spring Framework]** è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello enterprise.</span><span class="sxs-lookup"><span data-stu-id="16941-104">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="16941-105">Uno dei progetti più comuni che si basa su questa piattaforma è [Spring Boot], che fornisce un approccio semplificato per la creazione di applicazioni Java autonome.</span><span class="sxs-lookup"><span data-stu-id="16941-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="16941-106">**[Docker]** è una soluzione open source che consente agli sviluppatori di automatizzare la distribuzione, il ridimensionamento e la gestione delle applicazioni in esecuzione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="16941-106">**[Docker]** is open-source solutions that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="16941-107">Questa esercitazione illustra l'uso di Docker per sviluppare e distribuire un'applicazione Spring Boot a un host Linux nel [servizio contenitore di Azure].</span><span class="sxs-lookup"><span data-stu-id="16941-107">This tutorial walks you through using Docker to develop and deploy a Spring Boot application to a Linux host in the [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16941-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="16941-108">Prerequisites</span></span>

<span data-ttu-id="16941-109">Per completare la procedura di questa esercitazione, sono necessari i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="16941-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="16941-110">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="16941-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="16941-111">[Interfaccia della riga di comando di Azure].</span><span class="sxs-lookup"><span data-stu-id="16941-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="16941-112">Un [Java Developer Kit (JDK)] aggiornato.</span><span class="sxs-lookup"><span data-stu-id="16941-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="16941-113">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="16941-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="16941-114">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="16941-114">A [Git] client.</span></span>
* <span data-ttu-id="16941-115">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="16941-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="16941-116">A causa dei requisiti di virtualizzazione di questa esercitazione, non è possibile seguire la procedura illustrata in questo articolo in una macchina virtuale. È necessario usare un computer fisico in cui sono abilitate le funzionalità di virtualizzazione.</span><span class="sxs-lookup"><span data-stu-id="16941-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="16941-117">Creare l'app Web introduttiva di Spring Boot in Docker</span><span class="sxs-lookup"><span data-stu-id="16941-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="16941-118">I passaggi seguenti illustrano i passaggi necessari per creare una semplice applicazione Web Spring Boot e testarla localmente.</span><span class="sxs-lookup"><span data-stu-id="16941-118">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="16941-119">Aprire un prompt dei comandi e creare una directory locale in cui contenere l'applicazione, quindi passare a tale directory. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="16941-120">- o-</span><span class="sxs-lookup"><span data-stu-id="16941-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="16941-121">Clonare il progetto di esempio [Spring Boot on Docker Getting Started] (Introduzione a Spring Boot in Docker) nella directory appena creata, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="16941-122">Passare alla directory del progetto completato. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-122">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="16941-123">Compilare il file JAR usando Maven. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-123">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="16941-124">Dopo aver creato l'app Web, passare alla directory `target` in cui si trova il file JAR e avviare l'app Web. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-124">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="16941-125">Testare l'app Web esplorandola localmente tramite un Web browser.</span><span class="sxs-lookup"><span data-stu-id="16941-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="16941-126">Ad esempio, se è disponibile un cURL e il server Tomcat è configurato per l'esecuzione sulla porta 80:</span><span class="sxs-lookup"><span data-stu-id="16941-126">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="16941-127">Dovrebbe essere visualizzato il messaggio seguente: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="16941-127">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Esplorare l'app di esempio in locale][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="16941-129">Creare un Registro contenitori di Azure da usare come registro Docker privato</span><span class="sxs-lookup"><span data-stu-id="16941-129">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="16941-130">La procedura seguente illustra come usare il portale di Azure per creare un Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="16941-130">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="16941-131">Se si vuole usare l'interfaccia della riga di comando di Azure anziché il portale di Azure, seguire i passaggi in [Creare un registro per contenitori Docker privati usando l'interfaccia della riga di comando di Azure 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="16941-131">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="16941-132">Aprire il [portale di Azure] ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="16941-132">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="16941-133">Dopo aver effettuato l'accesso all'account nel portale di Azure, è possibile seguire la procedura illustrata nell'articolo [Creare un registro per contenitori Docker privati con il portale di Azure], parafrasata per semplicità nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="16941-133">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="16941-134">Fare clic sull'icona di menu **+ Nuovo**, su **Contenitori** e quindi su **Registro contenitori di Azure**.</span><span class="sxs-lookup"><span data-stu-id="16941-134">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Creare un nuovo Registro contenitori di Azure][AR01]

1. <span data-ttu-id="16941-136">Quando viene visualizzata la pagina delle informazioni per il modello di Registro contenitori di Azure, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="16941-136">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Creare un nuovo Registro contenitori di Azure][AR02]

1. <span data-ttu-id="16941-138">Quando viene visualizzata la pagina **Crea registro contenitori**, immettere **Nome registro** e **Gruppo di risorse**, scegliere **Abilita** per **Utente amministratore** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="16941-138">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurare le impostazioni del Registro contenitori di Azure][AR03]

1. <span data-ttu-id="16941-140">Una volta creato il registro contenitori, passare al registro contenitori stesso nel portale di Azure e quindi fare clic su **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="16941-140">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="16941-141">Prendere nota del nome utente e della password per i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="16941-141">Take note of the username and password for the next steps.</span></span>

   ![Chiavi di accesso al Registro contenitori di Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="16941-143">Configurare Maven per l'uso delle chiavi di accesso del Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="16941-143">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="16941-144">Passare alla directory di configurazione dell'installazione di Maven e aprire il file *settings.xml* con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="16941-144">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="16941-145">Aggiungere le impostazioni di accesso al Registro contenitori di Azure dalla sezione precedente di questa esercitazione alla raccolta `<servers>` nel file *settings.xml* file. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-145">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="16941-146">Passare alla directory del progetto completato per l'applicazione Spring Boot (ad esempio, "*C:\SpringBoot\gs-spring-boot-docker\complete*" o "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e aprire il file *pom.xml* con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="16941-146">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="16941-147">Aggiornare la raccolta `<properties>` nel file *pom.xml* con il valore del server di accesso per il Registro contenitori di Azure dalla sezione precedente di questa esercitazione. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-147">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="16941-148">Aggiornare la raccolta `<plugins>` nel file *pom.xml* in modo che `<plugin>` contenga l'indirizzo del server di accesso e il nome del registro per il Registro contenitori di Azure dalla sezione precedente di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="16941-148">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="16941-149">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-149">For example:</span></span>

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

1. <span data-ttu-id="16941-150">Passare alla directory del progetto completato per l'applicazione Spring Boot ed eseguire il comando seguente per ricompilare l'applicazione ed effettuare il push del contenitore nel Registro contenitori di Azure:</span><span class="sxs-lookup"><span data-stu-id="16941-150">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="16941-151">Quando si effettua il push del contenitore Docker in Azure, è possibile che venga visualizzato un messaggio di errore simile a uno dei seguenti, anche se il contenitore Docker è stato creato correttamente:</span><span class="sxs-lookup"><span data-stu-id="16941-151">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="16941-152">In questo caso, è possibile che sia necessario accedere all'account Azure dalla riga di comando di Docker. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-152">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="16941-153">È quindi possibile effettuare il push del contenitore dalla riga di comando. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16941-153">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="16941-154">Creare un'app Web in Linux nel servizio app di Azure usando l'immagine del contenitore</span><span class="sxs-lookup"><span data-stu-id="16941-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="16941-155">Aprire il [portale di Azure] ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="16941-155">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="16941-156">Fare clic sull'icona di menu **+ Nuovo**, su **Web e dispositivi mobili**, quindi su **App Web in Linux**.</span><span class="sxs-lookup"><span data-stu-id="16941-156">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Creare una nuova app Web nel portale di Azure][LX01]

1. <span data-ttu-id="16941-158">Quando viene visualizzata la pagina **App Web in Linux**, immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="16941-158">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="16941-159">a.</span><span class="sxs-lookup"><span data-stu-id="16941-159">a.</span></span> <span data-ttu-id="16941-160">Immettere un nome univoco per il **Nome app**, ad esempio: "*wingtiptoyslinux*".</span><span class="sxs-lookup"><span data-stu-id="16941-160">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="16941-161">b.</span><span class="sxs-lookup"><span data-stu-id="16941-161">b.</span></span> <span data-ttu-id="16941-162">Scegliere una **Sottoscrizione** dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="16941-162">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="16941-163">c.</span><span class="sxs-lookup"><span data-stu-id="16941-163">c.</span></span> <span data-ttu-id="16941-164">Selezionare un **Gruppo di risorse** esistente o specificare un nome per creare uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="16941-164">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="16941-165">d.</span><span class="sxs-lookup"><span data-stu-id="16941-165">d.</span></span> <span data-ttu-id="16941-166">Fare clic su **Configura contenitore** e immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="16941-166">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="16941-167">Scegliere **Registro di sistema privato**.</span><span class="sxs-lookup"><span data-stu-id="16941-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="16941-168">**Immagine e tag facoltativo**: specificare il nome del contenitore dai passaggi precedenti, ad esempio: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="16941-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="16941-169">**URL server**: specificare l'URL del registro dai passaggi precedenti, ad esempio: "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="16941-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="16941-170">**Nome utente di accesso** e **Password**: specificare le credenziali di accesso dalle **Chiavi di accesso** usate nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="16941-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="16941-171">e.</span><span class="sxs-lookup"><span data-stu-id="16941-171">e.</span></span> <span data-ttu-id="16941-172">Dopo aver immesso tutte le informazioni precedenti, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="16941-172">Once you have entered all of the above information, click **OK**.</span></span>

   ![Configurare le impostazioni dell'app Web][LX02]

1. <span data-ttu-id="16941-174">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="16941-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="16941-175">Azure eseguirà automaticamente il mapping delle richieste Internet al server Tomcat incorporato in esecuzione sulla porta standard 80 o 8080.</span><span class="sxs-lookup"><span data-stu-id="16941-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="16941-176">Se tuttavia il server Tomcat incorporato è stato configurato per l'esecuzione su una porta personalizzata, è necessario aggiungere all'app Web una variabile di ambiente che definisce la porta del server Tomcat incorporato.</span><span class="sxs-lookup"><span data-stu-id="16941-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="16941-177">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16941-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="16941-178">Aprire il [portale di Azure] ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="16941-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="16941-179">Fare clic sull'icona per **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="16941-179">Click the icon for **App Services**.</span></span> <span data-ttu-id="16941-180">(Vedere l'elemento 1 nell'immagine seguente.)</span><span class="sxs-lookup"><span data-stu-id="16941-180">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="16941-181">Selezionare l'app Web dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="16941-181">Select your web app from the list.</span></span> <span data-ttu-id="16941-182">(Elemento 2 nell'immagine seguente.)</span><span class="sxs-lookup"><span data-stu-id="16941-182">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="16941-183">Fare clic su **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="16941-183">Click **Application Settings**.</span></span> <span data-ttu-id="16941-184">(Elemento 3 nell'immagine seguente.)</span><span class="sxs-lookup"><span data-stu-id="16941-184">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="16941-185">Nella sezione **Impostazioni app** aggiungere una nuova variabile di ambiente denominata **PORT** e immettere il numero di porta personalizzato come valore.</span><span class="sxs-lookup"><span data-stu-id="16941-185">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="16941-186">(Elemento 4 nell'immagine seguente.)</span><span class="sxs-lookup"><span data-stu-id="16941-186">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="16941-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="16941-187">Click **Save**.</span></span> <span data-ttu-id="16941-188">(Elemento 5 nell'immagine seguente.)</span><span class="sxs-lookup"><span data-stu-id="16941-188">(Item #5 in the image below.)</span></span>
>
> ![Salvataggio di un numero di porta personalizzato nel portale di Azure][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="16941-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16941-190">Next steps</span></span>

<span data-ttu-id="16941-191">Per altre informazioni sull'uso delle applicazioni Spring Boot in Azure, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="16941-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="16941-192">Distribuire un'applicazione Spring Boot nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="16941-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="16941-193">Distribuire un'applicazione Spring Boot in un cluster Kubernetes nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="16941-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="16941-194">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="16941-194">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="16941-195">Per maggiori dettagli sul progetto di esempio di Spring Boot in Docker, vedere [Spring Boot on Docker Getting Started] (Introduzione a Spring Boot in Docker).</span><span class="sxs-lookup"><span data-stu-id="16941-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="16941-196">Per informazioni sulla Guida introduttiva con le proprie applicazioni Spring Boot, vedere **Spring Initializr** (Inizializzazione di SpringBoot) all'indirizzo https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="16941-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="16941-197">Per altre informazioni sul come iniziare a creare una semplice applicazione Spring Boot, vedere Spring Initializr all'indirizzo https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="16941-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="16941-198">Per altri esempi sull'uso delle immagini personalizzate di Docker con Azure, vedere [Uso di un'immagine Docker personalizzata per App Web di Azure in Linux].</span><span class="sxs-lookup"><span data-stu-id="16941-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="16941-199">[Interfaccia della riga di comando di Azure]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="16941-199">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="16941-200">[servizio contenitore di Azure]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="16941-200">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="16941-201">[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="16941-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="16941-202">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="16941-202">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="16941-203">[Creare un registro per contenitori Docker privati con il portale di Azure]: /azure/container-registry/container-registry-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="16941-203">[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal</span></span>
<span data-ttu-id="16941-204">[Uso di un'immagine Docker personalizzata per App Web di Azure in Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="16941-204">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="16941-205">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="16941-205">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="16941-206">[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="16941-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="16941-207">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="16941-207">[Git]: https://github.com/</span></span>
<span data-ttu-id="16941-208">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="16941-208">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="16941-209">[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="16941-209">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="16941-210">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="16941-210">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="16941-211">[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="16941-211">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="16941-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="16941-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="16941-213">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker (Introduzione a Spring Boot in Docker)</span><span class="sxs-lookup"><span data-stu-id="16941-213">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="16941-214">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="16941-214">[Spring Framework]: https://spring.io/</span></span>

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
