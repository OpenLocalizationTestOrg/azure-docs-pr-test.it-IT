---
title: aaaDeploy un'App di avvio molla su Kubernetes nel servizio contenitore di Azure | Documenti Microsoft
description: In questa esercitazione assiste l'utente tuttavia hello passaggi toodeploy un'applicazione di avvio Spring in un cluster Kubernetes in Microsoft Azure.
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="efb10-103">Distribuire un'applicazione di avvio Spring in un Kubernetes Cluster in hello servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="efb10-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="efb10-104">Hello  **[Spring Framework]**  è un framework open source più diffuso che consente agli sviluppatori Java di creare applicazioni API web e dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="efb10-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="efb10-105">Questa esercitazione viene utilizzato una app di esempio creata con [avvio Spring], un approccio basato su convenzione per l'utilizzo di tooget Spring in tempi brevi.</span><span class="sxs-lookup"><span data-stu-id="efb10-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="efb10-106">**[Kubernetes]**  e  **[Docker]**  sono soluzioni open source che consentono agli sviluppatori automatizzare la distribuzione di hello, scalabilità e gestione delle applicazioni in esecuzione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="efb10-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="efb10-107">In questa esercitazione viene illustrato anche se la combinazione di queste due tecnologie comuni, open source di toodevelop e distribuire un tooMicrosoft di primavera avvio applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="efb10-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="efb10-108">In particolare, utilizzare  *[avvio Spring]*  per lo sviluppo di applicazioni,  *[Kubernetes]*  per la distribuzione di contenitore e hello [Servizio contenitore di azure (ACS)] toohost l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="efb10-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="efb10-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="efb10-109">Prerequisites</span></span>

* <span data-ttu-id="efb10-110">Sottoscrizione di Azure; se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN] oppure iscriversi per ottenere un [account Azure gratuito].</span><span class="sxs-lookup"><span data-stu-id="efb10-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="efb10-111">Hello [Azure interfaccia della riga di comando (CLI)].</span><span class="sxs-lookup"><span data-stu-id="efb10-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="efb10-112">Un [Java Developer Kit (JDK)] aggiornato.</span><span class="sxs-lookup"><span data-stu-id="efb10-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="efb10-113">Lo strumento di compilazione [Maven] di Apache (versione 3).</span><span class="sxs-lookup"><span data-stu-id="efb10-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="efb10-114">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="efb10-114">A [Git] client.</span></span>
* <span data-ttu-id="efb10-115">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="efb10-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="efb10-116">A causa di requisiti della virtualizzazione toohello di questa esercitazione, non è possibile seguire i passaggi di hello in questo articolo in una macchina virtuale; è necessario utilizzare un computer fisico con le funzionalità di virtualizzazione abilitate.</span><span class="sxs-lookup"><span data-stu-id="efb10-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="efb10-117">Creare hello avvio molla nell'applicazione web di Guida introduttiva di Docker</span><span class="sxs-lookup"><span data-stu-id="efb10-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="efb10-118">Hello seguendo i passaggi illustrati la creazione di un'applicazione web Spring avvio e il relativo test in locale.</span><span class="sxs-lookup"><span data-stu-id="efb10-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="efb10-119">Aprire un prompt dei comandi e creare toohold una directory locale dell'applicazione e spostarsi nella directory toothat; Per esempio:</span><span class="sxs-lookup"><span data-stu-id="efb10-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="efb10-120">- o-</span><span class="sxs-lookup"><span data-stu-id="efb10-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="efb10-121">Hello clone [avvio molla su Docker Introduzione] progetto di esempio nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="efb10-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="efb10-122">Directory toohello completata progetto modificato.</span><span class="sxs-lookup"><span data-stu-id="efb10-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="efb10-123">Utilizzare toobuild Maven e app di esempio hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="efb10-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="efb10-124">Test hello web app esplorando toohttp://localhost:8080 o con il seguente hello `curl` comando:</span><span class="sxs-lookup"><span data-stu-id="efb10-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="efb10-125">Dovrebbe essere hello segue messaggio visualizzato: **Docker Hello World**</span><span class="sxs-lookup"><span data-stu-id="efb10-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Esplorare l'app di esempio in locale][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="efb10-127">Creare un Azure contenitore del Registro di sistema utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="efb10-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="efb10-128">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="efb10-128">Open a command prompt.</span></span>

