---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare un'App Web ASP.NET Core in un contenitore Docker dal Registro di sistema del contenitore di Azure | Microsoft Docs
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
ms.openlocfilehash: 2556947d7cdd1475ae82ac2e1d61ad30ebd0d29f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="7dce2-103">Creare un'App Web ASP.NET Core in un contenitore Docker dal Registro di sistema del contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="7dce2-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="7dce2-104">In questo scenario si apprenderà come creare un gruppo di risorse, un piano di servizio app di Linux e un'App Web e come distribuire un'applicazione ASP.NET Core usando un contenitore Docker dal Registro di sistema del contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dce2-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from the Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7dce2-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dce2-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7dce2-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="7dce2-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="7dce2-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7dce2-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7dce2-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7dce2-108">Sample script</span></span>

<span data-ttu-id="7dce2-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Registro di sistema del contenitore di Azure di Linux")]</span><span class="sxs-lookup"><span data-stu-id="7dce2-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7dce2-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7dce2-110">Script explanation</span></span>

<span data-ttu-id="7dce2-111">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="7dce2-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="7dce2-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="7dce2-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7dce2-113">Comando</span><span class="sxs-lookup"><span data-stu-id="7dce2-113">Command</span></span> | <span data-ttu-id="7dce2-114">Note</span><span class="sxs-lookup"><span data-stu-id="7dce2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7dce2-115">az group create</span><span class="sxs-lookup"><span data-stu-id="7dce2-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7dce2-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="7dce2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7dce2-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="7dce2-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7dce2-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="7dce2-118">Creates an App Service plan.</span></span> <span data-ttu-id="7dce2-119">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dce2-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="7dce2-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="7dce2-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="7dce2-121">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dce2-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="7dce2-122">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="7dce2-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="7dce2-123">Imposta il contenitore Docker per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="7dce2-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7dce2-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7dce2-124">Next steps</span></span>

<span data-ttu-id="7dce2-125">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7dce2-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7dce2-126">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7dce2-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
