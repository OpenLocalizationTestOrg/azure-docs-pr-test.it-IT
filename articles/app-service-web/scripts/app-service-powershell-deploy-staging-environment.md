---
title: Esempio di script di Azure PowerShell - Creare un'app Web e distribuire il codice nell'ambiente di gestione temporanea | Microsoft Docs
description: Esempio di script di Azure PowerShell - Creare un'app Web e distribuire il codice nell'ambiente di gestione temporanea
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 55adc13350eb0f4711efa3c901f6e4e7755dfb27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="d57fb-103">Creare un'App Web e distribuire il codice in un ambiente di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="d57fb-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="d57fb-104">Questo script di esempio crea un'App Web nel servizio app con uno slot di distribuzione aggiuntivo denominato "staging" e quindi distribuisce un'app di esempio allo slot "staging".</span><span class="sxs-lookup"><span data-stu-id="d57fb-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="d57fb-105">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="d57fb-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d57fb-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d57fb-106">Sample script</span></span>

<span data-ttu-id="d57fb-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Creare un'App Web e distribuire il codice in un ambiente di gestione temporanea")]</span><span class="sxs-lookup"><span data-stu-id="d57fb-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d57fb-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d57fb-108">Clean up deployment</span></span> 

<span data-ttu-id="d57fb-109">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="d57fb-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d57fb-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="d57fb-110">Script explanation</span></span>

<span data-ttu-id="d57fb-111">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d57fb-111">This script uses the following commands.</span></span> <span data-ttu-id="d57fb-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="d57fb-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d57fb-113">Comando</span><span class="sxs-lookup"><span data-stu-id="d57fb-113">Command</span></span> | <span data-ttu-id="d57fb-114">Note</span><span class="sxs-lookup"><span data-stu-id="d57fb-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d57fb-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d57fb-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d57fb-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="d57fb-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d57fb-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d57fb-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d57fb-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="d57fb-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d57fb-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d57fb-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d57fb-120">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="d57fb-120">Creates a web app.</span></span> |
| [<span data-ttu-id="d57fb-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d57fb-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="d57fb-122">Modifica un piano di servizio app per cambiarne il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="d57fb-122">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="d57fb-123">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="d57fb-123">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="d57fb-124">Crea uno slot di distribuzione per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="d57fb-124">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="d57fb-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d57fb-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="d57fb-126">Modifica una risorsa in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d57fb-126">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="d57fb-127">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="d57fb-127">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="d57fb-128">Trasferisce uno slot di distribuzione dell'app Web nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d57fb-128">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d57fb-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d57fb-129">Next steps</span></span>

<span data-ttu-id="d57fb-130">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d57fb-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d57fb-131">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d57fb-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
