---
title: Aggiornamento all'API REST di Ricerca di Azure versione 2016-09-01 | Documentazione Microsoft
description: Aggiornamento all'API REST di Ricerca di Azure versione 2016-09-01
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="a6d0e-103">Aggiornamento all'API REST di Ricerca di Azure versione 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="a6d0e-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="a6d0e-104">Se si usa la versione 2015-02-28 o 2015-02-28-Preview dell'[API REST di Ricerca di Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), questo articolo consente di aggiornare l'applicazione alla prima versione disponibile a livello generale dell'API, la versione 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="a6d0e-105">La versione 2016-09-01 dell'API REST include alcune modifiche rispetto alle versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="a6d0e-106">Le versioni sono abbastanza compatibili tra loro, pertanto la modifica del codice richiede un impegno minimo, a seconda della versione in uso prima.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="a6d0e-107">Per istruzioni su come modificare il codice per usare la nuova versione dell'API, vedere [Steps to upgrade](#UpgradeSteps) (Passaggi per eseguire l'aggiornamento).</span><span class="sxs-lookup"><span data-stu-id="a6d0e-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="a6d0e-108">L'istanza del servizio Ricerca di Azure supporta diverse versioni di API REST, inclusa quella più recente.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="a6d0e-109">È possibile continuare a usare una versione anche se non è la più recente, ma si consiglia di migrare il codice per usare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="a6d0e-110">Novità della versione 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="a6d0e-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="a6d0e-111">La versione 2016-09-01 è la seconda disponibile a livello generale dell'API REST di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="a6d0e-112">Le nuove funzionalità in questa versione dell'API includono:</span><span class="sxs-lookup"><span data-stu-id="a6d0e-112">New features in this API version include:</span></span>

* <span data-ttu-id="a6d0e-113">Gli [analizzatori personalizzati](https://aka.ms/customanalyzers), che consentono di controllare il processo di conversione del testo in token indicizzabili e ricercabili.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="a6d0e-114">Gli indicizzatori [Archiviazione BLOB di Azure](search-howto-indexing-azure-blob-storage.md) e [Archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md), che consentono di importare facilmente dati da Archiviazione di Azure in Ricerca di Azure in base a una pianificazione o su richiesta.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="a6d0e-115">[Mapping dei campi](search-indexer-field-mappings.md), che consentono di personalizzare la modalità di importazione dei dati da parte degli indicizzatori in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="a6d0e-116">ETag, che consentono di aggiornare le definizioni di indici, indicizzatori e origini dati in modo indipendente dalla concorrenza.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="a6d0e-117">Passaggi per eseguire l'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="a6d0e-117">Steps to upgrade</span></span>
<span data-ttu-id="a6d0e-118">Se esegue l'aggiornamento dalla versione 2015-02-28, probabilmente non è necessario apportare modifiche al codice, oltre alla modifica del numero di versione.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="a6d0e-119">Le uniche situazioni in cui può essere necessario modificare il codice si verificano quando:</span><span class="sxs-lookup"><span data-stu-id="a6d0e-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="a6d0e-120">Il codice ha esito negativo quando vengono restituite proprietà sconosciute in una risposta API.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="a6d0e-121">Per impostazione predefinita, l'applicazione deve ignorare le proprietà che non riconosce.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="a6d0e-122">Il codice rende persistenti le richieste API e tenta di inviarle nuovamente alla nuova versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="a6d0e-123">Ad esempio, questa situazione può verificarsi se l'applicazione mantiene i token di continuazione restituiti dall'API di ricerca. Per altre informazioni, cercare `@search.nextPageParameters` nel [riferimento all'API di ricerca](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="a6d0e-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="a6d0e-124">Se una delle situazioni seguenti si applica al caso dell'utente, può essere necessario modificare il codice in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="a6d0e-125">In caso contrario, non sono necessarie modifiche a meno che non si voglia iniziare a usre le [nuove funzionalità](#WhatsNew) della versione 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="a6d0e-126">Se si esegue l'aggiornamento dalla versione 2015-02-28-Preview, si applica la situazione precedente, ma è necessario essere consapevoli che alcune funzionalità di anteprima non sono disponibili nella versione 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="a6d0e-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="a6d0e-127">Supporto per gli indicizzatori di Archiviazione BLOB di Azure per i file e i BLOB con estensione csv contenenti matrici JSON.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="a6d0e-128">Sinonimi</span><span class="sxs-lookup"><span data-stu-id="a6d0e-128">Synonyms</span></span>
* <span data-ttu-id="a6d0e-129">Query "Altri elementi simili"</span><span class="sxs-lookup"><span data-stu-id="a6d0e-129">"More like this" queries</span></span>

<span data-ttu-id="a6d0e-130">Se il codice usa queste funzionalità, non sarà possibile eseguire l'aggiornamento alla versione 2016-09-01 senza rimuovere l'utilizzo di tali funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6d0e-131">Si ricordi che le API di anteprima servono per il test e la valutazione e non devono essere usate negli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="a6d0e-132">Conclusione</span><span class="sxs-lookup"><span data-stu-id="a6d0e-132">Conclusion</span></span>
<span data-ttu-id="a6d0e-133">Per altre informazioni sull'uso dell'API REST di Ricerca di Azure, vedere il [riferimento all'API](https://msdn.microsoft.com/library/azure/dn798935.aspx) su MSDN aggiornato di recente.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="a6d0e-134">I commenti degli utenti su Ricerca di Azure sono molto apprezzati.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="a6d0e-135">In caso di problemi, è possibile richiedere assistenza nel [forum MSDN su Ricerca di Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) o in [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="a6d0e-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="a6d0e-136">Se si pongono domande su Ricerca di Azure in StackOverflow, assicurarsi di contrassegnarle con `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="a6d0e-137">Grazie per avere usato Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d0e-137">Thank you for using Azure Search!</span></span>

