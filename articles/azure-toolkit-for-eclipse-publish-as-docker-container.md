---
title: un contenitore Docker utilizzando aaaPublish hello Azure Toolkit per Eclipse | Documenti Microsoft
description: Informazioni su come toopublish un tooMicrosoft app web Azure come un contenitore Docker usando hello Azure Toolkit per Eclipse.
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="d9501-103">Pubblicare un'app web come un contenitore Docker usando hello Azure Toolkit per Eclipse</span><span class="sxs-lookup"><span data-stu-id="d9501-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="d9501-104">I contenitori Docker sono un metodo molto diffuso per la distribuzione di applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="d9501-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="d9501-105">Usando i contenitori di Docker, gli sviluppatori possono consolidare tutti i relativi file di progetto e le dipendenze in un singolo pacchetto tooa come server di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d9501-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="d9501-106">Hello Azure Toolkit per Eclipse semplifica questo processo per gli sviluppatori Java aggiungendo *pubblica come contenitore Docker* funzionalità per tooMicrosoft distribuzione Azure.</span><span class="sxs-lookup"><span data-stu-id="d9501-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="d9501-107">In questo articolo illustra hello passaggi necessari toopublish tooAzure le applicazioni come contenitori Docker.</span><span class="sxs-lookup"><span data-stu-id="d9501-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="d9501-108">Ulteriori informazioni su Docker sono disponibili sul hello [sito Web di Docker].</span><span class="sxs-lookup"><span data-stu-id="d9501-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="d9501-109">Pubblicare il tooAzure app web con un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="d9501-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="d9501-110">Aprire il progetto dell'applicazione Web in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d9501-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="d9501-111">hello toostart **pubblica come contenitore Docker** procedura guidata, effettuare una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="d9501-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="d9501-112">In hello **Navigator** visualizzare mouse sul progetto, fare clic su **Azure**, quindi fare clic su **pubblica come contenitore Docker**.</span><span class="sxs-lookup"><span data-stu-id="d9501-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Comando Publish as Docker Container (Pubblica come contenitore Docker) nella vista Navigator (Strumento di navigazione)][PUB01]

   * <span data-ttu-id="d9501-114">Sulla barra degli strumenti di hello Eclipse, fare clic su hello **pubblica** pulsante e quindi fare clic su **pubblica come contenitore Docker**.</span><span class="sxs-lookup"><span data-stu-id="d9501-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Comando Publish as Docker Container (Pubblica come contenitore Docker) sulla barra degli strumenti di Eclipse][PUB02]
      
    <span data-ttu-id="d9501-116">Hello **distribuire contenitore Docker in Azure** apre la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="d9501-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Hello contenitore Docker Distribuisci nella procedura guidata di Azure][PUB03]

3. <span data-ttu-id="d9501-118">In hello **digitare un nome di immagine, selezionare il percorso dell'elemento hello e verificare un toobe host Docker utilizzato** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9501-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="d9501-119">a.</span><span class="sxs-lookup"><span data-stu-id="d9501-119">a.</span></span> <span data-ttu-id="d9501-120">In hello **nome immagine Docker** , immettere un nome univoco per l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="d9501-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="d9501-121">(hello verrà creata automaticamente un nome, ma è possibile modificarlo).</span><span class="sxs-lookup"><span data-stu-id="d9501-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="d9501-122">b.</span><span class="sxs-lookup"><span data-stu-id="d9501-122">b.</span></span> <span data-ttu-id="d9501-123">Hello **host** area vengono visualizzati tutti gli host Docker che è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="d9501-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="d9501-124">Effettuare una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="d9501-124">Do either of hello following:</span></span>

    * <span data-ttu-id="d9501-125">Se si dispone di un host Docker esistente, è possibile distribuire il tooit app web.</span><span class="sxs-lookup"><span data-stu-id="d9501-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="d9501-126">Fare clic su un nuovo host Docker, toocreate **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d9501-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="d9501-127">Hello **creare Host Docker** verrà visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d9501-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Procedura guidata Deploy Docker Container on Azure (Distribuisci contenitore Docker in Azure)][PUB04a]

