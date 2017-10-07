---
title: un contenitore Docker utilizzando aaaPublish hello Azure Toolkit per IntelliJ | Documenti Microsoft
description: Informazioni su come toopublish un tooMicrosoft app web Azure come un contenitore Docker usando hello Azure Toolkit per IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="74e6b-103">Pubblicare un'app web come un contenitore Docker usando hello Azure Toolkit per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="74e6b-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="74e6b-104">I contenitori Docker sono un metodo molto diffuso per la distribuzione di applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="74e6b-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="74e6b-105">Usando i contenitori di Docker, gli sviluppatori possono consolidare tutti i relativi file di progetto e le dipendenze in un singolo pacchetto tooa come server di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="74e6b-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="74e6b-106">Hello Azure Toolkit per IntelliJ semplifica questo processo per gli sviluppatori Java aggiungendo *pubblica come contenitore Docker* funzionalità per tooMicrosoft distribuzione Azure.</span><span class="sxs-lookup"><span data-stu-id="74e6b-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="74e6b-107">In questo articolo illustra hello passaggi necessari toopublish tooAzure le applicazioni come contenitori Docker.</span><span class="sxs-lookup"><span data-stu-id="74e6b-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="74e6b-108">Ulteriori informazioni su Docker sono disponibili sul hello [sito Web di Docker].</span><span class="sxs-lookup"><span data-stu-id="74e6b-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="74e6b-109">Pubblicare il tooAzure app web con un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="74e6b-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="74e6b-110">toopublish l'app web, è necessario creare un elemento pronto per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="74e6b-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="74e6b-111">toolearn informazioni, vedere hello [ulteriori informazioni sulla creazione di elementi](#artifacts) sezione.</span><span class="sxs-lookup"><span data-stu-id="74e6b-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="74e6b-112">Dopo aver completato la creazione guidata distribuzione hello almeno una volta, la maggior parte delle impostazioni vengono utilizzata come impostazioni predefinite quando si esegue nuovamente la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="74e6b-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="74e6b-113">Aprire il progetto dell'app Web in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="74e6b-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="74e6b-114">hello toostart **pubblica come contenitore Docker** procedura guidata, effettuare una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="74e6b-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="74e6b-115">In hello **progetto** finestra degli strumenti, mouse sul progetto, fare clic su **Azure**, quindi fare clic su **pubblica come contenitore Docker**:</span><span class="sxs-lookup"><span data-stu-id="74e6b-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Hello pubblica come comando contenitore Docker][PUB01]

   * <span data-ttu-id="74e6b-117">Sulla barra degli strumenti IntelliJ hello, fare clic su hello **gruppo pubblica** pulsante e quindi fare clic su **pubblica come contenitore Docker**:</span><span class="sxs-lookup"><span data-stu-id="74e6b-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="74e6b-118">![Hello pubblica come comando contenitore Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="74e6b-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="74e6b-119">Hello **distribuire contenitore Docker in Azure** apre la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="74e6b-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Hello contenitore Docker Distribuisci nella procedura guidata di Azure][PUB03]

3. <span data-ttu-id="74e6b-121">In hello **digitare un nome di immagine, selezionare il percorso dell'elemento hello e verificare un toobe host Docker utilizzato** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="74e6b-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="74e6b-122">a.</span><span class="sxs-lookup"><span data-stu-id="74e6b-122">a.</span></span> <span data-ttu-id="74e6b-123">In hello **nome immagine Docker** , immettere un nome univoco per l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="74e6b-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="74e6b-124">(hello verrà creata automaticamente un nome, ma è possibile modificarlo).</span><span class="sxs-lookup"><span data-stu-id="74e6b-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="74e6b-125">b.</span><span class="sxs-lookup"><span data-stu-id="74e6b-125">b.</span></span> <span data-ttu-id="74e6b-126">Hello **host** area vengono visualizzati tutti gli host Docker che è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="74e6b-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="74e6b-127">Effettuare una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="74e6b-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="74e6b-128">Se si dispone di un host Docker esistente, è possibile distribuire il tooit app web.</span><span class="sxs-lookup"><span data-stu-id="74e6b-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="74e6b-129">toocreate un host Docker, fare clic su verde hello sul segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="74e6b-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="74e6b-130">Hello **creare Host Docker** verrà visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="74e6b-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Procedura guidata Deploy Docker Container on Azure (Distribuisci contenitore Docker in Azure)][PUB04a]

