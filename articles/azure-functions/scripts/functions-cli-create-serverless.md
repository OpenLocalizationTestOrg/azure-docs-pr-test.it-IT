---
title: aaaAzure CLI Script di esempio - creare un'App di funzione per l'esecuzione senza | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'app per le funzioni per l'esecuzione senza server
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="f6d17-103">Creare un'app per le funzioni per l'esecuzione senza server</span><span class="sxs-lookup"><span data-stu-id="f6d17-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="f6d17-104">Questo script di esempio crea un'app per le funzioni di Azure che è un contenitore per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="f6d17-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="f6d17-105">Hello funzione App viene creata utilizzando hello [piano il consumo](../functions-scale.md#consumption-plan), che è ideale per basata sugli eventi senza server dei carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f6d17-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f6d17-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f6d17-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f6d17-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="f6d17-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f6d17-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f6d17-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f6d17-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f6d17-109">Sample script</span></span>

<span data-ttu-id="f6d17-110">Questo script crea un'app di Azure funzione usando hello [piano il consumo](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="f6d17-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f6d17-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f6d17-111">Script explanation</span></span>

<span data-ttu-id="f6d17-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="f6d17-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="f6d17-113">Questo script utilizza hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="f6d17-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="f6d17-114">Comando</span><span class="sxs-lookup"><span data-stu-id="f6d17-114">Command</span></span> | <span data-ttu-id="f6d17-115">Note</span><span class="sxs-lookup"><span data-stu-id="f6d17-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f6d17-116">az group create</span><span class="sxs-lookup"><span data-stu-id="f6d17-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f6d17-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="f6d17-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f6d17-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="f6d17-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="f6d17-119">Creare un account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6d17-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="f6d17-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="f6d17-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="f6d17-121">Crea una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6d17-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f6d17-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6d17-122">Next steps</span></span>

<span data-ttu-id="f6d17-123">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f6d17-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f6d17-124">Ulteriori esempi di script di Azure funzioni CLI sono reperibile in hello [documentazione di Azure funzioni](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f6d17-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
