---
title: Creare una funzione di Azure che si connette ad Archiviazione di Azure | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una funzione di Azure che si connette ad Archiviazione di Azure
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
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="7414a-103">Integrare l'app per le funzioni nell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7414a-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="7414a-104">Questo script di esempio crea un'app per le funzioni e un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7414a-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7414a-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="7414a-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7414a-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="7414a-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="7414a-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7414a-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7414a-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7414a-108">Sample script</span></span>

<span data-ttu-id="7414a-109">In questo esempio si crea un'app per le funzioni di Azure e si aggiunge la stringa di connessione di archiviazione a un'impostazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7414a-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="7414a-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrare un'app per le funzioni nell'account di archiviazione di Azure")]</span><span class="sxs-lookup"><span data-stu-id="7414a-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="7414a-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="7414a-111">Clean up deployment</span></span>

<span data-ttu-id="7414a-112">Dopo l'esecuzione dello script di esempio, eseguire questo comando per rimuovere il gruppo di risorse, l'app del servizio app e tutte le risorse correlate:</span><span class="sxs-lookup"><span data-stu-id="7414a-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7414a-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7414a-113">Script explanation</span></span>

<span data-ttu-id="7414a-114">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="7414a-114">This script uses the following commands.</span></span> <span data-ttu-id="7414a-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="7414a-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7414a-116">Comando</span><span class="sxs-lookup"><span data-stu-id="7414a-116">Command</span></span> | <span data-ttu-id="7414a-117">Note</span><span class="sxs-lookup"><span data-stu-id="7414a-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7414a-118">az login</span><span class="sxs-lookup"><span data-stu-id="7414a-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="7414a-119">Accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="7414a-119">Login to Azure.</span></span> |
| [<span data-ttu-id="7414a-120">az group create</span><span class="sxs-lookup"><span data-stu-id="7414a-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7414a-121">Creare un gruppo di risorse con una posizione</span><span class="sxs-lookup"><span data-stu-id="7414a-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="7414a-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="7414a-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="7414a-123">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7414a-123">Create a storage account</span></span> |
| [<span data-ttu-id="7414a-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="7414a-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="7414a-125">Creare una nuova app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="7414a-125">Create a new function app</span></span> |
| [<span data-ttu-id="7414a-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="7414a-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="7414a-127">Eseguire la pulizia</span><span class="sxs-lookup"><span data-stu-id="7414a-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7414a-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7414a-128">Next steps</span></span>

<span data-ttu-id="7414a-129">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7414a-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7414a-130">Altri esempi di script dell'interfaccia della riga di comando di Funzioni di Azure sono disponibili nella [documentazione di Funzioni di Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7414a-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
