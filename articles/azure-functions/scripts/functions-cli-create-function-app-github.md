---
title: aaaCreate un'App di funzione e distribuire codice della funzione da GitHub | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'app per le funzioni e distribuire codice di funzione da GitHub
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="8ad9c-103">Creare un'app per le funzioni e distribuire codice di funzione da GitHub</span><span class="sxs-lookup"><span data-stu-id="8ad9c-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="8ad9c-104">Questo script di esempio crea un'app di funzione usando hello [piano il consumo](../functions-scale.md#consumption-plan) con le relative risorse correlate e consente di distribuire il codice della funzione da un repository GitHub pubblico (senza la distribuzione continua).</span><span class="sxs-lookup"><span data-stu-id="8ad9c-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="8ad9c-105">Per la distribuzione continua del codice di funzione da GitHub, leggere [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md) (Creare un'app per le funzioni ed eseguire la distribuzione continua da GitHub)</span><span class="sxs-lookup"><span data-stu-id="8ad9c-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8ad9c-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8ad9c-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8ad9c-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="8ad9c-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8ad9c-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8ad9c-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8ad9c-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="8ad9c-109">Sample script</span></span>

<span data-ttu-id="8ad9c-110">Questo esempio crea un'app per le funzioni di Azure e distribuisce il codice di funzione da GitHub.</span><span class="sxs-lookup"><span data-stu-id="8ad9c-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8ad9c-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="8ad9c-111">Script explanation</span></span>

<span data-ttu-id="8ad9c-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="8ad9c-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="8ad9c-113">Questo script utilizza hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="8ad9c-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="8ad9c-114">Comando</span><span class="sxs-lookup"><span data-stu-id="8ad9c-114">Command</span></span> | <span data-ttu-id="8ad9c-115">Note</span><span class="sxs-lookup"><span data-stu-id="8ad9c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8ad9c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="8ad9c-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8ad9c-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="8ad9c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8ad9c-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="8ad9c-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8ad9c-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="8ad9c-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8ad9c-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="8ad9c-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="8ad9c-121">Crea un'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ad9c-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="8ad9c-122">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="8ad9c-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="8ad9c-123">Associa un'app per le funzioni con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="8ad9c-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8ad9c-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ad9c-124">Next steps</span></span>

<span data-ttu-id="8ad9c-125">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ad9c-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8ad9c-126">Ulteriori esempi di script di Azure funzioni CLI sono reperibile in hello [documentazione di Azure funzioni](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8ad9c-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
