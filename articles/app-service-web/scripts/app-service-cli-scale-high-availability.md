---
title: "Esempio di script dell'interfaccia della riga di comando di Azure - Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata | Microsoft Docs"
description: "Esempio di script dell'interfaccia della riga di comando di Azure - Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="c525e-103">Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="c525e-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="c525e-104">In questo scenario verranno creati un gruppo di risorse, due piani di servizio app, due App Web, una profilo di Gestione traffico e due endpoint di endpoint di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="c525e-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="c525e-105">Dopo aver completato l'esercizio si avrà un'architettura a disponibilità elevata che fornisce la disponibilità globale dell'App Web in base alla minima latenza di rete.</span><span class="sxs-lookup"><span data-stu-id="c525e-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c525e-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="c525e-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c525e-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="c525e-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="c525e-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c525e-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="c525e-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c525e-109">Sample script</span></span>

<span data-ttu-id="c525e-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Scalabilità geografica")]</span><span class="sxs-lookup"><span data-stu-id="c525e-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c525e-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c525e-111">Script explanation</span></span>

<span data-ttu-id="c525e-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, un'App Web, un profilo di Gestione traffico e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="c525e-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="c525e-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c525e-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c525e-114">Comando</span><span class="sxs-lookup"><span data-stu-id="c525e-114">Command</span></span> | <span data-ttu-id="c525e-115">Note</span><span class="sxs-lookup"><span data-stu-id="c525e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c525e-116">az group create</span><span class="sxs-lookup"><span data-stu-id="c525e-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c525e-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c525e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c525e-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c525e-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c525e-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="c525e-119">Creates an App Service plan.</span></span> <span data-ttu-id="c525e-120">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c525e-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="c525e-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c525e-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c525e-122">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c525e-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c525e-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="c525e-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="c525e-124">Crea un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="c525e-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="c525e-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="c525e-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="c525e-126">Aggiunge un endpoint a un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="c525e-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c525e-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c525e-127">Next steps</span></span>

<span data-ttu-id="c525e-128">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c525e-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c525e-129">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c525e-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
