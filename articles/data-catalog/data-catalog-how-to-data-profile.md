---
title: 'Procedura: Eseguire il profiling dati delle origini dati'
description: Articolo sulle procedure che illustra come includere profili dati a livello di tabella e di colonna durante la registrazione delle origini dati in Azure Data Catalog e come usare i profili dati per comprendere le origini dati.
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
ms.openlocfilehash: 8f4174f0ed74706b8275c8b1f0a62753f2834fa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="44eee-103">Eseguire il profiling dati delle origini dati</span><span class="sxs-lookup"><span data-stu-id="44eee-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="44eee-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="44eee-104">Introduction</span></span>
<span data-ttu-id="44eee-105">**Catalogo dati di Microsoft Azure** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali.</span><span class="sxs-lookup"><span data-stu-id="44eee-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="44eee-106">In altre parole, il **Catalogo dati di Azure** consente agli utenti di individuare, comprendere e usare origini dati e aiuta le organizzazioni a ottenere maggior valore dai dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="44eee-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="44eee-107">Quando un'origine dati viene registrata con **Azure Data Catalog**, i relativi metadati vengono copiati e indicizzati dal servizio, ma non è tutto.</span><span class="sxs-lookup"><span data-stu-id="44eee-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span>

<span data-ttu-id="44eee-108">La funzione di **profiling dati** di **Azure Data Catalog** esamina i dati delle origini dati supportate nel catalogo e raccoglie statistiche e informazioni sui dati.</span><span class="sxs-lookup"><span data-stu-id="44eee-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="44eee-109">È facile includere un profilo degli asset di dati.</span><span class="sxs-lookup"><span data-stu-id="44eee-109">It's easy to include a profile of your data assets.</span></span> <span data-ttu-id="44eee-110">Quando si registra un asset di dati, scegliere **Includi profilo dati** nello strumento di registrazione delle origini dati.</span><span class="sxs-lookup"><span data-stu-id="44eee-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="44eee-111">Informazioni sul profiling dati</span><span class="sxs-lookup"><span data-stu-id="44eee-111">What is Data Profiling</span></span>
<span data-ttu-id="44eee-112">Il profiling dati esamina i dati nell'origine dati di cui è in corso la registrazione e raccoglie statistiche e informazioni sui dati.</span><span class="sxs-lookup"><span data-stu-id="44eee-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="44eee-113">Durante l'individuazione delle origini dati, le statistiche consentono di determinare l'idoneità dei dati per la risoluzione del problema aziendale.</span><span class="sxs-lookup"><span data-stu-id="44eee-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span></span>

