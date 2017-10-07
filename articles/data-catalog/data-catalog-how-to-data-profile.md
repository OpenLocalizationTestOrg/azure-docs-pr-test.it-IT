---
title: origini dati di profilo tooData aaaHow
description: Come-tooarticle evidenziazione come dati a livello di tabella e di colonna tooinclude profili per la registrazione delle origini dati in Azure Data Catalog e come dati toouse profili toounderstand origini di dati.
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="16d58-103">Eseguire il profiling dati delle origini dati</span><span class="sxs-lookup"><span data-stu-id="16d58-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="16d58-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="16d58-104">Introduction</span></span>
<span data-ttu-id="16d58-105">**Microsoft Azure Data Catalog** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali.</span><span class="sxs-lookup"><span data-stu-id="16d58-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="16d58-106">In altre parole, **Azure Data Catalog** è tutte sulle persone assistenza individuare, comprendere e utilizzare origini dati e aiutare le organizzazioni tooget più valore dai dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="16d58-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="16d58-107">Quando un'origine dati è registrata con **Azure Data Catalog**, i relativi metadati viene copiato e indicizzato dal servizio hello, ma storia hello non finisce qui.</span><span class="sxs-lookup"><span data-stu-id="16d58-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="16d58-108">Hello **Profiling dati** funzionalità di **Azure Data Catalog** esamina hello dati da origini dati supportate nel catalogo e raccoglie le statistiche e informazioni relativi a tali dati.</span><span class="sxs-lookup"><span data-stu-id="16d58-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="16d58-109">È facile tooinclude un profilo di asset di dati.</span><span class="sxs-lookup"><span data-stu-id="16d58-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="16d58-110">Quando si registra un asset di dati, scegliere **includono dati profilo** nello strumento di registrazione origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="16d58-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="16d58-111">Informazioni sul profiling dati</span><span class="sxs-lookup"><span data-stu-id="16d58-111">What is Data Profiling</span></span>
<span data-ttu-id="16d58-112">Profiling dati esamina hello dati nell'origine dati hello in corso la registrazione e raccoglie le statistiche e informazioni relativi a tali dati.</span><span class="sxs-lookup"><span data-stu-id="16d58-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="16d58-113">Durante l'individuazione di origine dati, queste statistiche consentono di determinare idoneità hello di hello dati toosolve il problema aziendale.</span><span class="sxs-lookup"><span data-stu-id="16d58-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="16d58-114">Hello origini dati seguenti supportano dati di profilatura:</span><span class="sxs-lookup"><span data-stu-id="16d58-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="16d58-115">Viste e tabelle di SQL Server, inclusi database SQL di Azure e Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="16d58-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="16d58-116">Viste e tabelle di Oracle</span><span class="sxs-lookup"><span data-stu-id="16d58-116">Oracle tables and views</span></span>
* <span data-ttu-id="16d58-117">Viste e tabelle di Teradata</span><span class="sxs-lookup"><span data-stu-id="16d58-117">Teradata tables and views</span></span>
* <span data-ttu-id="16d58-118">Tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="16d58-118">Hive tables</span></span>

