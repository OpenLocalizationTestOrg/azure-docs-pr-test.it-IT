---
title: aaaWeb App clonazione tramite PowerShell
description: Informazioni su come tooclone App Web toonew App Web utilizzando PowerShell.
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
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="3ad4a-103">Clonazione di app del servizio app di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ad4a-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="3ad4a-104">Con versione di hello di Microsoft Azure PowerShell versione 1.1.0 una nuova opzione è stata aggiunta AzureRMWebApp tooNew che hello utente hello possibilità tooclone un'app di tooa appena creato App Web esistente in un'area diversa o in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="3ad4a-105">In questo modo i clienti toodeploy un numero di App in aree geografiche diverse in modo semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="3ad4a-106">La clonazione di app è attualmente supportata solo per i piani di servizio app Premium.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="3ad4a-107">Usa funzionalità nuova Hello hello stesso limitazioni delle funzionalità di Backup di applicazioni Web, vedere [eseguire il backup di un'app web in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="3ad4a-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="3ad4a-108">toolearn sull'utilizzo di gestione risorse di Azure basato su toomanage cmdlet PowerShell di Azure l'archiviazione di applicazioni Web [Gestione risorse di Azure basato su comandi di PowerShell per App Web di Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="3ad4a-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="3ad4a-109">Clonazione di un'app esistente</span><span class="sxs-lookup"><span data-stu-id="3ad4a-109">Cloning an existing App</span></span>
<span data-ttu-id="3ad4a-110">Scenario: Un'app web esistente nell'area centro-meridionali, utente hello sarebbe tooclone hello contenuto tooa nuova app web nell'area North Central US.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="3ad4a-111">Questo può essere eseguito con versione di Azure Resource Manager hello di hello PowerShell cmdlet toocreate una nuova app web con l'opzione - SourceWebApp hello.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="3ad4a-112">La conoscenza delle risorse hello nome del gruppo che contiene l'app web di origine hello, è possibile utilizzare le seguenti informazioni PowerShell comando tooget hello origine dell'app web (denominate in questo caso origine webapp) hello:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="3ad4a-113">toocreate un piano di servizio App nuovo, è possibile utilizzare il comando New-AzureRmAppServicePlan come hello di esempio seguente</span><span class="sxs-lookup"><span data-stu-id="3ad4a-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="3ad4a-114">Utilizzando il comando New-AzureRmWebApp hello, è possibile creare hello nuova app web nell'area di hello North Central US e ricollegarlo livello premium esistente tooan piano di servizio App, è inoltre possibile utilizzare hello stessa risorsa gruppo come app web di origine hello o definire un nuovo gruppo di risorse , esempio hello viene dimostrato che:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="3ad4a-115">un'app web esistente tra tutti gli slot di distribuzione associati, sarà necessario toouse l'utente hello tooclone hello parametro IncludeSourceWebAppSlots, hello comando PowerShell seguente viene illustrato l'utilizzo di hello del parametro con il comando New-AzureRmWebApp hello:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="3ad4a-116">un'app web esistente all'interno di hello tooclone stessa area, hello utente dovrà disporre di un nuovo gruppo di risorse e un nuovo servizio app piano hello toocreate stessa regione e utilizzando quindi hello seguenti app web di PowerShell comando tooclone hello</span><span class="sxs-lookup"><span data-stu-id="3ad4a-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="3ad4a-117">La clonazione di un tooan App esistenti di ambiente del servizio App</span><span class="sxs-lookup"><span data-stu-id="3ad4a-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="3ad4a-118">Scenario: Un'app web esistente nell'area centro-meridionali, utente hello sarebbe tooclone hello contenuto tooa nuova web app tooan ambiente del servizio App (ASE) esistente.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="3ad4a-119">La conoscenza delle risorse hello nome del gruppo che contiene l'app web di origine hello, è possibile utilizzare le seguenti informazioni PowerShell comando tooget hello origine dell'app web (denominate in questo caso origine webapp) hello:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="3ad4a-120">La conoscenza del hello ASE nome e nome di gruppo di risorse hello hello ASE a cui appartiene, utente di hello può utilizzare il comando New-AzureRmWebApp hello toocreate hello nuova app web in hello esistente ASE, hello seguente viene dimostrato che:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="3ad4a-121">parametro percorso Hello è necessario a causa di motivo toolegacy, ma nel caso di hello di creazione di un'app in un ASE verranno ignorato.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="3ad4a-122">Clonazione dello slot di un'app esistente</span><span class="sxs-lookup"><span data-stu-id="3ad4a-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="3ad4a-123">Scenario: utente hello sarebbe tooclone un tooeither Slot App Web esistente, una nuova App Web o un nuovo slot di App Web.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="3ad4a-124">nuova App Web può essere in hello Hello stessa area come slot di hello originale App Web o in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="3ad4a-125">La conoscenza delle risorse hello nome del gruppo che contiene l'app web di origine hello, possiamo utilizzare hello informazioni tooget hello origine web app dello slot (denominate in questo caso origine webappslot) associato tooWeb App origine-webapp comando di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="3ad4a-126">esempio Hello viene illustrata la creazione di un clone di hello web app tooa nuova app web di origine:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="3ad4a-127">Configurazione di Gestione traffico durante la clonazione di un'app</span><span class="sxs-lookup"><span data-stu-id="3ad4a-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="3ad4a-128">Creazione di applicazioni web con più aree e la configurazione di gestione traffico di Azure tooroute traffico tooall queste App web, è un tooinsure n scenario importante che le applicazioni dei clienti sono a disponibile elevata, durante la clonazione di un'app web esistente è hello opzione tooconnect i servizi web App tooeither un nuovo profilo di gestione traffico o utilizzarne uno esistente, si noti che Gestione risorse di Azure solo la versione di gestione traffico è supportato.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="3ad4a-129">Creazione di un nuovo profilo di Gestione traffico durante la clonazione di un'app</span><span class="sxs-lookup"><span data-stu-id="3ad4a-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="3ad4a-130">Scenario: utente hello sarebbe tooclone un'area tooanother app web, durante la configurazione di un profilo di gestione traffico di gestione risorse di Azure che includono sia applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="3ad4a-131">esempio Hello viene illustrata la creazione di un clone di hello web app tooa nuova app web di origine durante la configurazione di un nuovo profilo di Traffic Manager:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="3ad4a-132">Aggiunta di nuovo clonato App Web tooan esistente profilo di gestione traffico</span><span class="sxs-lookup"><span data-stu-id="3ad4a-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="3ad4a-133">Scenario: hello utente dispone già di un profilo di gestione traffico di gestione risorse di Azure che vorrebbe tooadd entrambi web App come endpoint.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="3ad4a-134">toodo in tal caso, è necessario innanzitutto tooassemble hello esistente id di profilo di gestione traffico, è necessario id sottoscrizione hello, nome del gruppo di risorse e hello traffic manager nome del profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="3ad4a-135">Dopo avere l'id di gestione traffico hello, seguente hello viene illustrato come creare un clone di hello web app tooa nuova app web di origine durante l'aggiunta di tooan profilo di gestione traffico esistente:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="3ad4a-136">Restrizioni attuali</span><span class="sxs-lookup"><span data-stu-id="3ad4a-136">Current Restrictions</span></span>
<span data-ttu-id="3ad4a-137">Questa funzionalità è attualmente in anteprima, Microsoft è impegnata tooadd nuove funzionalità nel tempo, hello seguente elenco sono hello restrizioni note sulla versione corrente di hello di clonazione app:</span><span class="sxs-lookup"><span data-stu-id="3ad4a-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="3ad4a-138">Le impostazioni di ridimensionamento automatico non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="3ad4a-139">Le impostazioni di pianificazione del backup non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="3ad4a-140">Le impostazioni della rete virtuale non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="3ad4a-141">App Insights non automaticamente impostate nell'applicazione web di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="3ad4a-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="3ad4a-142">Le impostazioni di Easy Auth non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="3ad4a-143">L'estensione Kudu non viene clonata.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="3ad4a-144">Le regole TiP non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="3ad4a-145">Il contenuto di database non viene clonato.</span><span class="sxs-lookup"><span data-stu-id="3ad4a-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="3ad4a-146">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="3ad4a-146">References</span></span>
* [<span data-ttu-id="3ad4a-147">Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="3ad4a-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="3ad4a-148">Clonazione di app Web con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3ad4a-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="3ad4a-149">Eseguire il backup di un'app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="3ad4a-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="3ad4a-150">Supporto di Azure Resource Manager per la versione di anteprima di Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="3ad4a-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="3ad4a-151">Introduzione tooApp ambiente del servizio</span><span class="sxs-lookup"><span data-stu-id="3ad4a-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="3ad4a-152">Uso di Azure PowerShell con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ad4a-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

