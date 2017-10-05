---
title: Esempio di script di Azure PowerShell - Creare un'app Web e distribuire il codice da un repository Git locale | Microsoft Docs
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
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="2fa39-103">Creare un'App Web e distribuire il codice da un archivio Git locale</span><span class="sxs-lookup"><span data-stu-id="2fa39-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="2fa39-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi distribuisce il codice dell'App Web in un archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="2fa39-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="2fa39-105">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="2fa39-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="2fa39-106">È inoltre necessario eseguire il commit del codice dell'applicazione in un repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="2fa39-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="2fa39-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="2fa39-107">Sample script</span></span>

<span data-ttu-id="2fa39-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Creare un'App Web e distribuire il codice da un archivio Git locale")]</span><span class="sxs-lookup"><span data-stu-id="2fa39-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2fa39-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="2fa39-109">Clean up deployment</span></span> 

<span data-ttu-id="2fa39-110">Dopo aver eseguito lo script di esempio, usare il comando seguente per rimuovere il gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="2fa39-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="2fa39-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="2fa39-111">Script explanation</span></span>

<span data-ttu-id="2fa39-112">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2fa39-112">This script uses the following commands.</span></span> <span data-ttu-id="2fa39-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="2fa39-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2fa39-114">Comando</span><span class="sxs-lookup"><span data-stu-id="2fa39-114">Command</span></span> | <span data-ttu-id="2fa39-115">Note</span><span class="sxs-lookup"><span data-stu-id="2fa39-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2fa39-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2fa39-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2fa39-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="2fa39-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2fa39-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="2fa39-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="2fa39-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="2fa39-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2fa39-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="2fa39-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="2fa39-121">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="2fa39-121">Creates a web app.</span></span> |
| [<span data-ttu-id="2fa39-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2fa39-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="2fa39-123">Modifica una risorsa in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2fa39-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="2fa39-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="2fa39-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="2fa39-125">Ottenere un profilo di pubblicazione delle app Web.</span><span class="sxs-lookup"><span data-stu-id="2fa39-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2fa39-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2fa39-126">Next steps</span></span>

<span data-ttu-id="2fa39-127">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2fa39-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2fa39-128">Altri esempi di Azure PowerShell per app Web del servizio app di Azure sono disponibili in [Azure PowerShell samples](../app-service-powershell-samples.md) (Esempi di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="2fa39-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
