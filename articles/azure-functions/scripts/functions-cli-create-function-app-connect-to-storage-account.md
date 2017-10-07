---
title: aaaCreate una funzione di Azure che si connette tooan di archiviazione di Azure | Documenti Microsoft
description: 'Azure CLI Script di esempio: creare una funzione di Azure che si connette tooan di archiviazione di Azure'
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="87ac0-103">Integrare l'app per le funzioni nell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="87ac0-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="87ac0-104">Questo script di esempio crea un'app per le funzioni e un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="87ac0-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="87ac0-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="87ac0-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="87ac0-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="87ac0-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="87ac0-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="87ac0-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="87ac0-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="87ac0-108">Sample script</span></span>

<span data-ttu-id="87ac0-109">In questo esempio crea un'app di Azure (funzione) e aggiunge l'impostazione dell'app tooan connessione stringa hello archiviazione.</span><span class="sxs-lookup"><span data-stu-id="87ac0-109">This sample creates an Azure Function app and adds hello storage connection string tooan app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="87ac0-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="87ac0-110">Clean up deployment</span></span>

<span data-ttu-id="87ac0-111">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello app del servizio App e tutte le relative risorse:</span><span class="sxs-lookup"><span data-stu-id="87ac0-111">After hello script sample has been run, hello following command can be used tooremove hello resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="87ac0-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="87ac0-112">Script explanation</span></span>

<span data-ttu-id="87ac0-113">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="87ac0-113">This script uses hello following commands.</span></span> <span data-ttu-id="87ac0-114">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="87ac0-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="87ac0-115">Comando</span><span class="sxs-lookup"><span data-stu-id="87ac0-115">Command</span></span> | <span data-ttu-id="87ac0-116">Note</span><span class="sxs-lookup"><span data-stu-id="87ac0-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="87ac0-117">az login</span><span class="sxs-lookup"><span data-stu-id="87ac0-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="87ac0-118">Account di accesso tooAzure.</span><span class="sxs-lookup"><span data-stu-id="87ac0-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="87ac0-119">az group create</span><span class="sxs-lookup"><span data-stu-id="87ac0-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="87ac0-120">Creare un gruppo di risorse con una posizione</span><span class="sxs-lookup"><span data-stu-id="87ac0-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="87ac0-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="87ac0-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="87ac0-122">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="87ac0-122">Create a storage account</span></span> |
| [<span data-ttu-id="87ac0-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="87ac0-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="87ac0-124">Creare una nuova app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="87ac0-124">Create a new function app</span></span> |
| [<span data-ttu-id="87ac0-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="87ac0-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="87ac0-126">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="87ac0-126">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="87ac0-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87ac0-127">Next steps</span></span>

<span data-ttu-id="87ac0-128">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="87ac0-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="87ac0-129">Ulteriori esempi di script di Azure funzioni CLI sono reperibile in hello [documentazione di Azure funzioni](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="87ac0-129">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
