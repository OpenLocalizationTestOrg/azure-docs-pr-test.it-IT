---
title: "Esempio di script di Azure PowerShell - Instradare il traffico per la disponibilità elevata delle applicazioni | Microsoft Docs"
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
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="584b4-103">Instradare il traffico per la disponibilità elevata delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="584b4-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="584b4-104">In questo script viene creato un gruppo di risorse, due piani di servizio app, due app Web, un profilo di gestione traffico e due endpoint di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="584b4-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="584b4-105">Gestione traffico indirizza il traffico verso l'applicazione in un'area come area primaria e nell'area secondaria quando l'applicazione nell'area primaria non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="584b4-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="584b4-106">Prima di eseguire lo script, è necessario modificare i valori MyWebApp, MyWebAppL1 e MyWebAppL2 in valori univoci in Azure.</span><span class="sxs-lookup"><span data-stu-id="584b4-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="584b4-107">Dopo aver eseguito lo script, è possibile accedere all'app nell'area primaria con l'URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="584b4-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="584b4-108">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="584b4-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="584b4-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="584b4-109">Sample script</span></span>

<span data-ttu-id="584b4-110">[!code-powershell[principale](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Instradare il traffico per la disponibilità elevata")]</span><span class="sxs-lookup"><span data-stu-id="584b4-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="584b4-111">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="584b4-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="584b4-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="584b4-112">Script explanation</span></span>

<span data-ttu-id="584b4-113">Questo script usa i comandi seguenti per creare un gruppo di risorse, un'App Web, un profilo di Gestione traffico e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="584b4-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="584b4-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="584b4-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="584b4-115">Comando</span><span class="sxs-lookup"><span data-stu-id="584b4-115">Command</span></span> | <span data-ttu-id="584b4-116">Note</span><span class="sxs-lookup"><span data-stu-id="584b4-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="584b4-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="584b4-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="584b4-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="584b4-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="584b4-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="584b4-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="584b4-120">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="584b4-120">Creates an App Service plan.</span></span> <span data-ttu-id="584b4-121">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="584b4-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="584b4-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="584b4-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="584b4-123">Consente di creare un'App Web di Azure all'interno del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="584b4-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="584b4-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="584b4-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="584b4-125">Consente di creare un'App Web di Azure all'interno del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="584b4-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="584b4-126">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="584b4-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="584b4-127">Crea un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="584b4-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="584b4-128">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="584b4-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="584b4-129">Aggiunge un endpoint a un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="584b4-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="584b4-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="584b4-130">Next steps</span></span>

<span data-ttu-id="584b4-131">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="584b4-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="584b4-132">Altri esempi di script di PowerShell per la rete sono disponibili nella [documentazione con la panoramica delle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="584b4-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>