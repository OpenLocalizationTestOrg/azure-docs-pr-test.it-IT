---
title: aaaDeploy processi Web usando Visual Studio
description: Informazioni su come toodeploy processi Web di Azure tooAzure applicazione servizio Web App con Visual Studio.
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="6bd1b-103">Distribuzione di processi Web usando Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6bd1b-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="6bd1b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6bd1b-104">Overview</span></span>
<span data-ttu-id="6bd1b-105">Questo argomento viene illustrato come toouse Visual Studio toodeploy un'applicazione Console progetto app web tooa [servizio App](http://go.microsoft.com/fwlink/?LinkId=529714) come un [processo Web di Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="6bd1b-106">Per informazioni su come toodeploy processi Web usando hello [portale Azure](https://portal.azure.com), vedere [attività eseguire in Background con processi Web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="6bd1b-107">Quando distribuisce un progetto di applicazione console abilitato per i processi Web, Visual Studio esegue due attività:</span><span class="sxs-lookup"><span data-stu-id="6bd1b-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="6bd1b-108">File di runtime di copie di toohello cartella appropriata in hello web app (*App_Data/processi/continua* per processi Web continui, *App_Data, processi/attivato* per processi Web pianificati e su richiesta).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="6bd1b-109">Consente di impostare [processi dell'utilità di pianificazione di Azure](#scheduler) per processi Web che vengono pianificati toorun in determinati momenti.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="6bd1b-110">Tale operazione non è necessaria per l'esecuzione dei processi Web in modalità continua.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="6bd1b-111">Un progetto processi Web abilitati presenta hello tooit aggiunti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6bd1b-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="6bd1b-112">Hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="6bd1b-113">File [webjob-publish-settings.json](#publishsettings) che contiene le impostazioni di distribuzione e dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagramma che mostra ciò che viene aggiunto tooa App Console tooenable deployment come un processo Web](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="6bd1b-115">È possibile aggiungere questi tooan elementi progetto di applicazione Console esistente o utilizzare un toocreate modello un nuovo progetto applicazione Console abilitata per processi Web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="6bd1b-116">È possibile distribuire un progetto come un processo Web da solo o collegare il progetto di web tooa in modo che venga distribuito automaticamente ogni volta che si distribuisce il progetto di web hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="6bd1b-117">toolink progetti di Visual Studio include il nome di hello del progetto abilitato processi Web hello in un [processi Web list.json](#webjobslist) file nel progetto web hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Diagramma che illustra il progetto processo Web collegamento tooweb progetto](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="6bd1b-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6bd1b-119">Prerequisites</span></span>
<span data-ttu-id="6bd1b-120">Funzionalità di distribuzione di processi Web sono disponibili in Visual Studio quando si installa hello Azure SDK per .NET:</span><span class="sxs-lookup"><span data-stu-id="6bd1b-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="6bd1b-121">[Azure SDK per .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="6bd1b-122"><a id="convert"></a>Abilitare la distribuzione dei processi Web per un progetto di applicazione console esistente</span><span class="sxs-lookup"><span data-stu-id="6bd1b-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="6bd1b-123">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="6bd1b-123">You have two options:</span></span>

* <span data-ttu-id="6bd1b-124">[Abilitare la distribuzione automatica con un progetto Web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="6bd1b-125">Configurare un progetto di applicazione console esistente in modo tale che venga distribuito automaticamente come processo Web quando viene distribuito un progetto Web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="6bd1b-126">Utilizzare questa opzione quando si desidera che il processo Web in hello toorun stessa app web in cui si esegue hello correlati dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="6bd1b-127">[Abilitare la distribuzione senza un progetto Web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="6bd1b-128">Configurare un toodeploy di progetto applicazione Console esistente come un processo Web da sola, con alcun progetto web tooa di collegamento.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="6bd1b-129">Utilizzare questa opzione quando si desidera toorun un processo Web in un'app web di per sé con nessuna applicazione web in esecuzione nell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="6bd1b-130">È possibile toodo questo ordine tooscale in grado di toobe le risorse di processo Web indipendentemente dalle risorse dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="6bd1b-131"><a id="convertlink"></a> Abilitare la distribuzione automatica dei processi Web con un progetto Web</span><span class="sxs-lookup"><span data-stu-id="6bd1b-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="6bd1b-132">Progetto web di hello pulsante destro del mouse in **Esplora**, quindi fare clic su **Aggiungi** > **progetto esistente come processo Web di Azure**.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Progetto esistente come processo Web Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="6bd1b-134">Hello [Aggiungi processo Web di Azure](#configure) viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="6bd1b-135">In hello **nome progetto** elenco a discesa, tooadd di progetto applicazione Console hello selezionare come un processo Web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Selezione del progetto nella finestra di dialogo Aggiungi processo Web Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="6bd1b-137">Hello completo [Aggiungi processo Web di Azure](#configure) finestra di dialogo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="6bd1b-138"><a id="convertnolink"></a> Abilitare la distribuzione dei processi Web senza un progetto Web</span><span class="sxs-lookup"><span data-stu-id="6bd1b-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="6bd1b-139">Progetto di applicazione Console hello pulsante destro del mouse in **Esplora**, quindi fare clic su **pubblica come processo Web di Azure...** .</span><span class="sxs-lookup"><span data-stu-id="6bd1b-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Pubblica come processo Web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="6bd1b-141">Hello [Aggiungi processo Web di Azure](#configure) viene visualizzata la finestra di dialogo, con progetto hello in hello **nome progetto** casella.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="6bd1b-142">Hello completo [Aggiungi processo Web di Azure](#configure) la finestra di dialogo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="6bd1b-143">Hello **pubblica sul Web** procedura guidata viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="6bd1b-144">Se si desidera toopublish immediatamente, chiudere la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="6bd1b-145">le impostazioni di Hello immessi vengono salvate per quando si desidera troppo[distribuire il progetto hello](#deploy).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="6bd1b-146"><a id="create"></a>Creare un nuovo progetto abilitato per i processi Web</span><span class="sxs-lookup"><span data-stu-id="6bd1b-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="6bd1b-147">toocreate un nuovo progetto processi Web abilitata, è possibile utilizzare hello applicazione Console progetto modello e abilitare processi Web distribuzione come spiegato in [hello precedente sezione](#convert).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="6bd1b-148">In alternativa, è possibile utilizzare modello nuovo progetto di hello processi Web:</span><span class="sxs-lookup"><span data-stu-id="6bd1b-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="6bd1b-149">Modello di hello processi Web nuovo progetto per un processo indipendente dal Web</span><span class="sxs-lookup"><span data-stu-id="6bd1b-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="6bd1b-150">Creare un progetto e configurare toodeploy da se stesso come un processo Web, un progetto di web tooa alcun collegamento.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="6bd1b-151">Utilizzare questa opzione quando si desidera toorun un processo Web in un'app web di per sé con nessuna applicazione web in esecuzione nell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="6bd1b-152">È possibile toodo questo ordine tooscale in grado di toobe le risorse di processo Web indipendentemente dalle risorse dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="6bd1b-153">Modello di hello processi Web nuovo progetto per un progetto di web tooa collegato processo Web</span><span class="sxs-lookup"><span data-stu-id="6bd1b-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="6bd1b-154">Creare un progetto toodeploy configurato automaticamente come un processo Web quando un progetto web nella stessa soluzione viene distribuita hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="6bd1b-155">Utilizzare questa opzione quando si desidera che il processo Web in hello toorun stessa app web in cui si esegue hello correlati dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="6bd1b-156">modello nuovo progetto processi Web di Hello automaticamente installa i pacchetti NuGet e include il codice in *Program.cs* per hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="6bd1b-157">Se non si desidera toouse hello WebJobs SDK, rimuovere o modificare hello `host.RunAndBlock` istruzione *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="6bd1b-158"><a id="createnolink"></a>Modello di hello processi Web nuovo progetto per un processo indipendente dal Web</span><span class="sxs-lookup"><span data-stu-id="6bd1b-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="6bd1b-159">Fare clic su **File** > **nuovo progetto**e quindi in hello **nuovo progetto** finestra di dialogo fare clic su **Cloud**  >   **Processo Web di Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Finestra di dialogo Nuovo progetto con il modello processo Web](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="6bd1b-161">Seguire le direzioni di hello illustrate in precedenza troppo[rendere hello progetto applicazione Console come un progetto processi Web indipendente](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="6bd1b-162"><a id="createlink"></a>Modello di hello processi Web nuovo progetto per un progetto di web tooa collegato processo Web</span><span class="sxs-lookup"><span data-stu-id="6bd1b-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="6bd1b-163">Progetto web di hello pulsante destro del mouse in **Esplora**, quindi fare clic su **Aggiungi** > **nuovo progetto processo Web di Azure**.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Voce del menu Nuovo progetto processo Web Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="6bd1b-165">Hello [Aggiungi processo Web di Azure](#configure) viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="6bd1b-166">Hello completo [Aggiungi processo Web di Azure](#configure) la finestra di dialogo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="6bd1b-167"><a id="configure"></a>finestra di dialogo Aggiungi processo Web di Azure Hello</span><span class="sxs-lookup"><span data-stu-id="6bd1b-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="6bd1b-168">Hello **Aggiungi processo Web di Azure** finestra di dialogo consente di immettere il nome di processo Web hello ed eseguire l'impostazione della modalità per il processo Web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Finestra di dialogo Aggiungi processo Web Azure](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="6bd1b-170">i campi di Hello in questa finestra di dialogo corrispondono toofields su hello **nuovo processo** finestra di dialogo di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="6bd1b-171">Per ulteriori informazioni, vedere [attività in Background eseguito con WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="6bd1b-172">Per informazioni sulla distribuzione da riga di comando, vedere [Abilitazione della riga di comando o del recapito continuo di processi Web Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="6bd1b-173">Se si distribuisce un processo Web e quindi si decide toochange hello tipo processo Web e ridistribuzione, è necessario file Settings pubblicare processi Web di toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="6bd1b-174">In questo modo Visual Studio Mostra hello opzioni di pubblicazione, pertanto è possibile modificare il tipo di hello del processo Web.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="6bd1b-175">Se si distribuisce un processo Web e successivamente si cambia modalità di esecuzione da continuo continua a toonon hello o viceversa, Visual Studio crea un nuovo processo di Web in Azure quando si ridistribuisce.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="6bd1b-176">Se è modificare altre impostazioni di pianificazione, ma lasciare eseguire modalità hello stesso o alternare pianificati e su richiesta, gli aggiornamenti di Visual Studio hello processo esistente anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="6bd1b-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="6bd1b-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="6bd1b-178">Quando si configura un'applicazione Console per la distribuzione di processi Web, Visual Studio installa hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package e archivi la programmazione di informazioni in un *Settings pubblicare processo Web*  file nel progetto hello *proprietà* nella cartella del progetto processi Web hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="6bd1b-179">Di seguito è riportato un esempio di tale file:</span><span class="sxs-lookup"><span data-stu-id="6bd1b-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="6bd1b-180">È possibile modificare questo file direttamente e Visual Studio fornisce IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="6bd1b-181">schema del file Hello è archiviato in [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) e può essere visualizzata.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="6bd1b-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="6bd1b-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="6bd1b-183">Quando si collega un progetto di web tooa progetto processi Web, Visual Studio archivia il nome di hello del progetto processi Web hello in un *processi Web list.json* file nel progetto hello web *proprietà* cartella.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="6bd1b-184">elenco di Hello potrebbe contenere più progetti processi Web, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="6bd1b-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="6bd1b-185">È possibile modificare questo file direttamente e Visual Studio fornisce IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="6bd1b-186">schema del file Hello è archiviato in [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) e può essere visualizzata.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="6bd1b-187"><a id="deploy"></a>Distribuire un progetto processi Web</span><span class="sxs-lookup"><span data-stu-id="6bd1b-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="6bd1b-188">Un progetto processi Web che è stato collegato un progetto web tooa distribuisce automaticamente un progetto web hello.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="6bd1b-189">Per informazioni sulla distribuzione dei progetti web, vedere [come toodeploy tooWeb app](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="6bd1b-190">un progetto processi Web di per sé toodeploy fare clic sul progetto hello in **Esplora** e fare clic su **pubblica come processo Web di Azure...** .</span><span class="sxs-lookup"><span data-stu-id="6bd1b-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Pubblica come processo Web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="6bd1b-192">Per un processo Web indipendenti, hello stesso **pubblica sul Web** procedura guidata che viene utilizzato per i progetti web viene visualizzato, ma con un numero inferiore toochange disponibili di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="6bd1b-193"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6bd1b-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="6bd1b-194">Questo articolo è stato spiegato come toodeploy processi Web usando Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6bd1b-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="6bd1b-195">Per ulteriori informazioni su come toodeploy processi Web di Azure, vedere [processi Web di Azure - consigliato risorse - distribuzione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="6bd1b-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

