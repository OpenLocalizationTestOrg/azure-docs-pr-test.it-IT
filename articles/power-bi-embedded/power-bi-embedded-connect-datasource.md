---
title: Microsoft Power BI Embedded - Connessione a un'origine dati
description: Microsoft Power BI Embedded - Connettersi a origini dati
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="3c225-103">Connettersi a un'origine dati</span><span class="sxs-lookup"><span data-stu-id="3c225-103">Connect to a data source</span></span>
<span data-ttu-id="3c225-104">Con **Power BI Embedded**è possibile incorporare report in proprie app.</span><span class="sxs-lookup"><span data-stu-id="3c225-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="3c225-105">Quando un report di Power BI viene incorporato in un'app, il report si connette ai dati sottostanti tramite l'**importazione** di una copia dei dati o tramite **connessione** diretta all'origine dati con **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="3c225-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="3c225-106">Di seguito sono spiegate le differenze tra l'**importazione** e **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="3c225-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="3c225-107">Importa</span><span class="sxs-lookup"><span data-stu-id="3c225-107">Import</span></span> | <span data-ttu-id="3c225-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="3c225-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="3c225-109">Tabelle, colonne *e dati* vengono importati o copiati nel set di dati del report.</span><span class="sxs-lookup"><span data-stu-id="3c225-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="3c225-110">Per visualizzare le modifiche apportate ai dati sottostanti, è necessario aggiornare o importare nuovamente un set di dati completo e corrente.</span><span class="sxs-lookup"><span data-stu-id="3c225-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="3c225-111">Vengono importate o copiate nel set di dati del report solo *tabelle e colonne* .</span><span class="sxs-lookup"><span data-stu-id="3c225-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="3c225-112">Vengono visualizzati sempre i dati più recenti.</span><span class="sxs-lookup"><span data-stu-id="3c225-112">You always view the most current data.</span></span> |

<span data-ttu-id="3c225-113">Con Power BI Embedded è attualmente possibile usare DirectQuery con le origini dati cloud ma non su origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="3c225-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="3c225-114">Il gateway dati locale non è al momento supportato con Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="3c225-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="3c225-115">Non è quindi possibile usare DirectQuery con origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="3c225-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="3c225-116">Origini dati supportate</span><span class="sxs-lookup"><span data-stu-id="3c225-116">Supported data sources</span></span>

<span data-ttu-id="3c225-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="3c225-117">**DirectQuery**</span></span>
* <span data-ttu-id="3c225-118">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="3c225-118">Azure SQL database</span></span>
* <span data-ttu-id="3c225-119">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3c225-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="3c225-120">**Import (Importa) (Import (Importa)a)**</span><span class="sxs-lookup"><span data-stu-id="3c225-120">**Import**</span></span>

<span data-ttu-id="3c225-121">È possibile usare per l'importazione tutte le origini dati disponibili in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="3c225-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="3c225-122">Tali dati **non** potranno essere aggiornati in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="3c225-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="3c225-123">Sarà necessario caricare le modifiche al file PBIX in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="3c225-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="3c225-124">Questo è dovuto al fatto che non è disponibile un gateway.</span><span class="sxs-lookup"><span data-stu-id="3c225-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="3c225-125">Vantaggi di DirectQuery</span><span class="sxs-lookup"><span data-stu-id="3c225-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="3c225-126">L'uso di **DirectQuery**presenta due vantaggi principali:</span><span class="sxs-lookup"><span data-stu-id="3c225-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="3c225-127">**DirectQuery** consente di creare visualizzazioni su set di dati molto grandi nei casi in cui sarebbe impossibile importare prima tutti i dati.</span><span class="sxs-lookup"><span data-stu-id="3c225-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="3c225-128">Le modifiche ai dati sottostanti possono richiedere un aggiornamento dei dati. Nel caso di alcuni report, per visualizzare i dati correnti, può essere quindi necessario trasferire molti dati, rendendo la re-importazione dei dati impossibile.</span><span class="sxs-lookup"><span data-stu-id="3c225-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="3c225-129">I report **DirectQuery** usano invece sempre dati correnti.</span><span class="sxs-lookup"><span data-stu-id="3c225-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="3c225-130">Limitazioni di DirectQuery</span><span class="sxs-lookup"><span data-stu-id="3c225-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="3c225-131">L'uso di **DirectQuery**presenta alcune limitazioni:</span><span class="sxs-lookup"><span data-stu-id="3c225-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="3c225-132">Tutte le tabelle devono provenire da un database singolo.</span><span class="sxs-lookup"><span data-stu-id="3c225-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="3c225-133">Se la query è troppo complessa, si verificherà un errore.</span><span class="sxs-lookup"><span data-stu-id="3c225-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="3c225-134">Per correggere l'errore è necessario eseguire il refactoring della query per renderla meno complessa.</span><span class="sxs-lookup"><span data-stu-id="3c225-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="3c225-135">Se la query deve essere necessariamente complessa, i dati saranno importati e non sarà possibile usare la modalità **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="3c225-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="3c225-136">Il filtro di relazione è limitato a un'unica direzione, piuttosto che ad entrambe le direzioni.</span><span class="sxs-lookup"><span data-stu-id="3c225-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="3c225-137">Non è possibile modificare il tipo di dati di una colonna.</span><span class="sxs-lookup"><span data-stu-id="3c225-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="3c225-138">Per impostazione predefinita, alle espressioni DAX valide per le misure sono imposte limitazioni.</span><span class="sxs-lookup"><span data-stu-id="3c225-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="3c225-139">Vedere [DirectQuery e misure](#measures).</span><span class="sxs-lookup"><span data-stu-id="3c225-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="3c225-140">DirectQuery e misure</span><span class="sxs-lookup"><span data-stu-id="3c225-140">DirectQuery and measures</span></span>
<span data-ttu-id="3c225-141">Per garantire che le prestazioni delle query inviate all'origine dati sottostante siano accettabili, vengono imposte limitazioni alle misure.</span><span class="sxs-lookup"><span data-stu-id="3c225-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="3c225-142">In **Power BI Desktop** gli utenti esperti possono scegliere di ignorare questa limitazione selezionando **File > Opzioni e impostazioni > Opzioni**.</span><span class="sxs-lookup"><span data-stu-id="3c225-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="3c225-143">Nella finestra di dialogo **Opzioni** scegliere **DirectQuery** e selezionare l'opzione **Consenti misure senza limitazioni in modalità DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="3c225-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="3c225-144">Se tale opzione viene selezionata, è possibile usare qualsiasi espressione DAX valida per una misura.</span><span class="sxs-lookup"><span data-stu-id="3c225-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="3c225-145">È tuttavia necessario sapere che alcune espressioni che funzionano molto bene quando i dati sono importati possono invece rallentare considerevolmente le query all'origine back-end se si usa la modalità **DirectQuery** .</span><span class="sxs-lookup"><span data-stu-id="3c225-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="3c225-146">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3c225-146">See Also</span></span>
* [<span data-ttu-id="3c225-147">Introduzione a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3c225-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="3c225-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3c225-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="3c225-149">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="3c225-149">More questions?</span></span> [<span data-ttu-id="3c225-150">Contattare la community di Power BI</span><span class="sxs-lookup"><span data-stu-id="3c225-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

