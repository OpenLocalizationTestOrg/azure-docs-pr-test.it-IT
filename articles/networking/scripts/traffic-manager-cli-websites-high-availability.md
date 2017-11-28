---
title: "aaaAzure CLI Script di esempio - instradare il traffico per la disponibilità elevata delle applicazioni | Documenti Microsoft"
description: "Esempio di script dell'interfaccia della riga di comando Azure - Instradare il traffico per la disponibilità elevata delle applicazioni"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="a6eb5-103">Instradare il traffico per la disponibilità elevata delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="a6eb5-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="a6eb5-104">In questo script viene creato un gruppo di risorse, due piani di servizio app, due app Web, un profilo di gestione traffico e due endpoint di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="a6eb5-105">Gestione traffico indirizza applicazione toohello il traffico in un'area come area primaria hello e area secondaria toohello quando un'applicazione hello nell'area primaria hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="a6eb5-106">Prima di eseguire script hello, è necessario modificare hello MyWebApp, MyWebAppL1 e MyWebAppL2 valori toounique valori in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="a6eb5-107">Dopo l'esecuzione di script hello, è possibile accedere app hello nell'area primaria di hello con mywebapp.trafficmanager.net URL hello.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a6eb5-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a6eb5-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="a6eb5-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a6eb5-109">Clean up deployment</span></span> 

<span data-ttu-id="a6eb5-110">Dopo l'esecuzione di script di esempio hello, comando seguire hello può essere utilizzato tooremove gruppo di risorse hello, applicazione di servizio App e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a6eb5-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="a6eb5-111">Script explanation</span></span>

<span data-ttu-id="a6eb5-112">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, app web, il profilo di gestione traffico hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="a6eb5-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a6eb5-114">Comando</span><span class="sxs-lookup"><span data-stu-id="a6eb5-114">Command</span></span> | <span data-ttu-id="a6eb5-115">Note</span><span class="sxs-lookup"><span data-stu-id="a6eb5-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a6eb5-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a6eb5-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a6eb5-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a6eb5-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a6eb5-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a6eb5-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-119">Creates an App Service plan.</span></span> <span data-ttu-id="a6eb5-120">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a6eb5-121">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="a6eb5-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="a6eb5-122">Crea un'app web di Azure all'interno di hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="a6eb5-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="a6eb5-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="a6eb5-124">Crea un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="a6eb5-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="a6eb5-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="a6eb5-126">Aggiunge un tooan endpoint del profilo di Traffic Manager di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6eb5-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a6eb5-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6eb5-127">Next steps</span></span>

<span data-ttu-id="a6eb5-128">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6eb5-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a6eb5-129">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [rete Azure documentazione](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a6eb5-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
