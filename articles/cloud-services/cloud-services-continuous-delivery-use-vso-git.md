---
title: Recapito continuo con Git e Visual Studio Team Services in Azure | Documentazione Microsoft
description: "Informazioni sulla configurazione dei progetti team di Visual Studio Team Services per usare Git per la compilazione e la distribuzione automatiche alla funzionalità App Web nel Servizio app di Azure o nei servizi cloud."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="47752-103">Recapito continuo in Azure tramite Visual Studio Team Services e Git</span><span class="sxs-lookup"><span data-stu-id="47752-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="47752-104">È possibile usare i progetti team di Visual Studio Team Services per ospitare un repository Git per il codice sorgente e compilarlo e distribuirlo automaticamente nelle app Web o nei servizi cloud di Azure quando si effettua il push di un commit nel repository.</span><span class="sxs-lookup"><span data-stu-id="47752-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="47752-105">È necessario che siano installati Visual Studio 2013 e Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="47752-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="47752-106">Se non si dispone ancora di Visual Studio 2013, scaricarlo scegliendo il collegamento **Inizia gratuitamente** all'indirizzo [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="47752-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="47752-107">Installare Azure SDK da [questa pagina](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="47752-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="47752-108">Per completare l'esercitazione, è necessario un account di Visual Studio Team Services: è possibile [aprire un account di Visual Studio Team Services gratuitamente](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="47752-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="47752-109">Per configurare un servizio cloud da compilare e distribuire automaticamente in Azure tramite Visual Studio Team Services, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="47752-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="47752-110">1: Creare un repository Git</span><span class="sxs-lookup"><span data-stu-id="47752-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="47752-111">Se non si ha già un account Visual Studio Team Services, è possibile ottenerne uno [qui](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="47752-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="47752-112">Quando si crea il progetto team, scegliere Git come sistema di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="47752-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="47752-113">Seguire le istruzioni per collegare Visual Studio al progetto team.</span><span class="sxs-lookup"><span data-stu-id="47752-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="47752-114">In **Team Explorer** fare clic sul collegamento **Clona questo repository**.</span><span class="sxs-lookup"><span data-stu-id="47752-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="47752-115">Specificare il percorso della copia locale e quindi scegliere il pulsante **Clona** .</span><span class="sxs-lookup"><span data-stu-id="47752-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="47752-116">2: Creare un progetto ed eseguirne il commit nel repository</span><span class="sxs-lookup"><span data-stu-id="47752-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="47752-117">Nella sezione **Soluzioni** di **Team Explorer** scegliere il collegamento **Nuovo** per creare un nuovo progetto nel repository locale.</span><span class="sxs-lookup"><span data-stu-id="47752-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="47752-118">È possibile distribuire un’app Web o un servizio cloud (applicazione Azure) seguendo i passaggi di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="47752-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="47752-119">Creare un nuovo progetto servizio cloud di Azure o un nuovo progetto ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="47752-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="47752-120">Assicurarsi che il progetto sia per .NET Framework 4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="47752-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="47752-121">Se si crea un progetto di servizio cloud, aggiungere un ruolo Web ASP.NET MVC e un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="47752-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="47752-122">Per creare un'app Web, scegliere il modello di progetto **Applicazione Web ASP.NET** e quindi **MVC**.</span><span class="sxs-lookup"><span data-stu-id="47752-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="47752-123">Per altre informazioni, vedere [Creare un'app Web ASP.NET in Servizio app di Azure](../app-service-web/app-service-web-get-started-dotnet.md) .</span><span class="sxs-lookup"><span data-stu-id="47752-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="47752-124">Aprire il menu di scelta rapida relativo alla soluzione e scegliere **Commit**.</span><span class="sxs-lookup"><span data-stu-id="47752-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="47752-125">Se è la prima volta che si usa Git in Visual Studio Team Services, sarà necessario fornire alcune informazioni per identificarsi in Git.</span><span class="sxs-lookup"><span data-stu-id="47752-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="47752-126">Nell'area **Modifiche in sospeso** di **Team Explorer** immettere il proprio nome utente e indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="47752-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="47752-127">Immettere un commento per il commit e quindi scegliere il pulsante **Commit** .</span><span class="sxs-lookup"><span data-stu-id="47752-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="47752-128">Notare le opzioni per includere o escludere modifiche specifiche quando si esegue l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="47752-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="47752-129">Se le modifiche desiderate sono escluse, scegliere **Includi tutto**.</span><span class="sxs-lookup"><span data-stu-id="47752-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="47752-130">È stato eseguito il commit delle modifiche nella copia locale del repository.</span><span class="sxs-lookup"><span data-stu-id="47752-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="47752-131">A questo punto, sincronizzare le modifiche con il server scegliendo il collegamento **Sincronizza** .</span><span class="sxs-lookup"><span data-stu-id="47752-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="47752-132">3: Collegare il progetto ad Azure</span><span class="sxs-lookup"><span data-stu-id="47752-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="47752-133">Ora si dispone di un repository Git in Visual Studio Team Services contenente codice sorgente ed è possibile connettere il repository ad Azure.</span><span class="sxs-lookup"><span data-stu-id="47752-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="47752-134">Nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885) selezionare il servizio cloud o l'app Web oppure crearne uno nuovo selezionando l'icona + in basso a sinistra e scegliendo **Servizio cloud** o **App Web** e quindi **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="47752-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="47752-135">Per i servizi cloud, scegliere il collegamento **Imposta pubblicazione con Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="47752-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="47752-136">Per le app Web scegliere il collegamento **Imposta distribuzione dal controllo del codice sorgente** .</span><span class="sxs-lookup"><span data-stu-id="47752-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="47752-137">Nella procedura guidata digitare il nome del proprio account di Visual Studio Team Services nella casella di testo e fare clic sul collegamento **Autorizza ora** .</span><span class="sxs-lookup"><span data-stu-id="47752-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="47752-138">È possibile che venga richiesto di effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="47752-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="47752-139">Nella finestra di dialogo popup **Connection Request** (Richiesta di connessione) scegliere **Accetta** per autorizzare Azure a configurare il progetto team in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="47752-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="47752-140">Dopo aver concesso l'autorizzazione verrà visualizzato un elenco a discesa contenente un elenco dei progetti team di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="47752-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="47752-141">Selezionare il nome del progetto team creato nei passaggi precedenti e fare clic sul pulsante con il segno di spunta della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="47752-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="47752-142">Quando si effettuerà di nuovo il push di un commit al repository, Visual Studio Team Services compilerà e distribuirà il progetto in Azure.</span><span class="sxs-lookup"><span data-stu-id="47752-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="47752-143">4: Attivare una ricompilazione e ridistribuire il progetto</span><span class="sxs-lookup"><span data-stu-id="47752-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="47752-144">In Visual Studio aprire un file e modificarlo.</span><span class="sxs-lookup"><span data-stu-id="47752-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="47752-145">Modificare ad esempio il file `_Layout.cshtml` nella cartella Views\\Shared in un ruolo Web MVC.</span><span class="sxs-lookup"><span data-stu-id="47752-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="47752-146">Modificare il testo del piè di pagina per il sito e salvare il file.</span><span class="sxs-lookup"><span data-stu-id="47752-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="47752-147">In **Esplora soluzioni** aprire il menu di scelta rapida relativo al nodo della soluzione, al nodo del progetto o al file modificato e quindi scegliere **Commit**.</span><span class="sxs-lookup"><span data-stu-id="47752-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="47752-148">Digitare un commento e scegliere **Commit**.</span><span class="sxs-lookup"><span data-stu-id="47752-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="47752-149">Scegliere il collegamento **Sincronizza** .</span><span class="sxs-lookup"><span data-stu-id="47752-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="47752-150">Scegliere il collegamento **Push** per effettuare il push del commit al repository in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="47752-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="47752-151">È anche possibile usare il pulsante **Sincronizza** per copiare i commit nel repository.</span><span class="sxs-lookup"><span data-stu-id="47752-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="47752-152">La differenza sta nel fatto che **Sincronizza** effettua anche il pull delle ultime modifiche dal repository.</span><span class="sxs-lookup"><span data-stu-id="47752-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="47752-153">Scegliere il pulsante **Home** per tornare alla pagina iniziale di **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="47752-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="47752-154">Scegliere **Compilazioni** per visualizzare le compilazioni in corso.</span><span class="sxs-lookup"><span data-stu-id="47752-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="47752-155">**Team Explorer** mostra che è stata attivata una compilazione per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="47752-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="47752-156">Fare doppio clic sul nome della compilazione in corso per visualizzare un log dettagliato con l'avanzare della compilazione.</span><span class="sxs-lookup"><span data-stu-id="47752-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="47752-157">Quando la compilazione è in corso, osservare la definizione di compilazione creata quando la procedura guidata è stata usata per eseguire il collegamento ad Azure.</span><span class="sxs-lookup"><span data-stu-id="47752-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="47752-158">Aprire il menu di scelta rapida relativo alla definizione di compilazione e scegliere **Modifica definizione di compilazione**.</span><span class="sxs-lookup"><span data-stu-id="47752-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="47752-159">Nella scheda **Trigger** è possibile osservare che, per impostazione predefinita, la definizione di compilazione è impostata per la compilazione a ogni archiviazione.</span><span class="sxs-lookup"><span data-stu-id="47752-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="47752-160">Per un servizio cloud, Visual Studio Team Services compila e distribuisce automaticamente il branch master nell'ambiente di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="47752-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="47752-161">È comunque necessario eseguire un'operazione manuale per distribuire il branch master nel sito attivo.</span><span class="sxs-lookup"><span data-stu-id="47752-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="47752-162">Per un'app Web senza un ambiente di gestione temporanea, il branch master viene distribuito direttamente nel sito attivo.</span><span class="sxs-lookup"><span data-stu-id="47752-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="47752-163">Nella scheda **Processo** è possibile osservare che l'ambiente di distribuzione è configurato con il nome del proprio servizio cloud o dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="47752-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="47752-164">Specificare i valori per le proprietà se si desidera che siano diversi da quelli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="47752-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="47752-165">Le proprietà per la pubblicazione in Azure si trovano nella sezione **Distribuzione** e potrebbe anche essere necessario impostare i parametri MSBuild.</span><span class="sxs-lookup"><span data-stu-id="47752-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="47752-166">In un progetto di servizio cloud, ad esempio, per specificare una configurazione del servizio diversa da "Cloud", impostare i parametri MSbuild su `/p:TargetProfile=[YourProfile]`, dove *[YourProfile]* corrisponde a un file di configurazione del servizio con un nome simile a ServiceConfiguration.*ProfiloPersonale*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="47752-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="47752-167">La tabella seguente illustra le proprietà disponibili nella sezione **Distribuzione** :</span><span class="sxs-lookup"><span data-stu-id="47752-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="47752-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="47752-168">Property</span></span> | <span data-ttu-id="47752-169">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="47752-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="47752-170">Consenti certificati non attendibili</span><span class="sxs-lookup"><span data-stu-id="47752-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="47752-171">Se è false, i certificati SSL devono essere firmati da un'autorità radice.</span><span class="sxs-lookup"><span data-stu-id="47752-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="47752-172">Consenti aggiornamento</span><span class="sxs-lookup"><span data-stu-id="47752-172">Allow Upgrade</span></span> |<span data-ttu-id="47752-173">Consente l'aggiornamento di una distribuzione esistente anziché crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="47752-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="47752-174">Conserva l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="47752-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="47752-175">Non eliminare</span><span class="sxs-lookup"><span data-stu-id="47752-175">Do Not Delete</span></span> |<span data-ttu-id="47752-176">Se è true, una distribuzione non correlata esistente non viene sovrascritta (l'aggiornamento è consentito).</span><span class="sxs-lookup"><span data-stu-id="47752-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="47752-177">Percorso impostazioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="47752-177">Path to Deployment Settings</span></span> |<span data-ttu-id="47752-178">Percorso del file con estensione pubxml di un’app Web, relativo alla cartella radice del repository.</span><span class="sxs-lookup"><span data-stu-id="47752-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="47752-179">Viene ignorato per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="47752-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="47752-180">Ambiente di distribuzione SharePoint</span><span class="sxs-lookup"><span data-stu-id="47752-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="47752-181">Analogo al nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="47752-181">The same as the service name.</span></span> |
    | <span data-ttu-id="47752-182">Ambiente di distribuzione Azure</span><span class="sxs-lookup"><span data-stu-id="47752-182">Azure Deployment Environment</span></span> |<span data-ttu-id="47752-183">Nome dell'app Web o del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="47752-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="47752-184">A questo punto la compilazione sarà stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="47752-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="47752-185">Facendo doppio clic sul nome della compilazione, Visual Studio visualizza un **Riepilogo compilazione**che include eventuali risultati del test restituiti dai progetti unit test associati.</span><span class="sxs-lookup"><span data-stu-id="47752-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="47752-186">Nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885)è possibile visualizzare la distribuzione associata nella scheda **Distribuzioni** quando si seleziona l'ambiente di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="47752-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="47752-187">Passare all'URL del proprio sito.</span><span class="sxs-lookup"><span data-stu-id="47752-187">Browse to your site's URL.</span></span> <span data-ttu-id="47752-188">Per un'app Web, scegliere semplicemente il pulsante **Esplora** nel portale.</span><span class="sxs-lookup"><span data-stu-id="47752-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="47752-189">Per un servizio cloud, scegliere l'URL nella sezione **Riepilogo rapido** della pagina **Dashboard** in cui è visualizzato l'ambiente di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="47752-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="47752-190">Le distribuzioni derivanti dall'integrazione continua per i servizi cloud vengono pubblicate nell'ambiente di gestione temporanea per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="47752-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="47752-191">È possibile modificare questa impostazione configurando la proprietà **Ambiente del servizio cloud alternativo** su **Produzione**.</span><span class="sxs-lookup"><span data-stu-id="47752-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="47752-192">Ecco dove si trova l'URL del sito nella pagina del dashboard del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="47752-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="47752-193">Il sito in esecuzione verrà aperto in una nuova scheda del browser.</span><span class="sxs-lookup"><span data-stu-id="47752-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="47752-194">Se si apportano altre modifiche al progetto, si attiveranno altre compilazioni e si accumuleranno più distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="47752-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="47752-195">L'ultima è contrassegnata come Attiva.</span><span class="sxs-lookup"><span data-stu-id="47752-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="47752-196">5: Ridistribuire una compilazione precedente</span><span class="sxs-lookup"><span data-stu-id="47752-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="47752-197">Questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="47752-197">This step is optional.</span></span> <span data-ttu-id="47752-198">Nel portale di Azure classico, selezionare una distribuzione precedente e fare clic sul pulsante **Ridistribuisci** per riportare il sito a un'archiviazione precedente.</span><span class="sxs-lookup"><span data-stu-id="47752-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="47752-199">Si noti che verrà attivata una nuova compilazione in TFS e verrà creata una nuova voce nella cronologia della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="47752-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="47752-200">6: Modificare la distribuzione di produzione</span><span class="sxs-lookup"><span data-stu-id="47752-200">6: Change the Production deployment</span></span>
<span data-ttu-id="47752-201">Quando si è pronti, è possibile alzare di livello l'ambiente di gestione temporanea all'ambiente di produzione scegliendo **Scambia** nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="47752-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="47752-202">L'ambiente di gestione temporanea appena distribuito verrà promosso alla produzione e il precedente ambiente di produzione (se presente) diventerà un ambiente di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="47752-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="47752-203">La distribuzione attiva potrebbe differire per gli ambienti di produzione e di gestione temporanea, ma la cronologia di distribuzione delle compilazioni recenti è la stessa indipendentemente dall'ambiente.</span><span class="sxs-lookup"><span data-stu-id="47752-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="47752-204">7: Eseguire la distribuzione da un ramo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="47752-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="47752-205">Quando si usa Git, in genere si apportano modifiche in un branch di lavoro che vengono integrate nel branch master quando lo sviluppo è terminato.</span><span class="sxs-lookup"><span data-stu-id="47752-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="47752-206">Durante la fase di sviluppo di un progetto, è consigliabile compilare e distribuire il branch di lavoro in Azure.</span><span class="sxs-lookup"><span data-stu-id="47752-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="47752-207">In **Team Explorer** scegliere il pulsante **Home** e quindi il pulsante **Rami**.</span><span class="sxs-lookup"><span data-stu-id="47752-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="47752-208">Scegliere il collegamento **Nuovo branch** .</span><span class="sxs-lookup"><span data-stu-id="47752-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="47752-209">Digitare il nome del branch, ad esempio "working", e scegliere **Crea branch**.</span><span class="sxs-lookup"><span data-stu-id="47752-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="47752-210">Verrà creato un nuovo branch locale.</span><span class="sxs-lookup"><span data-stu-id="47752-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="47752-211">Pubblicare il branch.</span><span class="sxs-lookup"><span data-stu-id="47752-211">Publish the branch.</span></span> <span data-ttu-id="47752-212">Scegliere il nome del ramo in **Rami non pubblicati** e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="47752-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="47752-213">Per impostazione predefinita, solo le modifiche al branch master attivano una compilazione continua.</span><span class="sxs-lookup"><span data-stu-id="47752-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="47752-214">Per configurare una compilazione continua per un ramo di lavoro, scegliere la pagina **Compilazioni** in **Team Explorer** e quindi **Modifica definizione di compilazione**.</span><span class="sxs-lookup"><span data-stu-id="47752-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="47752-215">Aprire la scheda **Impostazioni di origine** .</span><span class="sxs-lookup"><span data-stu-id="47752-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="47752-216">In **Rami monitorati per le compilazioni a integrazione continua e in corso** scegliere **Fare clic qui per aggiungere una nuova riga**.</span><span class="sxs-lookup"><span data-stu-id="47752-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="47752-217">Specificare il branch creato, ad esempio refs/heads/working.</span><span class="sxs-lookup"><span data-stu-id="47752-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="47752-218">Modificare il codice, aprire il menu di scelta rapida per il file modificato e scegliere **Commit**.</span><span class="sxs-lookup"><span data-stu-id="47752-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="47752-219">Scegliere il collegamento **Commit non sincronizzati** e quindi il pulsante **Sincronizzazione** o il collegamento **Push** per copiare le modifiche nella copia del ramo di lavoro in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="47752-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="47752-220">Passare alla visualizzazione **Compilazioni** e cercare la compilazione appena attivata per il branch di lavoro.</span><span class="sxs-lookup"><span data-stu-id="47752-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47752-221">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47752-221">Next steps</span></span>
<span data-ttu-id="47752-222">Per altri suggerimenti sull'uso di Git con Visual Studio Team Services, vedere l'articolo su come [sviluppare e condividere il codice con Git e Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017). Per informazioni sull'uso di un repository Git non gestito da Visual Studio Team Services per la pubblicazione in Azure, vedere [Distribuzione continua nel servizio app di Azure](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="47752-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="47752-223">Per altre informazioni su Visual Studio Team Services, vedere [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="47752-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
