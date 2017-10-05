---
title: Creare un'app per le funzioni e distribuire codice di funzione da GitHub | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'app per le funzioni e distribuire codice di funzione da GitHub
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="5a07a-103">Creare un'app per le funzioni e distribuire codice di funzione da GitHub</span><span class="sxs-lookup"><span data-stu-id="5a07a-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="5a07a-104">Questo script di esempio crea un'app per le funzioni usando il [piano a consumo](../functions-scale.md#consumption-plan) con le relative risorse correlate e distribuisce il codice di funzione da un archivio GitHub pubblico (senza la distribuzione continua).</span><span class="sxs-lookup"><span data-stu-id="5a07a-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="5a07a-105">Per la distribuzione continua del codice di funzione da GitHub, leggere [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md) (Creare un'app per le funzioni ed eseguire la distribuzione continua da GitHub)</span><span class="sxs-lookup"><span data-stu-id="5a07a-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5a07a-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a07a-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5a07a-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="5a07a-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5a07a-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5a07a-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5a07a-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5a07a-109">Sample script</span></span>

<span data-ttu-id="5a07a-110">Questo esempio crea un'app per le funzioni di Azure e distribuisce il codice di funzione da GitHub.</span><span class="sxs-lookup"><span data-stu-id="5a07a-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="5a07a-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Creare un'app per le funzioni con la distribuzione da GitHub")]</span><span class="sxs-lookup"><span data-stu-id="5a07a-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5a07a-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5a07a-112">Script explanation</span></span>

<span data-ttu-id="5a07a-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="5a07a-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="5a07a-114">Questo script usa i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a07a-114">This script uses the following commands:</span></span>

| <span data-ttu-id="5a07a-115">Comando</span><span class="sxs-lookup"><span data-stu-id="5a07a-115">Command</span></span> | <span data-ttu-id="5a07a-116">Note</span><span class="sxs-lookup"><span data-stu-id="5a07a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5a07a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="5a07a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5a07a-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5a07a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5a07a-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="5a07a-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5a07a-120">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="5a07a-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5a07a-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="5a07a-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="5a07a-122">Crea un'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a07a-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="5a07a-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="5a07a-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="5a07a-124">Associa un'app per le funzioni con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="5a07a-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a07a-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a07a-125">Next steps</span></span>

<span data-ttu-id="5a07a-126">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5a07a-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5a07a-127">Altri esempi di script dell'interfaccia della riga di comando di Funzioni di Azure sono disponibili nella [documentazione di Funzioni di Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5a07a-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
