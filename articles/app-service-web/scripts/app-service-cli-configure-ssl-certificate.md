---
title: Script di esempio CLI - aaaAzure associare un'app web tooa di certificato SSL personalizzata | Documenti Microsoft
description: Esempio di Script Azure CLI - Bind un'app web tooa di certificati SSL personalizzata
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
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="5b91a-103">Associare un'app web tooa di certificati SSL personalizzata</span><span class="sxs-lookup"><span data-stu-id="5b91a-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="5b91a-104">Questo script di esempio crea un'app web nel servizio App con le relative risorse correlate, quindi associa il certificato SSL hello di un tooit nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5b91a-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="5b91a-105">Per questo esempio sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5b91a-105">For this sample, you will need:</span></span>

* <span data-ttu-id="5b91a-106">Pagina di configurazione DNS del registrar di dominio tooyour di accesso.</span><span class="sxs-lookup"><span data-stu-id="5b91a-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="5b91a-107">Un oggetto valido. Il file PFX e la relativa password per hello SSL certificato desidera tooupload e il binding.</span><span class="sxs-lookup"><span data-stu-id="5b91a-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5b91a-108">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="5b91a-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5b91a-109">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="5b91a-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5b91a-110">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5b91a-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="5b91a-111">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5b91a-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5b91a-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5b91a-112">Script explanation</span></span>

<span data-ttu-id="5b91a-113">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5b91a-113">This script uses hello following commands.</span></span> <span data-ttu-id="5b91a-114">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="5b91a-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5b91a-115">Comando</span><span class="sxs-lookup"><span data-stu-id="5b91a-115">Command</span></span> | <span data-ttu-id="5b91a-116">Note</span><span class="sxs-lookup"><span data-stu-id="5b91a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5b91a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="5b91a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5b91a-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5b91a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5b91a-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5b91a-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5b91a-120">Consente di creare un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="5b91a-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5b91a-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5b91a-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5b91a-122">Crea un'App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b91a-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5b91a-123">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="5b91a-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="5b91a-124">Esegue il mapping di un'app web tooa di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5b91a-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="5b91a-125">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="5b91a-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="5b91a-126">Carica un'app di web tooa certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="5b91a-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="5b91a-127">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="5b91a-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="5b91a-128">Associa un'app web tooa di certificati SSL caricata.</span><span class="sxs-lookup"><span data-stu-id="5b91a-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5b91a-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b91a-129">Next steps</span></span>

<span data-ttu-id="5b91a-130">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5b91a-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5b91a-131">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5b91a-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
