---
title: aaaAzure CLI Script di esempio - creare un'app web e distribuire codice da un repository Git locale | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web e distribuire il codice da un archivio Git locale
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="90917-103">Creare un'App Web e distribuire il codice da un archivio Git locale</span><span class="sxs-lookup"><span data-stu-id="90917-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="90917-104">Questo script di esempio crea un'App Web nel servizio app con le relative risorse correlate e quindi distribuisce il codice dell'App Web in un archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="90917-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="90917-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="90917-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="90917-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="90917-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="90917-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="90917-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="90917-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="90917-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="90917-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="90917-109">Script explanation</span></span>

<span data-ttu-id="90917-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="90917-110">This script uses hello following commands.</span></span> <span data-ttu-id="90917-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="90917-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="90917-112">Comando</span><span class="sxs-lookup"><span data-stu-id="90917-112">Command</span></span> | <span data-ttu-id="90917-113">Note</span><span class="sxs-lookup"><span data-stu-id="90917-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="90917-114">az group create</span><span class="sxs-lookup"><span data-stu-id="90917-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="90917-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="90917-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="90917-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="90917-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="90917-117">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="90917-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="90917-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="90917-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="90917-119">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="90917-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="90917-120">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="90917-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="90917-121">Imposta le credenziali di distribuzione a livello di account hello per servizio App.</span><span class="sxs-lookup"><span data-stu-id="90917-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="90917-122">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="90917-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="90917-123">Crea una configurazione di controllo di origine per un archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="90917-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="90917-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="90917-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="90917-125">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="90917-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="90917-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90917-126">Next steps</span></span>

<span data-ttu-id="90917-127">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="90917-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="90917-128">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="90917-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
