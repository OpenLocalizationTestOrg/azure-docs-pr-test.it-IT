---
title: Strumenti da riga di comando multipiattaforma basati su Azure Resource Manager per app Web di Azure | Documentazione Microsoft
description: Informazioni su come usare i nuovi strumenti da riga di comando multipiattaforma basati su Azure Resource Manager per la gestione delle app Web di Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="6c8e2-103">Utilizzo dell'interfaccia della riga di comando multipiattaforma basata su Azure Resource Manager per servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="6c8e2-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c8e2-104">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6c8e2-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="6c8e2-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c8e2-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="6c8e2-106">Nella versione 0.10.5 degli strumenti da riga di comando multipiattaforma di Microsoft Azure sono stati aggiunti nuovi comandi</span><span class="sxs-lookup"><span data-stu-id="6c8e2-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="6c8e2-107">che offrono all'utente la possibilità di usare comandi di PowerShell basati su Azure Resource Manager per gestire il servizio app.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="6c8e2-108">Per altre informazioni sulla gestione dei gruppi di risorse, vedere [Usare l'interfaccia della riga di comando di Azure per gestire risorse e gruppi di risorse](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6c8e2-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="6c8e2-109">Si può anche usare l'[interfaccia della riga di comando di Azure 2.0 ](https://github.com/Azure/azure-cli), vale a dire un'interfaccia della riga di comando di nuova generazione in Python per il modello di distribuzione di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="6c8e2-110">Gestione di piani di servizio app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="6c8e2-111">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-111">Create an App Service Plan</span></span>
<span data-ttu-id="6c8e2-112">Per creare un piano di servizio app, usare il comando **azure appserviceplan create**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="6c8e2-113">Di seguito sono riportate le descrizioni dei diversi parametri.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="6c8e2-114">**--resource-group**: gruppo di risorse che include il piano di servizio app appena creato.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="6c8e2-115">**--name**: nome del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="6c8e2-116">**--location**: località del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="6c8e2-117">**--sku**:  sku di prezzo desiderato (le opzioni sono: F1 (Gratuito).</span><span class="sxs-lookup"><span data-stu-id="6c8e2-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="6c8e2-118">D1 (Condiviso),</span><span class="sxs-lookup"><span data-stu-id="6c8e2-118">D1 (Shared).</span></span> <span data-ttu-id="6c8e2-119">B1 (Basic Small), B2 (Basic Medium), B3 (Basic Large),</span><span class="sxs-lookup"><span data-stu-id="6c8e2-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="6c8e2-120">S1 (Standard Small), S2 (Standard Medium), S3 (Standard Large),</span><span class="sxs-lookup"><span data-stu-id="6c8e2-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="6c8e2-121">P1 (Premium Small), P2 (Premium Medium) e P3 (Premium Large).</span><span class="sxs-lookup"><span data-stu-id="6c8e2-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="6c8e2-122">**--instances**: numero di ruoli di lavoro nel piano di servizio app. Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="6c8e2-123">Esempio di uso del cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="6c8e2-124">Creare un nuovo piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="6c8e2-125">Usare lo stesso comando **azure appserviceplan create**, con il parametro aggiuntivo **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="6c8e2-126">Tenere presente le restrizioni e le aree descritte in [Introduzione al servizio app in Linux](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6c8e2-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="6c8e2-127">Visualizzare un elenco dei piani di servizio app esistenti</span><span class="sxs-lookup"><span data-stu-id="6c8e2-127">List Existing App Service Plans</span></span>
<span data-ttu-id="6c8e2-128">Per visualizzare un elenco dei piani di servizio app esistenti, usare il comando **azure appserviceplan list**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="6c8e2-129">Per visualizzare un elenco di tutti i piani di servizio app di uno specifico gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="6c8e2-130">Per ottenere un piano di servizio app specifico, usare il comando **azure appserviceplan show**:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="6c8e2-131">Configurare un piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="6c8e2-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="6c8e2-132">Per modificare le impostazioni di un piano di servizio app esistente, usare il comando **azure appserviceplan config**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="6c8e2-133">È possibile modificare lo SKU e il numero di ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="6c8e2-134">Ridimensionamento di un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="6c8e2-135">Per ridimensionare un piano di servizio app esistente, usare:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="6c8e2-136">Modifica dello SKU di un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="6c8e2-137">Per modificare lo SKU di un piano di servizio app esistente, usare:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="6c8e2-138">Eliminare un piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="6c8e2-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="6c8e2-139">Per eliminare un piano di servizio app esistente, è prima di tutto necessario spostare o eliminare tutte le app assegnate.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="6c8e2-140">Usare quindi il comando **azure webapp delete** per eliminare il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="6c8e2-141">Gestione delle app di servizio app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="6c8e2-142">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="6c8e2-142">Create a web app</span></span>
<span data-ttu-id="6c8e2-143">Per creare un'app Web, usare il comando **azure webapp create**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="6c8e2-144">Di seguito sono riportate le descrizioni dei diversi parametri.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="6c8e2-145">**--name**: nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="6c8e2-146">**--plan**: nome del piano di servizio usato per l'hosting dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="6c8e2-147">**--resource-group**: gruppo di risorse che ospita il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="6c8e2-148">**--location**: località dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-148">**--location**: the web app location.</span></span>

<span data-ttu-id="6c8e2-149">Esempio di uso del cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="6c8e2-150">Eliminare un'app esistente</span><span class="sxs-lookup"><span data-stu-id="6c8e2-150">Delete an existing app</span></span>
<span data-ttu-id="6c8e2-151">Per eliminare un'app esistente, è possibile utilizzare il comando **azure webapp delete**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="6c8e2-152">È necessario specificare il nome dell'app e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="6c8e2-153">Visualizzare un elenco delle app esistenti</span><span class="sxs-lookup"><span data-stu-id="6c8e2-153">List existing apps</span></span>
<span data-ttu-id="6c8e2-154">Per visualizzare un elenco delle app esistenti, usare il comando **azure webapp list**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="6c8e2-155">Per visualizzare un elenco di tutte le app di uno specifico gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="6c8e2-156">Per ottenere un'app specifica, usare il comando **azure webapp show**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="6c8e2-157">Configurare un'app esistente</span><span class="sxs-lookup"><span data-stu-id="6c8e2-157">Configure an existing app</span></span>
<span data-ttu-id="6c8e2-158">Per modificare le impostazioni e le configurazioni di un'app esistente, usare il comando **azure webapp config set**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="6c8e2-159">Esempio (1): modificare la versione php di un'app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="6c8e2-160">Esempio (2): aggiungere o modificare le impostazioni dell'app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="6c8e2-161">Per conoscere le altre configurazioni modificabili, usare il comando **azure webapp config set -h**.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="6c8e2-162">Modificare lo stato di un'app esistente</span><span class="sxs-lookup"><span data-stu-id="6c8e2-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="6c8e2-163">Riavviare un'app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-163">Restart an app</span></span>
<span data-ttu-id="6c8e2-164">Per riavviare un'app, è necessario specificare il nome e il gruppo di risorse dell'app.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="6c8e2-165">Arrestare un'app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-165">Stop an app</span></span>
<span data-ttu-id="6c8e2-166">Per arrestare un'app, è necessario specificare il nome e il gruppo di risorse dell'app.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="6c8e2-167">Avviare un'app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-167">Start an app</span></span>
<span data-ttu-id="6c8e2-168">Per avviare un'app, è necessario specificare il nome e il gruppo di risorse dell'app.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="6c8e2-169">Gestire i profili di pubblicazione di un'app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="6c8e2-170">Ogni app dispone di un profilo di pubblicazione che può essere usato per pubblicare il codice.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="6c8e2-171">Recuperare il profilo di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="6c8e2-171">Get Publishing Profile</span></span>
<span data-ttu-id="6c8e2-172">Per recuperare il profilo di pubblicazione di un'app, usare:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="6c8e2-173">Questo comando restituisce il nome utente e la password del profilo di pubblicazione nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6c8e2-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="6c8e2-174">Gestire i nomi host dell'app</span><span class="sxs-lookup"><span data-stu-id="6c8e2-174">Manage app hostnames</span></span>
<span data-ttu-id="6c8e2-175">Per gestire le associazioni nome host per l'app, usare il comando **azure webapp config hostnames**</span><span class="sxs-lookup"><span data-stu-id="6c8e2-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="6c8e2-176">Elencare le associazioni nome host</span><span class="sxs-lookup"><span data-stu-id="6c8e2-176">List hostname bindings</span></span>
<span data-ttu-id="6c8e2-177">Per ottenere le associazioni nome host correnti per un'app, usare:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="6c8e2-178">Aggiungere associazioni nome host</span><span class="sxs-lookup"><span data-stu-id="6c8e2-178">Add hostname bindings</span></span>
<span data-ttu-id="6c8e2-179">Per aggiungere associazioni nome host a un'app, usare:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="6c8e2-180">Eliminare associazioni nome host</span><span class="sxs-lookup"><span data-stu-id="6c8e2-180">Delete hostname bindings</span></span>
<span data-ttu-id="6c8e2-181">Per eliminare associazioni nome host, usare:</span><span class="sxs-lookup"><span data-stu-id="6c8e2-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="6c8e2-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c8e2-182">Next Steps</span></span>
* <span data-ttu-id="6c8e2-183">Per altre informazioni sul supporto dell'interfaccia della riga di comando di Azure Resource Manager, vedere [Usare l'interfaccia della riga di comando di Azure per gestire risorse e gruppi di risorse](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6c8e2-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="6c8e2-184">Per altre informazioni sulla gestione del servizio app tramite PowerShell, vedere [Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure](app-service-web-app-azure-resource-manager-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6c8e2-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="6c8e2-185">Per informazioni sul servizio app di Azure in Linux, vedere [Introduzione al servizio app in Linux](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6c8e2-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
