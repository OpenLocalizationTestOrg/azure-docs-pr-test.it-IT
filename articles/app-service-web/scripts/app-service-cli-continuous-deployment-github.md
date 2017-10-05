---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web con distribuzione continua da GitHub | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web con distribuzione continua da GitHub
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
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="c468f-103">Creare un'App Web con distribuzione continua da GitHub</span><span class="sxs-lookup"><span data-stu-id="c468f-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="c468f-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi configura la distribuzione continua da un archivio GitHub.</span><span class="sxs-lookup"><span data-stu-id="c468f-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="c468f-105">Per la distribuzione GitHub senza distribuzione continua, vedere [Creare un'App Web e distribuire il codice da GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="c468f-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="c468f-106">In questo esempio sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c468f-106">In this sample, you will need:</span></span>

* <span data-ttu-id="c468f-107">Repository GitHub contenente il codice dell'applicazione, con le relative autorizzazioni di amministratore.</span><span class="sxs-lookup"><span data-stu-id="c468f-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="c468f-108">[Token di accesso personale](https://help.github.com/articles/creating-an-access-token-for-command-line-use) per il proprio account GitHub.</span><span class="sxs-lookup"><span data-stu-id="c468f-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c468f-109">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="c468f-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c468f-110">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="c468f-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="c468f-111">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c468f-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c468f-112">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c468f-112">Sample script</span></span>

<span data-ttu-id="c468f-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Creare un'App Web con distribuzione continua da GitHub")]</span><span class="sxs-lookup"><span data-stu-id="c468f-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c468f-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c468f-114">Script explanation</span></span>

<span data-ttu-id="c468f-115">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c468f-115">This script uses the following commands.</span></span> <span data-ttu-id="c468f-116">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c468f-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c468f-117">Comando</span><span class="sxs-lookup"><span data-stu-id="c468f-117">Command</span></span> | <span data-ttu-id="c468f-118">Note</span><span class="sxs-lookup"><span data-stu-id="c468f-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c468f-119">az group create</span><span class="sxs-lookup"><span data-stu-id="c468f-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c468f-120">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c468f-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c468f-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c468f-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c468f-122">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="c468f-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c468f-123">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c468f-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c468f-124">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c468f-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c468f-125">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="c468f-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="c468f-126">Associa un'App Web di Azure con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="c468f-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="c468f-127">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="c468f-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="c468f-128">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="c468f-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c468f-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c468f-129">Next steps</span></span>

<span data-ttu-id="c468f-130">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c468f-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c468f-131">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c468f-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
