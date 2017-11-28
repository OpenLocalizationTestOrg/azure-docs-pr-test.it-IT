---
title: Esempio di Script di PowerShell - aaaAzure un'app web di creare e distribuire codice da un repository Git locale | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare un'app Web e distribuire il codice da un repository Git locale
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="44562-103">Creare un'App Web e distribuire il codice da un archivio Git locale</span><span class="sxs-lookup"><span data-stu-id="44562-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="44562-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi distribuisce il codice dell'App Web in un archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="44562-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="44562-105">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="44562-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="44562-106">Inoltre, il codice dell'applicazione è necessario toobe eseguito il commit in un repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="44562-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="44562-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="44562-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="44562-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="44562-108">Clean up deployment</span></span> 

<span data-ttu-id="44562-109">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="44562-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="44562-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="44562-110">Script explanation</span></span>

<span data-ttu-id="44562-111">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="44562-111">This script uses hello following commands.</span></span> <span data-ttu-id="44562-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="44562-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="44562-113">Comando</span><span class="sxs-lookup"><span data-stu-id="44562-113">Command</span></span> | <span data-ttu-id="44562-114">Note</span><span class="sxs-lookup"><span data-stu-id="44562-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="44562-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="44562-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="44562-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="44562-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="44562-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="44562-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="44562-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="44562-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="44562-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="44562-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="44562-120">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="44562-120">Creates a web app.</span></span> |
| [<span data-ttu-id="44562-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="44562-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="44562-122">Modifica una risorsa in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="44562-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="44562-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="44562-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="44562-124">Ottenere un profilo di pubblicazione delle app Web.</span><span class="sxs-lookup"><span data-stu-id="44562-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="44562-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="44562-125">Next steps</span></span>

<span data-ttu-id="44562-126">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="44562-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="44562-127">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="44562-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
