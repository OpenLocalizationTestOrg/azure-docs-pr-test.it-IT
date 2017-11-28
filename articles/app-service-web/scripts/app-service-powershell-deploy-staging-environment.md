---
title: aaaAzure Script di PowerShell di esempio - creare un'app web e distribuire codice tooa ambiente di gestione temporanea | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - creare un'app web e distribuire codice tooa ambiente di gestione temporanea
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
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="21509-103">Creare un'app web e distribuire codice tooa ambiente di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="21509-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="21509-104">Questo script di esempio crea un'app web nel servizio App con uno slot di distribuzione aggiuntivo denominato "gestione temporanea" e quindi distribuisce un toohello di app di esempio "gestione temporanea" slot.</span><span class="sxs-lookup"><span data-stu-id="21509-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="21509-105">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="21509-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="21509-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="21509-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="21509-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="21509-107">Clean up deployment</span></span> 

<span data-ttu-id="21509-108">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="21509-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="21509-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="21509-109">Script explanation</span></span>

<span data-ttu-id="21509-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="21509-110">This script uses hello following commands.</span></span> <span data-ttu-id="21509-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="21509-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="21509-112">Comando</span><span class="sxs-lookup"><span data-stu-id="21509-112">Command</span></span> | <span data-ttu-id="21509-113">Note</span><span class="sxs-lookup"><span data-stu-id="21509-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="21509-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="21509-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="21509-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="21509-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="21509-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="21509-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="21509-117">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="21509-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="21509-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="21509-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="21509-119">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="21509-119">Creates a web app.</span></span> |
| [<span data-ttu-id="21509-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="21509-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="21509-121">Modifica il livello di prezzo di un toochange piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="21509-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="21509-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="21509-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="21509-123">Crea uno slot di distribuzione per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="21509-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="21509-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="21509-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="21509-125">Modifica una risorsa in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="21509-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="21509-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="21509-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="21509-127">Trasferisce uno slot di distribuzione dell'app Web nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="21509-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21509-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21509-128">Next steps</span></span>

<span data-ttu-id="21509-129">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="21509-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="21509-130">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="21509-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
