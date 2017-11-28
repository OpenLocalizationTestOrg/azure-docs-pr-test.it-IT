---
title: distribuzione aaaContinuous per le funzioni di Azure | Documenti Microsoft
description: "Utilizzare le funzionalità di distribuzione continua del servizio App di Azure toopublish delle funzioni di Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="311d3-103">Distribuzione continua per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="311d3-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="311d3-104">Funzioni di Azure rende facile toodeploy app funzione mediante l'integrazione continua di servizio App.</span><span class="sxs-lookup"><span data-stu-id="311d3-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="311d3-105">Le funzioni si integrano con Dropbox, GitHub, BitBucket e Visual Studio Team Services, VSTS.</span><span class="sxs-lookup"><span data-stu-id="311d3-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="311d3-106">In questo modo un flusso di lavoro in cui il codice di funzione viene aggiornato utilizzando uno di questi tooAzure di distribuzione di servizi integrati trigger.</span><span class="sxs-lookup"><span data-stu-id="311d3-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="311d3-107">Nel caso di nuove funzioni tooAzure, iniziare con [panoramica delle funzioni di Azure](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="311d3-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="311d3-108">La distribuzione continua è un'ottima opzione per i progetti in cui vengono integrati contributi numerosi e frequenti.</span><span class="sxs-lookup"><span data-stu-id="311d3-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="311d3-109">Consente anche di mantenere il controllo dell'origine del codice funzione.</span><span class="sxs-lookup"><span data-stu-id="311d3-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="311d3-110">Hello seguenti origini di distribuzione è attualmente supportata:</span><span class="sxs-lookup"><span data-stu-id="311d3-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="311d3-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="311d3-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="311d3-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="311d3-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="311d3-113">Archivio esterno (Git o Mercurial)</span><span class="sxs-lookup"><span data-stu-id="311d3-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="311d3-114">Archivio locale GIT</span><span class="sxs-lookup"><span data-stu-id="311d3-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="311d3-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="311d3-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="311d3-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="311d3-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="311d3-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="311d3-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="311d3-118">Le distribuzioni sono configurate in base alla singola app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="311d3-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="311d3-119">Dopo aver abilitata la distribuzione continua, l'accesso di codice toofunction nel portale di hello è impostato troppo*sola lettura*.</span><span class="sxs-lookup"><span data-stu-id="311d3-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="311d3-120">Requisiti per la distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="311d3-120">Continuous deployment requirements</span></span>

