---
title: Creare un'app per le funzioni e distribuire codice di funzione da GitHub | Documentazione Microsoft
description: Creare un'app per le funzioni e distribuire codice di funzione da GitHub
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 67eb41d89328ab57741c419d8b718e19b947dab1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="c5f2f-103">Creare un servizio app</span><span class="sxs-lookup"><span data-stu-id="c5f2f-103">Create an App Service</span></span>

<span data-ttu-id="c5f2f-104">Questo script di esempio crea un'app per le funzioni usando il [piano a consumo](../functions-scale.md#consumption-plan) con le relative risorse correlate e distribuisce in modo continuo il codice di funzione da un archivio GitHub.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="c5f2f-105">In questo esempio è necessario:</span><span class="sxs-lookup"><span data-stu-id="c5f2f-105">In this sample, you need:</span></span>

* <span data-ttu-id="c5f2f-106">Un archivio GitHub contenente il codice di funzione per il quale si hanno autorizzazioni amministrative.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="c5f2f-107">[Token di accesso personale](https://help.github.com/articles/creating-an-access-token-for-command-line-use) per il proprio account GitHub.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c5f2f-108">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c5f2f-109">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="c5f2f-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c5f2f-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c5f2f-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c5f2f-111">Sample script</span></span>

<span data-ttu-id="c5f2f-112">Questo esempio crea un'app per le funzioni di Azure e distribuisce il codice di funzione da GitHub.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="c5f2f-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Servizio di Azure")]</span><span class="sxs-lookup"><span data-stu-id="c5f2f-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c5f2f-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c5f2f-114">Script explanation</span></span>

<span data-ttu-id="c5f2f-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-115">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="c5f2f-116">Questo script usa i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5f2f-116">This script uses the following:</span></span>

| <span data-ttu-id="c5f2f-117">Comando</span><span class="sxs-lookup"><span data-stu-id="c5f2f-117">Command</span></span> | <span data-ttu-id="c5f2f-118">Note</span><span class="sxs-lookup"><span data-stu-id="c5f2f-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c5f2f-119">az group create</span><span class="sxs-lookup"><span data-stu-id="c5f2f-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c5f2f-120">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c5f2f-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="c5f2f-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c5f2f-122">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c5f2f-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="c5f2f-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="c5f2f-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="c5f2f-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="c5f2f-125">Associa un'app per le funzioni con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="c5f2f-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c5f2f-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5f2f-126">Next steps</span></span>

<span data-ttu-id="c5f2f-127">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5f2f-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c5f2f-128">Altri esempi di script dell'interfaccia della riga di comando di Funzioni di Azure sono disponibili nella [documentazione di Funzioni di Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c5f2f-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
