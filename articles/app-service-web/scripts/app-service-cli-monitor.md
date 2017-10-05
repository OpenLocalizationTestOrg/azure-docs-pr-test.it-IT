---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Monitorare un'App Web con i log del server Web | Microsoft Docs
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
ms.openlocfilehash: df4ca5b1270ada849e231ad9608a5b1d2edda8be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="cb921-103">Monitorare un'App Web con i log del server Web</span><span class="sxs-lookup"><span data-stu-id="cb921-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="cb921-104">In questo scenario verrà creato un gruppo di risorse, un piano di servizio app e un'App Web e verrà configurata l'App Web per abilitare i log del server Web.</span><span class="sxs-lookup"><span data-stu-id="cb921-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="cb921-105">Quindi si scaricheranno i file di log per visionarli.</span><span class="sxs-lookup"><span data-stu-id="cb921-105">You will then download the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cb921-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb921-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cb921-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="cb921-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="cb921-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cb921-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cb921-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="cb921-109">Sample script</span></span>

<span data-ttu-id="cb921-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitorare i log")]</span><span class="sxs-lookup"><span data-stu-id="cb921-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cb921-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="cb921-111">Script explanation</span></span>

<span data-ttu-id="cb921-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, l'App Web e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="cb921-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="cb921-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="cb921-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cb921-114">Comando</span><span class="sxs-lookup"><span data-stu-id="cb921-114">Command</span></span> | <span data-ttu-id="cb921-115">Note</span><span class="sxs-lookup"><span data-stu-id="cb921-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cb921-116">az group create</span><span class="sxs-lookup"><span data-stu-id="cb921-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cb921-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="cb921-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cb921-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="cb921-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="cb921-119">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="cb921-119">Creates an App Service plan.</span></span> <span data-ttu-id="cb921-120">Equivale a una server farm per l'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb921-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="cb921-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="cb921-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="cb921-122">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb921-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="cb921-123">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="cb921-123">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="cb921-124">Configura i log che devono essere mantenuti da un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb921-124">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="cb921-125">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="cb921-125">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="cb921-126">Scarica i log dell'App Web di Azure sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="cb921-126">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cb921-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb921-127">Next steps</span></span>

<span data-ttu-id="cb921-128">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cb921-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cb921-129">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cb921-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
