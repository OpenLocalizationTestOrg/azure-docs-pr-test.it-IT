---
title: Esempio di Script di PowerShell - aaaAzure ridimensionare un'app web manualmente | Documenti Microsoft
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
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="e31cd-103">Ridimensionare un'App Web manualmente</span><span class="sxs-lookup"><span data-stu-id="e31cd-103">Scale a web app manually</span></span>

<span data-ttu-id="e31cd-104">In questo scenario si apprenderà toocreate un gruppo di risorse, app web e il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="e31cd-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="e31cd-105">È quindi verrà ridimensionato hello piano di servizio App dalle istanze di toomultiple singola istanza.</span><span class="sxs-lookup"><span data-stu-id="e31cd-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="e31cd-106">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="e31cd-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e31cd-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="e31cd-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e31cd-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="e31cd-108">Clean up deployment</span></span> 

<span data-ttu-id="e31cd-109">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="e31cd-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="e31cd-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="e31cd-110">Script explanation</span></span>

<span data-ttu-id="e31cd-111">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="e31cd-111">This script uses hello following commands.</span></span> <span data-ttu-id="e31cd-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="e31cd-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e31cd-113">Comando</span><span class="sxs-lookup"><span data-stu-id="e31cd-113">Command</span></span> | <span data-ttu-id="e31cd-114">Note</span><span class="sxs-lookup"><span data-stu-id="e31cd-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e31cd-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e31cd-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e31cd-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="e31cd-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e31cd-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e31cd-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="e31cd-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="e31cd-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e31cd-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e31cd-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="e31cd-120">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="e31cd-120">Creates a web app.</span></span> |
| [<span data-ttu-id="e31cd-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e31cd-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="e31cd-122">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="e31cd-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e31cd-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e31cd-123">Next steps</span></span>

<span data-ttu-id="e31cd-124">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e31cd-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e31cd-125">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e31cd-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