1. <span data-ttu-id="efb10-129">Accedi tooyour account di Azure:</span><span class="sxs-lookup"><span data-stu-id="efb10-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="efb10-130">Creare un gruppo di risorse per hello risorse di Azure utilizzate in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="efb10-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="efb10-131">Creare un registro di sistema contenitore privato di Azure nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="efb10-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="efb10-132">esercitazione Hello inserisce hello app di esempio come un Docker immagine toothis del Registro di sistema nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="efb10-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="efb10-133">Sostituire `wingtiptoysregistry` con un nome univoco per il registro.</span><span class="sxs-lookup"><span data-stu-id="efb10-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="efb10-134">Eseguire il push del Registro di sistema di app toohello contenitore</span><span class="sxs-lookup"><span data-stu-id="efb10-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="efb10-135">Passare toohello directory di configurazione per l'installazione di Maven (~/.m2/ predefinito o C:\Users\username\.m2) e aprire hello *Settings* file con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="efb10-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="efb10-136">Recuperare la password di hello per il Registro di sistema del contenitore da hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="efb10-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="efb10-137">Aggiungere il nuovo tooa del Registro di sistema di Azure contenitore di id e password `<server>` insieme in hello *Settings* file.</span><span class="sxs-lookup"><span data-stu-id="efb10-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="efb10-138">Hello `id` e `username` sono il nome di hello del Registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="efb10-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="efb10-139">Hello utilizzare `password` valore dal comando precedente di hello (senza virgolette).</span><span class="sxs-lookup"><span data-stu-id="efb10-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="efb10-140">Passare una directory del progetto toohello completato per l'applicazione di avvio Spring (ad esempio, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker / completamento*") e aprire hello *pom.xml* file con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="efb10-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="efb10-141">Hello aggiornamento `<properties>` insieme in hello *pom.xml* file con valore hello di server di accesso per il Registro di sistema di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="efb10-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="efb10-142">Hello aggiornamento `<plugins>` insieme in hello *pom.xml* file in modo che hello `<plugin>` contiene hello server indirizzo e del Registro di sistema nome di accesso per il Registro di sistema di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="efb10-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="efb10-143">Passare directory del progetto toohello completato per l'applicazione di avvio molla ed eseguire hello comando toobuild hello Docker contenitore e push hello immagine toohello del Registro di sistema seguente:</span><span class="sxs-lookup"><span data-stu-id="efb10-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="efb10-144">Si potrebbe ricevere un messaggio di errore è simile tooone seguenti hello quando Maven inserisce hello immagine tooAzure:</span><span class="sxs-lookup"><span data-stu-id="efb10-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="efb10-145">Se questo errore si verifica, accedere tooAzure dalla riga di comando di Docker hello.</span><span class="sxs-lookup"><span data-stu-id="efb10-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="efb10-146">Effettuare quindi il push del contenitore:</span><span class="sxs-lookup"><span data-stu-id="efb10-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="efb10-147">Creare un Kubernetes Cluster in ACS utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="efb10-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="efb10-148">Creare un cluster Kubernetes nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="efb10-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="efb10-149">Hello comando seguente crea un *kubernetes* cluster in hello *wingtiptoys kubernetes* risorse al gruppo *servizio contenitore di wingtiptoys* come cluster hello nome, e *wingtiptoys kubernetes* come prefisso DNS hello:</span><span class="sxs-lookup"><span data-stu-id="efb10-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="efb10-150">Questo comando potrebbe richiedere qualche minuto toocomplete.</span><span class="sxs-lookup"><span data-stu-id="efb10-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="efb10-151">Installare `kubectl` utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="efb10-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="efb10-152">Gli utenti di Linux potrebbero essere tooprefix questo comando con `sudo` poiché distribuisce hello Kubernetes CLI troppo`/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="efb10-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="efb10-153">Scaricare le informazioni di configurazione del cluster di hello, pertanto è possibile gestire il cluster dall'interfaccia web di hello Kubernetes e `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="efb10-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="efb10-154">Distribuire hello immagine tooyour Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="efb10-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="efb10-155">In questa esercitazione consente di distribuire app hello usando `kubectl`, quindi consentono di distribuzione hello tooexplore tramite l'interfaccia web di Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="efb10-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="efb10-156">Distribuire con l'interfaccia web di hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="efb10-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="efb10-157">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="efb10-157">Open a command prompt.</span></span>

1. <span data-ttu-id="efb10-158">Aprire hello sito Web di configurazione per il cluster Kubernetes nel browser predefinito:</span><span class="sxs-lookup"><span data-stu-id="efb10-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="efb10-159">Al sito Web di configurazione Kubernetes hello apre nel browser, fare clic su collegamento hello troppo**distribuire un'app nei contenitori**:</span><span class="sxs-lookup"><span data-stu-id="efb10-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Sito Web di configurazione di Kubernetes][KB01]

1. <span data-ttu-id="efb10-161">Quando hello **distribuire un'app nei contenitori** viene visualizzata la pagina, specificare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="efb10-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="efb10-162">a.</span><span class="sxs-lookup"><span data-stu-id="efb10-162">a.</span></span> <span data-ttu-id="efb10-163">Selezionare **Specify app details below** (Specificare più avanti i dettagli dell'app).</span><span class="sxs-lookup"><span data-stu-id="efb10-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="efb10-164">b.</span><span class="sxs-lookup"><span data-stu-id="efb10-164">b.</span></span> <span data-ttu-id="efb10-165">Immettere il nome dell'applicazione di avvio molla per hello **nome App**, ad esempio: "*docker gs-spring-avvio*".</span><span class="sxs-lookup"><span data-stu-id="efb10-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="efb10-166">c.</span><span class="sxs-lookup"><span data-stu-id="efb10-166">c.</span></span> <span data-ttu-id="efb10-167">Immettere l'immagine di contenitore e server di accesso da versioni precedenti per hello **immagine contenitore**, ad esempio: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="efb10-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="efb10-168">d.</span><span class="sxs-lookup"><span data-stu-id="efb10-168">d.</span></span> <span data-ttu-id="efb10-169">Scegliere **esterno** per hello **servizio**.</span><span class="sxs-lookup"><span data-stu-id="efb10-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="efb10-170">e.</span><span class="sxs-lookup"><span data-stu-id="efb10-170">e.</span></span> <span data-ttu-id="efb10-171">Specificare le porte interne ed esterne in hello **porta** e **porta di destinazione** caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="efb10-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Sito Web di configurazione di Kubernetes][KB02]


1. <span data-ttu-id="efb10-173">Fare clic su **Distribuisci** contenitore hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="efb10-173">Click **Deploy** toodeploy hello container.</span></span>

   ![Distribuire un contenitore][KB05]

1. <span data-ttu-id="efb10-175">Al termine della distribuzione dell'applicazione, l'applicazione Spring Boot verrà elencata in **Services** (Servizi).</span><span class="sxs-lookup"><span data-stu-id="efb10-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Servizi Kubernetes][KB06]

1. <span data-ttu-id="efb10-177">Se si fa clic sul collegamento hello per **endpoint esterni**, è possibile visualizzare l'applicazione di avvio Spring in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="efb10-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Servizi Kubernetes][KB07]

   ![Esplorare l'app di esempio in Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="efb10-180">Eseguire la distribuzione con kubectl</span><span class="sxs-lookup"><span data-stu-id="efb10-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="efb10-181">Aprire un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="efb10-181">Open a command prompt.</span></span>

1. <span data-ttu-id="efb10-182">Eseguire il contenitore in cluster Kubernetes hello utilizzando hello `kubectl run` comando.</span><span class="sxs-lookup"><span data-stu-id="efb10-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="efb10-183">Assegnare un nome di servizio per l'app in Kubernetes e un nome di immagine completa hello.</span><span class="sxs-lookup"><span data-stu-id="efb10-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="efb10-184">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efb10-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="efb10-185">In questo comando:</span><span class="sxs-lookup"><span data-stu-id="efb10-185">In this command:</span></span>

   * <span data-ttu-id="efb10-186">nome del contenitore Hello `gs-spring-boot-docker` specificato immediatamente dopo hello `run` comando</span><span class="sxs-lookup"><span data-stu-id="efb10-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="efb10-187">Hello `--image` parametro specifica hello combinati di server di accesso e il nome immagine`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="efb10-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="efb10-188">Esporre il cluster Kubernetes esternamente tramite hello `kubectl expose` comando.</span><span class="sxs-lookup"><span data-stu-id="efb10-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="efb10-189">Specificare il nome del servizio, hello pubblico TCP porta utilizzata tooaccess hello app e la porta di destinazione interno hello su che l'app è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="efb10-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="efb10-190">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efb10-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="efb10-191">In questo comando:</span><span class="sxs-lookup"><span data-stu-id="efb10-191">In this command:</span></span>

   * <span data-ttu-id="efb10-192">nome del contenitore Hello `gs-spring-boot-docker` specificato immediatamente dopo hello `expose deployment` comando</span><span class="sxs-lookup"><span data-stu-id="efb10-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="efb10-193">Hello `--type` parametro specifica di tale cluster hello Usa bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="efb10-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="efb10-194">Hello `--port` parametro specifica hello pubblico la porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="efb10-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="efb10-195">Accedere all'app hello su questa porta.</span><span class="sxs-lookup"><span data-stu-id="efb10-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="efb10-196">Hello `--target-port` parametro specifica hello interno la porta TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="efb10-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="efb10-197">servizio di bilanciamento del carico Hello inoltra le richieste tooyour app su questa porta.</span><span class="sxs-lookup"><span data-stu-id="efb10-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="efb10-198">Una volta distribuita l'applicazione hello toohello cluster, eseguire una query l'indirizzo IP esterno hello e aprirlo nel web browser:</span><span class="sxs-lookup"><span data-stu-id="efb10-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Esplorare l'app di esempio in Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="efb10-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efb10-200">Next steps</span></span>

<span data-ttu-id="efb10-201">Per ulteriori informazioni sull'utilizzo di avvio Spring in Azure, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="efb10-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="efb10-202">Distribuire un servizio App di Azure di toohello Spring avvio applicazione</span><span class="sxs-lookup"><span data-stu-id="efb10-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="efb10-203">Distribuire un'applicazione di avvio molla su Linux in hello servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="efb10-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="efb10-204">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="efb10-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="efb10-205">Per ulteriori informazioni sull'avvio Spring hello nel progetto di esempio Docker, vedere [avvio molla su Docker Introduzione].</span><span class="sxs-lookup"><span data-stu-id="efb10-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="efb10-206">Hello seguenti collegamenti fornisce informazioni aggiuntive sulla creazione di applicazioni Spring avvio:</span><span class="sxs-lookup"><span data-stu-id="efb10-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="efb10-207">Per ulteriori informazioni sulla creazione di una semplice applicazione Spring avvio, vedere hello Spring Initializr in https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="efb10-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="efb10-208">Hello seguenti collegamenti forniscono informazioni aggiuntive sull'utilizzo di Kubernetes con Azure:</span><span class="sxs-lookup"><span data-stu-id="efb10-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="efb10-209">Introduzione a un cluster Kubernetes nel servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="efb10-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="efb10-210">Utilizzo di hello Kubernetes web dell'interfaccia utente con il servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="efb10-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="efb10-211">Ulteriori informazioni sull'utilizzo dell'interfaccia della riga di comando Kubernetes sono disponibile in hello **kubectl** Guida dell'utente al <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="efb10-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="efb10-212">sito Web Kubernetes Hello sono diversi articoli che illustrano l'utilizzo di immagini in registri privati:</span><span class="sxs-lookup"><span data-stu-id="efb10-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="efb10-213">[Configuring Service Accounts for Pods] (Configurazione degli account del servizio per i pod)</span><span class="sxs-lookup"><span data-stu-id="efb10-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="efb10-214">[Namespaces] (Spazi dei nomi)</span><span class="sxs-lookup"><span data-stu-id="efb10-214">[Namespaces]</span></span>
* <span data-ttu-id="efb10-215">[Pulling an Image from a Private Registry] (Effettuare il pull di un'immagine da un registro privato)</span><span class="sxs-lookup"><span data-stu-id="efb10-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="efb10-216">Per altri esempi per la modalità toouse immagini Docker personalizzato con Azure, vedere [utilizzando un'immagine Docker personalizzata per l'App Web di Azure in Linux].</span><span class="sxs-lookup"><span data-stu-id="efb10-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure interfaccia della riga di comando (CLI)]: /cli/azure/overview
[Servizio contenitore di azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[utilizzando un'immagine Docker personalizzata per l'App Web di Azure in Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[account Azure gratuito]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[vantaggi per i sottoscrittori di MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[avvio Spring]: http://projects.spring.io/spring-boot/
[avvio molla su Docker Introduzione]: https://github.com/spring-guides/gs-spring-boot-docker (Introduzione a Spring Boot in Docker)
[Spring Framework]: https://spring.io/ (Framework di Spring)
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Configurazione degli account del servizio per i pod)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/ (Spazi dei nomi)
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Effettuare il pull di un'immagine da un registro privato)

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
