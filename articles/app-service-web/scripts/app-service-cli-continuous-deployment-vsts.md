---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web con distribuzione continua da Visual Studio Team Services | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web con distribuzione continua da Visual Studio Team Services
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="c6648-103">Creare un'App Web con distribuzione continua da Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="c6648-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="c6648-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi configura la distribuzione continua da un repository di Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="c6648-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="c6648-105">Per questo esempio sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6648-105">For this sample, you will need:</span></span>

* <span data-ttu-id="c6648-106">Repository Visual Studio Team Services contenente il codice dell'applicazione, con le relative autorizzazioni di amministratore.</span><span class="sxs-lookup"><span data-stu-id="c6648-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="c6648-107">[Token di accesso personale](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) per il proprio account Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="c6648-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c6648-108">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6648-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c6648-109">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="c6648-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="c6648-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c6648-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c6648-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c6648-111">Sample script</span></span>

<span data-ttu-id="c6648-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Creare un'App Web con distribuzione continua da Visual Studio Team Services")]</span><span class="sxs-lookup"><span data-stu-id="c6648-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c6648-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c6648-113">Script explanation</span></span>

<span data-ttu-id="c6648-114">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c6648-114">This script uses the following commands.</span></span> <span data-ttu-id="c6648-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c6648-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c6648-116">Comando</span><span class="sxs-lookup"><span data-stu-id="c6648-116">Command</span></span> | <span data-ttu-id="c6648-117">Note</span><span class="sxs-lookup"><span data-stu-id="c6648-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c6648-118">az group create</span><span class="sxs-lookup"><span data-stu-id="c6648-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c6648-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c6648-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c6648-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c6648-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c6648-121">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="c6648-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c6648-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c6648-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c6648-123">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6648-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c6648-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="c6648-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="c6648-125">Associa un'App Web di Azure con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="c6648-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="c6648-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="c6648-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="c6648-127">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="c6648-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6648-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6648-128">Next steps</span></span>

<span data-ttu-id="c6648-129">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6648-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c6648-130">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c6648-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
