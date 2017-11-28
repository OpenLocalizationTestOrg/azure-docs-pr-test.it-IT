---
title: aaaAzure CLI Script di esempio - creare un'App di funzione in un piano di servizio App | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'app per le funzioni in un piano di servizio app
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="4d3fd-103">Creare un'app per le funzioni in un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="4d3fd-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="4d3fd-104">Questo script di esempio crea un'app per le funzioni di Azure che è un contenitore per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="4d3fd-105">Funzione App Hello viene creato utilizzando un piano di servizio App dedicato, ovvero che le risorse del server sono sempre attivi.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4d3fd-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4d3fd-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4d3fd-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4d3fd-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4d3fd-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="4d3fd-109">Sample script</span></span>

<span data-ttu-id="4d3fd-110">Questo script crea un'app per le funzioni di Azure usando un [piano di servizio app](../functions-scale.md#app-service-plan) dedicato.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4d3fd-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="4d3fd-111">Script explanation</span></span>

<span data-ttu-id="4d3fd-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="4d3fd-113">Questo script utilizza hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="4d3fd-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="4d3fd-114">Comando</span><span class="sxs-lookup"><span data-stu-id="4d3fd-114">Command</span></span> | <span data-ttu-id="4d3fd-115">Note</span><span class="sxs-lookup"><span data-stu-id="4d3fd-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4d3fd-116">az group create</span><span class="sxs-lookup"><span data-stu-id="4d3fd-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4d3fd-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4d3fd-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="4d3fd-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="4d3fd-119">Creare un account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="4d3fd-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="4d3fd-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="4d3fd-121">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4d3fd-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="4d3fd-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="4d3fd-123">Crea un'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3fd-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4d3fd-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d3fd-124">Next steps</span></span>

<span data-ttu-id="4d3fd-125">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4d3fd-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4d3fd-126">Ulteriori esempi di script di Azure funzioni CLI sono reperibile in hello [documentazione di Azure funzioni](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4d3fd-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
