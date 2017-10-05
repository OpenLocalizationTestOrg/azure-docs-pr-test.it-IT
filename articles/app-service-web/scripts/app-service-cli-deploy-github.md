---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web con distribuzione da GitHub | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web con distribuzione da GitHub
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="494f1-103">Creare un'App Web con la distribuzione da GitHub</span><span class="sxs-lookup"><span data-stu-id="494f1-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="494f1-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi distribuisce il codice dell'App Web da un archivio GitHub (senza la distribuzione continua).</span><span class="sxs-lookup"><span data-stu-id="494f1-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="494f1-105">Per la distribuzione di GitHub con distribuzione continua, vedere [Creare un'App Web con distribuzione continua da GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="494f1-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="494f1-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="494f1-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="494f1-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="494f1-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="494f1-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="494f1-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="494f1-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="494f1-109">Sample script</span></span>

<span data-ttu-id="494f1-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Creare un'App Web con la distribuzione da GitHub")]</span><span class="sxs-lookup"><span data-stu-id="494f1-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="494f1-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="494f1-111">Script explanation</span></span> 

<span data-ttu-id="494f1-112">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="494f1-112">This script uses the following commands.</span></span> <span data-ttu-id="494f1-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="494f1-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="494f1-114">Comando</span><span class="sxs-lookup"><span data-stu-id="494f1-114">Command</span></span> | <span data-ttu-id="494f1-115">Note</span><span class="sxs-lookup"><span data-stu-id="494f1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="494f1-116">az group create</span><span class="sxs-lookup"><span data-stu-id="494f1-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="494f1-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="494f1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="494f1-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="494f1-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="494f1-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="494f1-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="494f1-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="494f1-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="494f1-121">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="494f1-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="494f1-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="494f1-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="494f1-123">Associa un'App Web di Azure con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="494f1-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="494f1-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="494f1-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="494f1-125">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="494f1-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="494f1-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="494f1-126">Next steps</span></span>

<span data-ttu-id="494f1-127">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="494f1-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="494f1-128">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="494f1-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
