---
title: aaaAzure CLI Script di esempio - eseguire il mapping di un'app di funzione tooa dominio personalizzato | Documenti Microsoft
description: Azure CLI Script di esempio - mappa un'app di funzione tooa dominio personalizzato in Azure.
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
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="937f9-103">Eseguire il mapping di un'app di funzione tooa dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="937f9-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="937f9-104">Questo script di esempio crea un'app di funzione con le relative risorse e quindi esegue il mapping di `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="937f9-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="937f9-105">dominio personalizzato tooa toomap, è necessario creare l'app di funzione in un piano di servizio App e non in un piano di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="937f9-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="937f9-106">Funzioni di Azure supporta il mapping di un dominio personalizzato solo usando un record A.</span><span class="sxs-lookup"><span data-stu-id="937f9-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="937f9-107">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="937f9-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="937f9-108">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="937f9-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="937f9-109">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="937f9-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="937f9-110">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="937f9-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="937f9-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="937f9-111">Script explanation</span></span>

<span data-ttu-id="937f9-112">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="937f9-112">This script uses hello following commands.</span></span> <span data-ttu-id="937f9-113">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="937f9-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="937f9-114">Comando</span><span class="sxs-lookup"><span data-stu-id="937f9-114">Command</span></span> | <span data-ttu-id="937f9-115">Note</span><span class="sxs-lookup"><span data-stu-id="937f9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="937f9-116">az group create</span><span class="sxs-lookup"><span data-stu-id="937f9-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="937f9-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="937f9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="937f9-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="937f9-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="937f9-119">Crea un account di archiviazione richiesto da hello funzione app.</span><span class="sxs-lookup"><span data-stu-id="937f9-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="937f9-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="937f9-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="937f9-121">Crea un toomap necessario piano di servizio App di un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="937f9-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="937f9-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="937f9-122">az functionapp create</span></span>]() | <span data-ttu-id="937f9-123">Creare un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="937f9-123">Creates a function app.</span></span> |
| [<span data-ttu-id="937f9-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="937f9-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="937f9-125">Esegue il mapping di un'app di funzione tooa dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="937f9-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="937f9-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="937f9-126">Next steps</span></span>

<span data-ttu-id="937f9-127">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="937f9-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="937f9-128">Esempi di script aggiuntivi funzioni CLI sono reperibile in hello [documentazione di Azure funzioni]().</span><span class="sxs-lookup"><span data-stu-id="937f9-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
