---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Connettere un'App Web a un database SQL | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Connettere un'App Web a un database SQL
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
ms.openlocfilehash: ec5e22bfacc12a89f1fb5882487df4829369777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="146c6-103">Connettere un'App Web a un database SQL</span><span class="sxs-lookup"><span data-stu-id="146c6-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="146c6-104">Questo scenario illustra come creare un database SQL di Azure e un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="146c6-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="146c6-105">Il database SQL viene quindi collegato all'App Web usando le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="146c6-105">Then you will link the SQL database to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="146c6-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="146c6-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="146c6-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="146c6-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="146c6-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="146c6-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="146c6-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="146c6-109">Sample script</span></span>

<span data-ttu-id="146c6-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "Database SQL")]</span><span class="sxs-lookup"><span data-stu-id="146c6-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="146c6-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="146c6-111">Script explanation</span></span>

<span data-ttu-id="146c6-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'App Web, il database SQL e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="146c6-112">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="146c6-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="146c6-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="146c6-114">Comando</span><span class="sxs-lookup"><span data-stu-id="146c6-114">Command</span></span> | <span data-ttu-id="146c6-115">Note</span><span class="sxs-lookup"><span data-stu-id="146c6-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="146c6-116">az group create</span><span class="sxs-lookup"><span data-stu-id="146c6-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="146c6-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="146c6-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="146c6-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="146c6-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="146c6-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="146c6-119">Creates an App Service plan.</span></span> <span data-ttu-id="146c6-120">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="146c6-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="146c6-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="146c6-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="146c6-122">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="146c6-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="146c6-123">az sql server create</span><span class="sxs-lookup"><span data-stu-id="146c6-123">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="146c6-124">Consente di creare un server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="146c6-124">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="146c6-125">az sql db create</span><span class="sxs-lookup"><span data-stu-id="146c6-125">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="146c6-126">Consente di creare un nuovo database con il server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="146c6-126">Creates a new database with the SQL Database Server.</span></span> |
| [<span data-ttu-id="146c6-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="146c6-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="146c6-128">Crea o aggiorna un'impostazione per un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="146c6-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="146c6-129">Le impostazioni delle app vengono esposte come variabili di ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="146c6-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="146c6-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="146c6-130">Next steps</span></span>

<span data-ttu-id="146c6-131">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="146c6-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="146c6-132">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="146c6-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
