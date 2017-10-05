---
title: Recapito continuo con Visual Studio Team Services in Azure | Documentazione Microsoft
description: "Informazioni sulla configurazione dei progetti team di Visual Studio Team Services per la compilazione e la distribuzione automatiche alla funzionalità App Web nel Servizio app di Azure o nei servizi cloud."
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
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="9fbdb-103">Recapito continuo in Azure tramite Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9fbdb-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="9fbdb-104">È possibile configurare i progetti del proprio team di Visual Studio Team Services in modo da compilare ed eseguire automaticamente la distribuzione nelle app Web o nei servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="9fbdb-105">Per informazioni su come configurare un sistema di compilazione e distribuzione continua con un Team Foundation Server *locale* , vedere [Recapito continuo per Servizi cloud in Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="9fbdb-106">In questa esercitazione si presuppone che l'utente abbia installato Visual Studio 2013 e Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="9fbdb-107">Se non si dispone ancora di Visual Studio 2013, scaricarlo scegliendo il collegamento **Inizia gratuitamente** all'indirizzo [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="9fbdb-108">Installare Azure SDK da [questa pagina](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="9fbdb-109">Per completare l'esercitazione, è necessario un account di Visual Studio Team Services: è possibile [aprire un account di Visual Studio Team Services gratuitamente](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="9fbdb-110">Per configurare un servizio cloud da compilare e distribuire automaticamente in Azure tramite Visual Studio Team Services, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="9fbdb-111">1: Creare un progetto team</span><span class="sxs-lookup"><span data-stu-id="9fbdb-111">1: Create a team project</span></span>
<span data-ttu-id="9fbdb-112">Seguire le istruzioni [qui](http://go.microsoft.com/fwlink/?LinkId=512980) per creare il progetto team e collegarlo a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="9fbdb-113">In questa procedura dettagliata si presume che si usi Controllo della versione di Team Foundation (TFVC) come soluzione di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="9fbdb-114">Per usare Git per il controllo della versione, vedere [la versione per Git di questa procedura dettagliata](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="9fbdb-115">2: Archiviare un progetto nel controllo del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="9fbdb-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="9fbdb-116">In Visual Studio, aprire la soluzione che si desidera distribuire o crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="9fbdb-117">È possibile distribuire un’app Web o un servizio cloud (applicazione Azure) seguendo i passaggi di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="9fbdb-118">Se si desidera creare una nuova soluzione, creare un nuovo progetto di servizio cloud di Azure o un nuovo progetto ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="9fbdb-119">Assicurarsi che la destinazione del progetto sia .NET Framework 4 o 4.5 e, se si sta creando un progetto di servizio cloud, aggiungere un ruolo Web ASP.NET MVC e un ruolo di lavoro, quindi scegliere l'applicazione Internet per il ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="9fbdb-120">Quando richiesto, scegliere **Applicazione Internet**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="9fbdb-121">Per creare un’app Web, scegliere il modello di progetto Applicazione Web ASP.NET e quindi scegliere MVC.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="9fbdb-122">Vedere [Creare un'app Web ASP.NET in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9fbdb-123">Al momento, Visual Studio Team Services supporta solo le distribuzioni CI di applicazioni Web di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="9fbdb-124">I progetti di sito Web sono esterni all'ambito.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="9fbdb-125">Aprire il menu di scelta rapida relativo alla soluzione e selezionare **Aggiungi soluzione al controllo del codice sorgente**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="9fbdb-126">Accettare o modificare le impostazioni predefinite e quindi scegliere **OK** .</span><span class="sxs-lookup"><span data-stu-id="9fbdb-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="9fbdb-127">Dopo il completamento del processo, in **Esplora soluzioni**vengono visualizzate le icone del controllo codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="9fbdb-128">Aprire il menu di scelta rapida relativo alla soluzione e scegliere **Archivia**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="9fbdb-129">Nell'area **Modifiche in sospeso** di **Team Explorer** digitare un commento per l'archiviazione e scegliere il pulsante **Archivia**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="9fbdb-130">Notare le opzioni per includere o escludere modifiche specifiche quando si esegue l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="9fbdb-131">Se le modifiche desiderate sono escluse, scegliere il collegamento **Includi tutto** .</span><span class="sxs-lookup"><span data-stu-id="9fbdb-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="9fbdb-132">3: Collegare il progetto ad Azure</span><span class="sxs-lookup"><span data-stu-id="9fbdb-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="9fbdb-133">A questo punto, dopo avere creato un progetto team VS Team Services contenente il codice sorgente, è possibile connettere il progetto team ad Azure.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="9fbdb-134">Nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885) selezionare il servizio cloud o l'app Web oppure crearne uno nuovo selezionando l'icona **+** in basso a sinistra e scegliendo **Servizio cloud** o **App Web** e quindi **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="9fbdb-135">Scegliere il collegamento **Imposta pubblicazione con Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="9fbdb-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="9fbdb-136">Nella procedura guidata digitare il nome del proprio account di Visual Studio Team Services nella casella di testo e fare clic sul collegamento **Autorizza ora** .</span><span class="sxs-lookup"><span data-stu-id="9fbdb-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="9fbdb-137">È possibile che venga richiesto di effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="9fbdb-138">Nella finestra di dialogo popup **Connection Request** (Richiesta di connessione) scegliere il pulsante **Accetta** per autorizzare Azure a configurare il progetto team in VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="9fbdb-139">Dopo aver concesso l'autorizzazione verrà visualizzato un elenco a discesa contenente un elenco dei progetti team di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="9fbdb-140">Selezionare il nome del progetto team creato nei passaggi precedenti e quindi fare clic sul pulsante con il segno di spunta della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="9fbdb-141">Dopo aver collegato il progetto saranno visualizzate alcune istruzioni per l'archiviazione delle modifiche nel progetto team di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="9fbdb-142">Alla successiva archiviazione, Visual Studio Team Services compilerà e distribuirà il progetto in Azure.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="9fbdb-143">Provare subito facendo clic sul collegamento **Archivia da Visual Studio**, quindi sul collegamento **Avviare Visual Studio** o sul pulsante equivalente **Visual Studio** nella parte inferiore della schermata del portale.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="9fbdb-144">4: Attivare una ricompilazione e ridistribuire il progetto</span><span class="sxs-lookup"><span data-stu-id="9fbdb-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="9fbdb-145">In **Team Explorer** di Visual Studio fare clic sul collegamento **Esplora controllo codice sorgente**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="9fbdb-146">Passare al file della soluzione e aprirlo.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="9fbdb-147">In **Esplora soluzioni**aprire un file e modificarlo.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="9fbdb-148">Modificare ad esempio il file `_Layout.cshtml` nella cartella Views\\Shared in un ruolo Web MVC.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="9fbdb-149">Modificare il logo del sito e premere **CTRL+S** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="9fbdb-150">In **Team Explorer** scegliere il collegamento **Modifiche in sospeso**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="9fbdb-151">Immettere un commento e quindi scegliere il pulsante **Archivia** .</span><span class="sxs-lookup"><span data-stu-id="9fbdb-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="9fbdb-152">Scegliere il pulsante **Home** per tornare alla pagina iniziale di **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="9fbdb-153">Scegliere il collegamento **Compilazioni** per visualizzare le compilazioni in corso.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="9fbdb-154">**Team Explorer** mostra che è stata attivata una compilazione per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="9fbdb-155">Fare doppio clic sul nome della compilazione in corso per visualizzare un log dettagliato con l'avanzare della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="9fbdb-156">Quando la compilazione è in corso, osservare la definizione di compilazione creata quando TFS è stato collegato ad Azure mediante la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="9fbdb-157">Aprire il menu di scelta rapida relativo alla definizione di compilazione e scegliere **Modifica definizione di compilazione**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="9fbdb-158">Nella scheda **Trigger** si osserva che, per impostazione predefinita, la definizione di compilazione è configurata per la compilazione a ogni archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="9fbdb-159">Nella scheda **Processo** si osserva che l'ambiente di distribuzione è configurato con il nome del proprio servizio cloud o app Web.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="9fbdb-160">Se si lavora con le app Web, le proprietà visualizzate saranno diverse da quelle presenti nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="9fbdb-161">Specificare i valori per le proprietà se si desidera che siano diversi da quelli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="9fbdb-162">Le proprietà per la pubblicazione in Azure sono nella sezione **Distribuzione** .</span><span class="sxs-lookup"><span data-stu-id="9fbdb-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="9fbdb-163">La tabella seguente illustra le proprietà disponibili nella sezione **Distribuzione** :</span><span class="sxs-lookup"><span data-stu-id="9fbdb-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="9fbdb-164">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9fbdb-164">Property</span></span> | <span data-ttu-id="9fbdb-165">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="9fbdb-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="9fbdb-166">Consenti certificati non attendibili</span><span class="sxs-lookup"><span data-stu-id="9fbdb-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="9fbdb-167">Se è false, i certificati SSL devono essere firmati da un'autorità radice.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="9fbdb-168">Consenti aggiornamento</span><span class="sxs-lookup"><span data-stu-id="9fbdb-168">Allow Upgrade</span></span> |<span data-ttu-id="9fbdb-169">Consente l'aggiornamento di una distribuzione esistente anziché crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="9fbdb-170">Conserva l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="9fbdb-171">Non eliminare</span><span class="sxs-lookup"><span data-stu-id="9fbdb-171">Do Not Delete</span></span> |<span data-ttu-id="9fbdb-172">Se è true, una distribuzione non correlata esistente non viene sovrascritta (l'aggiornamento è consentito).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="9fbdb-173">Percorso impostazioni di distribuzione</span><span class="sxs-lookup"><span data-stu-id="9fbdb-173">Path to Deployment Settings</span></span> |<span data-ttu-id="9fbdb-174">Percorso del file con estensione pubxml di un’app Web, relativo alla cartella radice del repository.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="9fbdb-175">Viene ignorato per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="9fbdb-176">Ambiente di distribuzione SharePoint</span><span class="sxs-lookup"><span data-stu-id="9fbdb-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="9fbdb-177">Analogo al nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-177">The same as the service name.</span></span> |
    | <span data-ttu-id="9fbdb-178">Ambiente di distribuzione Azure</span><span class="sxs-lookup"><span data-stu-id="9fbdb-178">Azure Deployment Environment</span></span> |<span data-ttu-id="9fbdb-179">Nome dell'app Web o del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="9fbdb-180">Se si usano più configurazioni di servizio (file .cscfg), è possibile specificare la configurazione del servizio desiderata nell'impostazione **Compila, Avanzate, Argomenti MSBuild** .</span><span class="sxs-lookup"><span data-stu-id="9fbdb-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="9fbdb-181">Ad esempio, per usare ServiceConfiguration.Test.cscfg impostare l'opzione della riga degli argomenti di MSBuild `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="9fbdb-182">A questo punto la compilazione sarà stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="9fbdb-183">Facendo doppio clic sul nome della compilazione, Visual Studio visualizza un **Riepilogo compilazione**che include eventuali risultati del test restituiti dai progetti unit test associati.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="9fbdb-184">Nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885)è possibile visualizzare la distribuzione associata nella scheda **Distribuzioni** quando si seleziona l'ambiente di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="9fbdb-185">Passare all'URL del proprio sito.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-185">Browse to your site's URL.</span></span> <span data-ttu-id="9fbdb-186">Per un'app Web è sufficiente fare clic sul pulsante **Browse** della barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="9fbdb-187">Per un servizio cloud, scegliere l'URL nella sezione **Riepilogo rapido** della pagina **Dashboard** in cui è visualizzato l'ambiente di staging per un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="9fbdb-188">Le distribuzioni derivanti dall'integrazione continua per i servizi cloud vengono pubblicate nell'ambiente di gestione temporanea per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="9fbdb-189">È possibile modificare questa impostazione configurando la proprietà **Ambiente del servizio cloud alternativo** su **Produzione**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="9fbdb-190">La schermata seguente mostra dove si trova l'URL del sito nella pagina dashboard del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="9fbdb-191">Il sito in esecuzione verrà aperto in una nuova scheda del browser.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="9fbdb-192">Per i servizi cloud, se si apportano altre modifiche al progetto, si attiveranno altre compilazioni e si accumuleranno più distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="9fbdb-193">L'ultima è contrassegnata come Attiva.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="9fbdb-194">5: Ridistribuire una compilazione precedente</span><span class="sxs-lookup"><span data-stu-id="9fbdb-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="9fbdb-195">Questo passaggio si applica ai servizi cloud ed è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="9fbdb-196">Nel portale di Azure classico selezionare una distribuzione precedente e fare clic sul pulsante **Ridistribuisci** per riportare il sito a un'archiviazione precedente.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="9fbdb-197">Si noti che verrà attivata una nuova compilazione in TFS e verrà creata una nuova voce nella cronologia della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="9fbdb-198">6: Modificare la distribuzione di produzione</span><span class="sxs-lookup"><span data-stu-id="9fbdb-198">6: Change the Production deployment</span></span>
<span data-ttu-id="9fbdb-199">Questo passaggio si applica solo ai servizi cloud, non alle app Web.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="9fbdb-200">Quando si è pronti, è possibile promuovere l'ambiente di gestione temporanea all'ambiente di produzione scegliendo il pulsante **Scambia** nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="9fbdb-201">L'ambiente di gestione temporanea appena distribuito verrà promosso alla produzione e il precedente ambiente di produzione (se presente) diventerà un ambiente di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="9fbdb-202">La distribuzione attiva potrebbe differire per gli ambienti di produzione e di gestione temporanea, ma la cronologia di distribuzione delle compilazioni recenti è la stessa indipendentemente dall'ambiente.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="9fbdb-203">7: Eseguire unit test</span><span class="sxs-lookup"><span data-stu-id="9fbdb-203">7: Run unit tests</span></span>
<span data-ttu-id="9fbdb-204">Questo passaggio si applica solo alle app Web, non ai servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="9fbdb-205">Per inserire un controllo qualità nella distribuzione, è possibile eseguire alcuni unit test e, se non riescono, è possibile arrestare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="9fbdb-206">In Visual Studio aggiungere un progetto di unit test.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="9fbdb-207">Aggiungere i riferimenti al progetto da testare.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="9fbdb-208">Aggiungere alcuni unit test.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-208">Add some unit tests.</span></span> <span data-ttu-id="9fbdb-209">Per iniziare, provare un test fittizio che verrà sempre superato.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-209">To get started, try a dummy test that will always pass.</span></span>
   
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
4. <span data-ttu-id="9fbdb-210">Modificare la definizione di compilazione, scegliere la scheda **Processo** ed espandere il nodo **Test**.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="9fbdb-211">Impostare **Errore compilazione se test non superato** su True.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="9fbdb-212">Questo significa che la distribuzione non verrà eseguita se non dopo il superamento dei test.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="9fbdb-213">Inserire in coda una nuova compilazione.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="9fbdb-214">Mentre la compilazione è in corso, controllarne l'avanzamento.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="9fbdb-215">Al termine della compilazione, controllare i risultati del test.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="9fbdb-216">Provare a creare un test che non verrà superato.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-216">Try creating a test that will fail.</span></span> <span data-ttu-id="9fbdb-217">Aggiungere un nuovo test copiando il primo, rinominarlo e impostare come commento la riga di codice che indica che NotImplementedException è un'eccezione prevista.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="9fbdb-218">Archiviare la modifica per inserire in coda una nuova compilazione.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="9fbdb-219">Visualizzare i risultati del test per vedere i dettagli sull'errore.</span><span class="sxs-lookup"><span data-stu-id="9fbdb-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="9fbdb-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9fbdb-220">Next steps</span></span>
<span data-ttu-id="9fbdb-221">Per altre informazioni sull'esecuzione di test delle unità in Visual Studio Team Services, vedere [Eseguire test delle unità nella compilazione](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="9fbdb-222">Se si usa Git, vedere [Condividere il codice in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) e [Distribuzione continua nel servizio app di Azure](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="9fbdb-223">Per altre informazioni su Visual Studio Team Services, vedere [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="9fbdb-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
