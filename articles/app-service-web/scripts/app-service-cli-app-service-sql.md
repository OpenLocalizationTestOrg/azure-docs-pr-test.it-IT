---
title: aaaAzure CLI Script di esempio - connettersi a un database SQL di web app tooa | Documenti Microsoft
description: 'Azure CLI Script di esempio: la connessione a un database SQL tooa app web'
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="3f4af-103">La connessione a un database SQL tooa app web</span><span class="sxs-lookup"><span data-stu-id="3f4af-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="3f4af-104">In questo scenario si apprenderà come toocreate un database SQL di Azure e un Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3f4af-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="3f4af-105">Quindi si procederà al collegamento hello SQL database toohello web app con le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="3f4af-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3f4af-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="3f4af-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3f4af-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="3f4af-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3f4af-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3f4af-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3f4af-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="3f4af-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3f4af-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="3f4af-110">Script explanation</span></span>

<span data-ttu-id="3f4af-111">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, app web, database SQL e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="3f4af-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="3f4af-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="3f4af-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3f4af-113">Comando</span><span class="sxs-lookup"><span data-stu-id="3f4af-113">Command</span></span> | <span data-ttu-id="3f4af-114">Note</span><span class="sxs-lookup"><span data-stu-id="3f4af-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3f4af-115">az group create</span><span class="sxs-lookup"><span data-stu-id="3f4af-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3f4af-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="3f4af-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3f4af-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="3f4af-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="3f4af-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="3f4af-118">Creates an App Service plan.</span></span> <span data-ttu-id="3f4af-119">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f4af-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="3f4af-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="3f4af-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="3f4af-121">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f4af-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="3f4af-122">az sql server create</span><span class="sxs-lookup"><span data-stu-id="3f4af-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="3f4af-123">Consente di creare un server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="3f4af-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="3f4af-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="3f4af-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="3f4af-125">Crea un nuovo database con hello Server di Database SQL.</span><span class="sxs-lookup"><span data-stu-id="3f4af-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="3f4af-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="3f4af-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="3f4af-127">Crea o aggiorna un'impostazione per un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f4af-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="3f4af-128">Le impostazioni delle app vengono esposte come variabili di ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3f4af-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3f4af-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f4af-129">Next steps</span></span>

<span data-ttu-id="3f4af-130">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3f4af-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3f4af-131">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3f4af-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
