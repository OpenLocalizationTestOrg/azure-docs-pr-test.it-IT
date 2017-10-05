---
title: Distribuzione di processi Web usando Visual Studio
description: Informazioni su come distribuire processi Web di Azure in Servizio app per app Web di Azure.
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
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="cdf66-103">Distribuzione di processi Web usando Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cdf66-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="cdf66-104">Overview</span><span class="sxs-lookup"><span data-stu-id="cdf66-104">Overview</span></span>
<span data-ttu-id="cdf66-105">Questo argomento illustra come usare Visual Studio per distribuire un progetto di applicazione console in un'app Web in [Servizio app](http://go.microsoft.com/fwlink/?LinkId=529714) come un [processo Web Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="cdf66-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="cdf66-106">Per informazioni su come distribuire processi Web usando il [portale di Azure](https://portal.azure.com), vedere [Eseguire attività in background con processi Web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="cdf66-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="cdf66-107">Quando distribuisce un progetto di applicazione console abilitato per i processi Web, Visual Studio esegue due attività:</span><span class="sxs-lookup"><span data-stu-id="cdf66-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="cdf66-108">Copia i file di runtime nella cartella appropriata nell'app Web (*App_Data/jobs/continuous* per i processi Web in modalità continua, *App_Data/jobs/triggered* per i processi Web pianificati e su richiesta).</span><span class="sxs-lookup"><span data-stu-id="cdf66-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="cdf66-109">Configura i [processi dell'utilità di pianificazione di Azure](#scheduler) per i processi Web pianificati per essere eseguiti a orari specifici.</span><span class="sxs-lookup"><span data-stu-id="cdf66-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="cdf66-110">Tale operazione non è necessaria per l'esecuzione dei processi Web in modalità continua.</span><span class="sxs-lookup"><span data-stu-id="cdf66-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="cdf66-111">A un progetto abilitato per i processi Web vengono aggiunti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cdf66-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="cdf66-112">Pacchetto NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) .</span><span class="sxs-lookup"><span data-stu-id="cdf66-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="cdf66-113">File [webjob-publish-settings.json](#publishsettings) che contiene le impostazioni di distribuzione e dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="cdf66-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagramma che mostra gli elementi aggiunti a un'app console per abilitare la distribuzione come processo Web](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="cdf66-115">È possibile aggiungere questi elementi a un progetto di applicazione console esistente o usare un modello per creare un nuovo progetto di applicazione console abilitato per i processi Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="cdf66-116">È possibile distribuire un progetto come processo Web indipendente o collegarlo a un progetto Web in modo tale che venga distribuito automaticamente ogni volta che viene distribuito il progetto Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="cdf66-117">Per collegare i progetti, Visual Studio include il nome del progetto abilitato per i processi Web in un file [webjobs-list.json](#webjobslist) nel progetto Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagramma che mostra il collegamento del progetto processo Web al progetto Web](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="cdf66-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cdf66-119">Prerequisites</span></span>
<span data-ttu-id="cdf66-120">Le funzionalità di distribuzione di processi Web sono disponibili in Visual Studio quando si installa Azure SDK per .NET:</span><span class="sxs-lookup"><span data-stu-id="cdf66-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="cdf66-121">[Azure SDK per .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cdf66-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="cdf66-122"><a id="convert"></a>Abilitare la distribuzione dei processi Web per un progetto di applicazione console esistente</span><span class="sxs-lookup"><span data-stu-id="cdf66-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="cdf66-123">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="cdf66-123">You have two options:</span></span>

* <span data-ttu-id="cdf66-124">[Abilitare la distribuzione automatica con un progetto Web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="cdf66-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="cdf66-125">Configurare un progetto di applicazione console esistente in modo tale che venga distribuito automaticamente come processo Web quando viene distribuito un progetto Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="cdf66-126">Usare questa opzione quando si vuole eseguire il processo Web nella stessa app Web in cui viene eseguita l'applicazione Web correlata.</span><span class="sxs-lookup"><span data-stu-id="cdf66-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="cdf66-127">[Abilitare la distribuzione senza un progetto Web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="cdf66-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="cdf66-128">Configurare un progetto di applicazione console esistente in modo tale che venga distribuito come processo Web indipendente senza alcun collegamento a un progetto Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="cdf66-129">Usare questa opzione quando si vuole eseguire un processo Web in un'app Web in modo indipendente senza l'esecuzione dell'applicazione Web nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="cdf66-130">Questa opzione potrebbe essere utile per scalare le risorse del processo Web indipendentemente dalle risorse dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="cdf66-131"><a id="convertlink"></a> Abilitare la distribuzione automatica dei processi Web con un progetto Web</span><span class="sxs-lookup"><span data-stu-id="cdf66-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="cdf66-132">Fare clic con il pulsante destro del mouse sul progetto Web in **Esplora soluzioni**, quindi scegliere **Aggiungi** > **Progetto esistente come processo Web di Azure**.</span><span class="sxs-lookup"><span data-stu-id="cdf66-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Progetto esistente come processo Web Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="cdf66-134">Viene visualizzata la finestra di dialogo [Aggiungi processo Web Azure](#configure) .</span><span class="sxs-lookup"><span data-stu-id="cdf66-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="cdf66-135">Nell'elenco a discesa **Nome progetto** selezionare il progetto di applicazione console da aggiungere come processo Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Selezione del progetto nella finestra di dialogo Aggiungi processo Web Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="cdf66-137">Completare la finestra di dialogo [Aggiungi processo Web Azure](#configure) , quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdf66-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="cdf66-138"><a id="convertnolink"></a> Abilitare la distribuzione dei processi Web senza un progetto Web</span><span class="sxs-lookup"><span data-stu-id="cdf66-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="cdf66-139">Fare clic con il pulsante destro del mouse sul progetto di applicazione console in **Esplora soluzioni** e quindi scegliere **Pubblica come processo Web Azure...**.</span><span class="sxs-lookup"><span data-stu-id="cdf66-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Pubblica come processo Web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="cdf66-141">Viene visualizzata la finestra di dialogo [Aggiungi processo Web Azure](#configure) con il progetto selezionato nella casella **Nome progetto** .</span><span class="sxs-lookup"><span data-stu-id="cdf66-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="cdf66-142">Completare la finestra di dialogo [Aggiungi processo Web Azure](#configure) , quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdf66-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="cdf66-143">Viene visualizzata la procedura guidata **Pubblica sito Web** .</span><span class="sxs-lookup"><span data-stu-id="cdf66-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="cdf66-144">Se non si vuole eseguire subito la pubblicazione, chiudere la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="cdf66-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="cdf66-145">Le impostazioni immesse vengono salvate in modo da poter essere usate quando si vuole [distribuire il progetto](#deploy).</span><span class="sxs-lookup"><span data-stu-id="cdf66-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="cdf66-146"><a id="create"></a>Creare un nuovo progetto abilitato per i processi Web</span><span class="sxs-lookup"><span data-stu-id="cdf66-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="cdf66-147">Per creare un nuovo progetto abilitato per i processi Web, è possibile usare il modello del progetto di applicazione console e abilitare la distribuzione dei processi Web come descritto nella [sezione precedente](#convert).</span><span class="sxs-lookup"><span data-stu-id="cdf66-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="cdf66-148">In alternativa, è possibile usare il modello nuovo-progetto di processi Web:</span><span class="sxs-lookup"><span data-stu-id="cdf66-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="cdf66-149">Usare il modello nuovo-progetto di processi Web per un processo Web indipendente</span><span class="sxs-lookup"><span data-stu-id="cdf66-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="cdf66-150">Creare un progetto e configurarlo per essere distribuito in modo indipendente come processo Web senza alcun collegamento a un progetto Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="cdf66-151">Usare questa opzione quando si vuole eseguire un processo Web in un'app Web in modo indipendente senza l'esecuzione dell'applicazione Web nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="cdf66-152">Questa opzione potrebbe essere utile per scalare le risorse del processo Web indipendentemente dalle risorse dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="cdf66-153">Usare il modello nuovo-progetto di processi Web per un processo Web collegato a un progetto Web</span><span class="sxs-lookup"><span data-stu-id="cdf66-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="cdf66-154">Creare un progetto configurato in modo da essere distribuito automaticamente come processo Web quando viene distribuito un progetto Web nella stessa soluzione.</span><span class="sxs-lookup"><span data-stu-id="cdf66-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="cdf66-155">Usare questa opzione quando si vuole eseguire il processo Web nella stessa app Web in cui viene eseguita l'applicazione Web correlata.</span><span class="sxs-lookup"><span data-stu-id="cdf66-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="cdf66-156">Il modello new-project di Processi Web installa automaticamente pacchetti NuGet e in *Program.cs* include codice per [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="cdf66-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="cdf66-157">Se non si vuole usare WebJobs SDK, rimuovere o modificare l'istruzione `host.RunAndBlock` in *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="cdf66-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="cdf66-158"><a id="createnolink"></a> Usare il modello nuovo-progetto di processi Web per un processo Web indipendente</span><span class="sxs-lookup"><span data-stu-id="cdf66-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="cdf66-159">Fare clic su **File** > **Nuovo progetto** e quindi nella finestra di dialogo **Nuovo progetto** fare clic su **Cloud** > **Processo Web Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="cdf66-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Finestra di dialogo Nuovo progetto con il modello processo Web](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="cdf66-161">Seguire le istruzioni illustrate in precedenza per [rendere il progetto di applicazione console un progetto processi Web indipendente](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="cdf66-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="cdf66-162"><a id="createlink"></a> Usare il modello nuovo-progetto di processi Web per un processo Web collegato a un progetto Web</span><span class="sxs-lookup"><span data-stu-id="cdf66-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="cdf66-163">Fare clic con il pulsante destro del mouse sul progetto Web in **Esplora soluzioni**, quindi scegliere **Aggiungi** > **Nuovo progetto processo Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="cdf66-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Voce del menu Nuovo progetto processo Web Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="cdf66-165">Viene visualizzata la finestra di dialogo [Aggiungi processo Web Azure](#configure) .</span><span class="sxs-lookup"><span data-stu-id="cdf66-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="cdf66-166">Completare la finestra di dialogo [Aggiungi processo Web Azure](#configure) , quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdf66-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="cdf66-167"><a id="configure"></a>Finestra di dialogo Aggiungi processo Web Azure</span><span class="sxs-lookup"><span data-stu-id="cdf66-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="cdf66-168">La finestra di dialogo **Aggiungi processo Web Azure** consente di immettere il nome del processo Web ed eseguire l'impostazione della modalità per il processo Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Finestra di dialogo Aggiungi processo Web Azure](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="cdf66-170">I campi in questa finestra di dialogo corrispondono ai campi presenti nella finestra di dialogo **Nuovo processo** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdf66-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="cdf66-171">Per ulteriori informazioni, vedere [attività in Background eseguito con WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="cdf66-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="cdf66-172">Per informazioni sulla distribuzione da riga di comando, vedere [Abilitazione della riga di comando o del recapito continuo di processi Web Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="cdf66-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="cdf66-173">Se si distribuisce un processo Web e si desidera modificare il tipo di processo Web e ridistribuire, è necessario eliminare il file settings.json webjobs di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="cdf66-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="cdf66-174">In questo modo Visual Studio Mostra le opzioni di pubblicazione, è possibile modificare il tipo di processo Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="cdf66-175">Se si distribuisce un processo Web e successivamente si modifica la modalità di esecuzione da continua a non continua o viceversa, Visual Studio crea un nuovo processo Web in Azure quando si esegue nuovamente la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cdf66-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="cdf66-176">Se si modificano le altre impostazioni di pianificazione lasciando invariata la modalità di esecuzione o passando dalla modalità pianificata a quella su richiesta o viceversa, Visual Studio aggiorna il processo esistente anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="cdf66-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="cdf66-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="cdf66-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="cdf66-178">Quando si configura un'applicazione console per la distribuzione dei processi Web, Visual Studio installa il pacchetto NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) e archivia le informazioni di pianificazione in un file *webjob-publish-settings.json* nella cartella *Proprietà* del progetto processi Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="cdf66-179">Di seguito è riportato un esempio di tale file:</span><span class="sxs-lookup"><span data-stu-id="cdf66-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="cdf66-180">È possibile modificare questo file direttamente e Visual Studio fornisce IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="cdf66-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="cdf66-181">Lo schema del file viene archiviato in [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) da dove può essere visualizzato.</span><span class="sxs-lookup"><span data-stu-id="cdf66-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="cdf66-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="cdf66-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="cdf66-183">Quando si collega un progetto abilitato per i processi Web a un progetto Web, Visual Studio archivia il nome del progetto processi Web in un file *webjobs-list.json* nella cartella *Proprietà* del progetto Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="cdf66-184">L'elenco potrebbe contenere più progetti processi Web, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="cdf66-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

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

<span data-ttu-id="cdf66-185">È possibile modificare questo file direttamente e Visual Studio fornisce IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="cdf66-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="cdf66-186">Lo schema del file viene archiviato in [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) da dove può essere visualizzato.</span><span class="sxs-lookup"><span data-stu-id="cdf66-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="cdf66-187"><a id="deploy"></a>Distribuire un progetto processi Web</span><span class="sxs-lookup"><span data-stu-id="cdf66-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="cdf66-188">Un progetto processi Web collegato a un progetto Web viene distribuito automaticamente con il progetto Web.</span><span class="sxs-lookup"><span data-stu-id="cdf66-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="cdf66-189">Per informazioni sulla distribuzione dei progetti Web, vedere [Come distribuire su App Web](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="cdf66-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="cdf66-190">Per distribuire un progetto processi Web indipendente, fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni**, quindi scegliere **Pubblica come processo Web Azure...**.</span><span class="sxs-lookup"><span data-stu-id="cdf66-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Pubblica come processo Web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="cdf66-192">Per un processo Web indipendente viene visualizzata la stessa procedura guidata **Pubblica sito Web** usata per i progetti Web ma con meno impostazioni disponibili da modificare.</span><span class="sxs-lookup"><span data-stu-id="cdf66-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="cdf66-193"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cdf66-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="cdf66-194">Questo articolo ha descritto come distribuire processi Web tramite Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdf66-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="cdf66-195">Per altre informazioni su come distribuire Processi Web di Azure, vedere [Risorse di documentazione di Processi Web di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="cdf66-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

