---
title: 'Esempio di script dell''interfaccia della riga di comando di Azure : connettere un''app Web a Cosmos DB | Microsoft Docs'
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: connettere un''app Web a Cosmos DB'
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
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="211a9-103">Connettere un'app Web a Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="211a9-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="211a9-104">Questo scenario illustra come creare un account Cosmos DB di Azure e un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="211a9-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="211a9-105">Cosmos DB viene quindi collegato all'app Web tramite le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="211a9-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="211a9-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="211a9-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="211a9-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="211a9-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="211a9-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="211a9-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="211a9-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="211a9-109">Sample script</span></span>

<span data-ttu-id="211a9-110">[!code-azurecli-interactive[principale](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="211a9-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="211a9-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="211a9-111">Script explanation</span></span>

<span data-ttu-id="211a9-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'app Web, il Cosmos DB e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="211a9-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="211a9-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="211a9-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="211a9-114">Comando</span><span class="sxs-lookup"><span data-stu-id="211a9-114">Command</span></span> | <span data-ttu-id="211a9-115">Note</span><span class="sxs-lookup"><span data-stu-id="211a9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="211a9-116">az group create</span><span class="sxs-lookup"><span data-stu-id="211a9-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="211a9-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="211a9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="211a9-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="211a9-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="211a9-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="211a9-119">Creates an App Service plan.</span></span> <span data-ttu-id="211a9-120">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="211a9-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="211a9-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="211a9-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="211a9-122">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="211a9-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="211a9-123">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="211a9-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="211a9-124">Crea un account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="211a9-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="211a9-125">Qui vengono archiviati i dati.</span><span class="sxs-lookup"><span data-stu-id="211a9-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="211a9-126">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="211a9-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="211a9-127">Elenca le chiavi di accesso per l'account Cosmos DB specificato.</span><span class="sxs-lookup"><span data-stu-id="211a9-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="211a9-128">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="211a9-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="211a9-129">Crea o aggiorna un'impostazione per un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="211a9-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="211a9-130">Le impostazioni delle app vengono esposte come variabili di ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="211a9-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="211a9-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="211a9-131">Next steps</span></span>

<span data-ttu-id="211a9-132">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="211a9-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="211a9-133">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="211a9-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