4. <span data-ttu-id="74e6b-132">In hello **configurare hello nuova macchina virtuale** finestra, fornire le seguenti informazioni sull'host Docker hello.</span><span class="sxs-lookup"><span data-stu-id="74e6b-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="74e6b-133">(la maggior parte delle informazioni hello hello generato automaticamente, ma è possibile modificare ciascuno di essi).</span><span class="sxs-lookup"><span data-stu-id="74e6b-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="74e6b-134">a.</span><span class="sxs-lookup"><span data-stu-id="74e6b-134">a.</span></span> <span data-ttu-id="74e6b-135">In hello **nome** , immettere un nome univoco per l'host Docker hello.</span><span class="sxs-lookup"><span data-stu-id="74e6b-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="74e6b-136">(È hello non uguali a quelli hello Nome immagine con Docker specificato in precedenza).</span><span class="sxs-lookup"><span data-stu-id="74e6b-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="74e6b-137">b.</span><span class="sxs-lookup"><span data-stu-id="74e6b-137">b.</span></span> <span data-ttu-id="74e6b-138">In hello **sottoscrizione** immettere hello sottoscrizione di Azure in uso per l'host.</span><span class="sxs-lookup"><span data-stu-id="74e6b-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="74e6b-139">c.</span><span class="sxs-lookup"><span data-stu-id="74e6b-139">c.</span></span> <span data-ttu-id="74e6b-140">In hello **area** , immettere l'area geografica di hello in cui si trova nell'host.</span><span class="sxs-lookup"><span data-stu-id="74e6b-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="74e6b-141">d.</span><span class="sxs-lookup"><span data-stu-id="74e6b-141">d.</span></span> <span data-ttu-id="74e6b-142">In hello **del sistema operativo e le dimensioni** scheda, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="74e6b-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="74e6b-143">**Host del sistema operativo**: immettere hello del sistema operativo per la macchina virtuale hello che contiene l'host.</span><span class="sxs-lookup"><span data-stu-id="74e6b-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="74e6b-144">**Dimensioni**: immettere una dimensione di macchina virtuale hello per l'host.</span><span class="sxs-lookup"><span data-stu-id="74e6b-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="74e6b-145">e.</span><span class="sxs-lookup"><span data-stu-id="74e6b-145">e.</span></span> <span data-ttu-id="74e6b-146">In hello **gruppo di risorse** selezionare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="74e6b-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="74e6b-147">**New resource group** (Nuovo gruppo di risorse): consente di creare un nuovo gruppo di risorse per l'host.</span><span class="sxs-lookup"><span data-stu-id="74e6b-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="74e6b-148">**Existing resource group** (Gruppo di risorse esistente): consente di specificare un gruppo di risorse dal proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="74e6b-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="74e6b-149">f.</span><span class="sxs-lookup"><span data-stu-id="74e6b-149">f.</span></span> <span data-ttu-id="74e6b-150">In hello **rete** selezionare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="74e6b-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="74e6b-151">**New virtual network** (Nuova rete virtuale): consente di creare una nuova rete virtuale per l'host.</span><span class="sxs-lookup"><span data-stu-id="74e6b-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="74e6b-152">**Existing virtual network** (Rete virtuale esistente): consente di specificare una rete virtuale esistente dal proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="74e6b-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="74e6b-153">g.</span><span class="sxs-lookup"><span data-stu-id="74e6b-153">g.</span></span> <span data-ttu-id="74e6b-154">In hello **archiviazione** selezionare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="74e6b-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="74e6b-155">**New storage account** (Nuovo account di archiviazione): consente di creare un nuovo account di archiviazione per l'host.</span><span class="sxs-lookup"><span data-stu-id="74e6b-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="74e6b-156">**Existing storage account** (Account di archiviazione esistente): consente di specificare un account di archiviazione esistente dal proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="74e6b-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="74e6b-157">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="74e6b-157">Click **Next**.</span></span>  
     <span data-ttu-id="74e6b-158">Hello **configurare log nelle credenziali e le impostazioni delle porte** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="74e6b-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![log Configura Hello nella finestra di impostazioni di porta e credenziali][PUB05]

