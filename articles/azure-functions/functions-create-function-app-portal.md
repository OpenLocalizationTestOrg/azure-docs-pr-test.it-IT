---
title: un'app di funzione dal portale di Azure hello aaaCreate | Documenti Microsoft
description: Creare una nuova funzione app in Azure App Service dal portale hello.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="9aa3d-103">Creare un'app di funzione dal portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="9aa3d-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="9aa3d-104">Le app di Azure (funzione) utilizza l'infrastruttura di Azure App Service hello.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="9aa3d-105">In questo argomento illustra come un'app di funzione nel portale di Azure hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="9aa3d-106">Un'app di funzione è contenitore hello che ospita l'esecuzione di hello delle singole funzioni.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="9aa3d-107">Quando si crea un'app di funzione nel piano di hosting del servizio App hello, l'app di funzione può utilizzare tutte le funzionalità di hello di servizio App.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="9aa3d-108">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="9aa3d-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="9aa3d-109">Quando si crea un'app per le funzioni, inserire un **nome dell'app** valido, che contenga solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="9aa3d-110">Il carattere di sottolineatura (**_**) non è consentito.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="9aa3d-111">I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="9aa3d-112">Nome dell'account di archiviazione deve essere univoco all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="9aa3d-113">Dopo la creazione di app di funzione hello, è possibile creare le singole funzioni in uno o più lingue diverse.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="9aa3d-114">Creare funzioni [tramite il portale di hello](functions-create-first-azure-function.md#create-function), [distribuzione continua](functions-continuous-deployment.md), o da [caricamento con FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="9aa3d-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="9aa3d-115">Piani di servizio</span><span class="sxs-lookup"><span data-stu-id="9aa3d-115">Service plans</span></span>

<span data-ttu-id="9aa3d-116">Funzioni di Azure offre due piani di servizio diversi: piano a consumo e piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="9aa3d-117">piano di consumo Hello alloca automaticamente potenza di calcolo quando viene eseguito il codice, scale-out come carico toohandle necessarie e quindi scale-in quando codice non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="9aa3d-118">piano di servizio App Hello offre la funzione funzionalità di app accesso tooall hello del servizio App.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="9aa3d-119">È necessario scegliere il piano di servizio quando viene creata l'app per le funzioni, che al momento non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="9aa3d-120">Per altre informazioni, vedere [Scegliere un piano di hosting di Funzioni di Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="9aa3d-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="9aa3d-121">Se si intende toorun funzioni JavaScript in un piano di servizio App, è consigliabile scegliere un piano con un minor numero di core.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="9aa3d-122">Per ulteriori informazioni, vedere hello [riferimento JavaScript per le funzioni](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="9aa3d-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="9aa3d-123">Requisiti dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9aa3d-123">Storage account requirements</span></span>

<span data-ttu-id="9aa3d-124">Quando si crea un'app di funzione nel servizio App, è necessario creare o collegare tooa generico account di archiviazione di Azure che supporta l'archiviazione Blob, coda e tabella.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="9aa3d-125">Le funzioni usano internamente l'archiviazione per operazioni come la gestione dei trigger e la registrazione dell'esecuzione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="9aa3d-126">Alcuni account di archiviazione, come gli account di archiviazione solo BLOB, Archiviazione Premium di Azure e gli account di archiviazione di uso generico con replica ZRS, non supportano code e tabelle.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="9aa3d-127">Questi account vengono filtrati dal Pannello di Account di archiviazione hello durante la creazione di un'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="9aa3d-128">Quando si utilizza piano di hosting hello consumo, i file di configurazione codice e l'associazione di funzione sono archiviati nell'archiviazione di File di Azure nell'account di archiviazione principale hello.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="9aa3d-129">Quando si elimina l'account di archiviazione principale hello, questo contenuto viene eliminato e non può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="9aa3d-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="9aa3d-130">toolearn ulteriori informazioni sui tipi di account di archiviazione, vedere [Introduzione a servizi di archiviazione di Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="9aa3d-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9aa3d-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9aa3d-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