<!-- In [How to discover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How to include a data profile when registering a data source](#howto). -->

<span data-ttu-id="44eee-114">Le origini dati seguenti supportano il profiling dati:</span><span class="sxs-lookup"><span data-stu-id="44eee-114">The following data sources support data profiling:</span></span>

* <span data-ttu-id="44eee-115">Viste e tabelle di SQL Server, inclusi database SQL di Azure e Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44eee-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="44eee-116">Viste e tabelle di Oracle</span><span class="sxs-lookup"><span data-stu-id="44eee-116">Oracle tables and views</span></span>
* <span data-ttu-id="44eee-117">Viste e tabelle di Teradata</span><span class="sxs-lookup"><span data-stu-id="44eee-117">Teradata tables and views</span></span>
* <span data-ttu-id="44eee-118">Tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="44eee-118">Hive tables</span></span>

<span data-ttu-id="44eee-119">Includendo i profili dati durante la registrazione degli asset di dati gli utenti possono rispondere a domande sulle origini dati, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="44eee-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="44eee-120">Può essere usata per risolvere il problema aziendale?</span><span class="sxs-lookup"><span data-stu-id="44eee-120">Can it be used to solve my business problem?</span></span>
* <span data-ttu-id="44eee-121">I dati sono conformi a standard o modelli particolari?</span><span class="sxs-lookup"><span data-stu-id="44eee-121">Does the data conform to particular standards or patterns?</span></span>
* <span data-ttu-id="44eee-122">Quali sono alcune delle anomalie dell'origine dati?</span><span class="sxs-lookup"><span data-stu-id="44eee-122">What are some of the anomalies of the data source?</span></span>
* <span data-ttu-id="44eee-123">Quali sono i possibili problemi legati all'integrazione di questi dati nell'applicazione?</span><span class="sxs-lookup"><span data-stu-id="44eee-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="44eee-124">È anche possibile aggiungere della documentazione a un asset per descrivere come integrare i dati in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="44eee-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span></span> <span data-ttu-id="44eee-125">Vedere l'articolo relativo alla [documentazione delle origini dati](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="44eee-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-to-include-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="44eee-126">Come includere un profilo dati durante la registrazione di un'origine dati</span><span class="sxs-lookup"><span data-stu-id="44eee-126">How to include a data profile when registering a data source</span></span>
<span data-ttu-id="44eee-127">È facile includere un profilo dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="44eee-127">It's easy to include a profile of your data source.</span></span> <span data-ttu-id="44eee-128">Quando si registra un'origine dati, nel pannello **Oggetti da registrare** dello strumento di registrazione delle origini dati scegliere **Includi profilo dati**.</span><span class="sxs-lookup"><span data-stu-id="44eee-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="44eee-129">Per altre informazioni su come registrare le origini dati, vedere [Come registrare le origini dati](data-catalog-how-to-register.md) e [Introduzione ad Azure Data Catalog](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44eee-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="44eee-130">Applicazione di filtri su asset di dati che includono profili dati</span><span class="sxs-lookup"><span data-stu-id="44eee-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="44eee-131">Per trovare asset di dati che includono un profilo dati, è possibile specificare `has:tableDataProfiles` o `has:columnsDataProfiles` come termini di ricerca.</span><span class="sxs-lookup"><span data-stu-id="44eee-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="44eee-132">Selezionando **Includi profilo dati** nello strumento di registrazione dell'origine dati, è possibile includere le informazioni del profilo a livello di tabella e a livello di colonna.</span><span class="sxs-lookup"><span data-stu-id="44eee-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="44eee-133">Tuttavia, l'API del catalogo dati consente la registrazione degli asset di dati con un solo set di informazioni sul profilo.</span><span class="sxs-lookup"><span data-stu-id="44eee-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="44eee-134">Visualizzazione delle informazioni sul profilo dati</span><span class="sxs-lookup"><span data-stu-id="44eee-134">Viewing data profile information</span></span>
<span data-ttu-id="44eee-135">Dopo aver individuato un'origine dati adatta con un profilo, è possibile visualizzare i dettagli relativi al profilo dati.</span><span class="sxs-lookup"><span data-stu-id="44eee-135">Once you find a suitable data source with a profile, you can view the data profile details.</span></span> <span data-ttu-id="44eee-136">Per visualizzare il profilo dati, selezionare un asset di dati e scegliere **Profilo dati** nella finestra del portale di Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="44eee-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="44eee-137">Un profilo dati in **Azure Data Catalog** include informazioni sul profilo a livello di tabella e di colonna, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="44eee-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="44eee-138">Profilo dati dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="44eee-138">Object data profile</span></span>
* <span data-ttu-id="44eee-139">Numero di righe</span><span class="sxs-lookup"><span data-stu-id="44eee-139">Number of rows</span></span>
* <span data-ttu-id="44eee-140">Dimensioni della tabella</span><span class="sxs-lookup"><span data-stu-id="44eee-140">Table size</span></span>
* <span data-ttu-id="44eee-141">Ultimo aggiornamento dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="44eee-141">When the object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="44eee-142">Profilo dati della colonna</span><span class="sxs-lookup"><span data-stu-id="44eee-142">Column data profile</span></span>
* <span data-ttu-id="44eee-143">Tipo di dati della colonna</span><span class="sxs-lookup"><span data-stu-id="44eee-143">Column data type</span></span>
* <span data-ttu-id="44eee-144">Numero di valori distinct</span><span class="sxs-lookup"><span data-stu-id="44eee-144">Number of distinct values</span></span>
* <span data-ttu-id="44eee-145">Numero di righe con valori NULL</span><span class="sxs-lookup"><span data-stu-id="44eee-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="44eee-146">Deviazione minima, massima, media e standard per i valori di colonna</span><span class="sxs-lookup"><span data-stu-id="44eee-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="44eee-147">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="44eee-147">Summary</span></span>
<span data-ttu-id="44eee-148">Il profiling dati fornisce statistiche e informazioni sugli asset di dati registrati per consentire di determinare l'idoneità dei dati per la risoluzione di problemi aziendali.</span><span class="sxs-lookup"><span data-stu-id="44eee-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span></span> <span data-ttu-id="44eee-149">Oltre che annotare e documentare le origini dati, i profili dati permettono agli utenti di comprendere meglio i dati.</span><span class="sxs-lookup"><span data-stu-id="44eee-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="44eee-150">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="44eee-150">See Also</span></span>
* [<span data-ttu-id="44eee-151">Come registrare le origini dati</span><span class="sxs-lookup"><span data-stu-id="44eee-151">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="44eee-152">Introduzione ad Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="44eee-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