<span data-ttu-id="311d3-121">È necessario disporre dell'origine di distribuzione configurati e il codice funzioni nell'origine distribuzione hello prima di impostare la distribuzione continua.</span><span class="sxs-lookup"><span data-stu-id="311d3-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="311d3-122">In una distribuzione di app di funzione specificata, ogni funzione si trova in una sottodirectory denominata, dove il nome di directory hello è il nome di hello della funzione hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="311d3-123">Configurare la distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="311d3-123">Set up continuous deployment</span></span>
<span data-ttu-id="311d3-124">Utilizzare questa distribuzione continua tooconfigure di procedure per un'app di funzione esistente.</span><span class="sxs-lookup"><span data-stu-id="311d3-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="311d3-125">Questa procedura illustra l'integrazione con un archivio di GitHub. Una procedura analoga si applica a Visual Studio Team Services o ad altri servizi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="311d3-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="311d3-126">Nell'app di funzione in hello [portale di Azure](https://portal.azure.com), fare clic su **funzionalità della piattaforma** e **opzioni di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="311d3-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="311d3-128">Quindi in hello **distribuzioni** fare clic su pannello **installazione**.</span><span class="sxs-lookup"><span data-stu-id="311d3-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="311d3-130">In hello **origine distribuzione** pannello, fare clic su **origine scegliere**, quindi immettere le informazioni di hello per l'origine di distribuzione scelto e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="311d3-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![Scegliere l'origine della distribuzione](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="311d3-132">Dopo aver configurata la distribuzione continua, tutte le modifiche ai file dell'origine di distribuzione vengono copiati toohello app di funzione e viene attivata una distribuzione completa del sito.</span><span class="sxs-lookup"><span data-stu-id="311d3-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="311d3-133">sito Hello viene ridistribuito quando vengono aggiornati i file di origine hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="311d3-134">Opzioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="311d3-134">Deployment options</span></span>

<span data-ttu-id="311d3-135">di seguito Hello sono alcuni scenari di distribuzione tipiche:</span><span class="sxs-lookup"><span data-stu-id="311d3-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="311d3-136">Creare una distribuzione di staging</span><span class="sxs-lookup"><span data-stu-id="311d3-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="311d3-137">Spostare una distribuzione esistente toocontinuous di funzioni</span><span class="sxs-lookup"><span data-stu-id="311d3-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="311d3-138">Creare una distribuzione di staging</span><span class="sxs-lookup"><span data-stu-id="311d3-138">Create a staging deployment</span></span>

<span data-ttu-id="311d3-139">Le app per le funzioni non supportano ancora slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="311d3-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="311d3-140">È comunque possibile gestire distribuzioni di staging e di produzione separate tramite l'integrazione continua.</span><span class="sxs-lookup"><span data-stu-id="311d3-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="311d3-141">processo tooconfigure Hello e di lavoro con una distribuzione di gestione temporanea è in genere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="311d3-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="311d3-142">Creare due applicazioni di funzione nella sottoscrizione, uno per il codice di produzione hello e uno per la gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="311d3-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="311d3-143">Creare un'origine della distribuzione, se non è già presente.</span><span class="sxs-lookup"><span data-stu-id="311d3-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="311d3-144">Questo esempio usa [GitHub].</span><span class="sxs-lookup"><span data-stu-id="311d3-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="311d3-145">Per l'app di funzione di produzione, hello completo precedente i passaggi **impostare la distribuzione continua** e set hello distribuzione ramo toohello ramo master del repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="311d3-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![Scegliere il ramo della distribuzione](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="311d3-147">Ripetere questo passaggio per hello app di funzione di gestione temporanea, ma scegliere hello gestione temporanea invece di ramo nel repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="311d3-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="311d3-148">Se l'origine della distribuzione non supporta le diramazioni, usare una cartella diversa.</span><span class="sxs-lookup"><span data-stu-id="311d3-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="311d3-149">Apportare aggiornamenti tooyour codice hello ramo o una cartella di gestione temporanea, quindi verificare che tali modifiche si rifletteranno in hello distribuzione di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="311d3-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="311d3-150">Al termine del test, unire le modifiche dal ramo di gestione temporanea nel ramo master hello hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="311d3-151">Questo tipo di merge Attiva distribuzione toohello produzione funzione app.</span><span class="sxs-lookup"><span data-stu-id="311d3-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="311d3-152">Se l'origine di distribuzione non supporta i rami, sovrascrivere i file nella cartella di produzione hello hello con file hello hello cartella di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="311d3-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="311d3-153">Spostare una distribuzione esistente toocontinuous di funzioni</span><span class="sxs-lookup"><span data-stu-id="311d3-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="311d3-154">Quando si dispongono di funzioni esistenti creati e gestiti nel portale di hello, è necessario toodownload esistente funzione tramite FTP o hello repository Git locale prima di impostare la distribuzione continua come descritto in precedenza i file di codice.</span><span class="sxs-lookup"><span data-stu-id="311d3-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="311d3-155">È possibile farlo in hello le impostazioni di servizio App per l'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="311d3-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="311d3-156">Dopo che vengono scaricati i file, è possibile caricare le origine distribuzione continua tooyour scelto.</span><span class="sxs-lookup"><span data-stu-id="311d3-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="311d3-157">Dopo aver configurato l'integrazione continua, non sarà non è più in grado di tooedit l'origine dei file nel portale le funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="311d3-158">Procedura: Configurare le credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="311d3-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="311d3-159">Procedura: Scaricare i file con FTP</span><span class="sxs-lookup"><span data-stu-id="311d3-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="311d3-160">Procedura: scaricare file utilizzando l'archivio Git locale hello</span><span class="sxs-lookup"><span data-stu-id="311d3-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="311d3-161">Procedura: Configurare le credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="311d3-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="311d3-162">Prima di poter scaricare i file dall'app di funzione con FTP o nell'archivio Git locale, è necessario configurare il sito di hello tooaccess credenziali.</span><span class="sxs-lookup"><span data-stu-id="311d3-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="311d3-163">Le credenziali vengono impostate a livello di app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="311d3-164">Utilizzare hello seguenti passaggi viene tooset le credenziali di distribuzione nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="311d3-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="311d3-165">Nell'app di funzione in hello [portale di Azure](https://portal.azure.com), fare clic su **funzionalità della piattaforma** e **le credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="311d3-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Impostare le credenziali di distribuzione locali](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="311d3-167">Immettere un nome utente e una password, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="311d3-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="311d3-168">Ora è possibile utilizzare questi tooaccess credenziali app funzione dal repository Git predefinito hello o FTP.</span><span class="sxs-lookup"><span data-stu-id="311d3-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="311d3-169">Procedura: Scaricare i file tramite FTP</span><span class="sxs-lookup"><span data-stu-id="311d3-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="311d3-170">Nell'app di funzione in hello [portale di Azure](https://portal.azure.com), fare clic su **funzionalità della piattaforma** e **proprietà**, quindi copiare i valori hello per **utente FTP/distribuzione**, **Nome Host FTP**, e **nome Host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="311d3-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="311d3-171">**Utente FTP/distribuzione** deve essere immesso come visualizzato nel portale di hello, incluso il nome dell'applicazione hello, tooprovide contesto appropriato per il server FTP hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![Ottenere le informazioni di distribuzione](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="311d3-173">Dal client FTP, utilizzare le informazioni di connessione hello raccolte tooconnect tooyour app e scaricare i file di origine hello per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="311d3-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="311d3-174">Procedura: scaricare file tramite l'archivio GIT locale</span><span class="sxs-lookup"><span data-stu-id="311d3-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="311d3-175">Nell'app di funzione in hello [portale di Azure](https://portal.azure.com), fare clic su **funzionalità della piattaforma** e **opzioni di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="311d3-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="311d3-177">Quindi in hello **distribuzioni** fare clic su pannello **installazione**.</span><span class="sxs-lookup"><span data-stu-id="311d3-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="311d3-179">In hello **origine distribuzione** pannello, fare clic su **repository Git locale** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="311d3-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="311d3-180">In **funzionalità della piattaforma**, fare clic su **proprietà** e annotare il valore di hello dell'URL di Git.</span><span class="sxs-lookup"><span data-stu-id="311d3-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="311d3-182">Clonare il repository hello sul computer locale utilizzando un prompt dei comandi basato su Git o lo strumento preferito di Git.</span><span class="sxs-lookup"><span data-stu-id="311d3-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="311d3-183">comando di Git clone Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="311d3-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="311d3-184">Recuperare i file dal clone toohello app di funzione nel computer locale, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="311d3-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="311d3-185">Se richiesto inserire le [credenziali di distribuzione configurate](#credentials).</span><span class="sxs-lookup"><span data-stu-id="311d3-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
