---
title: Esempio di Script di PowerShell - aaaAzure assegnare un'app web tooa di dominio personalizzato | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - assegna un'app web tooa di dominio personalizzato
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
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="f4203-103">Assegnare un'app web tooa di dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="f4203-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="f4203-104">Questo script di esempio crea un'app web nel servizio App con le relative risorse correlate e quindi esegue il mapping di `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="f4203-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="f4203-105">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="f4203-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="f4203-106">Inoltre, è necessario pagina di configurazione del Registro di toohave accesso tooyour dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="f4203-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f4203-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f4203-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f4203-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f4203-108">Clean up deployment</span></span> 

<span data-ttu-id="f4203-109">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="f4203-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f4203-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f4203-110">Script explanation</span></span>

<span data-ttu-id="f4203-111">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="f4203-111">This script uses hello following commands.</span></span> <span data-ttu-id="f4203-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="f4203-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f4203-113">Comando</span><span class="sxs-lookup"><span data-stu-id="f4203-113">Command</span></span> | <span data-ttu-id="f4203-114">Note</span><span class="sxs-lookup"><span data-stu-id="f4203-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f4203-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f4203-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f4203-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="f4203-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f4203-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f4203-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f4203-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="f4203-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f4203-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f4203-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f4203-120">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="f4203-120">Creates a web app.</span></span> |
| [<span data-ttu-id="f4203-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f4203-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="f4203-122">Modifica il livello di prezzo di un toochange piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="f4203-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="f4203-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f4203-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f4203-124">Modifica la configurazione di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="f4203-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f4203-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4203-125">Next steps</span></span>

<span data-ttu-id="f4203-126">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f4203-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f4203-127">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f4203-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
