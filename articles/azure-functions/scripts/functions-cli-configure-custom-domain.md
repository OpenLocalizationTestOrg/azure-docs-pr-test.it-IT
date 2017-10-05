---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Eseguire il mapping di un dominio personalizzato a un'app per le funzioni | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Eseguire il mapping di un dominio personalizzato a un'app per le funzioni in Azure.
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="c75a9-103">Esegue il mapping di un dominio personalizzato a un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="c75a9-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="c75a9-104">Questo script di esempio crea un'app per le funzioni con le relative risorse e quindi esegue il mapping di `www.<yourdomain>` a essa.</span><span class="sxs-lookup"><span data-stu-id="c75a9-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="c75a9-105">Per eseguire il mapping a un dominio personalizzato, è necessario creare l'app per le funzioni in un piano di servizio app e non in un piano a consumo.</span><span class="sxs-lookup"><span data-stu-id="c75a9-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="c75a9-106">Funzioni di Azure supporta il mapping di un dominio personalizzato solo usando un record A.</span><span class="sxs-lookup"><span data-stu-id="c75a9-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c75a9-107">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="c75a9-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c75a9-108">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="c75a9-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="c75a9-109">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c75a9-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="c75a9-110">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c75a9-110">Sample script</span></span>

<span data-ttu-id="c75a9-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Eseguire il mapping di un dominio personalizzato a un'app per le funzioni")]</span><span class="sxs-lookup"><span data-stu-id="c75a9-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c75a9-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c75a9-112">Script explanation</span></span>

<span data-ttu-id="c75a9-113">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c75a9-113">This script uses the following commands.</span></span> <span data-ttu-id="c75a9-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c75a9-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c75a9-115">Comando</span><span class="sxs-lookup"><span data-stu-id="c75a9-115">Command</span></span> | <span data-ttu-id="c75a9-116">Note</span><span class="sxs-lookup"><span data-stu-id="c75a9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c75a9-117">az group create</span><span class="sxs-lookup"><span data-stu-id="c75a9-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c75a9-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c75a9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c75a9-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="c75a9-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="c75a9-120">Crea un account di archiviazione necessario per l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="c75a9-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="c75a9-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c75a9-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c75a9-122">Crea un piano di servizio app necessario per eseguire il mapping di un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c75a9-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="c75a9-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="c75a9-123">az functionapp create</span></span>]() | <span data-ttu-id="c75a9-124">Creare un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="c75a9-124">Creates a function app.</span></span> |
| [<span data-ttu-id="c75a9-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="c75a9-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="c75a9-126">Esegue il mapping di un dominio personalizzato a un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="c75a9-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c75a9-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c75a9-127">Next steps</span></span>

<span data-ttu-id="c75a9-128">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c75a9-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c75a9-129">Altri esempi di script dell'interfaccia della riga di comando di Funzioni di Azure sono disponibili nella [documentazione di Funzioni di Azure]().</span><span class="sxs-lookup"><span data-stu-id="c75a9-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
