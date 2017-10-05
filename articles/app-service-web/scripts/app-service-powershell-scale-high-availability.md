---
title: "Esempio di script di Azure PowerShell - Ridimensionare un'app Web a livello globale con un'architettura a disponibilità elevata | Microsoft Docs"
description: "Esempio di script di Azure PowerShell - Ridimensionare un'app Web a livello globale con un'architettura a disponibilità elevata"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 9acd1cf4d1a5705811c4dedc545505ec0ac55fc7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="5d0b5-103">Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="5d0b5-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="5d0b5-104">In questo scenario verranno creati un gruppo di risorse, due piani di servizio app, due App Web, una profilo di Gestione traffico e due endpoint di endpoint di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="5d0b5-105">Dopo aver completato l'esercizio si avrà un'architettura a disponibilità elevata che fornisce la disponibilità globale dell'App Web in base alla minima latenza di rete.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="5d0b5-106">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="5d0b5-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5d0b5-107">Sample script</span></span>

<span data-ttu-id="5d0b5-108">[!code-powershell[principale](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Ridimensionare un'app Web a livello globale con un'architettura a disponibilità elevata")]</span><span class="sxs-lookup"><span data-stu-id="5d0b5-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5d0b5-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="5d0b5-109">Clean up deployment</span></span> 

<span data-ttu-id="5d0b5-110">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="5d0b5-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5d0b5-111">Script explanation</span></span>

<span data-ttu-id="5d0b5-112">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-112">This script uses the following commands.</span></span> <span data-ttu-id="5d0b5-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5d0b5-114">Comando</span><span class="sxs-lookup"><span data-stu-id="5d0b5-114">Command</span></span> | <span data-ttu-id="5d0b5-115">Note</span><span class="sxs-lookup"><span data-stu-id="5d0b5-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d0b5-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5d0b5-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5d0b5-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5d0b5-118">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="5d0b5-118">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="5d0b5-119">Crea un profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-119">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="5d0b5-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5d0b5-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="5d0b5-121">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5d0b5-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5d0b5-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="5d0b5-123">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-123">Creates a web app.</span></span> |
| [<span data-ttu-id="5d0b5-124">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="5d0b5-124">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="5d0b5-125">Crea un endpoint nel profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="5d0b5-125">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5d0b5-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d0b5-126">Next steps</span></span>

<span data-ttu-id="5d0b5-127">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d0b5-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5d0b5-128">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5d0b5-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
