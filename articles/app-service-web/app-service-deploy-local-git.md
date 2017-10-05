---
title: Distribuzione dell'archivio Git locale nel servizio app di Azure
description: Informazioni su come abilitare la distribuzione dell'archivio Git locale nel servizio app di Azure.
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
ms.openlocfilehash: f1c4911670d3aa32e74b3dfebd83cf3dc3830805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="fe376-103">Distribuzione dell'archivio Git locale nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="fe376-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="fe376-104">In questa esercitazione viene illustrato come distribuire l'applicazione nel [servizio app di Azure] da un repository Git nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="fe376-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="fe376-105">Il servizio app supporta questo approccio tramite l'opzione di distribuzione **Archivio Git locale** del [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="fe376-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="fe376-106">Molti comandi Git descritti in questo articolo vengono eseguiti automaticamente quando si crea un'app del servizio app usando l'[interfaccia della riga di comando di Azure] come descritto [qui](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fe376-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe376-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fe376-107">Prerequisites</span></span>
<span data-ttu-id="fe376-108">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="fe376-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="fe376-109">Git.</span><span class="sxs-lookup"><span data-stu-id="fe376-109">Git.</span></span> <span data-ttu-id="fe376-110">È possibile scaricare il file di installazione binario [qui](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="fe376-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="fe376-111">Conoscenze di base di Git.</span><span class="sxs-lookup"><span data-stu-id="fe376-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="fe376-112">Un account Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fe376-112">A Microsoft Azure account.</span></span> <span data-ttu-id="fe376-113">Se non si ha un account, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial) oppure [attivare i vantaggi per i sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="fe376-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="fe376-114">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="fe376-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="fe376-115">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="fe376-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="fe376-116"><a name="Step1"></a>Passaggio 1: Creare un repository locale</span><span class="sxs-lookup"><span data-stu-id="fe376-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="fe376-117">Per creare un nuovo repository Git, eseguire le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="fe376-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="fe376-118">Avviare uno strumento da riga di comando, ad esempio **GitBash** (Windows) o **Bash** (shell Unix).</span><span class="sxs-lookup"><span data-stu-id="fe376-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="fe376-119">Nei sistemi OS X è possibile accedere alla riga di comando tramite l'applicazione **Terminale** .</span><span class="sxs-lookup"><span data-stu-id="fe376-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="fe376-120">Passare alla directory in cui deve essere collocato il contenuto da distribuire.</span><span class="sxs-lookup"><span data-stu-id="fe376-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="fe376-121">Eseguire il comando seguente per inizializzare un nuovo repository Git:</span><span class="sxs-lookup"><span data-stu-id="fe376-121">Use the following command to initialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="fe376-122"><a name="Step2"></a>Passaggio 2: Eseguire il commit del contenuto</span><span class="sxs-lookup"><span data-stu-id="fe376-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="fe376-123">Il servizio app supporta applicazioni create in diversi linguaggi di programmazione.</span><span class="sxs-lookup"><span data-stu-id="fe376-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="fe376-124">Se il repository include già il contenuto ignorare questo passaggio e passare al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="fe376-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="fe376-125">Se non include ancora il contenuto, popolare il repository con un file HTML statico come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fe376-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="fe376-126">Usando un editor di testo creare un nuovo file denominato **index.html** nella radice del repository Git</span><span class="sxs-lookup"><span data-stu-id="fe376-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="fe376-127">Aggiungere il testo seguente come contenuto del file index.html e salvarlo: *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="fe376-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="fe376-128">Dalla riga di comando verificare che sia selezionata la radice del repository Git.</span><span class="sxs-lookup"><span data-stu-id="fe376-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="fe376-129">Usare quindi il comando seguente per aggiungere file al repository:</span><span class="sxs-lookup"><span data-stu-id="fe376-129">Then use the following command to add files to your repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="fe376-130">In seguito, eseguire il commit delle modifiche al repository con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fe376-130">Next, commit the changes to the repository by using the following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="fe376-131"><a name="Step3"></a>Passaggio 3: Abilitare il repository dell'app del servizio app</span><span class="sxs-lookup"><span data-stu-id="fe376-131"><a name="Step3"></a>Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="fe376-132">Eseguire la procedura seguente per abilitare un repository Git per l'app del servizio app.</span><span class="sxs-lookup"><span data-stu-id="fe376-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="fe376-133">Accedere al [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="fe376-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="fe376-134">Nel pannello dell'app del servizio app fare clic su **Impostazioni > Origine distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="fe376-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="fe376-135">Fare clic su **Scegliere l'origine**, quindi su **Repository Git locale** e infine su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe376-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Repository Git locale](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="fe376-137">Se si tratta della prima impostazione di un repository in Azure, è necessario creare le credenziali di accesso,</span><span class="sxs-lookup"><span data-stu-id="fe376-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="fe376-138">che verranno usate per accedere al repository di Azure e per effettuare il push delle modifiche dal repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="fe376-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="fe376-139">Dal pannello dell'app fare clic su **Impostazioni > Credenziali per la distribuzione**, quindi configurare il nome utente e la password per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fe376-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="fe376-140">Al termine, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fe376-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="fe376-141"><a name="Step4"></a>Passaggio 4: Distribuire il progetto</span><span class="sxs-lookup"><span data-stu-id="fe376-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="fe376-142">Eseguire la procedura seguente per pubblicare l'app nel servizio app usando l'archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="fe376-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="fe376-143">Nel pannello dell'app nel portale di Azure fare clic su **Impostazioni > Proprietà** per l'**URL GIT**.</span><span class="sxs-lookup"><span data-stu-id="fe376-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="fe376-144">**URL Git** è il riferimento remoto in cui eseguire la distribuzione dal repository locale.</span><span class="sxs-lookup"><span data-stu-id="fe376-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="fe376-145">Questo URL verrà utilizzato nella procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="fe376-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="fe376-146">Usando la riga di comando verificare che sia selezionata la radice del repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="fe376-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="fe376-147">Utilizzare `git remote` per aggiungere il riferimento remoto elencato in **URL Git** dal passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="fe376-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="fe376-148">Il comando sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fe376-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="fe376-149">Il comando **remote** consente di aggiungere un riferimento denominato a un repository remoto.</span><span class="sxs-lookup"><span data-stu-id="fe376-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="fe376-150">In questo esempio viene creato un riferimento denominato 'azure' per il repository dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="fe376-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="fe376-151">Effettuare il push del contenuto nel servizio app usando il nuovo riferimento remoto **azure** creato.</span><span class="sxs-lookup"><span data-stu-id="fe376-151">Push your content to App Service using the new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal. Enter the password (note that Gitbash does not echo asterisks to the console as you type your password). 
5. <span data-ttu-id="fe376-152">Tornare all'app nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe376-152">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="fe376-153">Nel pannello **Distribuzioni** verrà visualizzata una voce di log dell'ultimo push effettuato.</span><span class="sxs-lookup"><span data-stu-id="fe376-153">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="fe376-154">Fare clic sul pulsante **Sfoglia** nella parte superiore del pannello dell'app per verificare che il contenuto sia stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="fe376-154">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <span data-ttu-id="fe376-155"><a name="Step5"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="fe376-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="fe376-156">Di seguito sono riportati gli errori o i problemi che si verificano comunemente durante l'uso di Git per la pubblicazione in un'app del servizio app di Azure:</span><span class="sxs-lookup"><span data-stu-id="fe376-156">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="fe376-157">**Sintomo**: non è possibile accedere a '[siteURL]'. La connessione a [scmAddress] non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="fe376-157">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="fe376-158">**Causa**: questo errore può verificarsi se l'app non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fe376-158">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="fe376-159">**Soluzione**: avviare l'app nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe376-159">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="fe376-160">La distribuzione Git non funziona se l'app non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fe376-160">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="fe376-161">**Sintomo**: non è possibile risolvere il nome dell'host 'nomehost'.</span><span class="sxs-lookup"><span data-stu-id="fe376-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="fe376-162">**Causa**: questo errore può verificarsi se le informazioni sull'indirizzo immesse durante la creazione del repository remoto 'azure' non sono corrette.</span><span class="sxs-lookup"><span data-stu-id="fe376-162">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="fe376-163">**Soluzione**: usare il comando `git remote -v` per elencare tutti i repository remoti, insieme agli URL associati.</span><span class="sxs-lookup"><span data-stu-id="fe376-163">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="fe376-164">Verificare che l'URL del repository remoto 'azure' sia corretto.</span><span class="sxs-lookup"><span data-stu-id="fe376-164">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="fe376-165">Se necessario, rimuovere e ricreare questo repository remoto usando l'URL corretto.</span><span class="sxs-lookup"><span data-stu-id="fe376-165">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="fe376-166">**Sintomo**: non sono stati trovati riferimenti in comune e non ne sono stati specificati. Non viene eseguita alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="fe376-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="fe376-167">Forse è necessario specificare un ramo, ad esempio 'master'.</span><span class="sxs-lookup"><span data-stu-id="fe376-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="fe376-168">**Causa**: questo errore può verificarsi se non si specifica un ramo quando si effettua un'operazione push in Git e non è stato impostato il valore push.default usato da Git.</span><span class="sxs-lookup"><span data-stu-id="fe376-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="fe376-169">**Soluzione**: ripetere l'operazione push, specificando il ramo master.</span><span class="sxs-lookup"><span data-stu-id="fe376-169">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="fe376-170">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fe376-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="fe376-171">**Sintomo**: non sono state trovate corrispondenze per src refspec [nomeramo].</span><span class="sxs-lookup"><span data-stu-id="fe376-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="fe376-172">**Causa**: questo errore può verificarsi se si tenta di effettuare il push in un ramo diverso dal master nel repository remoto 'azure'.</span><span class="sxs-lookup"><span data-stu-id="fe376-172">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="fe376-173">**Soluzione**: ripetere l'operazione push, specificando il ramo master.</span><span class="sxs-lookup"><span data-stu-id="fe376-173">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="fe376-174">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fe376-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="fe376-175">**Sintomo**: RPC non riuscita; risultato = 22, codice HTTP = 502.</span><span class="sxs-lookup"><span data-stu-id="fe376-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="fe376-176">**Causa**: questo errore può verificarsi se si tenta di effettuare il push di un repository Git di grandi dimensioni tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fe376-176">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="fe376-177">**Soluzione**: modificare la configurazione Git nel computer locale per ingrandire il postBuffer</span><span class="sxs-lookup"><span data-stu-id="fe376-177">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="fe376-178">**Sintomo**: errore. Le modifiche vengono sottoposte a commit nel repository remoto ma l'app Web non viene aggiornata.</span><span class="sxs-lookup"><span data-stu-id="fe376-178">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="fe376-179">**Causa**: questo errore può verificarsi se si distribuisce un'app Node.js contenente un file package.json che specifica altri moduli necessari.</span><span class="sxs-lookup"><span data-stu-id="fe376-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="fe376-180">**Risoluzione**: i messaggi aggiuntivi contenenti 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="fe376-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="fe376-181">dovrebbero essere registrati prima di questo errore e possono fornire contesto aggiuntivo sul problema.</span><span class="sxs-lookup"><span data-stu-id="fe376-181">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="fe376-182">Di seguito sono riportate le cause note di questo errore e del corrispondente messaggio 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="fe376-182">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="fe376-183">messaggio:</span><span class="sxs-lookup"><span data-stu-id="fe376-183">message:</span></span>

* <span data-ttu-id="fe376-184">**File package.json in formato non corretto**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="fe376-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="fe376-185">Non è stato possibile leggere le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="fe376-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="fe376-186">**Modulo nativo senza una distribuzione binaria per Windows**:</span><span class="sxs-lookup"><span data-stu-id="fe376-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="fe376-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="fe376-187">npm ERR!</span></span> <span data-ttu-id="fe376-188">Si è verificato un errore di \`cmd "/c" "node-gyp rebuild"\` con 1</span><span class="sxs-lookup"><span data-stu-id="fe376-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="fe376-189">OPPURE</span><span class="sxs-lookup"><span data-stu-id="fe376-189">OR</span></span>
  * <span data-ttu-id="fe376-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="fe376-190">npm ERR!</span></span> <span data-ttu-id="fe376-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="fe376-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe376-192">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fe376-192">Additional Resources</span></span>
* [<span data-ttu-id="fe376-193">Documentazione su Git</span><span class="sxs-lookup"><span data-stu-id="fe376-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="fe376-194">Documentazione del progetto Kudu</span><span class="sxs-lookup"><span data-stu-id="fe376-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="fe376-195">Distribuzione continua nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="fe376-195">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="fe376-196">Come usare PowerShell per Azure</span><span class="sxs-lookup"><span data-stu-id="fe376-196">How to use PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="fe376-197">Come usare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fe376-197">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="fe376-198">[servizio app di Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="fe376-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span></span>
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
<span data-ttu-id="fe376-199">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="fe376-199">[Azure Portal]: https://portal.azure.com</span></span>
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="fe376-200">[interfaccia della riga di comando di Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span><span class="sxs-lookup"><span data-stu-id="fe376-200">[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span></span>

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
