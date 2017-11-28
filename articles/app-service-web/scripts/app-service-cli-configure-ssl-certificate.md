---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Associare un certificato SSL personalizzato a un'App Web | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Associare un certificato SSL personalizzato a un'App Web
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d4fab3fb2c297bf5f498b63bee46692febb9180b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="817e9-103">Associare un certificato SSL personalizzato a un'app web</span><span class="sxs-lookup"><span data-stu-id="817e9-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="817e9-104">Questo script di esempio crea un'app Web nel servizio app con le relative risorse correlate, quindi associa ad essa il certificato SSL di un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="817e9-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="817e9-105">Per questo esempio sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="817e9-105">For this sample, you will need:</span></span>

* <span data-ttu-id="817e9-106">Accesso alla pagina di configurazione DNS del registrar.</span><span class="sxs-lookup"><span data-stu-id="817e9-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="817e9-107">File PFX valido e relativa password per il certificato SSL da caricare e associare.</span><span class="sxs-lookup"><span data-stu-id="817e9-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="817e9-108">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="817e9-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="817e9-109">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="817e9-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="817e9-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="817e9-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="817e9-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="817e9-111">Sample script</span></span>

<span data-ttu-id="817e9-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Associare un certificato SSL personalizzato a un'App Web")]</span><span class="sxs-lookup"><span data-stu-id="817e9-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="817e9-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="817e9-113">Script explanation</span></span>

<span data-ttu-id="817e9-114">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="817e9-114">This script uses the following commands.</span></span> <span data-ttu-id="817e9-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="817e9-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="817e9-116">Comando</span><span class="sxs-lookup"><span data-stu-id="817e9-116">Command</span></span> | <span data-ttu-id="817e9-117">Note</span><span class="sxs-lookup"><span data-stu-id="817e9-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="817e9-118">az group create</span><span class="sxs-lookup"><span data-stu-id="817e9-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="817e9-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="817e9-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="817e9-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="817e9-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="817e9-121">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="817e9-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="817e9-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="817e9-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="817e9-123">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="817e9-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="817e9-124">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="817e9-124">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="817e9-125">Esegue il mapping di un dominio personalizzato a un'app Web.</span><span class="sxs-lookup"><span data-stu-id="817e9-125">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="817e9-126">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="817e9-126">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="817e9-127">Carica un certificato SSL in un'app Web.</span><span class="sxs-lookup"><span data-stu-id="817e9-127">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="817e9-128">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="817e9-128">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="817e9-129">Associa un certificato SSL caricato a un'app Web.</span><span class="sxs-lookup"><span data-stu-id="817e9-129">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="817e9-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="817e9-130">Next steps</span></span>

<span data-ttu-id="817e9-131">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="817e9-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="817e9-132">Altri esempi di script dell'interfaccia della riga di comando del servizio app sono disponibili nella [documentazione del servizio app di Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="817e9-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
