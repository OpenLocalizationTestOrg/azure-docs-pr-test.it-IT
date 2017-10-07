---
title: aaaAzure CLI Script di esempio - creare un'app web con la distribuzione da GitHub | Documenti Microsoft
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
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="b8a4f-103">Creare un'App Web con la distribuzione da GitHub</span><span class="sxs-lookup"><span data-stu-id="b8a4f-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="b8a4f-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi distribuisce il codice dell'App Web da un archivio GitHub (senza la distribuzione continua).</span><span class="sxs-lookup"><span data-stu-id="b8a4f-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="b8a4f-105">Per la distribuzione di GitHub con distribuzione continua, vedere [Creare un'App Web con distribuzione continua da GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="b8a4f-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b8a4f-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b8a4f-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b8a4f-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b8a4f-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b8a4f-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="b8a4f-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b8a4f-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="b8a4f-110">Script explanation</span></span> 

<span data-ttu-id="b8a4f-111">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-111">This script uses hello following commands.</span></span> <span data-ttu-id="b8a4f-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b8a4f-113">Comando</span><span class="sxs-lookup"><span data-stu-id="b8a4f-113">Command</span></span> | <span data-ttu-id="b8a4f-114">Note</span><span class="sxs-lookup"><span data-stu-id="b8a4f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b8a4f-115">az group create</span><span class="sxs-lookup"><span data-stu-id="b8a4f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b8a4f-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b8a4f-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="b8a4f-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b8a4f-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="b8a4f-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="b8a4f-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b8a4f-120">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b8a4f-121">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="b8a4f-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="b8a4f-122">Associa un'App Web di Azure con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="b8a4f-123">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="b8a4f-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="b8a4f-124">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="b8a4f-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b8a4f-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8a4f-125">Next steps</span></span>

<span data-ttu-id="b8a4f-126">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b8a4f-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b8a4f-127">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b8a4f-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
