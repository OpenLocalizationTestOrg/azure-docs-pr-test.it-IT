---
title: aaaAzure CLI Script di esempio - connettersi a un tooCosmos app web DB | Documenti Microsoft
description: Azure CLI Script di esempio - Connetti un tooCosmos app web DB
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="352ac-103">Connettersi a un tooCosmos app web DB</span><span class="sxs-lookup"><span data-stu-id="352ac-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="352ac-104">In questo scenario si apprenderà come un account Azure Cosmos DB toocreate e un Azure web app.</span><span class="sxs-lookup"><span data-stu-id="352ac-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="352ac-105">Quindi si procederà al collegamento hello Cosmos DB toohello app web utilizzando le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="352ac-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="352ac-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="352ac-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="352ac-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="352ac-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="352ac-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="352ac-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="352ac-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="352ac-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="352ac-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="352ac-110">Script explanation</span></span>

<span data-ttu-id="352ac-111">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, app web, DB Cosmos e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="352ac-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="352ac-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="352ac-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="352ac-113">Comando</span><span class="sxs-lookup"><span data-stu-id="352ac-113">Command</span></span> | <span data-ttu-id="352ac-114">Note</span><span class="sxs-lookup"><span data-stu-id="352ac-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="352ac-115">az group create</span><span class="sxs-lookup"><span data-stu-id="352ac-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="352ac-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="352ac-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="352ac-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="352ac-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="352ac-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="352ac-118">Creates an App Service plan.</span></span> <span data-ttu-id="352ac-119">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="352ac-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="352ac-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="352ac-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="352ac-121">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="352ac-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="352ac-122">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="352ac-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="352ac-123">Crea un account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="352ac-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="352ac-124">Si tratta in cui verranno archiviati dati hello.</span><span class="sxs-lookup"><span data-stu-id="352ac-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="352ac-125">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="352ac-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="352ac-126">Chiavi di accesso di hello elenchi per hello specificato Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="352ac-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="352ac-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="352ac-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="352ac-128">Crea o aggiorna un'impostazione per un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="352ac-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="352ac-129">Le impostazioni delle app vengono esposte come variabili di ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="352ac-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="352ac-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="352ac-130">Next steps</span></span>

<span data-ttu-id="352ac-131">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="352ac-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="352ac-132">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="352ac-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
