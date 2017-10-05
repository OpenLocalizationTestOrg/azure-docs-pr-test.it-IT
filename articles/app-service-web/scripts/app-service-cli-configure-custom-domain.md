---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Eseguire il mapping di un dominio personalizzato a un'App Web | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Eseguire il mapping di un dominio personalizzato a un'App Web
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6712be8a551731fbafd92ef19564e89399e23e76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-web-app"></a><span data-ttu-id="9da9b-103">Eseguire il mapping di un dominio personalizzato a un'App Web</span><span class="sxs-lookup"><span data-stu-id="9da9b-103">Map a custom domain to a web app</span></span>

<span data-ttu-id="9da9b-104">Questo script di esempio crea un'App Web nel servizio App con le relative risorse correlate e quindi esegue il mapping di `www.<yourdomain>` a essa.</span><span class="sxs-lookup"><span data-stu-id="9da9b-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9da9b-105">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9da9b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9da9b-106">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="9da9b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="9da9b-107">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9da9b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9da9b-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9da9b-108">Sample script</span></span>

<span data-ttu-id="9da9b-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Eseguire il mapping di un dominio personalizzato a un'App Web")]</span><span class="sxs-lookup"><span data-stu-id="9da9b-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9da9b-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="9da9b-110">Script explanation</span></span>

<span data-ttu-id="9da9b-111">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9da9b-111">This script uses the following commands.</span></span> <span data-ttu-id="9da9b-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="9da9b-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9da9b-113">Comando</span><span class="sxs-lookup"><span data-stu-id="9da9b-113">Command</span></span> | <span data-ttu-id="9da9b-114">Note</span><span class="sxs-lookup"><span data-stu-id="9da9b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9da9b-115">az group create</span><span class="sxs-lookup"><span data-stu-id="9da9b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9da9b-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="9da9b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9da9b-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="9da9b-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9da9b-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="9da9b-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9da9b-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="9da9b-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="9da9b-120">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="9da9b-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="9da9b-121">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="9da9b-121">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="9da9b-122">Esegue il mapping di un dominio personalizzato a un'app Web.</span><span class="sxs-lookup"><span data-stu-id="9da9b-122">Maps a custom domain to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9da9b-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9da9b-123">Next steps</span></span>

<span data-ttu-id="9da9b-124">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9da9b-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9da9b-125">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9da9b-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
