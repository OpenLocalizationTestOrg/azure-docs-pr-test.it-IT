---
title: Script di esempio CLI - aaaAzure associare un'app di funzione tooa di certificato SSL personalizzata | Documenti Microsoft
description: Esempio di Script Azure CLI - binding SSL certificato tooa funzione app personalizzata in Azure
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
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="9683c-103">Associare un'app di funzione tooa di certificati SSL personalizzata</span><span class="sxs-lookup"><span data-stu-id="9683c-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="9683c-104">Questo script di esempio crea un'app di funzione nel servizio App con le relative risorse correlate, quindi associa il certificato SSL hello di un tooit nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9683c-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="9683c-105">Per questo esempio è necessario:</span><span class="sxs-lookup"><span data-stu-id="9683c-105">For this sample, you need:</span></span>

* <span data-ttu-id="9683c-106">Pagina di configurazione DNS del registrar di dominio tooyour di accesso.</span><span class="sxs-lookup"><span data-stu-id="9683c-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="9683c-107">Un oggetto valido. Il file PFX e la relativa password per hello SSL certificato desidera tooupload e il binding.</span><span class="sxs-lookup"><span data-stu-id="9683c-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="9683c-108">toobind un certificato SSL, è necessario creare l'app di funzione in un piano di servizio App e non in un piano di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9683c-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9683c-109">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9683c-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9683c-110">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="9683c-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9683c-111">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9683c-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9683c-112">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9683c-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9683c-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="9683c-113">Script explanation</span></span>

<span data-ttu-id="9683c-114">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9683c-114">This script uses hello following commands.</span></span> <span data-ttu-id="9683c-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="9683c-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9683c-116">Comando</span><span class="sxs-lookup"><span data-stu-id="9683c-116">Command</span></span> | <span data-ttu-id="9683c-117">Note</span><span class="sxs-lookup"><span data-stu-id="9683c-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9683c-118">az group create</span><span class="sxs-lookup"><span data-stu-id="9683c-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9683c-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="9683c-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9683c-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="9683c-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9683c-121">Crea un toobind necessario piano di servizio App di certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="9683c-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="9683c-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="9683c-122">az functionapp create</span></span>]() | <span data-ttu-id="9683c-123">Creare un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="9683c-123">Creates a function app.</span></span> |
| [<span data-ttu-id="9683c-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="9683c-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="9683c-125">Esegue il mapping di un'app di funzione toohello dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9683c-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="9683c-126">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="9683c-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="9683c-127">Carica un'app di funzione tooa certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="9683c-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="9683c-128">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="9683c-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="9683c-129">Associa un'app di funzione tooa di certificati SSL caricata.</span><span class="sxs-lookup"><span data-stu-id="9683c-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9683c-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9683c-130">Next steps</span></span>

<span data-ttu-id="9683c-131">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9683c-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9683c-132">Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service]().</span><span class="sxs-lookup"><span data-stu-id="9683c-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
