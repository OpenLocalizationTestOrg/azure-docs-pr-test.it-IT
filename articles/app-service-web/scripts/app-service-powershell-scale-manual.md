---
title: Esempio di script di Azure PowerShell - Ridimensionare un'app Web manualmente | Microsoft Docs
description: Esempio di script di Azure PowerShell - Ridimensionare un'app Web manualmente
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="61750-103">Ridimensionare un'App Web manualmente</span><span class="sxs-lookup"><span data-stu-id="61750-103">Scale a web app manually</span></span>

<span data-ttu-id="61750-104">In questo scenario si apprenderà come creare un gruppo di risorse, un piano di servizio app e un'App Web.</span><span class="sxs-lookup"><span data-stu-id="61750-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="61750-105">Quindi si dimensionerà il piano di servizio app da una singola istanza a più istanze.</span><span class="sxs-lookup"><span data-stu-id="61750-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="61750-106">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="61750-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="61750-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="61750-107">Sample script</span></span>

<span data-ttu-id="61750-108">[!code-powershell[principale](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Ridimensionare un'app Web manualmente")]</span><span class="sxs-lookup"><span data-stu-id="61750-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="61750-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="61750-109">Clean up deployment</span></span> 

<span data-ttu-id="61750-110">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="61750-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="61750-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="61750-111">Script explanation</span></span>

<span data-ttu-id="61750-112">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="61750-112">This script uses the following commands.</span></span> <span data-ttu-id="61750-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="61750-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="61750-114">Comando</span><span class="sxs-lookup"><span data-stu-id="61750-114">Command</span></span> | <span data-ttu-id="61750-115">Note</span><span class="sxs-lookup"><span data-stu-id="61750-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="61750-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61750-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="61750-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="61750-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="61750-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="61750-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="61750-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="61750-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="61750-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="61750-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="61750-121">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="61750-121">Creates a web app.</span></span> |
| [<span data-ttu-id="61750-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="61750-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="61750-123">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="61750-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61750-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61750-124">Next steps</span></span>

<span data-ttu-id="61750-125">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61750-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="61750-126">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="61750-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
