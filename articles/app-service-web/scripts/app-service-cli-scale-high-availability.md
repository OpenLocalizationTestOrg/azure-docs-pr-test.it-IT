---
title: "aaaAzure CLI Script di esempio - ridimensionare un'app web in tutto il mondo con un'architettura a elevata disponibilità | Documenti Microsoft"
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
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="0bf5e-103">Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="0bf5e-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="0bf5e-104">In questo scenario verranno creati un gruppo di risorse, due piani di servizio app, due App Web, una profilo di Gestione traffico e due endpoint di endpoint di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="0bf5e-105">Una volta completato l'esercizio hello è un'elevata disponibilità architettura che consente fornisce disponibilità globale dell'app web in base alla latenza di rete più bassa hello.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0bf5e-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0bf5e-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0bf5e-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0bf5e-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="0bf5e-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="0bf5e-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0bf5e-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="0bf5e-110">Script explanation</span></span>

<span data-ttu-id="0bf5e-111">Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, app web, il profilo di gestione traffico hello e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="0bf5e-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0bf5e-113">Comando</span><span class="sxs-lookup"><span data-stu-id="0bf5e-113">Command</span></span> | <span data-ttu-id="0bf5e-114">Note</span><span class="sxs-lookup"><span data-stu-id="0bf5e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0bf5e-115">az group create</span><span class="sxs-lookup"><span data-stu-id="0bf5e-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0bf5e-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0bf5e-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="0bf5e-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0bf5e-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-118">Creates an App Service plan.</span></span> <span data-ttu-id="0bf5e-119">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="0bf5e-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="0bf5e-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="0bf5e-121">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="0bf5e-122">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="0bf5e-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="0bf5e-123">Crea un profilo di Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="0bf5e-124">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="0bf5e-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="0bf5e-125">Aggiunge un tooan endpoint del profilo di Traffic Manager di Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf5e-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0bf5e-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0bf5e-126">Next steps</span></span>

<span data-ttu-id="0bf5e-127">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0bf5e-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0bf5e-128">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0bf5e-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