4. <span data-ttu-id="d9501-129">In hello **configurare hello nuova macchina virtuale** finestra, specificare le opzioni per l'host Docker seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="d9501-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="d9501-130">(la maggior parte delle opzioni hello hello generato automaticamente, ma è possibile modificare ciascuno di essi).</span><span class="sxs-lookup"><span data-stu-id="d9501-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="d9501-131">a.</span><span class="sxs-lookup"><span data-stu-id="d9501-131">a.</span></span> <span data-ttu-id="d9501-132">**Nome**: immettere un nome univoco per l'host Docker hello.</span><span class="sxs-lookup"><span data-stu-id="d9501-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="d9501-133">(È hello non uguali a quelli hello Nome immagine con Docker specificato in precedenza).</span><span class="sxs-lookup"><span data-stu-id="d9501-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="d9501-134">b.</span><span class="sxs-lookup"><span data-stu-id="d9501-134">b.</span></span> <span data-ttu-id="d9501-135">**Sottoscrizione**: immettere hello sottoscrizione di Azure in uso per l'host.</span><span class="sxs-lookup"><span data-stu-id="d9501-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="d9501-136">c.</span><span class="sxs-lookup"><span data-stu-id="d9501-136">c.</span></span> <span data-ttu-id="d9501-137">**Area**: entrare hello un'area geografica in cui si trova nell'host.</span><span class="sxs-lookup"><span data-stu-id="d9501-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="d9501-138">d.</span><span class="sxs-lookup"><span data-stu-id="d9501-138">d.</span></span> <span data-ttu-id="d9501-139">In hello **del sistema operativo Host e le dimensioni** scheda:</span><span class="sxs-lookup"><span data-stu-id="d9501-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="d9501-140">**Host del sistema operativo**: immettere hello del sistema operativo per la macchina virtuale hello che contiene l'host.</span><span class="sxs-lookup"><span data-stu-id="d9501-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="d9501-141">**Dimensioni**: immettere una dimensione di macchina virtuale hello per l'host.</span><span class="sxs-lookup"><span data-stu-id="d9501-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="d9501-142">e.</span><span class="sxs-lookup"><span data-stu-id="d9501-142">e.</span></span> <span data-ttu-id="d9501-143">In hello **gruppo di risorse** scheda:</span><span class="sxs-lookup"><span data-stu-id="d9501-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="d9501-144">**New resource group** (Nuovo gruppo di risorse): creare un nuovo gruppo di risorse per l'host.</span><span class="sxs-lookup"><span data-stu-id="d9501-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="d9501-145">**Existing resource group** (Gruppo di risorse esistente): immettere un gruppo di risorse dal proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="d9501-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="d9501-146">f.</span><span class="sxs-lookup"><span data-stu-id="d9501-146">f.</span></span> <span data-ttu-id="d9501-147">In hello **rete** scheda:</span><span class="sxs-lookup"><span data-stu-id="d9501-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="d9501-148">**New virtual network** (Nuova rete virtuale): creare una nuova rete virtuale per l'host.</span><span class="sxs-lookup"><span data-stu-id="d9501-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="d9501-149">**Existing virtual network** (Rete virtuale esistente): immettere una rete virtuale esistente dal proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="d9501-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="d9501-150">g.</span><span class="sxs-lookup"><span data-stu-id="d9501-150">g.</span></span> <span data-ttu-id="d9501-151">In hello **archiviazione** scheda:</span><span class="sxs-lookup"><span data-stu-id="d9501-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="d9501-152">**New storage account** (Nuovo account di archiviazione): creare un nuovo account di archiviazione per l'host.</span><span class="sxs-lookup"><span data-stu-id="d9501-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="d9501-153">**Existing storage account** (Account di archiviazione esistente): immettere un account di archiviazione esistente dal proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="d9501-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="d9501-154">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d9501-154">Click **Next**.</span></span>

