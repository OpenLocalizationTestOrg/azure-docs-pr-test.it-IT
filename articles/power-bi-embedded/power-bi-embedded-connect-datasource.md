---
title: Power BI Embedded - connessione origine dati di tooa aaaMicrosoft
description: Power BI incorporato, connettere origini toodata
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
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="b4df2-103">Connessione origine dati tooa</span><span class="sxs-lookup"><span data-stu-id="b4df2-103">Connect tooa data source</span></span>
<span data-ttu-id="b4df2-104">Con **Power BI Embedded**è possibile incorporare report in proprie app.</span><span class="sxs-lookup"><span data-stu-id="b4df2-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="b4df2-105">Quando si incorpora un report di Power BI nell'app, report hello si connette toohello sottostante dei dati da **importazione** una copia di dati hello o da **la connessione diretta** toohello origine dati mediante  **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="b4df2-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="b4df2-106">Di seguito sono differenze nell'utilizzo hello **importazione** e **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="b4df2-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="b4df2-107">Importa</span><span class="sxs-lookup"><span data-stu-id="b4df2-107">Import</span></span> | <span data-ttu-id="b4df2-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="b4df2-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="b4df2-109">Tabelle, colonne, *e dati* sono importato o copiato in set di dati del report hello.</span><span class="sxs-lookup"><span data-stu-id="b4df2-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="b4df2-110">toosee modifica i dati sottostanti toohello durante l'esecuzione, è necessario aggiornare o importare, nuovamente un dataset corrente non completato.</span><span class="sxs-lookup"><span data-stu-id="b4df2-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="b4df2-111">Solo *tabelle e colonne* sono importato o copiato in set di dati del report hello.</span><span class="sxs-lookup"><span data-stu-id="b4df2-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="b4df2-112">È sempre possibile visualizzare dati più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="b4df2-112">You always view hello most current data.</span></span> |

<span data-ttu-id="b4df2-113">Con Power BI Embedded è attualmente possibile usare DirectQuery con le origini dati cloud ma non su origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="b4df2-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="b4df2-114">Hello Gateway dati locale non è supportata con Power BI incorporato in questo momento.</span><span class="sxs-lookup"><span data-stu-id="b4df2-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="b4df2-115">Non è quindi possibile usare DirectQuery con origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="b4df2-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="b4df2-116">Origini dati supportate</span><span class="sxs-lookup"><span data-stu-id="b4df2-116">Supported data sources</span></span>

<span data-ttu-id="b4df2-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="b4df2-117">**DirectQuery**</span></span>
* <span data-ttu-id="b4df2-118">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="b4df2-118">Azure SQL database</span></span>
* <span data-ttu-id="b4df2-119">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b4df2-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="b4df2-120">**Import (Importa) (Import (Importa)a)**</span><span class="sxs-lookup"><span data-stu-id="b4df2-120">**Import**</span></span>

<span data-ttu-id="b4df2-121">È possibile importare tramite tutte le origini dati disponibili hello in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="b4df2-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="b4df2-122">Sarà possibile **non** essere in grado di toorefresh dati all'interno di Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b4df2-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="b4df2-123">Sarà necessario modifiche tooupload tooyour PBIX file tooPower BI incorporata.</span><span class="sxs-lookup"><span data-stu-id="b4df2-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="b4df2-124">Questo è dovuto toono disponibile gateway.</span><span class="sxs-lookup"><span data-stu-id="b4df2-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="b4df2-125">Vantaggi di DirectQuery</span><span class="sxs-lookup"><span data-stu-id="b4df2-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="b4df2-126">L'uso di **DirectQuery**presenta due vantaggi principali:</span><span class="sxs-lookup"><span data-stu-id="b4df2-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="b4df2-127">**DirectQuery** consente di creare visualizzazioni su set di dati molto grandi, in cui in caso contrario non sarebbe fattibile toofirst Importa tutti i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="b4df2-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="b4df2-128">Modifica dei dati sottostanti può richiedere un aggiornamento dei dati e per alcuni report, hello necessitano toodisplay corrente dati può richiedere trasferimenti di dati di grandi dimensioni, rendendo impraticabile reimportare i dati.</span><span class="sxs-lookup"><span data-stu-id="b4df2-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="b4df2-129">I report **DirectQuery** usano invece sempre dati correnti.</span><span class="sxs-lookup"><span data-stu-id="b4df2-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="b4df2-130">Limitazioni di DirectQuery</span><span class="sxs-lookup"><span data-stu-id="b4df2-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="b4df2-131">Esistono alcune limitazioni toousing **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="b4df2-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="b4df2-132">Tutte le tabelle devono provenire da un database singolo.</span><span class="sxs-lookup"><span data-stu-id="b4df2-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="b4df2-133">Se la query hello è eccessivamente complessa, si verificherà un errore.</span><span class="sxs-lookup"><span data-stu-id="b4df2-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="b4df2-134">Errore di hello tooremedy deve effettuare il refactoring query hello è meno complessa.</span><span class="sxs-lookup"><span data-stu-id="b4df2-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="b4df2-135">Se query hello devono essere complesse, sarà necessario dati hello tooimport anziché **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="b4df2-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="b4df2-136">Il filtro delle relazioni è limitato tooa unica direzione, invece di entrambe le direzioni.</span><span class="sxs-lookup"><span data-stu-id="b4df2-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="b4df2-137">È possibile modificare il tipo di dati hello di una colonna.</span><span class="sxs-lookup"><span data-stu-id="b4df2-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="b4df2-138">Per impostazione predefinita, alle espressioni DAX valide per le misure sono imposte limitazioni.</span><span class="sxs-lookup"><span data-stu-id="b4df2-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="b4df2-139">Vedere [DirectQuery e misure](#measures).</span><span class="sxs-lookup"><span data-stu-id="b4df2-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="b4df2-140">DirectQuery e misure</span><span class="sxs-lookup"><span data-stu-id="b4df2-140">DirectQuery and measures</span></span>
<span data-ttu-id="b4df2-141">le query di tooensure inviate l'origine dati sottostante toohello hanno prestazioni accettabili, vengono imposte limitazioni alle misure.</span><span class="sxs-lookup"><span data-stu-id="b4df2-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="b4df2-142">Quando si utilizza **Power BI Desktop**avanzate gli utenti possono scegliere toobypass questa limitazione selezionando **File > Opzioni e impostazioni > Opzioni**.</span><span class="sxs-lookup"><span data-stu-id="b4df2-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="b4df2-143">In hello **opzioni** finestra di dialogo, scegliere **DirectQuery**e selezionare l'opzione hello **Consenti misure senza limitazioni in modalità DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="b4df2-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="b4df2-144">Se tale opzione viene selezionata, è possibile usare qualsiasi espressione DAX valida per una misura.</span><span class="sxs-lookup"><span data-stu-id="b4df2-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="b4df2-145">Gli utenti devono tenere; Tuttavia, che alcune espressioni che prestazioni molto elevate quando si importano dati hello può comportare back-end toohello query molto lente nell'origine **DirectQuery** modalità.</span><span class="sxs-lookup"><span data-stu-id="b4df2-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="b4df2-146">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b4df2-146">See Also</span></span>
* [<span data-ttu-id="b4df2-147">Introduzione a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b4df2-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="b4df2-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b4df2-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="b4df2-149">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="b4df2-149">More questions?</span></span> [<span data-ttu-id="b4df2-150">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="b4df2-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

