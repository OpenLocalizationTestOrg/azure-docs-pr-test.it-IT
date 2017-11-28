---
title: aaaAzure CLI Script di esempio - creare un'app web con la distribuzione continua da Visual Studio Team Services | Documenti Microsoft
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
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="6df5c-103">Creare un'App Web con distribuzione continua da Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6df5c-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="6df5c-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi configura la distribuzione continua da un repository di Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="6df5c-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="6df5c-105">Per questo esempio sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6df5c-105">For this sample, you will need:</span></span>

* <span data-ttu-id="6df5c-106">Repository Visual Studio Team Services contenente il codice dell'applicazione, con le relative autorizzazioni di amministratore.</span><span class="sxs-lookup"><span data-stu-id="6df5c-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="6df5c-107">[Token di accesso personale](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) per il proprio account Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6df5c-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6df5c-108">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6df5c-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6df5c-109">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="6df5c-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6df5c-110">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6df5c-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6df5c-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="6df5c-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6df5c-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="6df5c-112">Script explanation</span></span>

<span data-ttu-id="6df5c-113">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="6df5c-113">This script uses hello following commands.</span></span> <span data-ttu-id="6df5c-114">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="6df5c-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6df5c-115">Comando</span><span class="sxs-lookup"><span data-stu-id="6df5c-115">Command</span></span> | <span data-ttu-id="6df5c-116">Note</span><span class="sxs-lookup"><span data-stu-id="6df5c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6df5c-117">az group create</span><span class="sxs-lookup"><span data-stu-id="6df5c-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6df5c-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="6df5c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6df5c-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="6df5c-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6df5c-120">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="6df5c-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6df5c-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="6df5c-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6df5c-122">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="6df5c-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6df5c-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="6df5c-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="6df5c-124">Associa un'App Web di Azure con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="6df5c-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="6df5c-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="6df5c-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="6df5c-126">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="6df5c-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6df5c-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6df5c-127">Next steps</span></span>

<span data-ttu-id="6df5c-128">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6df5c-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6df5c-129">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6df5c-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