6. <span data-ttu-id="74e6b-160">Selezionare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="74e6b-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="74e6b-161">**Import credentials from Azure Key Vault** (Importa credenziali da Azure Key Vault): consente di specificare un set di credenziali salvato in precedenza e archiviato nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="74e6b-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="74e6b-162">Un insieme di credenziali chiave Azure creato con un account specifico o un'entità servizio non è accessibile automaticamente da un altro account o entità servizio che condivide sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="74e6b-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="74e6b-163">insieme di credenziali di un altro account o un servizio principale toouse hello chiave tooallow, è necessario utilizzare hello account hello tooadd portale Azure o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="74e6b-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="74e6b-164">**New log in credentials** (Nuove credenziali di accesso): consente di creare un nuovo set di credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="74e6b-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="74e6b-165">Se si seleziona questa opzione, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="74e6b-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="74e6b-166">a.</span><span class="sxs-lookup"><span data-stu-id="74e6b-166">a.</span></span> <span data-ttu-id="74e6b-167">In hello **credenziali VM** scheda, fornire le seguenti informazioni per le credenziali di accesso di macchina virtuale hello dell'host Docker hello: * **Username**: immettere un nome utente hello per l'account di accesso di macchina virtuale credenziali.</span><span class="sxs-lookup"><span data-stu-id="74e6b-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="74e6b-168">* **Password** e **conferma**: immettere la password di hello per le credenziali di accesso di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="74e6b-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="74e6b-169">* **SSH**: immettere le impostazioni di hello Secure Shell (SSH) per l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="74e6b-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="74e6b-170">È possibile selezionare una delle seguenti opzioni hello: * **Nessuna**: Specifica che la macchina virtuale non consente le connessioni SSH.</span><span class="sxs-lookup"><span data-stu-id="74e6b-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="74e6b-171">* **Generare automaticamente**: crea automaticamente hello le impostazioni necessarie per la connessione via SSH.</span><span class="sxs-lookup"><span data-stu-id="74e6b-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="74e6b-172">* **Importa da directory**: consente di toospecify una directory che contiene un set di impostazioni SSH salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="74e6b-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="74e6b-173">directory Hello deve contenere i seguenti due file hello:</span><span class="sxs-lookup"><span data-stu-id="74e6b-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="74e6b-174">b.</span><span class="sxs-lookup"><span data-stu-id="74e6b-174">b.</span></span> <span data-ttu-id="74e6b-175">In hello **Docker Daemon accesso** scheda, fornire hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="74e6b-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Creare un host Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="74e6b-177">Dopo avere immesso le informazioni necessarie hello, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="74e6b-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="74e6b-178">Hello **distribuire contenitore Docker in Azure** procedura guidata viene visualizzata di nuovo.</span><span class="sxs-lookup"><span data-stu-id="74e6b-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Procedura guidata Deploy Docker Container on Azure (Distribuisci contenitore Docker in Azure)][PUB07]

8. <span data-ttu-id="74e6b-180">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="74e6b-180">Click **Next**.</span></span>  
    <span data-ttu-id="74e6b-181">Hello **configurare hello Docker contenitore toobe creato** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="74e6b-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![finestra di Hello Configura hello Docker contenitore toobe creato][PUB08]