<span data-ttu-id="16d58-119">Includendo i profili dati durante la registrazione degli asset di dati gli utenti possono rispondere a domande sulle origini dati, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16d58-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="16d58-120">Può essere utilizzato toosolve il problema aziendale?</span><span class="sxs-lookup"><span data-stu-id="16d58-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="16d58-121">Dati hello rispetta gli standard tooparticular o modelli?</span><span class="sxs-lookup"><span data-stu-id="16d58-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="16d58-122">Quali sono alcune delle anomalie hello dell'origine dati hello?</span><span class="sxs-lookup"><span data-stu-id="16d58-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="16d58-123">Quali sono i possibili problemi legati all'integrazione di questi dati nell'applicazione?</span><span class="sxs-lookup"><span data-stu-id="16d58-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="16d58-124">È anche possibile aggiungere documentazione tooan asset toodescribe come è possibile integrare i dati in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="16d58-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="16d58-125">Vedere [come origini dati toodocument](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="16d58-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="16d58-126">Come tooinclude un tipo di dati del profilo quando si registra un'origine dati</span><span class="sxs-lookup"><span data-stu-id="16d58-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="16d58-127">È facile tooinclude un profilo dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="16d58-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="16d58-128">Quando si registra un'origine dati, in hello **toobe oggetti registrati** pannello della registrazione dell'origine dati hello strumento, scegliere **includono dati profilo**.</span><span class="sxs-lookup"><span data-stu-id="16d58-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="16d58-129">altre informazioni sulle toolearn tooregister le origini dati, vedere [come origini dati tooregister](data-catalog-how-to-register.md) e [Guida introduttiva di Azure Data Catalog](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16d58-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="16d58-130">Applicazione di filtri su asset di dati che includono profili dati</span><span class="sxs-lookup"><span data-stu-id="16d58-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="16d58-131">toodiscover gli asset di dati che includono un profilo dati, è possibile includere `has:tableDataProfiles` o `has:columnsDataProfiles` come uno dei termini di ricerca.</span><span class="sxs-lookup"><span data-stu-id="16d58-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="16d58-132">Selezione **includono dati profilo** di hello dati strumento di registrazione di origine include sia la tabella informazioni sul profilo a livello di colonna.</span><span class="sxs-lookup"><span data-stu-id="16d58-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="16d58-133">Tuttavia, hello API di catalogo dati consente dati asset toobe registrato con un solo set di informazioni sul profilo inclusi.</span><span class="sxs-lookup"><span data-stu-id="16d58-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="16d58-134">Visualizzazione delle informazioni sul profilo dati</span><span class="sxs-lookup"><span data-stu-id="16d58-134">Viewing data profile information</span></span>
<span data-ttu-id="16d58-135">Dopo aver individuato l'origine dati appropriata con un profilo, è possibile visualizzare i dettagli del profilo dati hello.</span><span class="sxs-lookup"><span data-stu-id="16d58-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="16d58-136">dati hello tooview del profilo, selezionare un asset di dati e scegliere **profilo dati** nella finestra del portale di hello catalogo dati.</span><span class="sxs-lookup"><span data-stu-id="16d58-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="16d58-137">Un profilo dati in **Azure Data Catalog** include informazioni sul profilo a livello di tabella e di colonna, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16d58-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="16d58-138">Profilo dati dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="16d58-138">Object data profile</span></span>
* <span data-ttu-id="16d58-139">Numero di righe</span><span class="sxs-lookup"><span data-stu-id="16d58-139">Number of rows</span></span>
* <span data-ttu-id="16d58-140">Dimensioni della tabella</span><span class="sxs-lookup"><span data-stu-id="16d58-140">Table size</span></span>
* <span data-ttu-id="16d58-141">Ultimo aggiornamento dell'oggetto hello</span><span class="sxs-lookup"><span data-stu-id="16d58-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="16d58-142">Profilo dati della colonna</span><span class="sxs-lookup"><span data-stu-id="16d58-142">Column data profile</span></span>
* <span data-ttu-id="16d58-143">Tipo di dati della colonna</span><span class="sxs-lookup"><span data-stu-id="16d58-143">Column data type</span></span>
* <span data-ttu-id="16d58-144">Numero di valori distinct</span><span class="sxs-lookup"><span data-stu-id="16d58-144">Number of distinct values</span></span>
* <span data-ttu-id="16d58-145">Numero di righe con valori NULL</span><span class="sxs-lookup"><span data-stu-id="16d58-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="16d58-146">Deviazione minima, massima, media e standard per i valori di colonna</span><span class="sxs-lookup"><span data-stu-id="16d58-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="16d58-147">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="16d58-147">Summary</span></span>
<span data-ttu-id="16d58-148">Profiling dati fornisce le statistiche e informazioni registrate toohelp asset di dati è determinare l'idoneità hello di problemi di hello dati toosolve aziendali.</span><span class="sxs-lookup"><span data-stu-id="16d58-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="16d58-149">Oltre che annotare e documentare le origini dati, i profili dati permettono agli utenti di comprendere meglio i dati.</span><span class="sxs-lookup"><span data-stu-id="16d58-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="16d58-150">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="16d58-150">See Also</span></span>
* [<span data-ttu-id="16d58-151">Come origini dati tooregister</span><span class="sxs-lookup"><span data-stu-id="16d58-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="16d58-152">Introduzione ad Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="16d58-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
