---
title: Comandi di PowerShell basati su Azure Resource Manager per app Web di Azure | Documentazione Microsoft
description: Informazioni su come usare i nuovi comandi di PowerShell basati su Azure Resource Manager per la gestione delle app Web di Azure.
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
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="53848-103">Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="53848-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="53848-104">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="53848-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="53848-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="53848-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="53848-106">Con Microsoft Azure PowerShell versione 1.0.0 sono stati aggiunti nuovi comandi che offrono all'utente la possibilità di usare comandi di PowerShell basati su Azure Resource Manager per gestire app Web.</span><span class="sxs-lookup"><span data-stu-id="53848-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="53848-107">Per informazioni sulla gestione di gruppi di risorse, vedere [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="53848-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="53848-108">Per l'elenco completo dei parametri e delle opzioni per i cmdlet di PowerShell, vedere le [informazioni di riferimento complete per i cmdlet di PowerShell basati su Azure Resource Manager per le app Web](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="53848-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="53848-109">Gestione di piani di servizio app</span><span class="sxs-lookup"><span data-stu-id="53848-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="53848-110">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="53848-110">Create an App Service Plan</span></span>
<span data-ttu-id="53848-111">Per creare un piano di servizio app, usare il cmdlet **New-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="53848-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="53848-112">Di seguito sono riportate le descrizioni dei diversi parametri.</span><span class="sxs-lookup"><span data-stu-id="53848-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="53848-113">**Name**: nome del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="53848-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="53848-114">**Location**: località del piano di servizio.</span><span class="sxs-lookup"><span data-stu-id="53848-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="53848-115">**ResourceGroupName**: gruppo di risorse che include il piano di servizio app appena creato.</span><span class="sxs-lookup"><span data-stu-id="53848-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="53848-116">**Tier**: piano tariffario desiderato. Il valore predefinito è Free, le altre opzioni sono Shared, Basic, Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="53848-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="53848-117">**WorkerSize**: dimensioni dei ruoli di lavoro. Se il parametro Tier specificato è Basic, Standard o Premium, il valore predefinito è small.</span><span class="sxs-lookup"><span data-stu-id="53848-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="53848-118">Le altre opzioni sono Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="53848-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="53848-119">**NumberofWorkers**: numero di ruoli di lavoro nel piano di servizio app. Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="53848-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="53848-120">Esempio di uso del cmdlet:</span><span class="sxs-lookup"><span data-stu-id="53848-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="53848-121">Creare un piano di servizio app in un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="53848-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="53848-122">Per creare un piano di servizio app in un ambiente del servizio app, usare lo stesso comando **New-AzureRmAppServicePlan** con parametri aggiuntivi per specificare il nome dell'ambiente del servizio app e il nome del gruppo di risorse dell'ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="53848-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="53848-123">Esempio di uso del cmdlet:</span><span class="sxs-lookup"><span data-stu-id="53848-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="53848-124">Per altre informazioni sull'ambiente del servizio app, vedere [Introduzione all'ambiente del servizio app](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="53848-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="53848-125">Visualizzare un elenco dei piani di servizio app esistenti</span><span class="sxs-lookup"><span data-stu-id="53848-125">List Existing App Service Plans</span></span>
<span data-ttu-id="53848-126">Per visualizzare un elenco dei piani di servizio app esistenti, usare il cmdlet **Get-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="53848-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="53848-127">Per visualizzare un elenco di tutti i piani di servizio app della propria sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="53848-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="53848-128">Per visualizzare un elenco di tutti i piani di servizio app di uno specifico gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="53848-129">Per ottenere un piano di servizio app specifico, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="53848-130">Configurare un piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="53848-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="53848-131">Per modificare le impostazioni di un piano di servizio app esistente, usare il cmdlet **Set-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="53848-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="53848-132">È possibile modificare il piano tariffario e il numero e le dimensioni dei ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="53848-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="53848-133">Ridimensionamento di un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="53848-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="53848-134">Per ridimensionare un piano di servizio app esistente, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="53848-135">Modifica delle dimensioni dei ruoli di lavoro in un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="53848-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="53848-136">Per modificare le dimensioni dei ruoli di lavoro in un piano di servizio app esistente, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="53848-137">Modifica del piano tariffario di un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="53848-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="53848-138">Per modificare il piano tariffario di un piano di servizio app esistente, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="53848-139">Eliminare un piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="53848-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="53848-140">Per eliminare un piano di servizio app esistente, è prima di tutto necessario spostare o eliminare tutte le app Web assegnate.</span><span class="sxs-lookup"><span data-stu-id="53848-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="53848-141">Usando il cmdlet **Remove-AzureRmAppServicePlan** è quindi possibile eliminare il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="53848-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="53848-142">Gestione di app Web del servizio app</span><span class="sxs-lookup"><span data-stu-id="53848-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="53848-143">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="53848-143">Create a Web App</span></span>
<span data-ttu-id="53848-144">Per creare un'app Web, usare il cmdlet **New-AzureRmWebApp**.</span><span class="sxs-lookup"><span data-stu-id="53848-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="53848-145">Di seguito sono riportate le descrizioni dei diversi parametri.</span><span class="sxs-lookup"><span data-stu-id="53848-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="53848-146">**Name**: nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="53848-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="53848-147">**AppServicePlan**: nome del piano di servizio usato per l'hosting dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="53848-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="53848-148">**ResourceGroupName**: gruppo di risorse che ospita il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="53848-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="53848-149">**Location**: località dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="53848-149">**Location**: the web app location.</span></span>

<span data-ttu-id="53848-150">Esempio di uso del cmdlet:</span><span class="sxs-lookup"><span data-stu-id="53848-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="53848-151">Creare un'app Web in un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="53848-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="53848-152">Per creare un'app Web in un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="53848-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="53848-153">Usare lo stesso comando **New-AzureRmWebApp** con parametri aggiuntivi per specificare il nome dell'ambiente del servizio app e il nome del gruppo di risorse a cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="53848-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="53848-154">Per altre informazioni sull'ambiente del servizio app, vedere [Introduzione all'ambiente del servizio app](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="53848-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="53848-155">Eliminare un'app Web esistente</span><span class="sxs-lookup"><span data-stu-id="53848-155">Delete an existing Web App</span></span>
<span data-ttu-id="53848-156">Per eliminare un'app Web esistente, è possibile usare il cmdlet **Remove-AzureRmWebApp**. È necessario specificare il nome dell'app Web e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="53848-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="53848-157">Visualizzare un elenco delle app Web esistenti</span><span class="sxs-lookup"><span data-stu-id="53848-157">List existing Web Apps</span></span>
<span data-ttu-id="53848-158">Per visualizzare un elenco delle app Web esistenti, usare il cmdlet **Get-AzureRmWebApp** .</span><span class="sxs-lookup"><span data-stu-id="53848-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="53848-159">Per visualizzare un elenco di tutte le app Web della propria sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="53848-160">Per visualizzare un elenco di tutte le app Web di uno specifico gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="53848-161">Per ottenere un'app Web specifica, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="53848-162">Configurare un'app Web esistente</span><span class="sxs-lookup"><span data-stu-id="53848-162">Configure an existing Web App</span></span>
<span data-ttu-id="53848-163">Per modificare le impostazioni e le configurazioni di un'app Web esistente, usare il cmdlet **Set-AzureRmWebApp** .</span><span class="sxs-lookup"><span data-stu-id="53848-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="53848-164">Per un elenco completo dei parametri, vedere le [informazioni di riferimento sul cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="53848-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="53848-165">Esempio (1): usare il cmdlet per modificare le stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="53848-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="53848-166">Esempio (2): aggiungere o modificare le impostazioni dell'app</span><span class="sxs-lookup"><span data-stu-id="53848-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="53848-167">Esempio (3): impostare l'app Web per l'esecuzione in modalità a 64 bit</span><span class="sxs-lookup"><span data-stu-id="53848-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="53848-168">Modificare lo stato di un'app Web esistente</span><span class="sxs-lookup"><span data-stu-id="53848-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="53848-169">Riavviare un'app Web</span><span class="sxs-lookup"><span data-stu-id="53848-169">Restart a web app</span></span>
<span data-ttu-id="53848-170">Per riavviare un'app Web, è necessario specificare il nome e il gruppo di risorse dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="53848-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="53848-171">Arrestare un'app Web</span><span class="sxs-lookup"><span data-stu-id="53848-171">Stop a web app</span></span>
<span data-ttu-id="53848-172">Per arrestare un'app Web, è necessario specificare il nome e il gruppo di risorse dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="53848-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="53848-173">Avviare un'app Web</span><span class="sxs-lookup"><span data-stu-id="53848-173">Start a web app</span></span>
<span data-ttu-id="53848-174">Per avviare un'app Web, è necessario specificare il nome e il gruppo di risorse dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="53848-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="53848-175">Gestire i profili di pubblicazione delle app Web</span><span class="sxs-lookup"><span data-stu-id="53848-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="53848-176">Ogni app Web ha un profilo di pubblicazione che può essere usato per pubblicare le app. Sui profili di pubblicazione possono essere eseguite alcune operazioni.</span><span class="sxs-lookup"><span data-stu-id="53848-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="53848-177">Recuperare il profilo di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="53848-177">Get Publishing Profile</span></span>
<span data-ttu-id="53848-178">Per recuperare il profilo di pubblicazione di un'app Web, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="53848-179">Questo comando restituisce il profilo di pubblicazione sia nella riga di comando che in un file di testo.</span><span class="sxs-lookup"><span data-stu-id="53848-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="53848-180">Reimpostare il profilo di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="53848-180">Reset Publishing Profile</span></span>
<span data-ttu-id="53848-181">Per reimpostare la password di pubblicazione per la distribuzione FTP e Web di un'app Web, usare:</span><span class="sxs-lookup"><span data-stu-id="53848-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="53848-182">Gestire i certificati delle app Web</span><span class="sxs-lookup"><span data-stu-id="53848-182">Manage Web App Certificates</span></span>
<span data-ttu-id="53848-183">Per informazioni sulla gestione dei certificati delle app Web, vedere l'articolo relativo all' [associazione di certificati SSL con PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="53848-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="53848-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="53848-184">Next Steps</span></span>
* <span data-ttu-id="53848-185">Per informazioni sul supporto di PowerShell per Azure Resource Manager, vedere [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="53848-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="53848-186">Per informazioni sugli ambienti del servizio app, vedere [Introduzione all'ambiente del servizio app](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="53848-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="53848-187">Per informazioni sulla gestione dei certificati SSL del servizio app con PowerShell, vedere l'articolo relativo all' [associazione di certificati SSL con PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="53848-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="53848-188">Per l'elenco completo dei cmdlet di PowerShell basati su Azure Resource Manager per le app Web di Azure, vedere le [informazioni di riferimento](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="53848-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="53848-189">Per altre informazioni sulla gestione del servizio app mediante l'interfaccia della riga di comando, vedere [Using Azure Resource Manager-Based XPlat CLI for Azure Web App](app-service-web-app-azure-resource-manager-xplat-cli.md) (Uso dell'interfaccia della riga di comando di XPlat basata su Azure Resource Manager per le app Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="53848-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

