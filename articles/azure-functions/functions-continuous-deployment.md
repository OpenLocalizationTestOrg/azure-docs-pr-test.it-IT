---
title: Distribuzione continua per Funzioni di Azure | Documentazione Microsoft
description: "Per pubblicare Funzioni di Azure, usare le funzionalità di distribuzione continua del servizio app di Azure."
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
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="fb19d-103">Distribuzione continua per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="fb19d-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="fb19d-104">Le funzioni di Azure semplificano la distribuzione dell'app per le funzioni usando l'integrazione continua del servizio app.</span><span class="sxs-lookup"><span data-stu-id="fb19d-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="fb19d-105">Le funzioni si integrano con Dropbox, GitHub, BitBucket e Visual Studio Team Services, VSTS.</span><span class="sxs-lookup"><span data-stu-id="fb19d-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="fb19d-106">In questo modo viene abilitato un flusso di lavoro in cui gli aggiornamenti al codice della funzione vengono eseguiti tramite una di queste distribuzioni del trigger dei servizi integrati in Azure.</span><span class="sxs-lookup"><span data-stu-id="fb19d-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="fb19d-107">Se non si ha familiarità con Funzioni di Azure, iniziare con [Panoramica di Funzioni di Azure](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb19d-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="fb19d-108">La distribuzione continua è un'ottima opzione per i progetti in cui vengono integrati contributi numerosi e frequenti.</span><span class="sxs-lookup"><span data-stu-id="fb19d-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="fb19d-109">Consente anche di mantenere il controllo dell'origine del codice funzione.</span><span class="sxs-lookup"><span data-stu-id="fb19d-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="fb19d-110">Sono attualmente supportate le origini di distribuzione seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb19d-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="fb19d-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="fb19d-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="fb19d-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="fb19d-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="fb19d-113">Archivio esterno (Git o Mercurial)</span><span class="sxs-lookup"><span data-stu-id="fb19d-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="fb19d-114">Archivio locale GIT</span><span class="sxs-lookup"><span data-stu-id="fb19d-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="fb19d-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="fb19d-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="fb19d-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="fb19d-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="fb19d-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="fb19d-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="fb19d-118">Le distribuzioni sono configurate in base alla singola app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="fb19d-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="fb19d-119">Dopo aver abilitato la distribuzione continua, l'accesso al codice di funzione nel portale viene impostato su *sola lettura*.</span><span class="sxs-lookup"><span data-stu-id="fb19d-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="fb19d-120">Requisiti per la distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="fb19d-120">Continuous deployment requirements</span></span>

<span data-ttu-id="fb19d-121">È necessario che l'origine della distribuzione sia configurata e che il codice funzioni sia presente nell'origine della distribuzione prima di configurare la distribuzione continua.</span><span class="sxs-lookup"><span data-stu-id="fb19d-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="fb19d-122">In una determinata distribuzione di app per le funzioni, ogni funzione si trova in una sottodirectory denominata, dove il nome della directory è il nome della funzione.</span><span class="sxs-lookup"><span data-stu-id="fb19d-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="fb19d-123">Configurare la distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="fb19d-123">Set up continuous deployment</span></span>
<span data-ttu-id="fb19d-124">Usare la procedura seguente per configurare la distribuzione continua per un'app per le funzioni esistente.</span><span class="sxs-lookup"><span data-stu-id="fb19d-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="fb19d-125">Questa procedura illustra l'integrazione con un archivio di GitHub. Una procedura analoga si applica a Visual Studio Team Services o ad altri servizi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fb19d-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="fb19d-126">Nell'app per le funzioni nel [portale di Azure](https://portal.azure.com) fare clic su **Funzionalità della piattaforma** e **Opzioni di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="fb19d-128">Quindi, nel pannello **Distribuzione** fare clic su **Installazione**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="fb19d-130">Nel pannello **Origine distribuzione** fare clic su **Scegliere l'origine**, quindi inserire le informazioni per l'origine della distribuzione scelta e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Scegliere l'origine della distribuzione](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="fb19d-132">Dopo aver configurato la distribuzione continua, tutti le modifiche dei file nell'origine della distribuzione vengono copiate nell'app per le funzioni e viene attivata una distribuzione completa del sito.</span><span class="sxs-lookup"><span data-stu-id="fb19d-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="fb19d-133">Il sito viene ridistribuito quando vengono aggiornati i file nell'origine.</span><span class="sxs-lookup"><span data-stu-id="fb19d-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="fb19d-134">Opzioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="fb19d-134">Deployment options</span></span>

<span data-ttu-id="fb19d-135">Di seguito sono indicati alcuni scenari di distribuzione tipici:</span><span class="sxs-lookup"><span data-stu-id="fb19d-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="fb19d-136">Creare una distribuzione di staging</span><span class="sxs-lookup"><span data-stu-id="fb19d-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="fb19d-137">Trasferire le funzioni esistenti nella distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="fb19d-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="fb19d-138">Creare una distribuzione di staging</span><span class="sxs-lookup"><span data-stu-id="fb19d-138">Create a staging deployment</span></span>

<span data-ttu-id="fb19d-139">Le app per le funzioni non supportano ancora slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fb19d-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="fb19d-140">È comunque possibile gestire distribuzioni di staging e di produzione separate tramite l'integrazione continua.</span><span class="sxs-lookup"><span data-stu-id="fb19d-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="fb19d-141">Il processo per la configurazione e l'uso di una distribuzione di staging è in genere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fb19d-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="fb19d-142">Creare due app per le funzioni nella sottoscrizione, una per il codice di produzione e una per lo staging.</span><span class="sxs-lookup"><span data-stu-id="fb19d-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="fb19d-143">Creare un'origine della distribuzione, se non è già presente.</span><span class="sxs-lookup"><span data-stu-id="fb19d-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="fb19d-144">Questo esempio usa [GitHub].</span><span class="sxs-lookup"><span data-stu-id="fb19d-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="fb19d-145">Per l'app per le funzioni di produzione, eseguire i passaggi illustrati sopra in **Configurare la distribuzione continua** e impostare il ramo di distribuzione sul ramo master dell'archivio GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb19d-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Scegliere il ramo della distribuzione](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="fb19d-147">Ripetere questo passaggio per l'app per le funzioni di staging, ma scegliere il ramo di staging nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb19d-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="fb19d-148">Se l'origine della distribuzione non supporta le diramazioni, usare una cartella diversa.</span><span class="sxs-lookup"><span data-stu-id="fb19d-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="fb19d-149">Apportare aggiornamenti al codice nel ramo o nella cartella di staging, quindi verificare che le modifiche vengono apportate nella distribuzione di staging.</span><span class="sxs-lookup"><span data-stu-id="fb19d-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="fb19d-150">Dopo i test, unire le modifiche dal ramo di staging nel ramo master.</span><span class="sxs-lookup"><span data-stu-id="fb19d-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="fb19d-151">Questa unione attiva la distribuzione nell'app per le funzioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="fb19d-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="fb19d-152">Se l'origine della distribuzione non supporta i rami, sovrascrivere i file nella cartella di produzione con i file dalla cartella di staging.</span><span class="sxs-lookup"><span data-stu-id="fb19d-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="fb19d-153">Trasferire le funzioni esistenti nella distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="fb19d-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="fb19d-154">Quando si hanno funzioni esistenti che sono state create e gestite nel portale, è necessario scaricare i file del codice di funzione esistenti tramite FTP o il repository Git locale prima di configurare la distribuzione continua come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fb19d-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="fb19d-155">Questa operazione può essere eseguita nelle impostazioni del servizio app dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="fb19d-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="fb19d-156">Dopo aver scaricato i file, è possibile caricarli nell'origine scelta per la distribuzione continua.</span><span class="sxs-lookup"><span data-stu-id="fb19d-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="fb19d-157">Dopo aver configurato l'integrazione continua, non sarà più possibile modificare i file di origine nel portale di Funzioni.</span><span class="sxs-lookup"><span data-stu-id="fb19d-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="fb19d-158">Procedura: Configurare le credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="fb19d-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="fb19d-159">Procedura: Scaricare i file con FTP</span><span class="sxs-lookup"><span data-stu-id="fb19d-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="fb19d-160">Procedura: scaricare file tramite l'archivio GIT locale</span><span class="sxs-lookup"><span data-stu-id="fb19d-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="fb19d-161">Procedura: Configurare le credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="fb19d-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="fb19d-162">Prima di poter scaricare i file dall'app per le funzioni con FTP o l'archivio GIT locale, è necessario configurare le credenziali per accedere al sito.</span><span class="sxs-lookup"><span data-stu-id="fb19d-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="fb19d-163">Le credenziali vengono impostate a livello di app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="fb19d-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="fb19d-164">Usare la procedura seguente per impostare le credenziali di distribuzione nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="fb19d-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="fb19d-165">Nell'app per le funzioni nel [portale di Azure](https://portal.azure.com) fare clic su **Funzionalità della piattaforma** e **Credenziali distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Impostare le credenziali di distribuzione locali](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="fb19d-167">Immettere un nome utente e una password, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="fb19d-168">È ora possibile usare queste credenziali per accedere all'app per le funzioni da FTP o dal repository Git predefinito.</span><span class="sxs-lookup"><span data-stu-id="fb19d-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="fb19d-169">Procedura: Scaricare i file tramite FTP</span><span class="sxs-lookup"><span data-stu-id="fb19d-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="fb19d-170">Nell'app per le funzioni nel [portale di Azure](https://portal.azure.com) fare clic su **Funzionalità della piattaforma** e su **Proprietà**, quindi copiare i valori di **Utente FTP/distribuzione**, **Nome host FTP** e **Nome host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="fb19d-171">**Utente FTP/distribuzione** deve essere immesso come visualizzato nel portale, includendo il nome dell'app, per rendere disponibile un contesto appropriato per il server FTP.</span><span class="sxs-lookup"><span data-stu-id="fb19d-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Ottenere le informazioni di distribuzione](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="fb19d-173">Dal client FTP, usare le informazioni di connessione raccolte per connettersi all'app e scaricare i file di origine per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="fb19d-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="fb19d-174">Procedura: scaricare file tramite l'archivio GIT locale</span><span class="sxs-lookup"><span data-stu-id="fb19d-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="fb19d-175">Nell'app per le funzioni nel [portale di Azure](https://portal.azure.com) fare clic su **Funzionalità della piattaforma** e **Opzioni di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="fb19d-177">Quindi, nel pannello **Distribuzione** fare clic su **Installazione**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="fb19d-179">Nel pannello **Origine distribuzione** fare clic su **Archivio Git locale** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb19d-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="fb19d-180">In **Funzionalità della piattaforma** fare clic su **Proprietà** e prendere nota del valore dell'URL GIT.</span><span class="sxs-lookup"><span data-stu-id="fb19d-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Configurare la distribuzione continua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="fb19d-182">Clonare l'archivio nel computer locale tramite il prompt dei comandi compatibile con GIT o con lo strumento GIT preferito.</span><span class="sxs-lookup"><span data-stu-id="fb19d-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="fb19d-183">Il comando clone GIT è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fb19d-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="fb19d-184">Recuperare i file dell'app per le funzioni nel clone nel computer locale, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="fb19d-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="fb19d-185">Se richiesto inserire le [credenziali di distribuzione configurate](#credentials).</span><span class="sxs-lookup"><span data-stu-id="fb19d-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="fb19d-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="fb19d-186">[GitHub]: https://github.com/</span></span>
