---
title: aaaAzure CLI Script di esempio - connettersi a un account di archiviazione web app tooa | Documenti Microsoft
description: Azure CLI Script di esempio - connettersi a un account di archiviazione tooa app web
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: affee2d39ef3f98c6043010850e08b67fb9ce54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="09a1c-103">Connettersi a un account di archiviazione tooa app web</span><span class="sxs-lookup"><span data-stu-id="09a1c-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="09a1c-104">In questo scenario si apprenderà come toocreate un account di archiviazione di Azure e un Azure web app.</span><span class="sxs-lookup"><span data-stu-id="09a1c-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="09a1c-105">Quindi si procederà al collegamento hello archiviazione toohello web app dell'account utilizzando le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="09a1c-105">Then you will link hello storage account toohello web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="09a1c-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="09a1c-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="09a1c-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="09a1c-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="09a1c-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="09a1c-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="09a1c-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="09a1c-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="09a1c-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="09a1c-110">Script explanation</span></span>

<span data-ttu-id="09a1c-111">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, app web, account di archiviazione e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="09a1c-111">This script uses hello following commands toocreate a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="09a1c-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="09a1c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="09a1c-113">Comando</span><span class="sxs-lookup"><span data-stu-id="09a1c-113">Command</span></span> | <span data-ttu-id="09a1c-114">Note</span><span class="sxs-lookup"><span data-stu-id="09a1c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="09a1c-115">az group create</span><span class="sxs-lookup"><span data-stu-id="09a1c-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="09a1c-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="09a1c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="09a1c-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="09a1c-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="09a1c-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="09a1c-118">Creates an App Service plan.</span></span> <span data-ttu-id="09a1c-119">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="09a1c-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="09a1c-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="09a1c-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="09a1c-121">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="09a1c-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="09a1c-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="09a1c-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="09a1c-123">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="09a1c-123">Creates a storage account.</span></span> <span data-ttu-id="09a1c-124">Si tratta in cui verranno archiviati asset statico hello.</span><span class="sxs-lookup"><span data-stu-id="09a1c-124">This is where hello static assets will be stored.</span></span> |
| [<span data-ttu-id="09a1c-125">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="09a1c-125">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="09a1c-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="09a1c-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="09a1c-127">Crea o aggiorna un'impostazione per un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="09a1c-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="09a1c-128">Le impostazioni delle app vengono esposte come variabili di ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="09a1c-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="09a1c-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09a1c-129">Next steps</span></span>

<span data-ttu-id="09a1c-130">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="09a1c-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="09a1c-131">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="09a1c-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
