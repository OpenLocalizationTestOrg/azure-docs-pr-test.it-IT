---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'app per le funzioni in un piano di servizio app | Documentazione Microsoft
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
ms.openlocfilehash: 40c3fa6fa6c07d59e4bf55531e116ba50aa92b91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="5064d-103">Creare un'app per le funzioni in un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="5064d-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="5064d-104">Questo script di esempio crea un'app per le funzioni di Azure che è un contenitore per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="5064d-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="5064d-105">L'app per le funzioni viene creata usando un piano di servizio app dedicato, ovvero le risorse del server sono sempre attive.</span><span class="sxs-lookup"><span data-stu-id="5064d-105">The Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5064d-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5064d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5064d-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="5064d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5064d-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5064d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5064d-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5064d-109">Sample script</span></span>

<span data-ttu-id="5064d-110">Questo script crea un'app per le funzioni di Azure usando un [piano di servizio app](../functions-scale.md#app-service-plan) dedicato.</span><span class="sxs-lookup"><span data-stu-id="5064d-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

<span data-ttu-id="5064d-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Creare una funzione di Azure in un piano di servizio app")]</span><span class="sxs-lookup"><span data-stu-id="5064d-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5064d-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5064d-112">Script explanation</span></span>

<span data-ttu-id="5064d-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="5064d-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="5064d-114">Questo script usa i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5064d-114">This script uses the following commands:</span></span>

| <span data-ttu-id="5064d-115">Comando</span><span class="sxs-lookup"><span data-stu-id="5064d-115">Command</span></span> | <span data-ttu-id="5064d-116">Note</span><span class="sxs-lookup"><span data-stu-id="5064d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5064d-117">az group create</span><span class="sxs-lookup"><span data-stu-id="5064d-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5064d-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5064d-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5064d-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="5064d-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="5064d-120">Creare un account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5064d-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="5064d-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5064d-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="5064d-122">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="5064d-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5064d-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="5064d-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="5064d-124">Crea un'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="5064d-124">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5064d-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5064d-125">Next steps</span></span>

<span data-ttu-id="5064d-126">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5064d-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5064d-127">Altri esempi di script dell'interfaccia della riga di comando di Funzioni di Azure sono disponibili nella [documentazione di Funzioni di Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5064d-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
