---
title: Creare un'app per le funzioni e distribuire codice di funzione da Visual Studio Team Services | Documentazione Microsoft
description: Creare un'app per le funzioni e distribuire codice di funzione da Visual Studio Team Services
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 2ef177b55ad7ffd351156821f429e6ff8fbeccc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="30672-103">Creare un servizio app</span><span class="sxs-lookup"><span data-stu-id="30672-103">Create an App Service</span></span>

<span data-ttu-id="30672-104">In questo scenario si apprenderà come creare un'app per le funzioni usando il [piano a consumo](../functions-scale.md#consumption-plan) con le risorse correlate e come distribuire in modo continuo il codice di funzione da un archivio di Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="30672-104">In this scenario you will learn how to create a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="30672-105">In questo esempio sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="30672-105">In this sample, you will need:</span></span>

* <span data-ttu-id="30672-106">Archivio VSTS contenente il codice di funzione per il quale si hanno autorizzazioni amministrative.</span><span class="sxs-lookup"><span data-stu-id="30672-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="30672-107">[Token di accesso personale](https://help.github.com/articles/creating-an-access-token-for-command-line-use) per il proprio account GitHub.</span><span class="sxs-lookup"><span data-stu-id="30672-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="30672-108">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="30672-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="30672-109">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="30672-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="30672-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="30672-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="30672-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="30672-111">Sample script</span></span>

<span data-ttu-id="30672-112">Questo esempio crea un'app per le funzioni di Azure e distribuisce il codice di funzione da Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="30672-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

<span data-ttu-id="30672-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Servizio di Azure")]</span><span class="sxs-lookup"><span data-stu-id="30672-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="30672-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="30672-114">Script explanation</span></span>

<span data-ttu-id="30672-115">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'App Web, il DocumentDB e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="30672-115">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="30672-116">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="30672-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="30672-117">Comando</span><span class="sxs-lookup"><span data-stu-id="30672-117">Command</span></span> | <span data-ttu-id="30672-118">Note</span><span class="sxs-lookup"><span data-stu-id="30672-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="30672-119">az group create</span><span class="sxs-lookup"><span data-stu-id="30672-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="30672-120">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="30672-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="30672-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="30672-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="30672-122">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="30672-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="30672-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="30672-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="30672-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="30672-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="30672-125">Associa un'app per le funzioni con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="30672-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="30672-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="30672-126">Next steps</span></span>

<span data-ttu-id="30672-127">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="30672-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="30672-128">Altri esempi di script dell'interfaccia della riga di comando di Funzioni di Azure sono disponibili nella [documentazione di Funzioni di Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="30672-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
