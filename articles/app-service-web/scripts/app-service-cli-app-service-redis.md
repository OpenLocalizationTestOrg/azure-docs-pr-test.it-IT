---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Connettere un'App Web a una cache Redis | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Connettere un'App Web a una cache Redis
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="08dda-103">Connettere un'App Web a una cache Redis</span><span class="sxs-lookup"><span data-stu-id="08dda-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="08dda-104">Questo scenario illustra come creare una cache Redis di Azure e un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="08dda-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="08dda-105">La cache Redis viene quindi collegata all'App Web usando le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="08dda-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="08dda-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="08dda-106">Sample script</span></span>

<span data-ttu-id="08dda-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Cache Redis di Azure")]</span><span class="sxs-lookup"><span data-stu-id="08dda-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="08dda-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="08dda-108">Script explanation</span></span>

<span data-ttu-id="08dda-109">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'App Web, la cache Redis e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="08dda-109">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="08dda-110">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="08dda-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="08dda-111">Comando</span><span class="sxs-lookup"><span data-stu-id="08dda-111">Command</span></span> | <span data-ttu-id="08dda-112">Note</span><span class="sxs-lookup"><span data-stu-id="08dda-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="08dda-113">az group create</span><span class="sxs-lookup"><span data-stu-id="08dda-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="08dda-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="08dda-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="08dda-115">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="08dda-115">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="08dda-116">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="08dda-116">Creates an App Service plan.</span></span> <span data-ttu-id="08dda-117">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="08dda-117">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="08dda-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="08dda-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="08dda-119">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="08dda-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="08dda-120">az redis create</span><span class="sxs-lookup"><span data-stu-id="08dda-120">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="08dda-121">Creare una nuova istanza della cache Redis.</span><span class="sxs-lookup"><span data-stu-id="08dda-121">Create new Redis Cache instance.</span></span> <span data-ttu-id="08dda-122">Qui vengono archiviati i dati.</span><span class="sxs-lookup"><span data-stu-id="08dda-122">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="08dda-123">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="08dda-123">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="08dda-124">Elenca le chiavi di accesso per l'istanza della cache Redis.</span><span class="sxs-lookup"><span data-stu-id="08dda-124">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="08dda-125">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="08dda-125">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="08dda-126">Crea o aggiorna un'impostazione per un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="08dda-126">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="08dda-127">Le impostazioni delle app vengono esposte come variabili di ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08dda-127">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08dda-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08dda-128">Next steps</span></span>

<span data-ttu-id="08dda-129">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08dda-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="08dda-130">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="08dda-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
