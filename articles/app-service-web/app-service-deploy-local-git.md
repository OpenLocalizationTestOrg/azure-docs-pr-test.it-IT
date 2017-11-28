---
title: aaaLocal distribuzione Git tooAzure servizio App
description: Informazioni su come tooenable locale Git distribuzione tooAzure servizio App.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="868d6-103">TooAzure distribuzione Git locale del servizio App</span><span class="sxs-lookup"><span data-stu-id="868d6-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="868d6-104">In questa esercitazione illustra come toodeploy app troppo[Azure App Service] da un archivio Git nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="868d6-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="868d6-105">Servizio App supporta questo approccio con hello **Git locale** opzione di distribuzione in hello [portale Azure].</span><span class="sxs-lookup"><span data-stu-id="868d6-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="868d6-106">Molti dei comandi Git hello descritti in questo articolo vengono eseguite automaticamente durante la creazione di un'applicazione di servizio App utilizzando hello [interfaccia della riga di comando di Azure] come descritto [qui](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="868d6-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="868d6-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="868d6-107">Prerequisites</span></span>
<span data-ttu-id="868d6-108">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="868d6-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="868d6-109">Git.</span><span class="sxs-lookup"><span data-stu-id="868d6-109">Git.</span></span> <span data-ttu-id="868d6-110">È possibile scaricare installazione hello binario [qui](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="868d6-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="868d6-111">Conoscenze di base di Git.</span><span class="sxs-lookup"><span data-stu-id="868d6-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="868d6-112">Un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="868d6-112">A Microsoft Azure account.</span></span> <span data-ttu-id="868d6-113">Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="868d6-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="868d6-114">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="868d6-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="868d6-115">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="868d6-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="868d6-116"><a name="Step1"></a>Passaggio 1: Creare un repository locale</span><span class="sxs-lookup"><span data-stu-id="868d6-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="868d6-117">Eseguire hello seguenti attività toocreate un nuovo repository Git.</span><span class="sxs-lookup"><span data-stu-id="868d6-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="868d6-118">Avviare uno strumento da riga di comando, ad esempio **GitBash** (Windows) o **Bash** (shell Unix).</span><span class="sxs-lookup"><span data-stu-id="868d6-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="868d6-119">Nei sistemi di OS X è possibile accedere hello della riga di comando tramite hello **Terminal** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="868d6-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="868d6-120">Passare toohello directory in cui deve essere collocato toodeploy contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="868d6-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="868d6-121">Utilizzare hello comando tooinitialize un nuovo repository Git di seguito:</span><span class="sxs-lookup"><span data-stu-id="868d6-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="868d6-122"><a name="Step2"></a>Passaggio 2: Eseguire il commit del contenuto</span><span class="sxs-lookup"><span data-stu-id="868d6-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="868d6-123">Il servizio app supporta applicazioni create in diversi linguaggi di programmazione.</span><span class="sxs-lookup"><span data-stu-id="868d6-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="868d6-124">Se il repository include già contenuto ignorare questo punto e spostare toopoint 2 di seguito.</span><span class="sxs-lookup"><span data-stu-id="868d6-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="868d6-125">Se non include ancora il contenuto, popolare il repository con un file HTML statico come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="868d6-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="868d6-126">Utilizzando un editor di testo, creare un nuovo file denominato **index.html** nella radice di hello del repository Git hello</span><span class="sxs-lookup"><span data-stu-id="868d6-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="868d6-127">Aggiungere hello dopo il testo contenuto hello per index.html hello del file e salvarlo: *Git Hello!*</span><span class="sxs-lookup"><span data-stu-id="868d6-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="868d6-128">Da hello della riga di comando, verificare che nella directory radice di hello del repository Git.</span><span class="sxs-lookup"><span data-stu-id="868d6-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="868d6-129">Utilizzare quindi hello repository tooyour file tooadd di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="868d6-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="868d6-130">Successivamente, eseguire il commit del repository di hello modifiche toohello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="868d6-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="868d6-131"><a name="Step3"></a>Passaggio 3: Abilitare hello repository di applicazione di servizio App</span><span class="sxs-lookup"><span data-stu-id="868d6-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="868d6-132">Eseguire hello seguendo i passaggi tooenable un repository Git per l'applicazione di servizio App.</span><span class="sxs-lookup"><span data-stu-id="868d6-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="868d6-133">Accedi toohello [portale Azure].</span><span class="sxs-lookup"><span data-stu-id="868d6-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="868d6-134">Nel pannello dell'app del servizio app fare clic su **Impostazioni > Origine distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="868d6-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="868d6-135">Fare clic su **Scegliere l'origine**, quindi su **Repository Git locale** e infine su **OK**.</span><span class="sxs-lookup"><span data-stu-id="868d6-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Repository Git locale](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="868d6-137">Se questa è la prima impostazione del tempo di un archivio in Azure, è necessario toocreate le credenziali di accesso per tale.</span><span class="sxs-lookup"><span data-stu-id="868d6-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="868d6-138">Utilizzare li toolog in hello Azure repository e push delle modifiche dall'archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="868d6-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="868d6-139">Dal pannello dell'app fare clic su **Impostazioni > Credenziali per la distribuzione**, quindi configurare il nome utente e la password per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="868d6-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="868d6-140">Al termine, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="868d6-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="868d6-141"><a name="Step4"></a>Passaggio 4: Distribuire il progetto</span><span class="sxs-lookup"><span data-stu-id="868d6-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="868d6-142">Utilizzare hello seguendo i passaggi toopublish il tooApp app servizio tramite Git locale.</span><span class="sxs-lookup"><span data-stu-id="868d6-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="868d6-143">Nel pannello dell'app nel portale di Azure hello, fare clic su **Impostazioni > proprietà** per hello **URL Git**.</span><span class="sxs-lookup"><span data-stu-id="868d6-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="868d6-144">**URL GIT** è hello riferimento remoto toodeploy toofrom il repository locale.</span><span class="sxs-lookup"><span data-stu-id="868d6-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="868d6-145">Utilizzare questo URL in hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="868d6-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="868d6-146">Utilizzando hello della riga di comando, verificare che trovano nella radice di hello del repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="868d6-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="868d6-147">Utilizzare `git remote` riferimento remoto hello tooadd elencato in **URL Git** ottenuto al passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="868d6-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="868d6-148">Il comando avrà un aspetto simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="868d6-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="868d6-149">Hello **remoto** comando aggiunge un repository remoto tooa di riferimento con nome.</span><span class="sxs-lookup"><span data-stu-id="868d6-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="868d6-150">In questo esempio viene creato un riferimento denominato 'azure' per il repository dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="868d6-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="868d6-151">Eseguire il push del contenuto tooApp servizio utilizzando hello nuovo **azure** remoto appena creato.</span><span class="sxs-lookup"><span data-stu-id="868d6-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="868d6-152">Tornare tooyour app nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="868d6-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="868d6-153">Una voce di log il push più recente deve essere visualizzata in hello **distribuzioni** blade.</span><span class="sxs-lookup"><span data-stu-id="868d6-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="868d6-154">Fare clic su hello **Sfoglia** pulsante nella parte superiore di hello di hello di tooverify pannello hello dell'app contenuto è stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="868d6-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="868d6-155"><a name="Step5"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="868d6-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="868d6-156">di seguito Hello sono errori o problemi comunemente riscontrati durante l'uso di Git toopublish tooan app del servizio App in Azure:</span><span class="sxs-lookup"><span data-stu-id="868d6-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="868d6-157">**Sintomo**: Impossibile tooaccess [siteURL]: Impossibile troppo tooconnect [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="868d6-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="868d6-158">**Causa**: questo errore può verificarsi se l'applicazione hello non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="868d6-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="868d6-159">**Risoluzione**: inizio hello app nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="868d6-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="868d6-160">Distribuzione GIT non funzionerà a meno che non è in esecuzione app hello.</span><span class="sxs-lookup"><span data-stu-id="868d6-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="868d6-161">**Sintomo**: non è possibile risolvere il nome dell'host 'nomehost'.</span><span class="sxs-lookup"><span data-stu-id="868d6-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="868d6-162">**Causa**: questo errore può verificarsi se le informazioni sull'indirizzo hello immessi durante la creazione di hello 'azure' remoto non è corretta.</span><span class="sxs-lookup"><span data-stu-id="868d6-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="868d6-163">**Risoluzione**: hello utilizzare `git remote -v` comando toolist tutti i componenti remoti, insieme a URL hello associata.</span><span class="sxs-lookup"><span data-stu-id="868d6-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="868d6-164">Verificare che l'URL di hello per hello 'azure' remoto sia corretto.</span><span class="sxs-lookup"><span data-stu-id="868d6-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="868d6-165">Se necessario, rimuovere e ricreare questo remoto hello URL sia corretto.</span><span class="sxs-lookup"><span data-stu-id="868d6-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="868d6-166">**Sintomo**: non sono stati trovati riferimenti in comune e non ne sono stati specificati. Non viene eseguita alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="868d6-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="868d6-167">Forse è necessario specificare un ramo, ad esempio 'master'.</span><span class="sxs-lookup"><span data-stu-id="868d6-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="868d6-168">**Causa**: questo errore può verificarsi se non si specifica un ramo, quando si esegue un'operazione di push git e non set hello push.default valore utilizzato da Git.</span><span class="sxs-lookup"><span data-stu-id="868d6-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="868d6-169">**Risoluzione**: operazione hello push nuovamente specificando ramo master hello.</span><span class="sxs-lookup"><span data-stu-id="868d6-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="868d6-170">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="868d6-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="868d6-171">**Sintomo**: non sono state trovate corrispondenze per src refspec [nomeramo].</span><span class="sxs-lookup"><span data-stu-id="868d6-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="868d6-172">**Causa**: questo errore può verificarsi se si tenta di ramo tooa toopush diverso da quello master in hello 'azure' remoto.</span><span class="sxs-lookup"><span data-stu-id="868d6-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="868d6-173">**Risoluzione**: operazione hello push nuovamente specificando ramo master hello.</span><span class="sxs-lookup"><span data-stu-id="868d6-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="868d6-174">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="868d6-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="868d6-175">**Sintomo**: RPC non riuscita; risultato = 22, codice HTTP = 502.</span><span class="sxs-lookup"><span data-stu-id="868d6-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="868d6-176">**Causa**: questo errore può verificarsi se si tenta di toopush un repository git di grandi dimensioni tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="868d6-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="868d6-177">**Risoluzione**: modificare la configurazione di git hello in più grande successivo hello toomake macchina locale hello</span><span class="sxs-lookup"><span data-stu-id="868d6-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="868d6-178">**Sintomo**: errore - repository tooremote eseguito il commit di modifiche ma l'app web non è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="868d6-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="868d6-179">**Causa**: questo errore può verificarsi se si distribuisce un'app Node.js contenente un file package.json che specifica altri moduli necessari.</span><span class="sxs-lookup"><span data-stu-id="868d6-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="868d6-180">**Risoluzione**: i messaggi aggiuntivi contenenti 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="868d6-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="868d6-181">deve essere connesso toothis precedente errore e può fornire contesto aggiuntivo in caso di errore hello.</span><span class="sxs-lookup"><span data-stu-id="868d6-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="868d6-182">esempio Hello è note le cause di questo errore e hello corrispondente 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="868d6-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="868d6-183">messaggio:</span><span class="sxs-lookup"><span data-stu-id="868d6-183">message:</span></span>

* <span data-ttu-id="868d6-184">**File package.json in formato non corretto**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="868d6-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="868d6-185">Non è stato possibile leggere le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="868d6-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="868d6-186">**Modulo nativo senza una distribuzione binaria per Windows**:</span><span class="sxs-lookup"><span data-stu-id="868d6-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="868d6-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="868d6-187">npm ERR!</span></span> <span data-ttu-id="868d6-188">Si è verificato un errore di \`cmd "/c" "node-gyp rebuild"\` con 1</span><span class="sxs-lookup"><span data-stu-id="868d6-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="868d6-189">OPPURE</span><span class="sxs-lookup"><span data-stu-id="868d6-189">OR</span></span>
  * <span data-ttu-id="868d6-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="868d6-190">npm ERR!</span></span> <span data-ttu-id="868d6-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="868d6-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="868d6-192">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="868d6-192">Additional Resources</span></span>
* [<span data-ttu-id="868d6-193">Documentazione su Git</span><span class="sxs-lookup"><span data-stu-id="868d6-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="868d6-194">Documentazione del progetto Kudu</span><span class="sxs-lookup"><span data-stu-id="868d6-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="868d6-195">La distribuzione continua tooAzure servizio App</span><span class="sxs-lookup"><span data-stu-id="868d6-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="868d6-196">Come toouse PowerShell per Azure</span><span class="sxs-lookup"><span data-stu-id="868d6-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="868d6-197">Come toouse hello interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="868d6-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[portale Azure]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[interfaccia della riga di comando di Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
