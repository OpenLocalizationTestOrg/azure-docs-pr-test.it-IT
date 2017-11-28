---
title: "Esempio di Script di PowerShell - instradare il traffico per la disponibilità elevata delle applicazioni aaaAzure | Documenti Microsoft"
description: "Esempio di script di Azure PowerShell - Instradare il traffico per la disponibilità elevata delle applicazioni"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="252c2-103">Instradare il traffico per la disponibilità elevata delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="252c2-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="252c2-104">In questo script viene creato un gruppo di risorse, due piani di servizio app, due app Web, un profilo di gestione traffico e due endpoint di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="252c2-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="252c2-105">Gestione traffico indirizza applicazione toohello il traffico in un'area come area primaria hello e area secondaria toohello quando un'applicazione hello nell'area primaria hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="252c2-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="252c2-106">Prima di eseguire script hello, è necessario modificare hello MyWebApp, MyWebAppL1 e MyWebAppL2 valori toounique valori in Azure.</span><span class="sxs-lookup"><span data-stu-id="252c2-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="252c2-107">Dopo l'esecuzione di script hello, è possibile accedere app hello nell'area primaria di hello con mywebapp.trafficmanager.net URL hello.</span><span class="sxs-lookup"><span data-stu-id="252c2-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="252c2-108">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="252c2-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="252c2-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="252c2-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="252c2-110">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="252c2-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="252c2-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="252c2-111">Script explanation</span></span>

<span data-ttu-id="252c2-112">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, app web, il profilo di gestione traffico hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="252c2-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="252c2-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="252c2-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="252c2-114">Comando</span><span class="sxs-lookup"><span data-stu-id="252c2-114">Command</span></span> | <span data-ttu-id="252c2-115">Note</span><span class="sxs-lookup"><span data-stu-id="252c2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="252c2-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="252c2-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="252c2-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="252c2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="252c2-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="252c2-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="252c2-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="252c2-119">Creates an App Service plan.</span></span> <span data-ttu-id="252c2-120">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="252c2-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="252c2-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="252c2-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="252c2-122">Crea un'app web di Azure all'interno di hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="252c2-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="252c2-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="252c2-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="252c2-124">Crea un'app web di Azure all'interno di hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="252c2-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="252c2-125">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="252c2-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="252c2-126">Crea un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="252c2-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="252c2-127">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="252c2-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="252c2-128">Aggiunge un tooan endpoint del profilo di Traffic Manager di Azure.</span><span class="sxs-lookup"><span data-stu-id="252c2-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="252c2-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="252c2-129">Next steps</span></span>

<span data-ttu-id="252c2-130">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="252c2-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="252c2-131">Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="252c2-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
