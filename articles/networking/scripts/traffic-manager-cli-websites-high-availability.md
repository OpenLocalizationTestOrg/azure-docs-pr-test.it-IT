---
title: "Esempio di script dell'interfaccia della riga di comando Azure - Instradare il traffico per la disponibilità elevata delle applicazioni | Documentazione Microsoft"
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
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="9aed1-103">Instradare il traffico per la disponibilità elevata delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="9aed1-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="9aed1-104">In questo script viene creato un gruppo di risorse, due piani di servizio app, due app Web, un profilo di gestione traffico e due endpoint di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="9aed1-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="9aed1-105">Gestione traffico indirizza il traffico verso l'applicazione in un'area come area primaria e nell'area secondaria quando l'applicazione nell'area primaria non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="9aed1-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="9aed1-106">Prima di eseguire lo script, è necessario modificare i valori MyWebApp, MyWebAppL1 e MyWebAppL2 in valori univoci in Azure.</span><span class="sxs-lookup"><span data-stu-id="9aed1-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="9aed1-107">Dopo aver eseguito lo script, è possibile accedere all'app nell'area primaria con l'URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="9aed1-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9aed1-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9aed1-108">Sample script</span></span>

<span data-ttu-id="9aed1-109">[!code-azurecli-interactive[principale](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Instradare il traffico per la disponibilità elevata")]</span><span class="sxs-lookup"><span data-stu-id="9aed1-109">[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="9aed1-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="9aed1-110">Clean up deployment</span></span> 

<span data-ttu-id="9aed1-111">Dopo l'esecuzione dello script di esempio, eseguire questo comando per rimuovere il gruppo di risorse, l'app del servizio app e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="9aed1-111">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9aed1-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="9aed1-112">Script explanation</span></span>

<span data-ttu-id="9aed1-113">Questo script usa i comandi seguenti per creare un gruppo di risorse, un'App Web, un profilo di Gestione traffico e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="9aed1-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="9aed1-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="9aed1-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9aed1-115">Comando</span><span class="sxs-lookup"><span data-stu-id="9aed1-115">Command</span></span> | <span data-ttu-id="9aed1-116">Note</span><span class="sxs-lookup"><span data-stu-id="9aed1-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9aed1-117">az group create</span><span class="sxs-lookup"><span data-stu-id="9aed1-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9aed1-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="9aed1-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9aed1-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="9aed1-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9aed1-120">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="9aed1-120">Creates an App Service plan.</span></span> <span data-ttu-id="9aed1-121">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="9aed1-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="9aed1-122">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="9aed1-122">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="9aed1-123">Consente di creare un'App Web di Azure all'interno del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="9aed1-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="9aed1-124">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="9aed1-124">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="9aed1-125">Crea un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="9aed1-125">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="9aed1-126">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="9aed1-126">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="9aed1-127">Aggiunge un endpoint a un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="9aed1-127">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9aed1-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9aed1-128">Next steps</span></span>

<span data-ttu-id="9aed1-129">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9aed1-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9aed1-130">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione della rete di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9aed1-130">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>
