---
title: Esempio di Script di PowerShell - aaaAzure creare un'app web con una distribuzione continua da GitHub | Documenti Microsoft
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
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="0fc83-103">Creare un'App Web con distribuzione continua da GitHub</span><span class="sxs-lookup"><span data-stu-id="0fc83-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="0fc83-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi configura la distribuzione continua da un archivio GitHub.</span><span class="sxs-lookup"><span data-stu-id="0fc83-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="0fc83-105">Per la distribuzione GitHub senza distribuzione continua, vedere [Creare un'App Web e distribuire il codice da GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="0fc83-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="0fc83-106">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0fc83-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="0fc83-107">Verificare inoltre se:</span><span class="sxs-lookup"><span data-stu-id="0fc83-107">Also, ensure that:</span></span>

- <span data-ttu-id="0fc83-108">Una connessione con Azure è stata creata utilizzando hello `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="0fc83-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="0fc83-109">il codice dell'applicazione Hello è in un repository GitHub pubblico o privato a cui si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="0fc83-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="0fc83-110">È stato [creato un token di accesso nell'account GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="0fc83-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="0fc83-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="0fc83-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0fc83-112">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="0fc83-112">Clean up deployment</span></span> 

<span data-ttu-id="0fc83-113">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="0fc83-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="0fc83-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="0fc83-114">Script explanation</span></span>

<span data-ttu-id="0fc83-115">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0fc83-115">This script uses hello following commands.</span></span> <span data-ttu-id="0fc83-116">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="0fc83-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0fc83-117">Comando</span><span class="sxs-lookup"><span data-stu-id="0fc83-117">Command</span></span> | <span data-ttu-id="0fc83-118">Note</span><span class="sxs-lookup"><span data-stu-id="0fc83-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0fc83-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0fc83-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0fc83-120">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="0fc83-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0fc83-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0fc83-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="0fc83-122">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="0fc83-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0fc83-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0fc83-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="0fc83-124">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="0fc83-124">Creates a web app.</span></span> |
| [<span data-ttu-id="0fc83-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="0fc83-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="0fc83-126">Modificare una risorsa in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0fc83-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0fc83-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0fc83-127">Next steps</span></span>

<span data-ttu-id="0fc83-128">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0fc83-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0fc83-129">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0fc83-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
