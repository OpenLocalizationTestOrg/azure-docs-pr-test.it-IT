---
title: una pipeline CI/CD-ROM in Azure con Team Services aaaCreate | Documenti Microsoft
description: Informazioni su come pipeline di toocreate un Visual Studio Team Services per l'integrazione continua e recapito che distribuisce un tooIIS app web in una macchina virtuale Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="b7d1f-103">Creare una pipeline di integrazione continua con Visual Studio Team Services e IIS</span><span class="sxs-lookup"><span data-stu-id="b7d1f-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="b7d1f-104">tooautomate hello compilazione, test e le fasi di distribuzione dello sviluppo di applicazioni, è possibile utilizzare un'integrazione continua e la pipeline di distribuzione (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="b7d1f-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="b7d1f-105">In questa esercitazione viene creata una pipeline CI/CD tramite Visual Studio Team Services e una macchina virtuale Windows in Azure che esegue IIS.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="b7d1f-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b7d1f-107">Pubblicare un progetto di Team Services tooa applicazione web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b7d1f-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="b7d1f-108">creare una definizione di compilazione che viene attivata dal commit del codice</span><span class="sxs-lookup"><span data-stu-id="b7d1f-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="b7d1f-109">installare e configurare IIS su una macchina virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="b7d1f-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="b7d1f-110">Aggiungi gruppo di distribuzione tooa istanze IIS hello in Team Services</span><span class="sxs-lookup"><span data-stu-id="b7d1f-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="b7d1f-111">Creare un nuovo web toopublish definizione versione distribuire pacchetti tooIIS</span><span class="sxs-lookup"><span data-stu-id="b7d1f-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="b7d1f-112">Testare hello CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="b7d1f-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="b7d1f-113">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="b7d1f-114">Eseguire `Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="b7d1f-115">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b7d1f-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="b7d1f-116">Creare un progetto in Team Services</span><span class="sxs-lookup"><span data-stu-id="b7d1f-116">Create project in Team Services</span></span>
<span data-ttu-id="b7d1f-117">Visual Studio Team Services consente per uno sviluppo e una collaborazione facilitata senza mantenere una soluzione di gestione del codice in locale.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="b7d1f-118">Team Services offre i test sul codice cloud, compilazione e informazioni approfondite sull'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="b7d1f-119">È possibile scegliere l'archivio di controllo della versione e l'IDE che meglio si adatta allo sviluppo del codice.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="b7d1f-120">Per questa esercitazione, è possibile utilizzare un account gratuito toocreate un'app web ASP.NET base e pipeline CI/CD-ROM.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="b7d1f-121">Se non si dispone già di un account Team Services, [crearne uno](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="b7d1f-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="b7d1f-122">processo di commit codice hello toomanage, definizioni di compilazione e rilasciare le definizioni, creare un progetto Team Services, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="b7d1f-123">Aprire il dashboard di Team Services in un browser Web e scegliere **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="b7d1f-124">Immettere *myWebApp* per hello **nome progetto**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="b7d1f-125">Lasciare tutti gli altri toouse di valori predefinito *Git* controllo della versione e *Agile* processo elemento di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="b7d1f-126">Opzione di hello troppo**condividere con** *i membri del Team*, quindi selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="b7d1f-127">Dopo aver creato il progetto, scegliere opzione hello troppo**inizializzare con un file Leggimi o gitignore**, quindi **inizializzare**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="b7d1f-128">All'interno del nuovo progetto, scegliere **dashboard** in alto di hello, quindi selezionare **aperta in Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="b7d1f-129">Creare un'applicazione Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b7d1f-129">Create ASP.NET web application</span></span>
<span data-ttu-id="b7d1f-130">Nel passaggio precedente hello, è stato creato un progetto Team Services.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="b7d1f-131">passaggio finale Hello apre il nuovo progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="b7d1f-132">Per gestire il commit di codice hello **Team Explorer** finestra.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="b7d1f-133">Creare una copia locale del nuovo progetto, quindi creare un'applicazione Web ASP.NET da un modello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="b7d1f-134">Selezionare **Clone** toocreate un repository git locale del progetto Team Services.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![Clonare l'archivio dal progetto Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="b7d1f-136">In **Soluzioni** selezionare **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-136">Under **Solutions**, select **New**.</span></span>

    ![Creare una soluzione per l'applicazione Web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="b7d1f-138">Selezionare **Web** modelli, quindi scegliere hello **applicazione Web ASP.NET** modello.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="b7d1f-139">Immettere un nome per l'applicazione, ad esempio *myWebApp*e deselezionare la casella di hello per **Crea directory per soluzione**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="b7d1f-140">Se l'opzione hello è disponibile, deselezionare la casella di hello troppo**Aggiungi Application Insights tooproject**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="b7d1f-141">Application Insights, è necessario per l'applicazione web con Azure Application Insights è tooauthorize.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="b7d1f-142">tookeep è semplice in questa esercitazione, ignorare questo processo.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="b7d1f-143">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-143">Select **OK**.</span></span>
4. <span data-ttu-id="b7d1f-144">Scegliere **MVC** dall'elenco di modelli di hello.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="b7d1f-145">Selezionare **Modifica autenticazione**, scegliere **No Authentication** (Nessuna autenticazione), quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="b7d1f-146">Selezionare **OK** toocreate la soluzione.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="b7d1f-147">In hello **Team Explorer** finestra, scegliere **modifiche**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![Eseguire il commit di repository git di servizi tooTeam modifiche locali](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="b7d1f-149">Nella casella di testo hello commit, immettere un messaggio, ad esempio *commit iniziale*.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="b7d1f-150">Scegliere **tutti il Commit e sincronizzazione** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="b7d1f-151">Creare una definizione di compilazione</span><span class="sxs-lookup"><span data-stu-id="b7d1f-151">Create build definition</span></span>
<span data-ttu-id="b7d1f-152">In Team Services, si utilizza un toooutline di definizione di compilazione come l'applicazione deve essere compilato.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="b7d1f-153">In questa esercitazione viene creata una definizione di base che accetta il codice sorgente, compilare la soluzione hello, quindi crea web distribuisce pacchetto è possibile utilizzare toorun hello web app in un server IIS.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="b7d1f-154">Nel progetto Team Services, scegliere **compilazione & versione** in alto di hello, quindi selezionare **compilazioni**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="b7d1f-155">Selezionare **+ Nuova definizione**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="b7d1f-156">Scegliere hello **ASP.NET (anteprima)** modello e selezionare **applica**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="b7d1f-157">Lasciare l'impostazione predefinita, tutti hello i valori delle attività.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-157">Leave all hello default task values.</span></span> <span data-ttu-id="b7d1f-158">In **Ottieni origini**, verificare che hello *myWebApp* repository e *master* branch è selezionato.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Creare la definizione di compilazione nel progetto Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="b7d1f-160">In hello **trigger** spostare hello dispositivo di scorrimento per **attiva trigger** troppo*abilitato*.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="b7d1f-161">Salvare la definizione di compilazione hello e coda di una nuova compilazione selezionando **Salva e coda** , quindi **Salva e coda** nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="b7d1f-162">Lasciare le impostazioni predefinite hello e selezionare **coda**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="b7d1f-163">Espressioni di controllo come compilazione hello viene pianificata su un agente ospitato, quindi avvia toobuild.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="b7d1f-164">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-164">hello output is similar toohello following example:</span></span>

![Completamento della compilazione del progetto Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="b7d1f-166">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b7d1f-166">Create virtual machine</span></span>
<span data-ttu-id="b7d1f-167">tooprovide toorun una piattaforma app web ASP.NET, è necessario che una macchina virtuale di Windows che esegue IIS.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="b7d1f-168">Team Services utilizza toointeract un agente con l'istanza IIS hello come si esegue il commit di codice e vengono attivate le compilazioni.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="b7d1f-169">Creare rapidamente una macchina virtuale Windows Server 2016 tramite [questo esempio di script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b7d1f-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="b7d1f-170">Accetta alcuni minuti per toorun script hello e creare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="b7d1f-171">Dopo aver creato hello macchina virtuale, aprire la porta 80 per il traffico web con [Aggiungi AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="b7d1f-172">tooconnect tooyour macchina virtuale, ottenere l'indirizzo IP pubblico hello con [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="b7d1f-173">Creare una macchina virtuale di tooyour sessione desktop remoto:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="b7d1f-174">In hello macchina virtuale, aprire un **amministratore PowerShell** prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="b7d1f-175">Installare IIS e le funzionalità .NET necessarie come segue:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="b7d1f-176">Creare un gruppo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="b7d1f-176">Create deployment group</span></span>
<span data-ttu-id="b7d1f-177">toopush out web hello server IIS toohello del pacchetto di distribuzione, si definisce un gruppo di distribuzione in Team Services.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="b7d1f-178">Questo gruppo consente toospecify quali server sono hello di nuove compilazioni come si esegue il commit di codice tooTeam servizi e le compilazioni vengono completate.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="b7d1f-179">In Team Services scegliere **Build & Release** (Compilazione e versione) e quindi selezionare **Gruppi di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="b7d1f-180">Scegliere **Aggiungi gruppo di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="b7d1f-181">Immettere un nome per il gruppo di hello, ad esempio *myIIS*, quindi selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="b7d1f-182">In hello **registrare macchine** sezione, verificare *Windows* è selezionata, quindi la casella hello troppo**utilizzare un token di accesso personali nello script hello per l'autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="b7d1f-183">Selezionare **copiare script tooclipboard**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="b7d1f-184">Aggiungere il gruppo di distribuzione di VM IIS toohello</span><span class="sxs-lookup"><span data-stu-id="b7d1f-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="b7d1f-185">Con il gruppo di distribuzione hello creato, aggiungere ogni gruppo toohello istanza IIS.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="b7d1f-186">Team Services genera uno script che scarica e configura un agente su hello macchina virtuale che riceve di nuovo web di distribuire pacchetti che viene quindi applicato tooIIS.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="b7d1f-187">In hello **amministratore PowerShell** sessione nella VM, incollare ed eseguire script hello copiato dal Team Services.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="b7d1f-188">Quando il tag tooconfigure richiesta per l'agente di hello, scegliere *Y* e immettere *web*.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="b7d1f-189">Quando richiesto per l'account utente di hello, premere *restituire* tooaccept hello predefinite.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="b7d1f-190">Attendere hello toofinish di script con un messaggio *vstsagent.account.computername servizio è stato avviato correttamente*.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="b7d1f-191">In hello **gruppi di distribuzione** pagina di hello **compilazione & versione** del menu aprirlo hello *myIIS* gruppo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="b7d1f-192">In hello **macchine** scheda, verificare che la macchina virtuale sia elencata.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![Macchina virtuale è stato aggiunto gruppo di distribuzione di servizi tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="b7d1f-194">Creare una definizione della versione</span><span class="sxs-lookup"><span data-stu-id="b7d1f-194">Create release definition</span></span>
<span data-ttu-id="b7d1f-195">toopublish le compilazioni, si crea una definizione di versione in Team Services.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="b7d1f-196">Questa definizione viene attivata automaticamente dalla corretta compilazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="b7d1f-197">Scegliendo hello distribuzione gruppo toopush pacchetto di distribuzione web e definire le impostazioni di IIS appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="b7d1f-198">Scegliere **Build & Release** (Compilazione e versione), quindi selezionare **Compilazioni**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="b7d1f-199">Scegliere una definizione di compilazione hello creato in un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="b7d1f-200">In **completati di recente**, scegliere la compilazione più recente di hello, quindi selezionare **versione**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="b7d1f-201">Scegliere **Sì** toocreate una definizione di versione.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="b7d1f-202">Scegliere hello **vuoto** modello, quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="b7d1f-203">Verificare la definizione di compilazione progetto e di origine hello vengono popolati con il progetto.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="b7d1f-204">Seleziona hello **distribuzione continua** casella di controllo, quindi selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="b7d1f-205">Selezionare la casella di riepilogo hello troppo Avanti**+ Aggiungi attività** e scegliere *aggiungere una fase di distribuzione gruppo*.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Definizione di attività toorelease componente aggiuntivo di Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="b7d1f-207">Scegliere **Aggiungi** Avanti troppo**Deploy(Preview) App Web di IIS**, quindi selezionare **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="b7d1f-208">Seleziona hello **esecuzione nel gruppo di distribuzione** attività padre.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="b7d1f-209">Per **gruppo distribuzione**, selezionare la distribuzione di hello gruppo creato in precedenza, ad esempio *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="b7d1f-210">In hello **computer tag** , quindi selezionare **Aggiungi** scegliere hello *web* tag.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![Attività del gruppo di distribuzione della definizione di versione per IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="b7d1f-212">Seleziona hello **distribuzione: distribuzione di App Web IIS** tooconfigure attività di IIS istanza impostazioni come segue:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="b7d1f-213">Per **Nome del sito Web**, immettere *Sito Web predefinito*.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="b7d1f-214">Lasciare hello tutte le altre impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="b7d1f-215">Scegliere **Slava**, quindi selezionare **OK** due volte.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="b7d1f-216">Creare e pubblicare una versione</span><span class="sxs-lookup"><span data-stu-id="b7d1f-216">Create a release and publish</span></span>
<span data-ttu-id="b7d1f-217">È ora possibile effettuare il push del pacchetto di distribuzione Web come una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="b7d1f-218">Questo passaggio comunica con l'agente di hello in ogni istanza che fa parte del gruppo di distribuzione hello, inserisce web hello distribuire il pacchetto, quindi Configura applicazione web IIS toorun hello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="b7d1f-219">Nella definizione di versione selezionare **+ Release** (+ Versione), quindi scegliere **Crea versione**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="b7d1f-220">Verificare che la build più recente di hello sia selezionata nell'elenco a discesa hello, insieme a **distribuzione automatizzata: dopo la creazione della versione**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="b7d1f-221">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-221">Select **Create**.</span></span>
3. <span data-ttu-id="b7d1f-222">Un banner di piccole dimensioni viene visualizzata nella parte superiore di hello della definizione di versione, ad esempio *versione 'Versione 1' è stato creato*.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="b7d1f-223">Collegamento di versione di hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-223">Select hello release link.</span></span>
4. <span data-ttu-id="b7d1f-224">Aprire hello **registri** scheda stato versione di hello toowatch.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![Push del pacchetto di distribuzione Web e versione di Team Services corretti](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="b7d1f-226">Una volta completata la versione hello, aprire un web browser e immettere l'indirizzo PIP pubblico hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="b7d1f-227">L'applicazione Web ASP.NET è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-227">Your ASP.NET web application is running.</span></span>

    ![App web ASP.NET in esecuzione sulla macchina virtuale IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="b7d1f-229">Testare hello intero CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="b7d1f-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="b7d1f-230">L'applicazione web in esecuzione in IIS, provare pipeline CI/CD intera hello.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="b7d1f-231">Dopo aver apportato una modifica in Visual Studio e commit viene attivato il codice, una compilazione che quindi attiva una versione del web aggiornata distribuire tooIIS pacchetto:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="b7d1f-232">In Visual Studio, aprire hello **Esplora** finestra.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="b7d1f-233">Passare tooand open *myWebApp | Viste | Home | Cshtml*</span><span class="sxs-lookup"><span data-stu-id="b7d1f-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="b7d1f-234">Modifica riga 6 tooread:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="b7d1f-235">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-235">Save hello file.</span></span>
5. <span data-ttu-id="b7d1f-236">Aprire hello **Team Explorer** finestra, seleziona hello *myWebApp* del progetto, quindi scegliere **modifiche**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="b7d1f-237">Immettere un messaggio di commit, ad esempio *test CI/CD pipeline*, quindi scegliere **tutti i Commit e sincronizzazione** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="b7d1f-238">Nell'area di lavoro di Team Services, viene attivata una nuova compilazione dal commit di codice hello.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="b7d1f-239">Scegliere **Build & Release** (Compilazione e versione), quindi selezionare **Compilazioni**.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="b7d1f-240">Scegliere la definizione di compilazione, quindi selezionare hello **in coda & esecuzione** toowatch compilazione come hello compilare l'avanzamento.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="b7d1f-241">Una volta compilazione hello ha esito positivo, viene attivata una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="b7d1f-242">Scegliere **compilazione & versione**, quindi **versioni** pacchetto inserito tooyour VM IIS di distribuzione web di hello toosee.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="b7d1f-243">Seleziona hello **aggiornamento** stato hello tooupdate di icona.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="b7d1f-244">Quando hello *ambienti* colonna viene visualizzato un segno di spunta verde, versione di hello è distribuita correttamente tooIIS.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="b7d1f-245">applicare le modifiche toosee, aggiornare il sito Web IIS in un browser.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![App web ASP.NET in esecuzione sulla macchina virtuale IIS dalla pipeline CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="b7d1f-247">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7d1f-247">Next steps</span></span>

<span data-ttu-id="b7d1f-248">In questa esercitazione è creata un'applicazione web ASP.NET in Team Services e compilazione configurata e versione definizioni toodeploy nuova distribuzione web tooIIS di pacchetti in ogni caso di commit di codice.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="b7d1f-249">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="b7d1f-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b7d1f-250">Pubblicare un progetto di Team Services tooa applicazione web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b7d1f-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="b7d1f-251">creare una definizione di compilazione che viene attivata dal commit del codice</span><span class="sxs-lookup"><span data-stu-id="b7d1f-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="b7d1f-252">installare e configurare IIS su una macchina virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="b7d1f-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="b7d1f-253">Aggiungi gruppo di distribuzione tooa istanze IIS hello in Team Services</span><span class="sxs-lookup"><span data-stu-id="b7d1f-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="b7d1f-254">Creare un nuovo web toopublish definizione versione distribuire pacchetti tooIIS</span><span class="sxs-lookup"><span data-stu-id="b7d1f-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="b7d1f-255">Testare hello CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="b7d1f-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="b7d1f-256">Spostare toolearn esercitazione successiva toohello come toosecure un server web con i certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="b7d1f-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b7d1f-257">Secure web server with SSL (Proteggere il server Web con SSL)</span><span class="sxs-lookup"><span data-stu-id="b7d1f-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)