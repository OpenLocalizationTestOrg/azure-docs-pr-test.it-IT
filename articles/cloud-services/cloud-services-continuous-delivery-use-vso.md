---
title: recapito aaaContinuous con Visual Studio Team Services in Azure | Documenti Microsoft
description: "Informazioni su come tooconfigure il Visual Studio Team Services i progetti team tooautomatically compilare e distribuire toohello funzionalità App Web di servizi cloud o di servizio App di Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="bd14e-103">TooAzure il recapito continuo con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="bd14e-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="bd14e-104">È possibile configurare la compilazione di Visual Studio Team Services team progetti tooautomatically e distribuire le app web tooAzure o servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="bd14e-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="bd14e-105">(Per informazioni su come tooset fino a una compilazione continua e distribuzione del sistema utilizzando un *locale* Team Foundation Server, vedere [il recapito continuo per servizi Cloud in Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="bd14e-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="bd14e-106">In questa esercitazione si presuppone di Visual Studio 2013 e Azure SDK installata hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="bd14e-107">Se si dispone già di Visual Studio 2013, scaricarlo scegliendo hello **possibile iniziare gratuitamente** collegamento [www.visualstudio.com](http://www.visualstudio.com). Installazione hello Azure SDK da [qui](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="bd14e-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="bd14e-108">È necessario un toocomplete di account di Visual Studio Team Services in questa esercitazione: È possibile [aprire un account di Visual Studio Team Services gratuito](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="bd14e-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="bd14e-109">tooset backup un tooautomatically servizio cloud compilare e distribuire tooAzure utilizzando Visual Studio Team Services, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="bd14e-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="bd14e-110">1: Creare un progetto team</span><span class="sxs-lookup"><span data-stu-id="bd14e-110">1: Create a team project</span></span>
<span data-ttu-id="bd14e-111">Seguire le istruzioni di hello [qui](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate il team di progetto e crea un collegamento tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd14e-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="bd14e-112">In questa procedura dettagliata si presume che si usi Controllo della versione di Team Foundation (TFVC) come soluzione di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="bd14e-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="bd14e-113">Se si desidera toouse Git per il controllo della versione, vedere [versione Git hello di questa procedura dettagliata](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="bd14e-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="bd14e-114">2: controllare in un controllo toosource progetto</span><span class="sxs-lookup"><span data-stu-id="bd14e-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="bd14e-115">In Visual Studio, aprire Esplora hello toodeploy desiderato oppure crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="bd14e-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="bd14e-116">È possibile distribuire un'app web o un servizio cloud (applicazione di Azure) da hello seguente passaggi in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="bd14e-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="bd14e-117">Se si desidera toocreate una nuova soluzione, creare un nuovo progetto di servizio Cloud di Azure o un nuovo progetto ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="bd14e-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="bd14e-118">Assicurarsi che hello progetto è destinato a .NET Framework 4 o 4.5 e se si sta creando un progetto di servizio cloud, aggiungere un ruolo web ASP.NET MVC e un ruolo di lavoro e scegliere l'applicazione Internet per il ruolo web hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="bd14e-119">Quando richiesto, scegliere **Applicazione Internet**.</span><span class="sxs-lookup"><span data-stu-id="bd14e-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="bd14e-120">Se si desidera toocreate un'app web, scegliere il modello di progetto applicazione Web ASP.NET di hello, quindi MVC.</span><span class="sxs-lookup"><span data-stu-id="bd14e-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="bd14e-121">Vedere [Creare un'app Web ASP.NET in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="bd14e-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bd14e-122">Al momento, Visual Studio Team Services supporta solo le distribuzioni CI di applicazioni Web di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd14e-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="bd14e-123">I progetti di sito Web sono esterni all'ambito.</span><span class="sxs-lookup"><span data-stu-id="bd14e-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="bd14e-124">Aprire hello menu di scelta rapida Esplora hello e scegliere **tooSource Aggiungi soluzione controllo**.</span><span class="sxs-lookup"><span data-stu-id="bd14e-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="bd14e-125">Accettare o modificare le impostazioni predefinite di hello e scegliere hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="bd14e-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="bd14e-126">Al termine del processo di hello, vengono visualizzate le icone di controllo di origine **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="bd14e-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="bd14e-127">Aprire il menu di scelta rapida hello per soluzione hello e scegliere **Archivia**.</span><span class="sxs-lookup"><span data-stu-id="bd14e-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="bd14e-128">In hello **modifiche in sospeso** area di **Team Explorer**, digitare un commento per l'archiviazione hello e scegliere hello **Archivia** pulsante.</span><span class="sxs-lookup"><span data-stu-id="bd14e-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="bd14e-129">Si noti hello opzioni tooinclude o escludere modifiche specifiche quando si archivia.</span><span class="sxs-lookup"><span data-stu-id="bd14e-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="bd14e-130">Se si desidera sono escluse le modifiche, scegliere hello **Includi tutto** collegamento.</span><span class="sxs-lookup"><span data-stu-id="bd14e-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="bd14e-131">3: connettere hello progetto tooAzure</span><span class="sxs-lookup"><span data-stu-id="bd14e-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="bd14e-132">Dopo avere creato un progetto team di Visual Studio Team Services con un codice di origine in essa contenuti, si è pronti tooconnect tooAzure del progetto team.</span><span class="sxs-lookup"><span data-stu-id="bd14e-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="bd14e-133">In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), selezionare l'applicazione web o servizio cloud o crearne uno nuovo scegliendo hello  **+**  icona in basso a sinistra di hello e scegliendo **servizio Cloud** o **App Web** e quindi **creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="bd14e-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="bd14e-134">Scegliere hello **impostare la pubblicazione con Visual Studio Team Services** collegamento.</span><span class="sxs-lookup"><span data-stu-id="bd14e-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="bd14e-135">Nella procedura guidata hello, digitare il nome di hello dell'account di Visual Studio Team Services nella casella di testo hello e fare clic su hello **autorizzare ora** collegamento.</span><span class="sxs-lookup"><span data-stu-id="bd14e-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="bd14e-136">Potrebbe essere necessario toosign in.</span><span class="sxs-lookup"><span data-stu-id="bd14e-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="bd14e-137">In hello **richiesta di connessione** finestra di dialogo popup scegliere hello **Accept** pulsante tooauthorize tooconfigure Azure il progetto team in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="bd14e-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="bd14e-138">Dopo aver concesso l'autorizzazione verrà visualizzato un elenco a discesa contenente un elenco dei progetti team di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="bd14e-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="bd14e-139">Scegliere il nome di hello del progetto team creato nei passaggi precedenti hello e quindi sul pulsante della procedura guidata di hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="bd14e-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="bd14e-140">Dopo che il progetto è collegato, verrà visualizzato alcune istruzioni per l'archiviazione del progetto team di Visual Studio Team Services tooyour le modifiche.</span><span class="sxs-lookup"><span data-stu-id="bd14e-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="bd14e-141">Il successivo check-in, Visual Studio Team Services verrà compilato e distribuito tooAzure il progetto.</span><span class="sxs-lookup"><span data-stu-id="bd14e-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="bd14e-142">Provare a questo punto, fare clic su hello **Check-In da Visual Studio** il collegamento e quindi hello **avviare Visual Studio** collegamento (o equivalente hello **Visual Studio** pulsante nella parte inferiore di hello del portale schermata Ciao).</span><span class="sxs-lookup"><span data-stu-id="bd14e-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="bd14e-143">4: Attivare una ricompilazione e ridistribuire il progetto</span><span class="sxs-lookup"><span data-stu-id="bd14e-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="bd14e-144">In Visual Studio **Team Explorer**, scegliere hello **Esplora controllo codice sorgente** collegamento.</span><span class="sxs-lookup"><span data-stu-id="bd14e-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="bd14e-145">Selezionare il file di soluzione tooyour e aprirlo.</span><span class="sxs-lookup"><span data-stu-id="bd14e-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="bd14e-146">In **Esplora soluzioni**aprire un file e modificarlo.</span><span class="sxs-lookup"><span data-stu-id="bd14e-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="bd14e-147">Ad esempio, modificare il file hello `_Layout.cshtml` in visualizzazioni hello\\cartella condivisa in un ruolo web MVC.</span><span class="sxs-lookup"><span data-stu-id="bd14e-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="bd14e-148">Modificare il logo hello per il sito hello e scegliere **Ctrl + S** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="bd14e-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="bd14e-149">In **Team Explorer**, scegliere hello **modifiche in sospeso** collegamento.</span><span class="sxs-lookup"><span data-stu-id="bd14e-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="bd14e-150">Immettere un commento e quindi scegliere hello **Archivia** pulsante.</span><span class="sxs-lookup"><span data-stu-id="bd14e-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="bd14e-151">Scegliere hello **Home** pulsante tooreturn toohello **Team Explorer** pagina iniziale.</span><span class="sxs-lookup"><span data-stu-id="bd14e-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="bd14e-152">Scegliere hello **compilazioni** hello tooview collegamento compilazioni in corso.</span><span class="sxs-lookup"><span data-stu-id="bd14e-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="bd14e-153">**Team Explorer** mostra che è stata attivata una compilazione per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bd14e-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="bd14e-154">Fare doppio clic sul nome hello di compilazione hello in corso tooview un log dettagliato come compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="bd14e-155">Durante la compilazione hello è in corso, esaminare una definizione di compilazione hello creata quando è stato collegato tooAzure TFS utilizzando la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="bd14e-156">Aprire il menu di scelta rapida hello hello la definizione di compilazione e scegliere **Modifica definizione di compilazione**.</span><span class="sxs-lookup"><span data-stu-id="bd14e-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="bd14e-157">In hello **Trigger** scheda, si noterà che la definizione di compilazione hello è toobuild attivata ogni check-in per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="bd14e-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="bd14e-158">In hello **processo** scheda, è possibile vedere ambiente di distribuzione hello è impostato toohello nome dell'app web o servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="bd14e-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="bd14e-159">Se si lavora con le app web, proprietà hello che viene visualizzato è diversa da quelle indicate qui.</span><span class="sxs-lookup"><span data-stu-id="bd14e-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="bd14e-160">Se si desiderano valori diversi da quelli predefiniti hello, specificare i valori per le proprietà di hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="bd14e-161">salve le proprietà per la pubblicazione di Azure sono in hello **distribuzione** sezione.</span><span class="sxs-lookup"><span data-stu-id="bd14e-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="bd14e-162">Hello nella tabella seguente mostra le proprietà disponibili hello in hello **distribuzione** sezione:</span><span class="sxs-lookup"><span data-stu-id="bd14e-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="bd14e-163">Proprietà</span><span class="sxs-lookup"><span data-stu-id="bd14e-163">Property</span></span> | <span data-ttu-id="bd14e-164">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="bd14e-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bd14e-165">Consenti certificati non attendibili</span><span class="sxs-lookup"><span data-stu-id="bd14e-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="bd14e-166">Se è false, i certificati SSL devono essere firmati da un'autorità radice.</span><span class="sxs-lookup"><span data-stu-id="bd14e-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="bd14e-167">Consenti aggiornamento</span><span class="sxs-lookup"><span data-stu-id="bd14e-167">Allow Upgrade</span></span> |<span data-ttu-id="bd14e-168">Consente di hello distribuzione tooupdate una distribuzione esistente anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="bd14e-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="bd14e-169">Consente di mantenere l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="bd14e-170">Non eliminare</span><span class="sxs-lookup"><span data-stu-id="bd14e-170">Do Not Delete</span></span> |<span data-ttu-id="bd14e-171">Se è true, una distribuzione non correlata esistente non viene sovrascritta (l'aggiornamento è consentito).</span><span class="sxs-lookup"><span data-stu-id="bd14e-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="bd14e-172">Percorso tooDeployment impostazioni</span><span class="sxs-lookup"><span data-stu-id="bd14e-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="bd14e-173">Hello percorso tooyour pubxml file per un'app web, toohello relativo di cartella radice del repository hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="bd14e-174">Viene ignorato per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="bd14e-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="bd14e-175">Ambiente di distribuzione SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd14e-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="bd14e-176">nome del servizio hello, Hello stesso.</span><span class="sxs-lookup"><span data-stu-id="bd14e-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="bd14e-177">Ambiente di distribuzione Azure</span><span class="sxs-lookup"><span data-stu-id="bd14e-177">Azure Deployment Environment</span></span> |<span data-ttu-id="bd14e-178">Hello app o cloud nome del servizio web.</span><span class="sxs-lookup"><span data-stu-id="bd14e-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="bd14e-179">Se si utilizza più configurazioni del servizio (file con estensione cscfg), è possibile specificare la configurazione del servizio desiderato hello in hello **argomenti di compilazione, avanzate, MSBuild** impostazione.</span><span class="sxs-lookup"><span data-stu-id="bd14e-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="bd14e-180">Ad esempio, toouse ServiceConfiguration.Test.cscfg, impostare gli argomenti MSBuild opzione della riga `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="bd14e-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="bd14e-181">A questo punto la compilazione sarà stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="bd14e-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="bd14e-182">Se si fa doppio clic sul nome di compilazione hello, Visual Studio visualizza un **Riepilogo compilazione**, compresi i risultati dei test da associati progetti di unit test.</span><span class="sxs-lookup"><span data-stu-id="bd14e-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="bd14e-183">In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), è possibile visualizzare la distribuzione di hello associata nella hello **distribuzioni** scheda quando viene selezionato l'ambiente di gestione temporanea hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="bd14e-184">Individuare l'URL del sito tooyour.</span><span class="sxs-lookup"><span data-stu-id="bd14e-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="bd14e-185">Per un'app web, fare clic hello **Sfoglia** pulsante sulla barra dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="bd14e-186">Per un servizio cloud, scegliere URL hello in hello **Quick Glance** sezione di hello **Dashboard** pagina che mostra l'ambiente di gestione temporanea hello per un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="bd14e-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="bd14e-187">Le distribuzioni di integrazione continua per i servizi cloud sono pubblicati toohello ambiente di gestione temporanea per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="bd14e-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="bd14e-188">È possibile modificare questa impostazione hello **ambiente del servizio Cloud alternativo** proprietà troppo**produzione**.</span><span class="sxs-lookup"><span data-stu-id="bd14e-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="bd14e-189">Questa schermata mostra dove hello che URL del sito è nella pagina dashboard del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="bd14e-190">Una nuova scheda del browser verrà aperto tooreveal del sito in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bd14e-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="bd14e-191">Per i servizi cloud, se si apporta altre progetto tooyour le modifiche, si trigger più compila e si accumuleranno più distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="bd14e-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="bd14e-192">Hello più recente contrassegnato come attivo.</span><span class="sxs-lookup"><span data-stu-id="bd14e-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="bd14e-193">5: Ridistribuire una compilazione precedente</span><span class="sxs-lookup"><span data-stu-id="bd14e-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="bd14e-194">Questo passaggio si applica toocloud services ed è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="bd14e-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="bd14e-195">Nel portale di Azure classico hello, scegliere una distribuzione precedente quindi hello **ridistribuire** pulsante toorewind il sito tooan precedentemente check-in.</span><span class="sxs-lookup"><span data-stu-id="bd14e-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="bd14e-196">Si noti che verrà attivata una nuova compilazione in TFS e verrà creata una nuova voce nella cronologia della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bd14e-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="bd14e-197">6: modificare la distribuzione di produzione hello</span><span class="sxs-lookup"><span data-stu-id="bd14e-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="bd14e-198">Questo passaggio si applica solo toocloud services, non le applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="bd14e-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="bd14e-199">Quando si è pronti, è possibile alzare di livello hello gestione temporanea toohello ambiente di produzione scegliendo hello **scambiare** pulsante hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="bd14e-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="bd14e-200">ambiente di gestione temporanea appena distribuito Hello è tooProduction innalzate di livello e ambiente di produzione hello precedente, se presente, diventa un ambiente di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="bd14e-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="bd14e-201">distribuzione attiva Hello potrebbe essere diverso per ambienti di gestione temporanea e produzione hello, ma la cronologia della distribuzione hello di compilazioni recenti è hello uguali indipendentemente dal fatto che dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="bd14e-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="bd14e-202">7: Eseguire unit test</span><span class="sxs-lookup"><span data-stu-id="bd14e-202">7: Run unit tests</span></span>
<span data-ttu-id="bd14e-203">Questo passaggio si applica solo le app tooweb, non i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="bd14e-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="bd14e-204">tooput controllo di qualità, alla distribuzione, è possibile eseguire unit test e in caso di errore, è possibile arrestare la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="bd14e-205">In Visual Studio aggiungere un progetto di unit test.</span><span class="sxs-lookup"><span data-stu-id="bd14e-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="bd14e-206">Aggiungere riferimenti toohello progetto desiderato tootest.</span><span class="sxs-lookup"><span data-stu-id="bd14e-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="bd14e-207">Aggiungere alcuni unit test.</span><span class="sxs-lookup"><span data-stu-id="bd14e-207">Add some unit tests.</span></span> <span data-ttu-id="bd14e-208">tooget avviato, provare a un test fittizio che passa sempre.</span><span class="sxs-lookup"><span data-stu-id="bd14e-208">tooget started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="bd14e-209">Modificare la definizione di compilazione hello, scegliere hello **processo** scheda ed espandere hello **Test** nodo.</span><span class="sxs-lookup"><span data-stu-id="bd14e-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="bd14e-210">Set hello **Errore compilazione se test** tooTrue.</span><span class="sxs-lookup"><span data-stu-id="bd14e-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="bd14e-211">Ciò significa che la distribuzione di hello non verrà eseguita a meno che non hello test vengono superati.</span><span class="sxs-lookup"><span data-stu-id="bd14e-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="bd14e-212">Inserire in coda una nuova compilazione.</span><span class="sxs-lookup"><span data-stu-id="bd14e-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="bd14e-213">Mentre è in corso la compilazione hello, controllare lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="bd14e-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="bd14e-214">Quando viene eseguita la compilazione hello, controllare i risultati dei test hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="bd14e-215">Provare a creare un test che non verrà superato.</span><span class="sxs-lookup"><span data-stu-id="bd14e-215">Try creating a test that will fail.</span></span> <span data-ttu-id="bd14e-216">Aggiungere un nuovo test copiando hello prima, rinominarlo e impostare come commento la riga hello del codice che indica il che NotImplementedException è un'eccezione prevista.</span><span class="sxs-lookup"><span data-stu-id="bd14e-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="bd14e-217">Il controllo in hello modifica tooqueue una nuova compilazione.</span><span class="sxs-lookup"><span data-stu-id="bd14e-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="bd14e-218">Visualizzare hello test risultati toosee i dettagli sull'errore hello.</span><span class="sxs-lookup"><span data-stu-id="bd14e-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="bd14e-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd14e-219">Next steps</span></span>
<span data-ttu-id="bd14e-220">Per altre informazioni sull'esecuzione di test delle unità in Visual Studio Team Services, vedere [Eseguire test delle unità nella compilazione](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="bd14e-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="bd14e-221">Se si usa Git, vedere [condividere il codice in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) e [tooAzure distribuzione continua servizio App](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="bd14e-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="bd14e-222">Per altre informazioni su Visual Studio Team Services, vedere [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="bd14e-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
