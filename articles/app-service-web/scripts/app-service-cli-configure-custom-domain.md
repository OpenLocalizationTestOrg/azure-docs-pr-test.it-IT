---
title: aaaAzure CLI Script di esempio - eseguire il mapping di un'app web tooa di dominio personalizzato | Documenti Microsoft
description: Esempio di Script Azure CLI - mappa un'app web tooa di dominio personalizzato
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
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="059aa-103">Eseguire il mapping di un'app web tooa di dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="059aa-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="059aa-104">Questo script di esempio crea un'app web nel servizio App con le relative risorse correlate e quindi esegue il mapping di `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="059aa-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="059aa-105">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="059aa-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="059aa-106">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="059aa-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="059aa-107">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="059aa-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="059aa-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="059aa-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="059aa-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="059aa-109">Script explanation</span></span>

<span data-ttu-id="059aa-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="059aa-110">This script uses hello following commands.</span></span> <span data-ttu-id="059aa-111">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="059aa-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="059aa-112">Comando</span><span class="sxs-lookup"><span data-stu-id="059aa-112">Command</span></span> | <span data-ttu-id="059aa-113">Note</span><span class="sxs-lookup"><span data-stu-id="059aa-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="059aa-114">az group create</span><span class="sxs-lookup"><span data-stu-id="059aa-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="059aa-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="059aa-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="059aa-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="059aa-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="059aa-117">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="059aa-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="059aa-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="059aa-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="059aa-119">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="059aa-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="059aa-120">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="059aa-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="059aa-121">Esegue il mapping di un'app web tooa di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="059aa-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="059aa-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="059aa-122">Next steps</span></span>

<span data-ttu-id="059aa-123">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="059aa-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="059aa-124">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="059aa-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
