---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Ridimensionare un'App Web manualmente usando l'interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Ridimensionare un'App Web manualmente usando l'interfaccia della riga di comando di Azure 2.0
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: fe05661eb4e2d5c37aebdbfde002b34588db69e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="cbb5c-103">Ridimensionare un'App Web manualmente</span><span class="sxs-lookup"><span data-stu-id="cbb5c-103">Scale a web app manually</span></span>

<span data-ttu-id="cbb5c-104">In questo scenario si apprenderà come creare un gruppo di risorse, un piano di servizio app e un'App Web.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="cbb5c-105">Quindi si dimensionerà il piano di servizio app da una singola istanza a più istanze.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cbb5c-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cbb5c-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="cbb5c-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cbb5c-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cbb5c-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="cbb5c-109">Sample script</span></span>

<span data-ttu-id="cbb5c-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Scalabilità manuale")]</span><span class="sxs-lookup"><span data-stu-id="cbb5c-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cbb5c-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="cbb5c-111">Script explanation</span></span>

<span data-ttu-id="cbb5c-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="cbb5c-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cbb5c-114">Comando</span><span class="sxs-lookup"><span data-stu-id="cbb5c-114">Command</span></span> | <span data-ttu-id="cbb5c-115">Note</span><span class="sxs-lookup"><span data-stu-id="cbb5c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cbb5c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="cbb5c-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cbb5c-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cbb5c-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="cbb5c-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="cbb5c-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-119">Creates an App Service plan.</span></span> <span data-ttu-id="cbb5c-120">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="cbb5c-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="cbb5c-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="cbb5c-122">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="cbb5c-123">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="cbb5c-123">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="cbb5c-124">Aggiorna le proprietà del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="cbb5c-124">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cbb5c-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cbb5c-125">Next steps</span></span>

<span data-ttu-id="cbb5c-126">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cbb5c-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cbb5c-127">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cbb5c-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
