---
title: aaaCreate un'App di funzione e distribuire codice della funzione da Visual Studio Team Services | Documenti Microsoft
description: Creare un'app per le funzioni e distribuire codice di funzione da Visual Studio Team Services
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 774bee73025cc9ac46f8b2a6c10edbfa3c2d353b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="501b3-103">Creare un servizio app</span><span class="sxs-lookup"><span data-stu-id="501b3-103">Create an App Service</span></span>

<span data-ttu-id="501b3-104">In questo scenario si apprenderà come un'app in funzione usando toocreate hello [piano il consumo](../functions-scale.md#consumption-plan) con le relative risorse correlate e distribuisce continuamente il codice della funzione da un repository di Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="501b3-104">In this scenario you will learn how toocreate a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="501b3-105">In questo esempio sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="501b3-105">In this sample, you will need:</span></span>

* <span data-ttu-id="501b3-106">Archivio VSTS contenente il codice di funzione per il quale si hanno autorizzazioni amministrative.</span><span class="sxs-lookup"><span data-stu-id="501b3-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="501b3-107">[Token di accesso personale](https://help.github.com/articles/creating-an-access-token-for-command-line-use) per il proprio account GitHub.</span><span class="sxs-lookup"><span data-stu-id="501b3-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="501b3-108">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="501b3-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="501b3-109">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="501b3-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="501b3-110">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="501b3-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="501b3-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="501b3-111">Sample script</span></span>

<span data-ttu-id="501b3-112">Questo esempio crea un'app per le funzioni di Azure e distribuisce il codice di funzione da Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="501b3-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="501b3-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="501b3-113">Script explanation</span></span>

<span data-ttu-id="501b3-114">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, app web, documentdb e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="501b3-114">This script uses hello following commands toocreate a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="501b3-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="501b3-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="501b3-116">Comando</span><span class="sxs-lookup"><span data-stu-id="501b3-116">Command</span></span> | <span data-ttu-id="501b3-117">Note</span><span class="sxs-lookup"><span data-stu-id="501b3-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="501b3-118">az group create</span><span class="sxs-lookup"><span data-stu-id="501b3-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="501b3-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="501b3-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="501b3-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="501b3-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="501b3-121">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="501b3-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="501b3-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="501b3-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="501b3-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="501b3-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="501b3-124">Associa un'app per le funzioni con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="501b3-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="501b3-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="501b3-125">Next steps</span></span>

<span data-ttu-id="501b3-126">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="501b3-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="501b3-127">Ulteriori esempi di script di Azure funzioni CLI sono reperibile in hello [documentazione di Azure funzioni](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="501b3-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
