---
title: Esempio di Script di PowerShell - aaaAzure un'app web di creare e distribuire codice da GitHub | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare un'app Web e distribuire il codice da GitHub
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="54cf1-103">Creare un'App Web e distribuire il codice da GitHub</span><span class="sxs-lookup"><span data-stu-id="54cf1-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="54cf1-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi distribuisce il codice dell'App Web da un archivio GitHub (senza la distribuzione continua).</span><span class="sxs-lookup"><span data-stu-id="54cf1-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="54cf1-105">Per la distribuzione di GitHub con distribuzione continua, vedere [Creare un'App Web con distribuzione continua da GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="54cf1-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="54cf1-106">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="54cf1-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="54cf1-107">Inoltre, è necessario un repository tooGitHub collegamento contenente codice dell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="54cf1-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="54cf1-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="54cf1-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="54cf1-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="54cf1-109">Clean up deployment</span></span> 

<span data-ttu-id="54cf1-110">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="54cf1-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="54cf1-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="54cf1-111">Script explanation</span></span>

<span data-ttu-id="54cf1-112">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="54cf1-112">This script uses hello following commands.</span></span> <span data-ttu-id="54cf1-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="54cf1-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="54cf1-114">Comando</span><span class="sxs-lookup"><span data-stu-id="54cf1-114">Command</span></span> | <span data-ttu-id="54cf1-115">Note</span><span class="sxs-lookup"><span data-stu-id="54cf1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="54cf1-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="54cf1-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="54cf1-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="54cf1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="54cf1-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="54cf1-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="54cf1-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="54cf1-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="54cf1-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="54cf1-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="54cf1-121">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="54cf1-121">Creates a web app.</span></span> |
| [<span data-ttu-id="54cf1-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="54cf1-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="54cf1-123">Modificare una risorsa in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="54cf1-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="54cf1-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="54cf1-124">Next steps</span></span>

<span data-ttu-id="54cf1-125">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="54cf1-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="54cf1-126">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="54cf1-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
