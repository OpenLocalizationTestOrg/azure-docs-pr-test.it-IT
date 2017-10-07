---
title: aaaAzure CLI Script di esempio - creare un'app web ASP.NET Core in un contenitore Docker dal Registro di sistema contenitore di Azure | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web ASP.NET Core in un contenitore Docker dal Registro di sistema del contenitore di Azure
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 0d4b1e706c2401ef813f48ef4de3d17fa2b6c9e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="a8d29-103">Creare un'App Web ASP.NET Core in un contenitore Docker dal Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="a8d29-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="a8d29-104">In questo scenario si apprenderà come toocreate un gruppo di risorse, Linux app service piano e app web e distribuire un'applicazione ASP.NET di base utilizzando un contenitore Docker da hello del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d29-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from hello Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a8d29-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a8d29-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a8d29-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a8d29-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a8d29-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a8d29-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a8d29-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a8d29-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a8d29-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="a8d29-109">Script explanation</span></span>

<span data-ttu-id="a8d29-110">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="a8d29-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="a8d29-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="a8d29-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a8d29-112">Comando</span><span class="sxs-lookup"><span data-stu-id="a8d29-112">Command</span></span> | <span data-ttu-id="a8d29-113">Note</span><span class="sxs-lookup"><span data-stu-id="a8d29-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a8d29-114">az group create</span><span class="sxs-lookup"><span data-stu-id="a8d29-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a8d29-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="a8d29-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a8d29-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a8d29-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a8d29-117">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="a8d29-117">Creates an App Service plan.</span></span> <span data-ttu-id="a8d29-118">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d29-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a8d29-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="a8d29-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a8d29-120">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d29-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a8d29-121">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="a8d29-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="a8d29-122">Imposta il contenitore Docker hello per hello Azure web app.</span><span class="sxs-lookup"><span data-stu-id="a8d29-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8d29-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8d29-123">Next steps</span></span>

<span data-ttu-id="a8d29-124">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a8d29-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a8d29-125">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a8d29-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
