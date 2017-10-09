---
title: aaaAzure CLI Script di esempio - creare un'app web e distribuire codice tooa ambiente di gestione temporanea | Documenti Microsoft
description: Esempio di Script di Azure CLI - creare un'app web e distribuire codice tooa ambiente di gestione temporanea
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="02e70-103">Creare un'app web e distribuire codice tooa ambiente di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="02e70-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="02e70-104">Questo script di esempio crea un'app web nel servizio App con uno slot di distribuzione aggiuntivo denominato "gestione temporanea" e quindi distribuisce un toohello di app di esempio "gestione temporanea" slot.</span><span class="sxs-lookup"><span data-stu-id="02e70-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="02e70-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="02e70-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="02e70-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="02e70-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="02e70-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="02e70-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="02e70-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="02e70-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="02e70-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="02e70-109">Script explanation</span></span>

<span data-ttu-id="02e70-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="02e70-110">This script uses hello following commands.</span></span> <span data-ttu-id="02e70-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="02e70-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="02e70-112">Comando</span><span class="sxs-lookup"><span data-stu-id="02e70-112">Command</span></span> | <span data-ttu-id="02e70-113">Note</span><span class="sxs-lookup"><span data-stu-id="02e70-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="02e70-114">az group create</span><span class="sxs-lookup"><span data-stu-id="02e70-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="02e70-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="02e70-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="02e70-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="02e70-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="02e70-117">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="02e70-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="02e70-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="02e70-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="02e70-119">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="02e70-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="02e70-120">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="02e70-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="02e70-121">Creare uno slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="02e70-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="02e70-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="02e70-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="02e70-123">Associa un'App Web di Azure con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="02e70-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="02e70-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="02e70-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="02e70-125">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="02e70-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="02e70-126">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="02e70-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="02e70-127">Trasferire un determinato slot di distribuzione nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="02e70-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="02e70-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02e70-128">Next steps</span></span>

<span data-ttu-id="02e70-129">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="02e70-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="02e70-130">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="02e70-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
