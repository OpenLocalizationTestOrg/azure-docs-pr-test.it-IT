---
title: Esempio di script di Azure PowerShell - Creare un'app Web con distribuzione continua da GitHub | Microsoft Docs
description: Esempio di script di Azure PowerShell - Creare un'app Web con distribuzione continua da GitHub
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="b3a73-103">Creare un'App Web con distribuzione continua da GitHub</span><span class="sxs-lookup"><span data-stu-id="b3a73-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="b3a73-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi configura la distribuzione continua da un archivio GitHub.</span><span class="sxs-lookup"><span data-stu-id="b3a73-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="b3a73-105">Per la distribuzione GitHub senza distribuzione continua, vedere [Creare un'App Web e distribuire il codice da GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="b3a73-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="b3a73-106">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3a73-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="b3a73-107">Verificare inoltre se:</span><span class="sxs-lookup"><span data-stu-id="b3a73-107">Also, ensure that:</span></span>

- <span data-ttu-id="b3a73-108">È stata creata una connessione con Azure usando il comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="b3a73-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="b3a73-109">Il codice dell'applicazione è in un archivio GitHub pubblico o privato di cui si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="b3a73-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="b3a73-110">È stato [creato un token di accesso nell'account GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="b3a73-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="b3a73-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="b3a73-111">Sample script</span></span>

<span data-ttu-id="b3a73-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Creare un'App Web con distribuzione continua da GitHub")]</span><span class="sxs-lookup"><span data-stu-id="b3a73-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b3a73-113">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b3a73-113">Clean up deployment</span></span> 

<span data-ttu-id="b3a73-114">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="b3a73-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="b3a73-115">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="b3a73-115">Script explanation</span></span>

<span data-ttu-id="b3a73-116">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b3a73-116">This script uses the following commands.</span></span> <span data-ttu-id="b3a73-117">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="b3a73-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b3a73-118">Comando</span><span class="sxs-lookup"><span data-stu-id="b3a73-118">Command</span></span> | <span data-ttu-id="b3a73-119">Note</span><span class="sxs-lookup"><span data-stu-id="b3a73-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3a73-120">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3a73-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b3a73-121">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="b3a73-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b3a73-122">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="b3a73-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="b3a73-123">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="b3a73-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="b3a73-124">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="b3a73-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="b3a73-125">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="b3a73-125">Creates a web app.</span></span> |
| [<span data-ttu-id="b3a73-126">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="b3a73-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="b3a73-127">Modificare una risorsa in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b3a73-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b3a73-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3a73-128">Next steps</span></span>

<span data-ttu-id="b3a73-129">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3a73-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b3a73-130">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b3a73-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
