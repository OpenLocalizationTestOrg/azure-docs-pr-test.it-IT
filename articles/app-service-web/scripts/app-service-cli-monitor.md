---
title: aaaAzure CLI Script di esempio - monitoraggio di un'app web con i registri del server web | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Monitorare un'App Web con i log del server Web
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="dcc28-103">Monitorare un'App Web con i log del server Web</span><span class="sxs-lookup"><span data-stu-id="dcc28-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="dcc28-104">In questo scenario si crea un gruppo di risorse, il piano di servizio app, app web e lo configura hello web app tooenable i log del server.</span><span class="sxs-lookup"><span data-stu-id="dcc28-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="dcc28-105">Quindi si scaricherà i file di log hello per la revisione.</span><span class="sxs-lookup"><span data-stu-id="dcc28-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dcc28-106">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="dcc28-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dcc28-107">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="dcc28-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dcc28-108">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dcc28-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dcc28-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="dcc28-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="dcc28-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="dcc28-110">Script explanation</span></span>

<span data-ttu-id="dcc28-111">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, app web e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="dcc28-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="dcc28-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="dcc28-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dcc28-113">Comando</span><span class="sxs-lookup"><span data-stu-id="dcc28-113">Command</span></span> | <span data-ttu-id="dcc28-114">Note</span><span class="sxs-lookup"><span data-stu-id="dcc28-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dcc28-115">az group create</span><span class="sxs-lookup"><span data-stu-id="dcc28-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dcc28-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="dcc28-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dcc28-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="dcc28-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="dcc28-118">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="dcc28-118">Creates an App Service plan.</span></span> <span data-ttu-id="dcc28-119">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcc28-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="dcc28-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="dcc28-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="dcc28-121">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcc28-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="dcc28-122">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="dcc28-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="dcc28-123">Configura i log che devono essere mantenuti da un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcc28-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="dcc28-124">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="dcc28-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="dcc28-125">Download hello registra di hello un computer locale di app tooyour web di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcc28-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcc28-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dcc28-126">Next steps</span></span>

<span data-ttu-id="dcc28-127">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcc28-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dcc28-128">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dcc28-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
