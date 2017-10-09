---
title: i comandi aaaAzure basate su Gestione risorse di PowerShell per App Web di Azure | Documenti Microsoft
description: Informazioni su come toouse hello toomanage di comandi basati su Gestione risorse di Azure PowerShell nuova App Web di Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="20286-103">Uso di PowerShell Azure Resource Manager-Based tooManage Azure Web App</span><span class="sxs-lookup"><span data-stu-id="20286-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20286-104">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="20286-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="20286-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="20286-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="20286-106">Con Microsoft Azure PowerShell versione 1.0.0 sono stati aggiunti nuovi comandi, in modo da fornire hello utente hello possibilità toouse basate su Gestione risorse di Azure PowerShell comandi toomanage App Web.</span><span class="sxs-lookup"><span data-stu-id="20286-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="20286-107">toolearn sulla gestione dei gruppi di risorse, vedere [tramite Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="20286-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="20286-108">toolearn sull'elenco completo di hello dei parametri e le opzioni di hello i cmdlet di PowerShell, vedere hello [completo riferimento ai Cmdlet basato su Web App Azure Resource Manager Cmdlets di PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="20286-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="20286-109">Gestione di piani di servizio app</span><span class="sxs-lookup"><span data-stu-id="20286-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="20286-110">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="20286-110">Create an App Service Plan</span></span>
<span data-ttu-id="20286-111">toocreate un piano di servizio app, usare hello **New AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20286-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="20286-112">Di seguito sono le descrizioni dei parametri diversi hello:</span><span class="sxs-lookup"><span data-stu-id="20286-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="20286-113">**Nome**: nome del piano di servizio app hello.</span><span class="sxs-lookup"><span data-stu-id="20286-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="20286-114">**Location**: località del piano di servizio.</span><span class="sxs-lookup"><span data-stu-id="20286-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="20286-115">**ResourceGroupName**: gruppo di risorse che include il piano di servizio app hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="20286-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="20286-116">**Livello**: hello desiderato piano tariffario (valore predefinito è gratuito, altre opzioni sono condiviso, Basic, Standard e Premium).</span><span class="sxs-lookup"><span data-stu-id="20286-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="20286-117">**WorkerSize**: hello dimensioni di processi di lavoro (impostazione predefinita è piccola se è stato specificato il parametro di livello hello come Basic, Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="20286-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="20286-118">Le altre opzioni sono Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="20286-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="20286-119">**Il numero di lavori**: hello numero di thread di lavoro nel piano di servizio app hello (valore predefinito è 1).</span><span class="sxs-lookup"><span data-stu-id="20286-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="20286-120">Esempio toouse questo cmdlet:</span><span class="sxs-lookup"><span data-stu-id="20286-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="20286-121">Creare un piano di servizio app in un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="20286-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="20286-122">toocreate piano di servizio app in un ambiente del servizio app, utilizzare hello stesso comando **New AzureRmAppServicePlan** con hello toospecify parametri aggiuntivi del ASE nome e il nome del gruppo di risorse di base.</span><span class="sxs-lookup"><span data-stu-id="20286-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="20286-123">Esempio toouse questo cmdlet:</span><span class="sxs-lookup"><span data-stu-id="20286-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="20286-124">altre informazioni sull'ambiente del servizio app, controllo toolearn [tooApp introduzione dell'ambiente del servizio](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="20286-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="20286-125">Visualizzare un elenco dei piani di servizio app esistenti</span><span class="sxs-lookup"><span data-stu-id="20286-125">List Existing App Service Plans</span></span>
<span data-ttu-id="20286-126">Utilizzare toolist hello esistente piani di servizio app, **Get AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20286-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="20286-127">toolist tutti i piani di servizio app nella sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="20286-128">toolist tutti i piani di servizio app in un gruppo di risorse specifico, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="20286-129">tooget un piano di servizio app specifica, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="20286-130">Configurare un piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="20286-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="20286-131">toochange hello impostazioni per un piano di servizio app esistente, utilizzare hello **Set AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20286-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="20286-132">È possibile modificare il livello di hello, dimensione di lavoro e il numero di lavori hello</span><span class="sxs-lookup"><span data-stu-id="20286-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="20286-133">Ridimensionamento di un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="20286-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="20286-134">tooscale un esistente piano di servizio App, usare:</span><span class="sxs-lookup"><span data-stu-id="20286-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="20286-135">Modifica delle dimensioni di lavoro hello di un piano di servizio App</span><span class="sxs-lookup"><span data-stu-id="20286-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="20286-136">dimensioni di hello toochange di processi di lavoro in un App servizio piano esistente, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="20286-137">Modifica hello a livello di un piano di servizio App</span><span class="sxs-lookup"><span data-stu-id="20286-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="20286-138">livello di hello toochange di un App servizio piano esistente, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="20286-139">Eliminare un piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="20286-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="20286-140">toodelete un piano di servizio app esistente, tutti assegnati web App necessità toobe spostati o eliminati per primi.</span><span class="sxs-lookup"><span data-stu-id="20286-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="20286-141">Utilizzando quindi hello **Remove AzureRmAppServicePlan** cmdlet è possibile eliminare il piano di servizio app hello.</span><span class="sxs-lookup"><span data-stu-id="20286-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="20286-142">Gestione di app Web del servizio app</span><span class="sxs-lookup"><span data-stu-id="20286-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="20286-143">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="20286-143">Create a Web App</span></span>
<span data-ttu-id="20286-144">toocreate un'app web, utilizzare hello **New AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20286-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="20286-145">Di seguito sono le descrizioni dei parametri diversi hello:</span><span class="sxs-lookup"><span data-stu-id="20286-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="20286-146">**Nome**: nome per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="20286-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="20286-147">**AppServicePlan**: assegnare un nome per il piano di servizio hello utilizzato toohost hello web app.</span><span class="sxs-lookup"><span data-stu-id="20286-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="20286-148">**ResourceGroupName**: gruppo di risorse che ospita il piano di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="20286-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="20286-149">**Percorso**: hello percorso app web.</span><span class="sxs-lookup"><span data-stu-id="20286-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="20286-150">Esempio toouse questo cmdlet:</span><span class="sxs-lookup"><span data-stu-id="20286-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="20286-151">Creare un'app Web in un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="20286-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="20286-152">toocreate un'app web in un ambiente di servizio App (ASE).</span><span class="sxs-lookup"><span data-stu-id="20286-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="20286-153">Utilizzare hello stesso **New AzureRmWebApp** comando con parametri aggiuntivi toospecify hello ASE nome e il nome di gruppo di risorse hello hello ASE a cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="20286-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="20286-154">altre informazioni sull'ambiente del servizio app, controllo toolearn [tooApp introduzione dell'ambiente del servizio](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="20286-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="20286-155">Eliminare un'app Web esistente</span><span class="sxs-lookup"><span data-stu-id="20286-155">Delete an existing Web App</span></span>
<span data-ttu-id="20286-156">un'app web esistente, è possibile utilizzare hello toodelete **Remove AzureRmWebApp** cmdlet, è necessario toospecify hello nome dell'app web hello e il nome del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="20286-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="20286-157">Visualizzare un elenco delle app Web esistenti</span><span class="sxs-lookup"><span data-stu-id="20286-157">List existing Web Apps</span></span>
<span data-ttu-id="20286-158">toolist hello esistente nelle App web, utilizzare hello **Get AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20286-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="20286-159">toolist tutte le app web nella sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="20286-160">toolist tutte le app web in un gruppo di risorse specifico, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="20286-161">tooget un'applicazione web specifica, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="20286-162">Configurare un'app Web esistente</span><span class="sxs-lookup"><span data-stu-id="20286-162">Configure an existing Web App</span></span>
<span data-ttu-id="20286-163">toochange hello impostazioni e configurazioni per un'app web esistente, utilizzare hello **Set AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20286-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="20286-164">Per un elenco completo dei parametri, controllare hello [collegamento di riferimento di Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="20286-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="20286-165">Esempio (1): utilizzare questo cmdlet toochange le stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="20286-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="20286-166">Esempio (2): aggiungere o modificare le impostazioni dell'app</span><span class="sxs-lookup"><span data-stu-id="20286-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="20286-167">Esempio (3): impostare hello web app toorun in modalità a 64 bit</span><span class="sxs-lookup"><span data-stu-id="20286-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="20286-168">Modifica dello stato di hello di un'App Web esistente</span><span class="sxs-lookup"><span data-stu-id="20286-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="20286-169">Riavviare un'app Web</span><span class="sxs-lookup"><span data-stu-id="20286-169">Restart a web app</span></span>
<span data-ttu-id="20286-170">toorestart un'app web, è necessario specificare hello nome e risorsa gruppo di hello web app.</span><span class="sxs-lookup"><span data-stu-id="20286-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="20286-171">Arrestare un'app Web</span><span class="sxs-lookup"><span data-stu-id="20286-171">Stop a web app</span></span>
<span data-ttu-id="20286-172">toostop un'app web, è necessario specificare hello nome e risorsa gruppo di hello web app.</span><span class="sxs-lookup"><span data-stu-id="20286-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="20286-173">Avviare un'app Web</span><span class="sxs-lookup"><span data-stu-id="20286-173">Start a web app</span></span>
<span data-ttu-id="20286-174">toostart un'app web, è necessario specificare hello nome e risorsa gruppo di hello web app.</span><span class="sxs-lookup"><span data-stu-id="20286-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="20286-175">Gestire i profili di pubblicazione delle app Web</span><span class="sxs-lookup"><span data-stu-id="20286-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="20286-176">Ciascuna applicazione web dispone di un profilo di pubblicazione che può essere utilizzati toopublish App, è possibile eseguire diverse operazioni in profili di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="20286-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="20286-177">Recuperare il profilo di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="20286-177">Get Publishing Profile</span></span>
<span data-ttu-id="20286-178">hello tooget pubblicazione profilo per un'app web, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="20286-179">Questo comando esegue l'eco dell'output di hello pubblicazione profilo toohello riga di comando e hello file di testo tooa profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="20286-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="20286-180">Reimpostare il profilo di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="20286-180">Reset Publishing Profile</span></span>
<span data-ttu-id="20286-181">tooreset entrambi hello la password di pubblicazione per FTP e distribuzione web per un'app web, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="20286-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="20286-182">Gestire i certificati delle app Web</span><span class="sxs-lookup"><span data-stu-id="20286-182">Manage Web App Certificates</span></span>
<span data-ttu-id="20286-183">toolearn sulle procedure toomanage web i certificati di app, vedere [binding a certificati SSL con PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="20286-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="20286-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20286-184">Next Steps</span></span>
* <span data-ttu-id="20286-185">toolearn sul supporto di gestione risorse di Azure PowerShell, vedere [tramite Azure PowerShell con Gestione risorse di Azure.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="20286-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="20286-186">toolearn sugli ambienti di servizio App, vedere [tooApp introduzione dell'ambiente del servizio.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="20286-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="20286-187">toolearn sulla gestione dei certificati SSL del servizio App tramite PowerShell, vedere [binding a certificati SSL tramite PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="20286-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="20286-188">toolearn sull'elenco completo di hello basate su Gestione risorse di Azure di cmdlet di PowerShell per le app Web di Azure, vedere [riferimento ai Cmdlet di Azure Web App Azure Resource Manager Cmdlets di PowerShell.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="20286-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="20286-189">toolearn sulla gestione del servizio App usando l'interfaccia CLI, vedere [Using Azure Resource Manager-Based XPlat CLI per l'App Web di Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="20286-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

