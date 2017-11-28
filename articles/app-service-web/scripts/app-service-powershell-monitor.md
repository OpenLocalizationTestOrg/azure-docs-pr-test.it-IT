---
title: Esempio di Script di PowerShell - aaaAzure monitorare un'app web con i registri del server web | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Monitorare un'app Web con i log del server Web
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="41861-103">Monitorare un'App Web con i log del server Web</span><span class="sxs-lookup"><span data-stu-id="41861-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="41861-104">In questo scenario si crea un gruppo di risorse, il piano di servizio app, app web e lo configura hello web app tooenable i log del server.</span><span class="sxs-lookup"><span data-stu-id="41861-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="41861-105">Quindi si scaricherà i file di log hello per la revisione.</span><span class="sxs-lookup"><span data-stu-id="41861-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="41861-106">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="41861-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="41861-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="41861-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="41861-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="41861-108">Clean up deployment</span></span> 

<span data-ttu-id="41861-109">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="41861-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="41861-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="41861-110">Script explanation</span></span>

<span data-ttu-id="41861-111">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="41861-111">This script uses hello following commands.</span></span> <span data-ttu-id="41861-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="41861-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="41861-113">Comando</span><span class="sxs-lookup"><span data-stu-id="41861-113">Command</span></span> | <span data-ttu-id="41861-114">Note</span><span class="sxs-lookup"><span data-stu-id="41861-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="41861-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="41861-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="41861-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="41861-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="41861-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="41861-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="41861-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="41861-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="41861-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="41861-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="41861-120">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="41861-120">Creates a web app.</span></span> |
| [<span data-ttu-id="41861-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="41861-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="41861-122">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="41861-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="41861-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="41861-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="41861-124">Ottiene la metrica di un'app web.</span><span class="sxs-lookup"><span data-stu-id="41861-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41861-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41861-125">Next steps</span></span>

<span data-ttu-id="41861-126">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41861-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="41861-127">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="41861-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
