---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Connettere un'App Web a un account di archiviazione | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Connettere un'App Web a un account di archiviazione
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
ms.openlocfilehash: 2520eecf54b77b88d6aa1ba2e538d05e3407f3d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="4846b-103">Connettere un'App Web a un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4846b-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="4846b-104">Questo scenario illustra come creare un account di archiviazione di Azure e un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="4846b-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="4846b-105">L'account di archiviazione viene quindi collegato all'App Web usando le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="4846b-105">Then you will link the storage account to the web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4846b-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="4846b-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4846b-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="4846b-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="4846b-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4846b-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="4846b-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="4846b-109">Sample script</span></span>

<span data-ttu-id="4846b-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Archiviazione di Azure")]</span><span class="sxs-lookup"><span data-stu-id="4846b-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4846b-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="4846b-111">Script explanation</span></span>

<span data-ttu-id="4846b-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'App Web, l'account di archiviazione e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="4846b-112">This script uses the following commands to create a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="4846b-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="4846b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4846b-114">Comando</span><span class="sxs-lookup"><span data-stu-id="4846b-114">Command</span></span> | <span data-ttu-id="4846b-115">Note</span><span class="sxs-lookup"><span data-stu-id="4846b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4846b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="4846b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4846b-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="4846b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4846b-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="4846b-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4846b-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="4846b-119">Creates an App Service plan.</span></span> <span data-ttu-id="4846b-120">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="4846b-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="4846b-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="4846b-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="4846b-122">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="4846b-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="4846b-123">az storage account create</span><span class="sxs-lookup"><span data-stu-id="4846b-123">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="4846b-124">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4846b-124">Creates a storage account.</span></span> <span data-ttu-id="4846b-125">Qui vengono archiviati gli asset statici.</span><span class="sxs-lookup"><span data-stu-id="4846b-125">This is where the static assets will be stored.</span></span> |
| [<span data-ttu-id="4846b-126">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="4846b-126">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="4846b-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="4846b-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="4846b-128">Crea o aggiorna un'impostazione per un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="4846b-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="4846b-129">Le impostazioni delle app vengono esposte come variabili di ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4846b-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4846b-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4846b-130">Next steps</span></span>

<span data-ttu-id="4846b-131">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4846b-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4846b-132">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4846b-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
