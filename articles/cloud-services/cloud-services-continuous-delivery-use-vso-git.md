---
title: il recapito aaaContinuous con Git e di Visual Studio Team Services in Azure | Documenti Microsoft
description: "Informazioni su come tooconfigure il Visual Studio Team Services i progetti team toouse Git tooautomatically compilare e distribuire toohello funzionalità App Web di servizi cloud o di servizio App di Azure."
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
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="be1c1-103">TooAzure il recapito continuo con Visual Studio Team Services e Git</span><span class="sxs-lookup"><span data-stu-id="be1c1-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="be1c1-104">È possibile utilizzare toohost di progetti team di Visual Studio Team Services un repository Git per il codice sorgente e automaticamente generare e distribuire le app web tooAzure o servizi cloud, ogni volta che si esegue il push del repository toohello un commit.</span><span class="sxs-lookup"><span data-stu-id="be1c1-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="be1c1-105">È necessario Visual Studio 2013 e Azure SDK installata hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="be1c1-106">Se si dispone già di Visual Studio 2013, scaricarlo scegliendo hello **possibile iniziare gratuitamente** collegamento [www.visualstudio.com](http://www.visualstudio.com). Installazione hello Azure SDK da [qui](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="be1c1-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="be1c1-107">È necessario un toocomplete di account di Visual Studio Team Services in questa esercitazione: È possibile [aprire un account di Visual Studio Team Services gratuito](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="be1c1-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="be1c1-108">tooset backup un tooautomatically servizio cloud compilare e distribuire tooAzure utilizzando Visual Studio Team Services, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="be1c1-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="be1c1-109">1: Creare un repository Git</span><span class="sxs-lookup"><span data-stu-id="be1c1-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="be1c1-110">Se non si ha già un account Visual Studio Team Services, è possibile ottenerne uno [qui](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="be1c1-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="be1c1-111">Quando si crea il progetto team, scegliere Git come sistema di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="be1c1-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="be1c1-112">Eseguire il progetto di team tooyour hello istruzioni tooconnect Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be1c1-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="be1c1-113">In **Team Explorer**, scegliere hello **clonare questo repository** collegamento.</span><span class="sxs-lookup"><span data-stu-id="be1c1-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="be1c1-114">Specificare il percorso di hello della copia locale di hello e quindi scegliere hello **Clone** pulsante.</span><span class="sxs-lookup"><span data-stu-id="be1c1-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="be1c1-115">2: creare un progetto e di eseguirne il commit toohello repository</span><span class="sxs-lookup"><span data-stu-id="be1c1-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="be1c1-116">In **Team Explorer**, in hello **soluzioni** , scegliere hello **New** collegare un nuovo progetto nel repository locale hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="be1c1-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="be1c1-117">È possibile distribuire un'app web o un servizio cloud (applicazione di Azure) da hello seguente passaggi in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="be1c1-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="be1c1-118">Creare un nuovo progetto servizio cloud di Azure o un nuovo progetto ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="be1c1-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="be1c1-119">Verificare che le destinazioni progetto hello hello .NET Framework 4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="be1c1-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="be1c1-120">Se si crea un progetto di servizio cloud, aggiungere un ruolo Web ASP.NET MVC e un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="be1c1-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="be1c1-121">Se si desidera toocreate un'app web, scegliere hello **applicazione Web ASP.NET** modello di progetto e quindi scegliere **MVC**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="be1c1-122">Per altre informazioni, vedere [Creare un'app Web ASP.NET in Servizio app di Azure](../app-service-web/app-service-web-get-started-dotnet.md) .</span><span class="sxs-lookup"><span data-stu-id="be1c1-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="be1c1-123">Aprire il menu di scelta rapida hello per soluzione hello e scegliere **Commit**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="be1c1-124">Se si tratta di hello prima volta che si utilizza Git in Visual Studio Team Services, è necessario tooprovide tooidentify alcune informazioni manualmente in Git.</span><span class="sxs-lookup"><span data-stu-id="be1c1-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="be1c1-125">In hello **modifiche in sospeso** area di **Team Explorer**, immettere il nome utente e l'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="be1c1-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="be1c1-126">Immettere un commento per il commit di hello e quindi scegliere hello **Commit** pulsante.</span><span class="sxs-lookup"><span data-stu-id="be1c1-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="be1c1-127">Si noti hello opzioni tooinclude o escludere modifiche specifiche quando si archivia.</span><span class="sxs-lookup"><span data-stu-id="be1c1-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="be1c1-128">Se le modifiche hello desidera sono esclusi, scegliere **Includi tutto**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="be1c1-129">È stato ora eseguito il commit hello modifiche nella copia locale del repository hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="be1c1-130">Successivamente, sincronizzare le modifiche con server hello scegliendo hello **sincronizzazione** collegamento.</span><span class="sxs-lookup"><span data-stu-id="be1c1-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="be1c1-131">3: connettere hello progetto tooAzure</span><span class="sxs-lookup"><span data-stu-id="be1c1-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="be1c1-132">Dopo aver creato un repository Git in Visual Studio Team Services con un codice di origine in essa contenuti, si è pronti tooconnect il tooAzure repository git.</span><span class="sxs-lookup"><span data-stu-id="be1c1-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="be1c1-133">In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), selezionare l'applicazione web o servizio cloud o crearne uno nuovo facendo clic sull'icona in basso a sinistra di hello e scegliendo + hello **servizio Cloud** o **App Web**quindi **creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="be1c1-134">Per i servizi cloud, scegliere hello **impostare la pubblicazione con Visual Studio Team Services** collegamento.</span><span class="sxs-lookup"><span data-stu-id="be1c1-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="be1c1-135">Per le app web, scegliere hello **imposta distribuzione dal controllo del codice sorgente** collegamento.</span><span class="sxs-lookup"><span data-stu-id="be1c1-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="be1c1-136">Nella procedura guidata hello, digitare il nome di hello dell'account di Visual Studio Team Services nella casella di testo hello e scegliere hello **autorizzare ora** collegamento.</span><span class="sxs-lookup"><span data-stu-id="be1c1-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="be1c1-137">Potrebbe essere necessario toosign in.</span><span class="sxs-lookup"><span data-stu-id="be1c1-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="be1c1-138">In hello **richiesta di connessione** finestra di dialogo popup scegliere **Accept** tooauthorize tooconfigure Azure il progetto team in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="be1c1-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="be1c1-139">Dopo aver concesso l'autorizzazione verrà visualizzato un elenco a discesa contenente un elenco dei progetti team di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="be1c1-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="be1c1-140">Selezionare il nome del progetto team creato nei passaggi precedenti hello hello e scegliere il pulsante di segno di spunta della procedura guidata di hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="be1c1-141">Hello successivo che si inserisce un repository tooyour commit, Visual Studio Team Services verrà compilato e distribuito tooAzure il progetto.</span><span class="sxs-lookup"><span data-stu-id="be1c1-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="be1c1-142">4: Attivare una ricompilazione e ridistribuire il progetto</span><span class="sxs-lookup"><span data-stu-id="be1c1-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="be1c1-143">In Visual Studio aprire un file e modificarlo.</span><span class="sxs-lookup"><span data-stu-id="be1c1-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="be1c1-144">Ad esempio, modificare il file hello `_Layout.cshtml` in visualizzazioni hello\\cartella condivisa in un ruolo web MVC.</span><span class="sxs-lookup"><span data-stu-id="be1c1-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="be1c1-145">Modificare il testo del piè di pagina hello per il sito hello e salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="be1c1-146">In **Esplora**, aprire il menu di scelta rapida di hello per hello nodo della soluzione, il nodo di progetto o hello file modificato e quindi scegliere **Commit**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="be1c1-147">Digitare un commento e scegliere **Commit**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="be1c1-148">Scegliere hello **sincronizzazione** collegamento.</span><span class="sxs-lookup"><span data-stu-id="be1c1-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="be1c1-149">Scegliere hello **Push** collegamento toopush il repository toohello commit in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="be1c1-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="be1c1-150">(È anche possibile usare hello **sincronizzazione** pulsante toocopy il repository toohello commit.</span><span class="sxs-lookup"><span data-stu-id="be1c1-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="be1c1-151">Hello differenza è che **sincronizzazione** inoltre esegue il pull hello modifiche più recenti dal repository hello.)</span><span class="sxs-lookup"><span data-stu-id="be1c1-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="be1c1-152">Scegliere hello **Home** pulsante tooreturn toohello **Team Explorer** pagina iniziale.</span><span class="sxs-lookup"><span data-stu-id="be1c1-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="be1c1-153">Scegliere **compilazioni** tooview hello compilazioni in corso.</span><span class="sxs-lookup"><span data-stu-id="be1c1-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="be1c1-154">**Team Explorer** mostra che è stata attivata una compilazione per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="be1c1-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="be1c1-155">tooview un log dettagliato hello compilazione avanza, fare doppio clic sul nome hello di hello compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="be1c1-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="be1c1-156">Durante la compilazione hello è in corso, esaminare una definizione di compilazione hello creato quando si utilizza hello guidata toolink tooAzure.</span><span class="sxs-lookup"><span data-stu-id="be1c1-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="be1c1-157">Aprire il menu di scelta rapida hello hello la definizione di compilazione e scegliere **Modifica definizione di compilazione**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="be1c1-158">In hello **Trigger** scheda, si noterà che la definizione di compilazione hello è impostata toobuild su ogni archiviazione, per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="be1c1-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="be1c1-159">(Per un servizio cloud, Visual Studio Team Services compila e distribuisce hello ramo master toohello ambiente di gestione temporanea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="be1c1-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="be1c1-160">È comunque necessario toodo un sito di passaggio manuale toodeploy toohello in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="be1c1-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="be1c1-161">Per un'applicazione web che non ha l'ambiente di gestione temporanea, distribuisce ramo master hello direttamente toohello live del sito.</span><span class="sxs-lookup"><span data-stu-id="be1c1-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="be1c1-162">In hello **processo** scheda, è possibile vedere ambiente di distribuzione hello è impostato toohello nome dell'app web o servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="be1c1-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="be1c1-163">Se si desiderano valori diversi da quelli predefiniti hello, specificare i valori per le proprietà di hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="be1c1-164">salve le proprietà per la pubblicazione di Azure sono in hello **distribuzione** sezione e si potrebbero anche essere necessario tooset MSBuild parametri.</span><span class="sxs-lookup"><span data-stu-id="be1c1-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="be1c1-165">Ad esempio, in un progetto di servizio cloud, toospecify una configurazione del servizio diverso da "Cloud", impostare i parametri di MSbuild hello troppo`/p:TargetProfile=[YourProfile]` in *[YourProfile]* corrisponde a un file di configurazione del servizio con un nome come ServiceConfiguration. *YourProfile*. cscfg.</span><span class="sxs-lookup"><span data-stu-id="be1c1-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="be1c1-166">Hello nella tabella seguente mostra le proprietà disponibili hello in hello **distribuzione** sezione:</span><span class="sxs-lookup"><span data-stu-id="be1c1-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="be1c1-167">Proprietà</span><span class="sxs-lookup"><span data-stu-id="be1c1-167">Property</span></span> | <span data-ttu-id="be1c1-168">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="be1c1-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="be1c1-169">Consenti certificati non attendibili</span><span class="sxs-lookup"><span data-stu-id="be1c1-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="be1c1-170">Se è false, i certificati SSL devono essere firmati da un'autorità radice.</span><span class="sxs-lookup"><span data-stu-id="be1c1-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="be1c1-171">Consenti aggiornamento</span><span class="sxs-lookup"><span data-stu-id="be1c1-171">Allow Upgrade</span></span> |<span data-ttu-id="be1c1-172">Consente di hello distribuzione tooupdate una distribuzione esistente anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="be1c1-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="be1c1-173">Consente di mantenere l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="be1c1-174">Non eliminare</span><span class="sxs-lookup"><span data-stu-id="be1c1-174">Do Not Delete</span></span> |<span data-ttu-id="be1c1-175">Se è true, una distribuzione non correlata esistente non viene sovrascritta (l'aggiornamento è consentito).</span><span class="sxs-lookup"><span data-stu-id="be1c1-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="be1c1-176">Percorso tooDeployment impostazioni</span><span class="sxs-lookup"><span data-stu-id="be1c1-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="be1c1-177">Hello percorso tooyour pubxml file per un'app web, toohello relativo di cartella radice del repository hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="be1c1-178">Viene ignorato per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="be1c1-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="be1c1-179">Ambiente di distribuzione SharePoint</span><span class="sxs-lookup"><span data-stu-id="be1c1-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="be1c1-180">nome del servizio hello, Hello stesso.</span><span class="sxs-lookup"><span data-stu-id="be1c1-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="be1c1-181">Ambiente di distribuzione Azure</span><span class="sxs-lookup"><span data-stu-id="be1c1-181">Azure Deployment Environment</span></span> |<span data-ttu-id="be1c1-182">Hello app o cloud nome del servizio web.</span><span class="sxs-lookup"><span data-stu-id="be1c1-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="be1c1-183">A questo punto la compilazione sarà stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="be1c1-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="be1c1-184">Se si fa doppio clic sul nome di compilazione hello, Visual Studio visualizza un **Riepilogo compilazione**, compresi i risultati dei test da associati progetti di unit test.</span><span class="sxs-lookup"><span data-stu-id="be1c1-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="be1c1-185">In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), è possibile visualizzare la distribuzione di hello associata nella hello **distribuzioni** scheda quando viene selezionato l'ambiente di gestione temporanea hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="be1c1-186">Individuare l'URL del sito tooyour.</span><span class="sxs-lookup"><span data-stu-id="be1c1-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="be1c1-187">Per un'app web, è sufficiente scegliere hello **Sfoglia** pulsante nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="be1c1-188">Per un servizio cloud, scegliere URL hello in hello **Quick Glance** sezione di hello **Dashboard** pagina che mostra l'ambiente di gestione temporanea hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="be1c1-189">Le distribuzioni di integrazione continua per i servizi cloud sono pubblicati toohello ambiente di gestione temporanea per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="be1c1-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="be1c1-190">È possibile modificare questa impostazione hello **ambiente del servizio Cloud alternativo** proprietà troppo**produzione**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="be1c1-191">Ecco dove l'URL del sito hello è nella pagina dashboard del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="be1c1-192">Una nuova scheda del browser verrà aperto tooreveal del sito in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="be1c1-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="be1c1-193">Se si apportano altre modifiche delle tooyour progetto, i trigger è più compila e si accumuleranno più distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="be1c1-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="be1c1-194">Hello più recente uno è contrassegnato come attivo.</span><span class="sxs-lookup"><span data-stu-id="be1c1-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="be1c1-195">5: Ridistribuire una compilazione precedente</span><span class="sxs-lookup"><span data-stu-id="be1c1-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="be1c1-196">Questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="be1c1-196">This step is optional.</span></span> <span data-ttu-id="be1c1-197">Nel portale di Azure classico hello, scegliere una distribuzione precedente e scegliere **ridistribuire** toorewind il sito tooan precedentemente check-in.</span><span class="sxs-lookup"><span data-stu-id="be1c1-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="be1c1-198">Si noti che verrà attivata una nuova compilazione in TFS e verrà creata una nuova voce nella cronologia della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="be1c1-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="be1c1-199">6: modificare la distribuzione di produzione hello</span><span class="sxs-lookup"><span data-stu-id="be1c1-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="be1c1-200">Quando si è pronti, è possibile alzare di livello hello gestione temporanea toohello ambiente di produzione scegliendo **scambiare** nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="be1c1-201">ambiente di gestione temporanea appena distribuito Hello è tooProduction innalzate di livello e ambiente di produzione hello precedente, se presente, diventa un ambiente di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="be1c1-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="be1c1-202">distribuzione attiva Hello potrebbe essere diverso per ambienti di gestione temporanea e produzione hello, ma la cronologia della distribuzione hello di compilazioni recenti è hello uguali indipendentemente dal fatto che dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="be1c1-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="be1c1-203">7: Eseguire la distribuzione da un ramo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="be1c1-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="be1c1-204">Quando si usa Git, vengono in genere modifiche in un ramo di lavoro e integra nel ramo master di hello quando lo sviluppo delle raggiunge uno stato completato.</span><span class="sxs-lookup"><span data-stu-id="be1c1-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="be1c1-205">Durante la fase di sviluppo hello di un progetto, sarà toobuild che desideri distribuire tooAzure ramo di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="be1c1-206">In **Team Explorer**, scegliere hello **Home** pulsante e quindi scegliere hello **rami** pulsante.</span><span class="sxs-lookup"><span data-stu-id="be1c1-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="be1c1-207">Scegliere hello **nuovo ramo** collegamento.</span><span class="sxs-lookup"><span data-stu-id="be1c1-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="be1c1-208">Immettere il nome di hello del ramo hello, ad esempio "working" e scegliere **Crea ramo**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="be1c1-209">Verrà creato un nuovo branch locale.</span><span class="sxs-lookup"><span data-stu-id="be1c1-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="be1c1-210">Pubblicare il ramo hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-210">Publish hello branch.</span></span> <span data-ttu-id="be1c1-211">Scegliere il nome di ramo hello in **non pubblicato rami**e scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="be1c1-212">Per impostazione predefinita, solo di modificare il trigger di ramo master toohello una compilazione continua.</span><span class="sxs-lookup"><span data-stu-id="be1c1-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="be1c1-213">tooset la compilazione continua per un ramo di lavoro, scegliere hello **compilazioni** pagina **Team Explorer**e scegliere **Modifica definizione di compilazione**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="be1c1-214">Aprire hello **le impostazioni dell'origine** scheda. In **monitorati rami per l'integrazione continua e compilazione**, scegliere **fare clic qui tooadd una nuova riga**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="be1c1-215">Specificare il ramo hello che è stato creato, ad esempio funzionante/testine/refs.</span><span class="sxs-lookup"><span data-stu-id="be1c1-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="be1c1-216">Apportare una modifica nel codice hello, menu di scelta rapida aprire hello hello modificato file e quindi scegliere **Commit**.</span><span class="sxs-lookup"><span data-stu-id="be1c1-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="be1c1-217">Scegliere hello **commit non sincronizzati** collegamento e scegliere hello **sincronizzazione** pulsante o hello **Push** hello toocopy collegamento Cambia copia toohello del ramo di lavoro hello in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="be1c1-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="be1c1-218">Passare toohello **compilazioni** consente di visualizzare e trovare compilazione hello attivate solo ottenuto per il ramo di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="be1c1-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be1c1-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be1c1-219">Next steps</span></span>
<span data-ttu-id="be1c1-220">toolearn ulteriori suggerimenti sull'uso di Git con Visual Studio Team Services, vedere [sviluppare e condividere il codice in Git in Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) e per informazioni sull'utilizzo di un repository Git che non è gestito da Visual Studio Team Services toopublish tooAzure, vedere [tooAzure distribuzione continua servizio App](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="be1c1-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="be1c1-221">Per altre informazioni su Visual Studio Team Services, vedere [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="be1c1-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
