---
title: aaaAzure CLI Script di esempio - ridimensionare un'App Web manualmente utilizzando l'interfaccia CLI di Azure 2.0 | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Ridimensionare un'App Web manualmente usando l'interfaccia della riga di comando di Azure 2.0
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="538e2-103">Ridimensionare un'App Web manualmente</span><span class="sxs-lookup"><span data-stu-id="538e2-103">Scale a web app manually</span></span>

<span data-ttu-id="538e2-104">In questo scenario si apprenderà toocreate un gruppo di risorse, app web e il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="538e2-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="538e2-105">È quindi verrà ridimensionato hello piano di servizio App dalle istanze di toomultiple singola istanza.</span><span class="sxs-lookup"><span data-stu-id="538e2-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="538e2-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="538e2-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="538e2-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="538e2-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="538e2-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="538e2-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="538e2-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="538e2-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="538e2-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="538e2-110">Script explanation</span></span>

<span data-ttu-id="538e2-111">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="538e2-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="538e2-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="538e2-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="538e2-113">Comando</span><span class="sxs-lookup"><span data-stu-id="538e2-113">Command</span></span> | <span data-ttu-id="538e2-114">Note</span><span class="sxs-lookup"><span data-stu-id="538e2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="538e2-115">az group create</span><span class="sxs-lookup"><span data-stu-id="538e2-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="538e2-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="538e2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="538e2-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="538e2-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="538e2-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="538e2-118">Creates an App Service plan.</span></span> <span data-ttu-id="538e2-119">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="538e2-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="538e2-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="538e2-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="538e2-121">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="538e2-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="538e2-122">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="538e2-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="538e2-123">Aggiorna le proprietà del piano di servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="538e2-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="538e2-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="538e2-124">Next steps</span></span>

<span data-ttu-id="538e2-125">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="538e2-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="538e2-126">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="538e2-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
