---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Associare un certificato SSL personalizzato a un'app per le funzioni | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Associare un certificato SSL personalizzato a un'app per le funzioni in Azure
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="72b29-103">Associare un certificato SSL personalizzato a un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="72b29-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="72b29-104">Questo script di esempio crea un'app per le funzioni nel servizio app con le relative risorse correlate, quindi associa a essa il certificato SSL di un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="72b29-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="72b29-105">Per questo esempio è necessario:</span><span class="sxs-lookup"><span data-stu-id="72b29-105">For this sample, you need:</span></span>

* <span data-ttu-id="72b29-106">Accesso alla pagina di configurazione DNS del registrar.</span><span class="sxs-lookup"><span data-stu-id="72b29-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="72b29-107">File PFX valido e relativa password per il certificato SSL da caricare e associare.</span><span class="sxs-lookup"><span data-stu-id="72b29-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="72b29-108">Per associare un certificato SSL, è necessario creare l'app per le funzioni in un piano di servizio app e non in un piano a consumo.</span><span class="sxs-lookup"><span data-stu-id="72b29-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="72b29-109">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="72b29-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="72b29-110">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="72b29-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="72b29-111">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="72b29-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="72b29-112">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="72b29-112">Sample script</span></span>

<span data-ttu-id="72b29-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Associare un certificato SSL personalizzato a un'App Web")]</span><span class="sxs-lookup"><span data-stu-id="72b29-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="72b29-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="72b29-114">Script explanation</span></span>

<span data-ttu-id="72b29-115">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="72b29-115">This script uses the following commands.</span></span> <span data-ttu-id="72b29-116">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="72b29-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="72b29-117">Comando</span><span class="sxs-lookup"><span data-stu-id="72b29-117">Command</span></span> | <span data-ttu-id="72b29-118">Note</span><span class="sxs-lookup"><span data-stu-id="72b29-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="72b29-119">az group create</span><span class="sxs-lookup"><span data-stu-id="72b29-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="72b29-120">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="72b29-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="72b29-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="72b29-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="72b29-122">Crea un piano di servizio app necessario per associare i certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="72b29-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="72b29-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="72b29-123">az functionapp create</span></span>]() | <span data-ttu-id="72b29-124">Creare un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="72b29-124">Creates a function app.</span></span> |
| [<span data-ttu-id="72b29-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="72b29-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="72b29-126">Esegue il mapping di un dominio personalizzato all'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="72b29-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="72b29-127">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="72b29-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="72b29-128">Carica un certificato SSL in un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="72b29-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="72b29-129">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="72b29-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="72b29-130">Associa un certificato SSL caricato a un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="72b29-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="72b29-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72b29-131">Next steps</span></span>

<span data-ttu-id="72b29-132">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="72b29-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="72b29-133">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure]().</span><span class="sxs-lookup"><span data-stu-id="72b29-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