9. <span data-ttu-id="74e6b-183">In hello **configurare hello Docker contenitore toobe creato** finestra forniscono hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="74e6b-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="74e6b-184">a.</span><span class="sxs-lookup"><span data-stu-id="74e6b-184">a.</span></span> <span data-ttu-id="74e6b-185">In hello **nome del contenitore Docker** , immettere un nome univoco per il contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="74e6b-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="74e6b-186">b.</span><span class="sxs-lookup"><span data-stu-id="74e6b-186">b.</span></span> <span data-ttu-id="74e6b-187">Scegliere una delle seguenti immagini Docker hello:</span><span class="sxs-lookup"><span data-stu-id="74e6b-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="74e6b-188">**Predefined Docker image** (Immagine Docker predefinita): consente di specificare un'immagine preesistente in Azure.</span><span class="sxs-lookup"><span data-stu-id="74e6b-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="74e6b-189">elenco di Hello delle immagini Docker in questa casella è costituito da diverse immagini che hello Azure Toolkit è stato configurato toopatch in modo che l'elemento viene distribuita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="74e6b-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="74e6b-190">**Custom Dockerfile** (Dockerfile personalizzato): consente di specificare un Dockerfile salvato in precedenza nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="74e6b-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="74e6b-191">Questa è una funzionalità più avanzata per gli sviluppatori che desiderano toodeploy i propri Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="74e6b-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="74e6b-192">È invece backup toodevelopers che utilizzano questo tooensure opzione i Dockerfile compilato correttamente.</span><span class="sxs-lookup"><span data-stu-id="74e6b-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="74e6b-193">Hello Azure Toolkit non in grado di convalidare il contenuto di hello in un Dockerfile personalizzato, la distribuzione di hello potrebbe non riuscire se hello Dockerfile presenta problemi.</span><span class="sxs-lookup"><span data-stu-id="74e6b-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="74e6b-194">Inoltre, poiché hello Azure Toolkit si aspetta hello personalizzato Dockerfile toocontain un artefatto di app web, viene effettuato un tentativo tooopen una connessione HTTP.</span><span class="sxs-lookup"><span data-stu-id="74e6b-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="74e6b-195">Pubblicando un diverso tipo di elemento, gli sviluppatori potrebbero ricevere errori non gravi dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="74e6b-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="74e6b-196">c.</span><span class="sxs-lookup"><span data-stu-id="74e6b-196">c.</span></span> <span data-ttu-id="74e6b-197">In hello **le impostazioni delle porte** immettere hello univoco TCP binding delle porte per il contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="74e6b-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="74e6b-198">Dopo aver completato i passaggi precedenti, hello, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="74e6b-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="74e6b-199">Hello Azure Toolkit inizia il tooAzure app web in un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="74e6b-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="74e6b-200">A meno che non è stato configurato toobe IntelliJ distribuito in background hello, un **distribuzione tooAzure** viene visualizzato l'indicatore di stato.</span><span class="sxs-lookup"><span data-stu-id="74e6b-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![indicatore di stato di distribuzione Hello][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="74e6b-202">Altre informazioni sulla creazione di elementi</span><span class="sxs-lookup"><span data-stu-id="74e6b-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="74e6b-203">hello toocreate un elemento, pronto per la distribuzione seguenti:</span><span class="sxs-lookup"><span data-stu-id="74e6b-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="74e6b-204">Aprire il progetto dell'app Web in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="74e6b-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="74e6b-205">Fare clic su **File** e quindi fare clic su **Project Structure** (Struttura del progetto).</span><span class="sxs-lookup"><span data-stu-id="74e6b-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Hello comando struttura del progetto][ART01]

3. <span data-ttu-id="74e6b-207">tooadd un elemento, fare clic su verde hello sul segno più (**+**), quindi fare clic su **applicazione Web: archivio**.</span><span class="sxs-lookup"><span data-stu-id="74e6b-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![il comando "Archivio Web applicazione:" Hello][ART02]

4. <span data-ttu-id="74e6b-209">In hello **nome** , immettere un nome per l'elemento (non includono hello *.war* estensione), quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="74e6b-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![casella nome di elemento Hello][ART03]

<span data-ttu-id="74e6b-211">Per ulteriori informazioni sulla creazione di elementi in IntelliJ, vedere [configurando elementi] nel sito Web JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="74e6b-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74e6b-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74e6b-212">Next steps</span></span>
<span data-ttu-id="74e6b-213">Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="74e6b-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="74e6b-214">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="74e6b-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="74e6b-215">[Novità di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="74e6b-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="74e6b-216">[L'installazione di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="74e6b-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="74e6b-217">[Istruzioni di accesso per hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="74e6b-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="74e6b-218">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="74e6b-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="74e6b-219">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="74e6b-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="74e6b-220">[Novità di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="74e6b-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="74e6b-221">[Installazione di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="74e6b-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="74e6b-222">[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="74e6b-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="74e6b-223">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="74e6b-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="74e6b-224">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="74e6b-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="74e6b-225">Per altre risorse per Docker, vedere ufficiale hello [sito Web di Docker].</span><span class="sxs-lookup"><span data-stu-id="74e6b-225">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Istruzioni di accesso per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/

[sito Web di Docker]: https://www.docker.com/
[configurando elementi]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configurazione di elementi)

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