6. <span data-ttu-id="d9501-155">In hello **configurare log nelle credenziali e le impostazioni delle porte** finestra, selezionare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="d9501-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="d9501-156">**Import credentials from Azure Key Vault** (Importa credenziali da Azure Key Vault): specifica un set di credenziali salvato in precedenza e archiviato nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9501-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="d9501-157">Un insieme di credenziali chiave di Azure che viene creato con un account specifico o un'entità servizio non è accessibile automaticamente da un altro account o entità servizio che condivide sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="d9501-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="d9501-158">tooallow un altro account o un servizio principale toouse hello insieme di credenziali chiave, è necessario utilizzare hello account hello tooadd portale Azure o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="d9501-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="d9501-159">**New log in credentials** (Nuove credenziali di accesso): crea un nuovo set di credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="d9501-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="d9501-160">Se si seleziona questa opzione, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9501-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="d9501-161">In hello **credenziali VM** scheda, scegliere una delle seguenti hello opzioni per le credenziali di accesso di macchina virtuale hello dell'host Docker:</span><span class="sxs-lookup"><span data-stu-id="d9501-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="d9501-162">**Nome utente**: immettere un nome utente hello per le credenziali di accesso della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d9501-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="d9501-163">**Password** e **conferma**: immettere la password di hello per le credenziali di accesso della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d9501-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="d9501-164">**SSH**: immettere le impostazioni di hello Secure Shell (SSH) per l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="d9501-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="d9501-165">È possibile scegliere tra hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9501-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="d9501-166">**None** (Nessuna): specifica che la macchina virtuale non consentirà connessioni SSH.</span><span class="sxs-lookup"><span data-stu-id="d9501-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="d9501-167">**Generare automaticamente**: crea automaticamente hello le impostazioni necessarie per la connessione via SSH.</span><span class="sxs-lookup"><span data-stu-id="d9501-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="d9501-168">**Import from directory** (Importa da directory): specifica una directory che contiene un set di impostazioni SSH salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d9501-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="d9501-169">directory Hello deve contenere i seguenti due file hello:</span><span class="sxs-lookup"><span data-stu-id="d9501-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="d9501-170">*id_rsa*: contiene l'identificazione di hello RSA per un utente.</span><span class="sxs-lookup"><span data-stu-id="d9501-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="d9501-171">*id_rsa.pub*: hello chiave pubblica RSA utilizzata per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d9501-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Creare un host Docker][PUB05]

      * <span data-ttu-id="d9501-173">In hello **Docker Daemon credenziali** specificare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9501-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="d9501-174">**Porta Daemon docker**: immettere la porta TCP hello univoca per l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="d9501-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="d9501-175">**Protezione TLS**: immettere le impostazioni di hello Transport Layer Security per l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="d9501-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="d9501-176">È possibile scegliere tra hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9501-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="d9501-177">**None** (Nessuna): specifica che la macchina virtuale non consentirà connessioni TLS.</span><span class="sxs-lookup"><span data-stu-id="d9501-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="d9501-178">**Generare automaticamente**: crea automaticamente hello le impostazioni necessarie per la connessione tramite TLS.</span><span class="sxs-lookup"><span data-stu-id="d9501-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="d9501-179">**Import from directory** (Importa da directory): specifica una directory che contiene un set di impostazioni TLS salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d9501-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="d9501-180">In particolare, directory hello deve contenere i seguenti sei file hello:</span><span class="sxs-lookup"><span data-stu-id="d9501-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="d9501-181">*CA.PEM* e *ca key.pem*: contengono certificato hello e una chiave pubblica per hello TLS autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="d9501-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="d9501-182">*CERT.PEM* e *key.pem*: contengono certificato client hello e una chiave pubblica che viene utilizzata per l'autenticazione TLS.</span><span class="sxs-lookup"><span data-stu-id="d9501-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="d9501-183">*Server.PEM* e *server key.pem*: contengono certificato server hello e una chiave pubblica per host hello.</span><span class="sxs-lookup"><span data-stu-id="d9501-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Creare un host Docker][PUB06]

