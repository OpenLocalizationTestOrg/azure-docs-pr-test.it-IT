---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web e distribuire il codice nell'ambiente di gestione temporanea | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web e distribuire il codice nell'ambiente di gestione temporanea
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
ms.openlocfilehash: d586b50258c32e44f55859aad0a89475e9e4d2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="5425f-103">Creare un'App Web e distribuire il codice in un ambiente di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="5425f-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="5425f-104">Questo script di esempio crea un'App Web nel servizio app con uno slot di distribuzione aggiuntivo denominato "staging" e quindi distribuisce un'app di esempio allo slot "staging".</span><span class="sxs-lookup"><span data-stu-id="5425f-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5425f-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5425f-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5425f-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="5425f-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="5425f-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5425f-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5425f-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5425f-108">Sample script</span></span>

<span data-ttu-id="5425f-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Creare un'App Web e distribuire il codice in un ambiente di gestione temporanea")]</span><span class="sxs-lookup"><span data-stu-id="5425f-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code to a staging environment")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5425f-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5425f-110">Script explanation</span></span>

<span data-ttu-id="5425f-111">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5425f-111">This script uses the following commands.</span></span> <span data-ttu-id="5425f-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="5425f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5425f-113">Comando</span><span class="sxs-lookup"><span data-stu-id="5425f-113">Command</span></span> | <span data-ttu-id="5425f-114">Note</span><span class="sxs-lookup"><span data-stu-id="5425f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5425f-115">az group create</span><span class="sxs-lookup"><span data-stu-id="5425f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5425f-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5425f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5425f-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5425f-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5425f-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="5425f-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5425f-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5425f-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5425f-120">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="5425f-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5425f-121">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="5425f-121">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="5425f-122">Creare uno slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5425f-122">Create a deployment slot.</span></span> |
| [<span data-ttu-id="5425f-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="5425f-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="5425f-124">Associa un'App Web di Azure con un archivio Git o Mercurial.</span><span class="sxs-lookup"><span data-stu-id="5425f-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="5425f-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="5425f-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="5425f-126">Apre un'App Web di Azure in un browser.</span><span class="sxs-lookup"><span data-stu-id="5425f-126">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="5425f-127">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="5425f-127">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="5425f-128">Trasferire un determinato slot di distribuzione nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5425f-128">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5425f-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5425f-129">Next steps</span></span>

<span data-ttu-id="5425f-130">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5425f-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5425f-131">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5425f-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
