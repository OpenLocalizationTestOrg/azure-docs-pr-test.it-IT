---
title: Esempio di script di Azure PowerShell - Assegnare un dominio personalizzato a un'App Web | Microsoft Docs
description: Esempio di script di Azure PowerShell - Assegnare un dominio personalizzato a un'App Web
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6d25fe8098848fc69470c77e3200bee554c1f875
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="f6ce0-103">Assegnare un dominio personalizzato a un'App Web</span><span class="sxs-lookup"><span data-stu-id="f6ce0-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="f6ce0-104">Questo script di esempio crea un'App Web nel servizio App con le relative risorse correlate e quindi esegue il mapping di `www.<yourdomain>` a essa.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="f6ce0-105">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="f6ce0-106">Occorre inoltre disporre dell'accesso alla pagina di configurazione DNS del registrar di dominio.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f6ce0-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f6ce0-107">Sample script</span></span>

<span data-ttu-id="f6ce0-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assegnare un dominio personalizzato a un'App Web")]</span><span class="sxs-lookup"><span data-stu-id="f6ce0-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f6ce0-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f6ce0-109">Clean up deployment</span></span> 

<span data-ttu-id="f6ce0-110">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f6ce0-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f6ce0-111">Script explanation</span></span>

<span data-ttu-id="f6ce0-112">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-112">This script uses the following commands.</span></span> <span data-ttu-id="f6ce0-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f6ce0-114">Comando</span><span class="sxs-lookup"><span data-stu-id="f6ce0-114">Command</span></span> | <span data-ttu-id="f6ce0-115">Note</span><span class="sxs-lookup"><span data-stu-id="f6ce0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f6ce0-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f6ce0-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f6ce0-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f6ce0-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f6ce0-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f6ce0-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f6ce0-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f6ce0-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f6ce0-121">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-121">Creates a web app.</span></span> |
| [<span data-ttu-id="f6ce0-122">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f6ce0-122">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="f6ce0-123">Modifica un piano di servizio app per cambiarne il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-123">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="f6ce0-124">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f6ce0-124">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f6ce0-125">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="f6ce0-125">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f6ce0-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6ce0-126">Next steps</span></span>

<span data-ttu-id="f6ce0-127">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f6ce0-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f6ce0-128">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="f6ce0-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