7. <span data-ttu-id="d9501-185">Dopo avere immesso le precedenti informazioni hello, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="d9501-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="d9501-186">In hello **distribuire contenitore Docker in Azure** procedura guidata, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d9501-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Hello contenitore Docker Distribuisci nella procedura guidata di Azure][PUB07]

9. <span data-ttu-id="d9501-188">In hello **configurare hello Docker contenitore toobe creato** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9501-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="d9501-189">a.</span><span class="sxs-lookup"><span data-stu-id="d9501-189">a.</span></span> <span data-ttu-id="d9501-190">In hello **nome del contenitore Docker** , immettere un nome univoco per il contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="d9501-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="d9501-191">b.</span><span class="sxs-lookup"><span data-stu-id="d9501-191">b.</span></span> <span data-ttu-id="d9501-192">Scegliere una delle seguenti immagini Docker hello:</span><span class="sxs-lookup"><span data-stu-id="d9501-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="d9501-193">**Predefined Docker image** (Immagine Docker predefinita): specifica un'immagine preesistente in Azure.</span><span class="sxs-lookup"><span data-stu-id="d9501-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="d9501-194">elenco di Hello delle immagini Docker in questa casella è costituito da diverse immagini che hello Azure Toolkit è stato configurato toopatch in modo che l'elemento viene distribuita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d9501-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="d9501-195">**Custom Dockerfile** (Dockerfile personalizzato): specifica un Dockerfile salvato in precedenza nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="d9501-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="d9501-196">Questa è una funzionalità più avanzata per gli sviluppatori che desiderano toodeploy i propri Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="d9501-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="d9501-197">È invece backup toodevelopers che utilizzano questo tooensure opzione i Dockerfile compilato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d9501-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="d9501-198">Hello Azure Toolkit non convalidare il contenuto di hello in un Dockerfile personalizzato, in modo distribuzione hello potrebbe non riuscire se hello Dockerfile presenta problemi.</span><span class="sxs-lookup"><span data-stu-id="d9501-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="d9501-199">Inoltre, hello Azure Toolkit prevede hello personalizzato Dockerfile toocontain un artefatto di app web, e verrà eseguito un tentativo tooopen una connessione HTTP.</span><span class="sxs-lookup"><span data-stu-id="d9501-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="d9501-200">Pubblicando un diverso tipo di elemento, gli sviluppatori potrebbero ricevere errori non gravi dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d9501-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="d9501-201">c.</span><span class="sxs-lookup"><span data-stu-id="d9501-201">c.</span></span> <span data-ttu-id="d9501-202">**Le impostazioni delle porte**: immettere hello univoco TCP binding delle porte per il contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="d9501-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![finestra di Hello Configura hello Docker contenitore toobe creato][PUB08]

10. <span data-ttu-id="d9501-204">Dopo aver completato tutti i passaggi precedenti, hello, fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="d9501-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="d9501-205">Hello Azure Toolkit inizia il tooAzure app web in un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="d9501-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d9501-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d9501-206">Next steps</span></span>
<span data-ttu-id="d9501-207">Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="d9501-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="d9501-208">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d9501-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d9501-209">[Novità di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d9501-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d9501-210">[L'installazione di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d9501-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d9501-211">[Istruzioni di accesso per hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d9501-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d9501-212">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d9501-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="d9501-213">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d9501-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d9501-214">[Novità di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d9501-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d9501-215">[Installazione di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d9501-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d9501-216">[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d9501-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d9501-217">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d9501-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="d9501-218">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d9501-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="d9501-219">Per altre risorse per Docker, vedere ufficiale hello [sito Web di Docker].</span><span class="sxs-lookup"><span data-stu-id="d9501-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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
[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/

[sito Web di Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png