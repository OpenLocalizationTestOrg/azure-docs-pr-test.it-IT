---
title: aaaAzure CLI Script di esempio - creare un'app web con una distribuzione continua da GitHub | Documenti Microsoft
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
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="aea38-103">Creare un'App Web con distribuzione continua da GitHub</span><span class="sxs-lookup"><span data-stu-id="aea38-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="aea38-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi configura la distribuzione continua da un archivio GitHub.</span><span class="sxs-lookup"><span data-stu-id="aea38-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="aea38-105">Per la distribuzione GitHub senza distribuzione continua, vedere [Creare un'App Web e distribuire il codice da GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="aea38-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="aea38-106">In questo esempio sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aea38-106">In this sample, you will need:</span></span>

* <span data-ttu-id="aea38-107">Repository GitHub contenente il codice dell'applicazione, con le relative autorizzazioni di amministratore.</span><span class="sxs-lookup"><span data-stu-id="aea38-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="aea38-108">[Token di accesso personale](https://help.github.com/articles/creating-an-access-token-for-command-line-use) per il proprio account GitHub.</span><span class="sxs-lookup"><span data-stu-id="aea38-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aea38-109">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="aea38-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="aea38-110">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="aea38-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="aea38-111">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aea38-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="aea38-112">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="aea38-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="aea38-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="aea38-113">Script explanation</span></span>

<span data-ttu-id="aea38-114">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="aea38-114">This script uses hello following commands.</span></span> <span data-ttu-id="aea38-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="aea38-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="aea38-116">Comando</span><span class="sxs-lookup"><span data-stu-id="aea38-116">Command</span></span> | <span data-ttu-id="aea38-117">Note</span><span class="sxs-lookup"><span data-stu-id="aea38-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aea38-118">az group create</span><span class="sxs-lookup"><span data-stu-id="aea38-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="aea38-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="aea38-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="aea38-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="aea38-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="aea38-121">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="aea38-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="aea38-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="aea38-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="aea38-123">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="aea38-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="aea38-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="aea38-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="aea38-125">Associa un'App Web di Azure con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="aea38-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="aea38-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="aea38-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="aea38-127">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="aea38-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aea38-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aea38-128">Next steps</span></span>

<span data-ttu-id="aea38-129">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aea38-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="aea38-130">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="aea38-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
