---
title: Creare un'app per le funzioni dal portale di Azure | Microsoft Docs
description: Creare una nuova app per le funzioni in Servizio app di Azure dal portale.
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
ms.openlocfilehash: 85a88c537415cd6f2b6bc005cc18e3baaa29e9a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-app-from-the-azure-portal"></a><span data-ttu-id="02f6f-103">Creare un'app per le funzioni dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="02f6f-103">Create a function app from the Azure portal</span></span>

<span data-ttu-id="02f6f-104">App per le funzioni di Azure usa l'infrastruttura di Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="02f6f-104">Azure Function Apps uses the Azure App Service infrastructure.</span></span> <span data-ttu-id="02f6f-105">In questo argomento viene illustrato come creare un'app per le funzioni nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="02f6f-105">This topic shows you how to create a function app in the Azure portal.</span></span> <span data-ttu-id="02f6f-106">Un'app per le funzioni è un contenitore che ospita l'esecuzione delle singole funzioni.</span><span class="sxs-lookup"><span data-stu-id="02f6f-106">A function app is the container that hosts the execution of individual functions.</span></span> <span data-ttu-id="02f6f-107">Quando si crea un'app per le funzioni nel servizio app che ospita il piano, l'app per le funzioni può usare tutte le funzionalità del servizio app.</span><span class="sxs-lookup"><span data-stu-id="02f6f-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="02f6f-108">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="02f6f-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="02f6f-109">Quando si crea un'app per le funzioni, inserire un **nome dell'app** valido, che contenga solo lettere, numeri e trattini.</span><span class="sxs-lookup"><span data-stu-id="02f6f-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="02f6f-110">Il carattere di sottolineatura (**_**) non è consentito.</span><span class="sxs-lookup"><span data-stu-id="02f6f-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="02f6f-111">I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="02f6f-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="02f6f-112">Nome dell'account di archiviazione deve essere univoco all'interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="02f6f-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="02f6f-113">Dopo aver creato l'app per le funzioni, è possibile creare singole funzioni in una o più lingue diverse.</span><span class="sxs-lookup"><span data-stu-id="02f6f-113">After the function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="02f6f-114">Creare funzioni [tramite il portale](functions-create-first-azure-function.md#create-function), [la distribuzione continua](functions-continuous-deployment.md) o tramite il [caricamento con FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="02f6f-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="02f6f-115">Piani di servizio</span><span class="sxs-lookup"><span data-stu-id="02f6f-115">Service plans</span></span>

<span data-ttu-id="02f6f-116">Funzioni di Azure offre due piani di servizio diversi: piano a consumo e piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="02f6f-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="02f6f-117">Il piano a consumo alloca automaticamente funzionalità di calcolo durante l'esecuzione del codice, aumenta il numero di istanze in base alla necessità per gestire il carico e quindi riduce il numero di istanze quando il codice non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="02f6f-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="02f6f-118">Il piano di servizio app consente all'app per le funzioni di accedere a tutte le funzionalità del servizio app.</span><span class="sxs-lookup"><span data-stu-id="02f6f-118">The App Service plan gives your function app access to all the facilities of App Service.</span></span> <span data-ttu-id="02f6f-119">È necessario scegliere il piano di servizio quando viene creata l'app per le funzioni, che al momento non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="02f6f-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="02f6f-120">Per altre informazioni, vedere [Scegliere un piano di hosting di Funzioni di Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="02f6f-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="02f6f-121">Se si prevede di eseguire funzioni JavaScript in un piano di servizio App, è necessario scegliere un piano con un minor numero di core.</span><span class="sxs-lookup"><span data-stu-id="02f6f-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="02f6f-122">Per altre informazioni, vedere le [informazioni di riferimento su JavaScript per le funzioni](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="02f6f-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="02f6f-123">Requisiti dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="02f6f-123">Storage account requirements</span></span>

<span data-ttu-id="02f6f-124">Quando si crea un'app per le funzioni in servizio app, è necessario creare o collegare un account di Archiviazione di Azure di uso generico che supporti l'archiviazione BLOB, code e tabelle.</span><span class="sxs-lookup"><span data-stu-id="02f6f-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="02f6f-125">Le funzioni usano internamente l'archiviazione per operazioni come la gestione dei trigger e la registrazione dell'esecuzione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="02f6f-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="02f6f-126">Alcuni account di archiviazione, come gli account di archiviazione solo BLOB, Archiviazione Premium di Azure e gli account di archiviazione di uso generico con replica ZRS, non supportano code e tabelle.</span><span class="sxs-lookup"><span data-stu-id="02f6f-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="02f6f-127">Questi account vengono filtrati dal pannello Account di archiviazione quando si crea una nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="02f6f-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="02f6f-128">Quando si usa il piano di hosting a consumo, i file del codice di funzione e la configurazione di binding vengono archiviati nell'archiviazione file di Azure nell'account di archiviazione principale.</span><span class="sxs-lookup"><span data-stu-id="02f6f-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span></span> <span data-ttu-id="02f6f-129">Quando si elimina l'account di archiviazione principale, il contenuto viene eliminato e non può essere ripristinato.</span><span class="sxs-lookup"><span data-stu-id="02f6f-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="02f6f-130">Per altre informazioni sui tipi di account di archiviazione, vedere l'[introduzione ai servizi di Archiviazione di Azure](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="02f6f-130">To learn more about storage account types, see [Introducing the Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="02f6f-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02f6f-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



