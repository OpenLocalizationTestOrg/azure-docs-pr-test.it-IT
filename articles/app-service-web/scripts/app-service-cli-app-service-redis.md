---
title: aaaAzure CLI Script di esempio - connettersi a una cache redis di web app tooa | Documenti Microsoft
description: Azure CLI Script di esempio - connettersi a una cache di redis tooa app web
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
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="a70d4-103">Connettersi a una cache di redis tooa app web</span><span class="sxs-lookup"><span data-stu-id="a70d4-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="a70d4-104">In questo scenario si apprenderà come toocreate di Azure redis cache e un'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a70d4-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="a70d4-105">Quindi si procederà al collegamento hello redis cache toohello web app con le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="a70d4-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a70d4-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a70d4-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a70d4-107">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="a70d4-107">Script explanation</span></span>

<span data-ttu-id="a70d4-108">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, app web, redis cache e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="a70d4-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="a70d4-109">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="a70d4-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a70d4-110">Comando</span><span class="sxs-lookup"><span data-stu-id="a70d4-110">Command</span></span> | <span data-ttu-id="a70d4-111">Note</span><span class="sxs-lookup"><span data-stu-id="a70d4-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a70d4-112">az group create</span><span class="sxs-lookup"><span data-stu-id="a70d4-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a70d4-113">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="a70d4-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a70d4-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a70d4-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a70d4-115">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="a70d4-115">Creates an App Service plan.</span></span> <span data-ttu-id="a70d4-116">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a70d4-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a70d4-117">az webapp create</span><span class="sxs-lookup"><span data-stu-id="a70d4-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a70d4-118">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a70d4-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a70d4-119">az redis create</span><span class="sxs-lookup"><span data-stu-id="a70d4-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="a70d4-120">Creare una nuova istanza della cache Redis.</span><span class="sxs-lookup"><span data-stu-id="a70d4-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="a70d4-121">Si tratta in cui verranno archiviati dati hello.</span><span class="sxs-lookup"><span data-stu-id="a70d4-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="a70d4-122">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="a70d4-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="a70d4-123">Elenca le chiavi di accesso hello per l'istanza di cache redis hello.</span><span class="sxs-lookup"><span data-stu-id="a70d4-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="a70d4-124">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="a70d4-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="a70d4-125">Crea o aggiorna un'impostazione per un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a70d4-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="a70d4-126">Le impostazioni delle app vengono esposte come variabili di ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a70d4-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a70d4-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a70d4-127">Next steps</span></span>

<span data-ttu-id="a70d4-128">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a70d4-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a70d4-129">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a70d4-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
