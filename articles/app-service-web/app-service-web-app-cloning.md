---
title: Clonazione di app Web con PowerShell
description: Come clonare le app Web in nuove app Web con PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="f1379-103">Clonazione di app del servizio app di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1379-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="f1379-104">Con il rilascio di Microsoft Azure PowerShell versione 1.1.0 è stata aggiunta una nuova opzione a New-AzureRMWebApp che consente all'utente di clonare un'app Web esistente in un'app appena creata in un'area diversa o nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="f1379-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="f1379-105">In questo modo i clienti possono distribuire una quantità di app in aree geografiche diverse rapidamente e con facilità.</span><span class="sxs-lookup"><span data-stu-id="f1379-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="f1379-106">La clonazione di app è attualmente supportata solo per i piani di servizio app Premium.</span><span class="sxs-lookup"><span data-stu-id="f1379-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="f1379-107">La nuova funzionalità usa le stesse limitazioni della funzionalità di backup di App Web. Vedere [Eseguire il backup di un'app Web nel servizio app di Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f1379-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="f1379-108">Per informazioni su come usare cmdlet di Azure PowerShell basati su Azure Resource Manager per gestire le app Web, vedere [Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f1379-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="f1379-109">Clonazione di un'app esistente</span><span class="sxs-lookup"><span data-stu-id="f1379-109">Cloning an existing App</span></span>
<span data-ttu-id="f1379-110">Scenario: l'utente vuole clonare il contenuto di un'app Web esistente nell'area South Central US in una nuova app Web nell'aera North Central US.</span><span class="sxs-lookup"><span data-stu-id="f1379-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="f1379-111">Questa operazione può essere eseguita con la versione Azure Resource Manager del cmdlet di PowerShell per creare una nuova app Web con l'opzione -SourceWebApp.</span><span class="sxs-lookup"><span data-stu-id="f1379-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="f1379-112">Conoscendo il nome del gruppo di risorse che include l'app Web di origine, è possibile usare il comando di PowerShell seguente per ottenere informazioni sull'app Web di origine, denominata in questo caso source-webapp:</span><span class="sxs-lookup"><span data-stu-id="f1379-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="f1379-113">Per creare un nuovo piano di servizio app, è possibile usare il comando New-AzureRmAppServicePlan come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f1379-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="f1379-114">Con il comando New-AzureRmWebApp è possibile creare la nuova app Web nell'area North Central US e collegarla a un piano di servizio app Premium esistente. È anche possibile usare lo stesso gruppo di risorse dell'app Web di origine o definirne uno nuovo, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f1379-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="f1379-115">Per clonare un'app Web esistente, inclusi tutti gli slot di distribuzione associati, l'utente dovrà usare il parametro IncludeSourceWebAppSlots. Il comando di PowerShell seguente illustra l'uso del parametro con il comando New-AzureRmWebApp:</span><span class="sxs-lookup"><span data-stu-id="f1379-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="f1379-116">Per clonare un'app Web esistente nella stessa area, l'utente dovrà creare un nuovo gruppo di risorse e un nuovo piano di servizio app nella stessa area e quindi usare il comando di PowerShell seguente per clonare l'app Web:</span><span class="sxs-lookup"><span data-stu-id="f1379-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="f1379-117">Clonazione di un'app esistente in un ambiente del servizio App</span><span class="sxs-lookup"><span data-stu-id="f1379-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="f1379-118">Scenario: l'utente vuole clonare il contenuto di un'app Web esistente nell'area South Central US in una nuova app Web in un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="f1379-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="f1379-119">Conoscendo il nome del gruppo di risorse che include l'app Web di origine, è possibile usare il comando di PowerShell seguente per ottenere informazioni sull'app Web di origine, denominata in questo caso source-webapp:</span><span class="sxs-lookup"><span data-stu-id="f1379-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="f1379-120">Conoscendo il nome dell'ambiente del servizio app e il nome del gruppo di risorse a cui appartiene l'ambiente del servizio app, l'utente può usare il comando New-AzureRmWebApp per creare la nuova app Web nell'ambiente del servizio app esistente, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f1379-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="f1379-121">Il parametro Location è obbligatorio per motivi di compatibilità con le versioni precedenti, ma verrà ignorato se si crea un'app in un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="f1379-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="f1379-122">Clonazione dello slot di un'app esistente</span><span class="sxs-lookup"><span data-stu-id="f1379-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="f1379-123">Scenario: l'utente vuole clonare lo slot di un'app Web esistente in una nuova app Web o un nuovo slot dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="f1379-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="f1379-124">La nuova app Web può trovarsi nella stessa area dello slot dell'app Web originale o in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="f1379-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="f1379-125">Conoscendo il nome del gruppo di risorse che include l'app Web di origine, è possibile usare il comando di PowerShell seguente per ottenere informazioni sullo slot dell'app Web di origine, denominata in questo caso source-webappslot, collegata all'app Web source-webapp:</span><span class="sxs-lookup"><span data-stu-id="f1379-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="f1379-126">Di seguito è illustrata la creazione di un clone dell'app Web di origine in una nuova app Web:</span><span class="sxs-lookup"><span data-stu-id="f1379-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="f1379-127">Configurazione di Gestione traffico durante la clonazione di un'app</span><span class="sxs-lookup"><span data-stu-id="f1379-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="f1379-128">La creazione di app Web con più aree e la configurazione di Gestione traffico di Azure per indirizzare il traffico a tali app Web sono importanti per garantire la disponibilità elevata delle app dei clienti. Durante la clonazione di un'app Web esistente è possibile scegliere di connettere entrambe le app Web a un nuovo profilo di Gestione traffico oppure a uno esistente. Si noti che è supportata unicamente la versione Azure Resource Manager di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="f1379-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="f1379-129">Creazione di un nuovo profilo di Gestione traffico durante la clonazione di un'app</span><span class="sxs-lookup"><span data-stu-id="f1379-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="f1379-130">Scenario: l'utente vuole clonare un'app Web in un'altra area mentre configura un profilo di Gestione traffico di Azure Resource Manager che include entrambe le app Web.</span><span class="sxs-lookup"><span data-stu-id="f1379-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="f1379-131">Di seguito è illustrata la creazione di un clone dell'app Web di origine in una nuova app Web durante la configurazione di un nuovo profilo di Gestione traffico:</span><span class="sxs-lookup"><span data-stu-id="f1379-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="f1379-132">Aggiunta di una nuova app Web clonata a un profilo di Gestione traffico esistente</span><span class="sxs-lookup"><span data-stu-id="f1379-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="f1379-133">Scenario: l'utente ha già un profilo di Gestione traffico di Azure Resource Manager a cui vorrebbe aggiungere entrambe le app Web come endpoint.</span><span class="sxs-lookup"><span data-stu-id="f1379-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="f1379-134">A questo scopo, è necessario assemblare prima di tutto l'ID del profilo di Gestione traffico esistente, per cui saranno necessari l'ID sottoscrizione, il nome del gruppo di risorse e il nome del profilo di Gestione traffico esistente.</span><span class="sxs-lookup"><span data-stu-id="f1379-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="f1379-135">Dopo aver recuperato l'ID di Gestione traffico, di seguito è illustrata la creazione di un clone dell'app Web di origine in una nuova app Web durante l'aggiunta a un profilo di Gestione traffico esistente:</span><span class="sxs-lookup"><span data-stu-id="f1379-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="f1379-136">Restrizioni attuali</span><span class="sxs-lookup"><span data-stu-id="f1379-136">Current Restrictions</span></span>
<span data-ttu-id="f1379-137">Questa funzionalità è attualmente in anteprima e sono allo studio nuove funzionalità che saranno aggiunte con il tempo. L'elenco seguente include le restrizioni note della versione corrente relative alla clonazione di app:</span><span class="sxs-lookup"><span data-stu-id="f1379-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="f1379-138">Le impostazioni di ridimensionamento automatico non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="f1379-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="f1379-139">Le impostazioni di pianificazione del backup non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="f1379-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="f1379-140">Le impostazioni della rete virtuale non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="f1379-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="f1379-141">Le informazioni sull'app non vengono configurate automaticamente nell'app Web di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f1379-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="f1379-142">Le impostazioni di Easy Auth non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="f1379-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="f1379-143">L'estensione Kudu non viene clonata.</span><span class="sxs-lookup"><span data-stu-id="f1379-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="f1379-144">Le regole TiP non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="f1379-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="f1379-145">Il contenuto di database non viene clonato.</span><span class="sxs-lookup"><span data-stu-id="f1379-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="f1379-146">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="f1379-146">References</span></span>
* [<span data-ttu-id="f1379-147">Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="f1379-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="f1379-148">Clonazione di app Web con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f1379-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="f1379-149">Eseguire il backup di un'app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="f1379-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="f1379-150">Supporto di Azure Resource Manager per la versione di anteprima di Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="f1379-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="f1379-151">Introduzione all'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="f1379-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="f1379-152">Uso di Azure PowerShell con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="f1379-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

