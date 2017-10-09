---
title: aaaUpgrading toohello Azure API REST di ricerca versione 2016-09-01 | Documenti Microsoft
description: L'aggiornamento toohello Azure API REST di ricerca versione 2016-09-01
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
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="3b0d6-103">L'aggiornamento toohello Azure API REST di ricerca versione 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="3b0d6-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="3b0d6-104">Se si utilizza la versione 2015-02-28 o 2015-02-28-Preview di hello [API REST di Azure ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx), in questo articolo consentirà di aggiornare l'applicazione toouse hello in genere disponibili API versione successiva, 01 / 09 / 2016.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="3b0d6-105">Versione 2016-09-01 di hello API REST include alcune modifiche apportate da versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="3b0d6-106">Le versioni sono abbastanza compatibili tra loro, pertanto la modifica del codice richiede un impegno minimo, a seconda della versione in uso prima.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="3b0d6-107">Vedere [tooupgrade passaggi](#UpgradeSteps) per istruzioni su come toochange il codice toouse hello nuova versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="3b0d6-108">L'istanza del servizio di ricerca di Azure supporta più versioni API REST, tra cui hello più recente.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="3b0d6-109">È possibile continuare toouse una versione quando non è più hello più recente, ma è consigliabile eseguire la migrazione la versione più recente del codice toouse hello.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="3b0d6-110">Novità della versione 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="3b0d6-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="3b0d6-111">Versione 2016-09-01 è secondo rilascio generalmente disponibili hello di hello API REST del servizio ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="3b0d6-112">Le nuove funzionalità in questa versione dell'API includono:</span><span class="sxs-lookup"><span data-stu-id="3b0d6-112">New features in this API version include:</span></span>

* <span data-ttu-id="3b0d6-113">[Gli analizzatori personalizzati](https://aka.ms/customanalyzers), che consentono di controllo tootake hello del processo di conversione di testo in token indicizzabili e disponibile per la ricerca.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="3b0d6-114">[Archiviazione Blob di Azure](search-howto-indexing-azure-blob-storage.md) e [archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md) indicizzatori, che consentono di tooeasily importare dati dall'archiviazione di Azure in ricerca di Azure in una pianificazione o su richiesta.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="3b0d6-115">[Campo di mapping](search-indexer-field-mappings.md), che consentono di toocustomize come importano dati di indicizzatori in ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="3b0d6-116">ETag, che consentono di definizioni di hello tooupdate degli indici, gli indicizzatori e origini dati in modo indipendente dalla concorrenza.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="3b0d6-117">Passaggi tooupgrade</span><span class="sxs-lookup"><span data-stu-id="3b0d6-117">Steps tooupgrade</span></span>
<span data-ttu-id="3b0d6-118">Se esegue l'aggiornamento dalla versione 2015-02-28, probabilmente sarà possibile toomake qualsiasi codice tooyour modifiche, diverso dal numero di versione di hello toochange.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="3b0d6-119">situazioni di Hello solo in cui potrebbe essere necessario codice toochange sono quando:</span><span class="sxs-lookup"><span data-stu-id="3b0d6-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="3b0d6-120">Il codice ha esito negativo quando vengono restituite proprietà sconosciute in una risposta API.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="3b0d6-121">Per impostazione predefinita, l'applicazione deve ignorare le proprietà che non riconosce.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="3b0d6-122">Il codice rende persistenti le richieste API e tenta tooresend li toohello nuova versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="3b0d6-123">Ad esempio, questa situazione può verificarsi se l'applicazione mantiene i token di continuazione restituiti dall'API di ricerca hello (per ulteriori informazioni, cercare `@search.nextPageParameters` in hello [riferimento all'API di ricerca](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="3b0d6-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="3b0d6-124">Se una delle situazioni seguenti si applicano tooyou, potrebbe essere toochange il codice di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="3b0d6-125">In caso contrario, non devono essere necessarie modifiche a meno che non si desidera toostart utilizzando hello [nuove funzionalità](#WhatsNew) della versione 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="3b0d6-126">Se esegue l'aggiornamento dalla versione 2015-02-28-Preview, si applica anche hello precedente, ma è inoltre necessario tenere presente che alcune funzionalità di anteprima non sono disponibili nella versione 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="3b0d6-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="3b0d6-127">Supporto per gli indicizzatori di Archiviazione BLOB di Azure per i file e i BLOB con estensione csv contenenti matrici JSON.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="3b0d6-128">Sinonimi</span><span class="sxs-lookup"><span data-stu-id="3b0d6-128">Synonyms</span></span>
* <span data-ttu-id="3b0d6-129">Query "Altri elementi simili"</span><span class="sxs-lookup"><span data-stu-id="3b0d6-129">"More like this" queries</span></span>

<span data-ttu-id="3b0d6-130">Se il codice utilizza queste funzionalità, non sarà in grado di tooupgrade too2016-09-01, senza rimuovere l'utilizzo di essi.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b0d6-131">Si ricordi che le API di anteprima servono per il test e la valutazione e non devono essere usate negli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="3b0d6-132">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="3b0d6-132">Conclusion</span></span>
<span data-ttu-id="3b0d6-133">Per ulteriori informazioni sull'utilizzo di hello API REST del servizio ricerca di Azure, vedere hello aggiornato di recente [riferimento all'API](https://msdn.microsoft.com/library/azure/dn798935.aspx) su MSDN.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="3b0d6-134">I commenti degli utenti su Ricerca di Azure sono molto apprezzati.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="3b0d6-135">Se si verificano problemi, è disponibile tooask ci per informazioni su hello [forum MSDN di ricerca di Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) o [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="3b0d6-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="3b0d6-136">Se si desidera che una domanda su Azure ricerca StackOverflow, assicurarsi che tootag con `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="3b0d6-137">Grazie per avere usato Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0d6-137">Thank you for using Azure Search!</span></span>

