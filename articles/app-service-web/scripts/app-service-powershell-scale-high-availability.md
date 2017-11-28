---
title: "Script di PowerShell di esempio - aaaAzure ridimensionare un'app web in tutto il mondo con un'architettura a disponibilità elevata | Documenti Microsoft"
description: "Esempio di script di Azure PowerShell - Ridimensionare un'app Web a livello globale con un'architettura a disponibilità elevata"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="59849-103">Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="59849-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="59849-104">In questo scenario verranno creati un gruppo di risorse, due piani di servizio app, due App Web, una profilo di Gestione traffico e due endpoint di endpoint di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="59849-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="59849-105">Una volta completato l'esercizio hello è un'elevata disponibilità architettura che consente fornisce disponibilità globale dell'app web in base alla latenza di rete più bassa hello.</span><span class="sxs-lookup"><span data-stu-id="59849-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="59849-106">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="59849-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="59849-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="59849-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="59849-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="59849-108">Clean up deployment</span></span> 

<span data-ttu-id="59849-109">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="59849-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="59849-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="59849-110">Script explanation</span></span>

<span data-ttu-id="59849-111">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="59849-111">This script uses hello following commands.</span></span> <span data-ttu-id="59849-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="59849-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="59849-113">Comando</span><span class="sxs-lookup"><span data-stu-id="59849-113">Command</span></span> | <span data-ttu-id="59849-114">Note</span><span class="sxs-lookup"><span data-stu-id="59849-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="59849-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="59849-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="59849-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="59849-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="59849-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="59849-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="59849-118">Crea un profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="59849-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="59849-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="59849-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="59849-120">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="59849-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="59849-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="59849-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="59849-122">Crea un'App Web.</span><span class="sxs-lookup"><span data-stu-id="59849-122">Creates a web app.</span></span> |
| [<span data-ttu-id="59849-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="59849-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="59849-124">Crea un endpoint nel profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="59849-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="59849-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59849-125">Next steps</span></span>

<span data-ttu-id="59849-126">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="59849-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="59849-127">Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="59849-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
