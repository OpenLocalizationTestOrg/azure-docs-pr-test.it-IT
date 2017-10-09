---
title: aaaAzure strumenti da riga di comando multipiattaforma basate su Gestione risorse per l'App Web di Azure | Documenti Microsoft
description: Informazioni su come toouse hello toomanage strumenti da riga di comando multipiattaforma basate su Gestione risorse di Azure nuova App Web di Azure.
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
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="a287e-103">Utilizzo dell'interfaccia della riga di comando multipiattaforma basata su Azure Resource Manager per servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a287e-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a287e-104">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a287e-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="a287e-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a287e-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="a287e-106">Con la versione di hello della versione di strumenti della riga di comando multipiattaforma di Microsoft Azure 0.10.5, sono stati aggiunti nuovi comandi.</span><span class="sxs-lookup"><span data-stu-id="a287e-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="a287e-107">Questi comandi assegnare hello utente hello possibilità toouse basate su Gestione risorse di Azure PowerShell comandi toomanage servizio App.</span><span class="sxs-lookup"><span data-stu-id="a287e-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="a287e-108">toolearn sulla gestione dei gruppi di risorse, vedere [toomanage CLI di Azure hello Azure usare risorse e gruppi di risorse](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a287e-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="a287e-109">Inoltre, provare [CLI di Azure 2.0](https://github.com/Azure/azure-cli), scritto in Python per modello di distribuzione di gestione risorse hello CLI prossima generazione.</span><span class="sxs-lookup"><span data-stu-id="a287e-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="a287e-110">Gestione di piani di servizio app</span><span class="sxs-lookup"><span data-stu-id="a287e-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="a287e-111">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="a287e-111">Create an App Service Plan</span></span>
<span data-ttu-id="a287e-112">toocreate un piano di servizio app, usare hello **appserviceplan azure creare** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="a287e-113">Di seguito sono le descrizioni dei parametri diversi hello:</span><span class="sxs-lookup"><span data-stu-id="a287e-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="a287e-114">**-gruppo di risorse**: gruppo di risorse che include il piano di servizio app hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="a287e-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="a287e-115">**-nome**: nome del piano di servizio app hello.</span><span class="sxs-lookup"><span data-stu-id="a287e-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="a287e-116">**--location**: località del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="a287e-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="a287e-117">**-sku**: hello desiderato sku di determinazione dei prezzi (hello opzioni sono: F1 (Free).</span><span class="sxs-lookup"><span data-stu-id="a287e-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="a287e-118">D1 (Condiviso),</span><span class="sxs-lookup"><span data-stu-id="a287e-118">D1 (Shared).</span></span> <span data-ttu-id="a287e-119">B1 (Basic Small), B2 (Basic Medium), B3 (Basic Large),</span><span class="sxs-lookup"><span data-stu-id="a287e-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="a287e-120">S1 (Standard Small), S2 (Standard Medium), S3 (Standard Large),</span><span class="sxs-lookup"><span data-stu-id="a287e-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="a287e-121">P1 (Premium Small), P2 (Premium Medium) e P3 (Premium Large).</span><span class="sxs-lookup"><span data-stu-id="a287e-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="a287e-122">**-istanze**: hello numero di thread di lavoro nel piano di servizio app hello (valore predefinito è 1).</span><span class="sxs-lookup"><span data-stu-id="a287e-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="a287e-123">Esempio toouse questo cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a287e-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="a287e-124">Creare un nuovo piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="a287e-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="a287e-125">Utilizzando hello stesso **appserviceplan azure creare** comando, con hello parametro aggiuntivo **true - islinux**.</span><span class="sxs-lookup"><span data-stu-id="a287e-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="a287e-126">Tenere presenti le restrizioni di hello e aree descritte nella [tooApp introduzione del servizio su Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="a287e-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="a287e-127">Visualizzare un elenco dei piani di servizio app esistenti</span><span class="sxs-lookup"><span data-stu-id="a287e-127">List Existing App Service Plans</span></span>
<span data-ttu-id="a287e-128">Utilizzare toolist hello esistente piani di servizio app, **appserviceplan azure elenco** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="a287e-129">toolist tutti i piani di servizio app in un gruppo di risorse specifico, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="a287e-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="a287e-130">Utilizzare un piano di servizio app specifica, tooget **appserviceplan azure Mostra** comando:</span><span class="sxs-lookup"><span data-stu-id="a287e-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="a287e-131">Configurare un piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="a287e-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="a287e-132">toochange hello impostazioni per un piano di servizio app esistente, utilizzare hello **configurazione azure appserviceplan** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="a287e-133">È possibile modificare lo sku hello e il numero di lavori hello</span><span class="sxs-lookup"><span data-stu-id="a287e-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="a287e-134">Ridimensionamento di un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="a287e-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="a287e-135">tooscale un esistente piano di servizio App, usare:</span><span class="sxs-lookup"><span data-stu-id="a287e-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="a287e-136">Modifica hello SKU di un piano di servizio App</span><span class="sxs-lookup"><span data-stu-id="a287e-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="a287e-137">toochange hello sku di un'esistente piano di servizio App, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="a287e-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="a287e-138">Eliminare un piano di servizio app esistente</span><span class="sxs-lookup"><span data-stu-id="a287e-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="a287e-139">toodelete un piano di servizio app esistente, tutti assegnati App necessità toobe spostati o eliminati per primi.</span><span class="sxs-lookup"><span data-stu-id="a287e-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="a287e-140">Utilizzando quindi hello **webapp azure eliminare** comando è possibile eliminare il piano di servizio app hello.</span><span class="sxs-lookup"><span data-stu-id="a287e-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="a287e-141">Gestione delle app di servizio app</span><span class="sxs-lookup"><span data-stu-id="a287e-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="a287e-142">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="a287e-142">Create a web app</span></span>
<span data-ttu-id="a287e-143">toocreate un'app web, utilizzare hello **webapp azure creare** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="a287e-144">Di seguito sono le descrizioni dei parametri diversi hello:</span><span class="sxs-lookup"><span data-stu-id="a287e-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="a287e-145">**-nome**: nome per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="a287e-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="a287e-146">**-piano**: assegnare un nome per il piano di servizio hello utilizzato toohost hello web app.</span><span class="sxs-lookup"><span data-stu-id="a287e-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="a287e-147">**-gruppo di risorse**: gruppo di risorse che ospita il piano di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="a287e-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="a287e-148">**-percorso**: hello percorso app web.</span><span class="sxs-lookup"><span data-stu-id="a287e-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="a287e-149">Esempio toouse questo cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a287e-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="a287e-150">Eliminare un'app esistente</span><span class="sxs-lookup"><span data-stu-id="a287e-150">Delete an existing app</span></span>
<span data-ttu-id="a287e-151">toodelete un'app esistente, è possibile utilizzare hello **webapp azure eliminare** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="a287e-152">È necessario toospecify hello nome dell'applicazione hello e il nome del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="a287e-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="a287e-153">Visualizzare un elenco delle app esistenti</span><span class="sxs-lookup"><span data-stu-id="a287e-153">List existing apps</span></span>
<span data-ttu-id="a287e-154">app di esistenti hello toolist, utilizzare hello **elenco webapp azure** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="a287e-155">toolist tutte le App in un gruppo di risorse specifico, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="a287e-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="a287e-156">tooget un'app specifica, utilizzare hello **webapp azure Mostra** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="a287e-157">Configurare un'app esistente</span><span class="sxs-lookup"><span data-stu-id="a287e-157">Configure an existing app</span></span>
<span data-ttu-id="a287e-158">toochange hello impostazioni e configurazioni per un'app esistente, utilizzare hello **set di configurazione di azure webapp** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="a287e-159">Esempio (1): modificare la versione di php hello di un'app</span><span class="sxs-lookup"><span data-stu-id="a287e-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="a287e-160">Esempio (2): aggiungere o modificare le impostazioni dell'app</span><span class="sxs-lookup"><span data-stu-id="a287e-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="a287e-161">tooknow altri della configurazione può essere modificata, utilizzare hello **set di configurazione azure webapp -h** comando.</span><span class="sxs-lookup"><span data-stu-id="a287e-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="a287e-162">Modifica dello stato di hello di un'app esistente</span><span class="sxs-lookup"><span data-stu-id="a287e-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="a287e-163">Riavviare un'app</span><span class="sxs-lookup"><span data-stu-id="a287e-163">Restart an app</span></span>
<span data-ttu-id="a287e-164">toorestart un'app, è necessario specificare gruppo hello di nome e la risorsa dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a287e-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="a287e-165">Arrestare un'app</span><span class="sxs-lookup"><span data-stu-id="a287e-165">Stop an app</span></span>
<span data-ttu-id="a287e-166">toostop un'app, è necessario specificare gruppo hello di nome e la risorsa dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a287e-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="a287e-167">Avviare un'app</span><span class="sxs-lookup"><span data-stu-id="a287e-167">Start an app</span></span>
<span data-ttu-id="a287e-168">toostart un'app, è necessario specificare gruppo hello di nome e la risorsa dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a287e-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="a287e-169">Gestire i profili di pubblicazione di un'app</span><span class="sxs-lookup"><span data-stu-id="a287e-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="a287e-170">Ogni app ha un profilo di pubblicazione che può essere utilizzati toopublish il codice.</span><span class="sxs-lookup"><span data-stu-id="a287e-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="a287e-171">Recuperare il profilo di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="a287e-171">Get Publishing Profile</span></span>
<span data-ttu-id="a287e-172">hello tooget profilo per un'app, l'utilizzo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="a287e-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="a287e-173">Questo comando restituisce hello profilo nome utente e password toohello riga di comando di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a287e-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="a287e-174">Gestire i nomi host dell'app</span><span class="sxs-lookup"><span data-stu-id="a287e-174">Manage app hostnames</span></span>
<span data-ttu-id="a287e-175">le associazioni nome host toomanage per l'app, usare hello **nomi host di configurazione di azure webapp** comando</span><span class="sxs-lookup"><span data-stu-id="a287e-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="a287e-176">Elencare le associazioni nome host</span><span class="sxs-lookup"><span data-stu-id="a287e-176">List hostname bindings</span></span>
<span data-ttu-id="a287e-177">tooget hello corrente le associazioni nome host per un'app, usare:</span><span class="sxs-lookup"><span data-stu-id="a287e-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="a287e-178">Aggiungere associazioni nome host</span><span class="sxs-lookup"><span data-stu-id="a287e-178">Add hostname bindings</span></span>
<span data-ttu-id="a287e-179">tooadd hostname associazioni tooan app, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="a287e-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="a287e-180">Eliminare associazioni nome host</span><span class="sxs-lookup"><span data-stu-id="a287e-180">Delete hostname bindings</span></span>
<span data-ttu-id="a287e-181">le associazioni nome host toodelete, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="a287e-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="a287e-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a287e-182">Next Steps</span></span>
* <span data-ttu-id="a287e-183">toolearn sul supporto di Azure Resource Manager CLI, vedere [toomanage CLI di Azure hello Azure usare risorse e gruppi di risorse.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="a287e-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="a287e-184">toolearn sulla gestione del servizio App tramite PowerShell, vedere [tooManage Using Azure Resource Manager-Based PowerShell App Web di Azure.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a287e-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="a287e-185">toolearn sul servizio App di Azure su Linux, vedere [tooApp introduzione del servizio su Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="a287e-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
