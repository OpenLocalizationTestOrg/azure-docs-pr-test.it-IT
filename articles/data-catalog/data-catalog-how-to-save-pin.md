---
title: Salvare le ricerche e aggiungere gli asset di dati in Azure Data Catalog | Microsoft Docs
description: "Articolo che include procedure che illustrano le funzionalità di Azure Data Catalog per il salvataggio delle origini dati e risorse dei dati per un uso successivo."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 8c319d0dcbe8b95af11b8be2368a9348b260446c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="8cc8a-103">Salvare le ricerche e aggiungere gli asset di dati in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="8cc8a-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="8cc8a-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="8cc8a-104">Introduction</span></span>
<span data-ttu-id="8cc8a-105">Azure Data Catalog fornisce le funzionalità per l'individuazione delle origini dati.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="8cc8a-106">È possibile eseguire ricerche e applicare filtri nel catalogo rapidamente per trovare le origini dati e comprenderne le finalità previste, semplificando l'individuazione dei dati corretti per il processo specifico.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-106">You can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span></span>

<span data-ttu-id="8cc8a-107">Nelle situazioni in cui è necessario utilizzare regolarmente gli stessi dati</span><span class="sxs-lookup"><span data-stu-id="8cc8a-107">But what if you need to regularly work with the same data?</span></span> <span data-ttu-id="8cc8a-108">o in cui tutti gli utenti contribuiscono regolarmente alle stesse origini dati del catalogo in base alle proprie competenze,</span><span class="sxs-lookup"><span data-stu-id="8cc8a-108">And what if you and other users regularly contribute your knowledge to the same data sources in the catalog?</span></span> <span data-ttu-id="8cc8a-109">dover eseguire ripetutamente le stesse ricerche può risultare inefficiente.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-109">In these situations, having to repeatedly issue the same searches can be inefficient.</span></span> <span data-ttu-id="8cc8a-110">In questi casi possono essere d'aiuto gli asset delle ricerche salvate e dei dati aggiunti.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="8cc8a-111">Ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="8cc8a-111">Saved searches</span></span>
<span data-ttu-id="8cc8a-112">Una ricerca salvata di Data Catalog è una definizione di ricerca riutilizzabile per singolo utente.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="8cc8a-113">È possibile definire una ricerca, inclusi termini di ricerca, tag e altri filtri e quindi salvarli.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="8cc8a-114">È possibile eseguire nuovamente la definizione della ricerca salvata in un momento successivo per restituire eventuali asset di dati corrispondenti ai criteri di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-114">You can re-run the saved search definition later to return any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="8cc8a-115">Creare una ricerca salvata</span><span class="sxs-lookup"><span data-stu-id="8cc8a-115">Create a saved search</span></span>
<span data-ttu-id="8cc8a-116">Per creare una ricerca salvata, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8cc8a-116">To create a saved search, do the following:</span></span>
1. <span data-ttu-id="8cc8a-117">Nella finestra **Ricerca corrente** del portale di Azure Data Catalog fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-117">In the Azure Data Catalog portal, in the **Current Search** window, click **Save**.</span></span> 

    ![Collegamento Salva nelle impostazioni di Ricerca corrente](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="8cc8a-119">Immettere i criteri di ricerca che si vuole usare di nuovo e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-119">Enter the search criteria that you want to reuse, and then click **Save**.</span></span>

    ![Nome della ricerca salvato nelle impostazioni di Ricerca corrente](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="8cc8a-121">Quando viene richiesto, immettere un nome per la ricerca salvata.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-121">When you are prompted, enter a name for the saved search.</span></span> <span data-ttu-id="8cc8a-122">Scegliere un nome significativo che descriva gli asset di dati che verranno restituiti dalla ricerca.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-122">Pick a name that is meaningful and that describes the data assets that will be returned by the search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="8cc8a-123">Gestire le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="8cc8a-123">Manage saved searches</span></span>
<span data-ttu-id="8cc8a-124">Dopo avere salvato una o più ricerche, viene visualizzata un'opzione **Ricerche salvate** sotto la casella **Ricerca corrente**.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath the **Current Search** box.</span></span> <span data-ttu-id="8cc8a-125">Quando l'elenco viene espanso, vengono visualizzate tutte le ricerche salvate.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-125">When the list is expanded, all saved searches are displayed.</span></span>

 ![Elenco di ricerche salvate](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="8cc8a-127">Eseguire una di queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="8cc8a-127">Do any of the following:</span></span>

* <span data-ttu-id="8cc8a-128">Per eseguire una ricerca, selezionare una ricerca salvata nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-128">To execute a search, select a saved search in the list.</span></span>

* <span data-ttu-id="8cc8a-129">Per visualizzare un elenco di opzioni di gestione per una ricerca salvata, fare clic sulla freccia verso il basso accanto al nome della ricerca.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-129">To view a list of management options for a saved search, click the down arrow next to the search name.</span></span>

    ![Opzioni per la gestione delle ricerche salvate](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="8cc8a-131">Per immettere un nuovo nome per la ricerca salvata, selezionare **Rinomina**.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-131">To enter a new name for the saved search, select **Rename**.</span></span> <span data-ttu-id="8cc8a-132">La definizione della ricerca non viene modificata.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-132">The search definition is not changed.</span></span>

* <span data-ttu-id="8cc8a-133">Per rimuovere la ricerca salvata dall'elenco, selezionare **Elimina** e quindi confermare l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-133">To remove the saved search from your list, select **Delete**, and then confirm the deletion.</span></span>

* <span data-ttu-id="8cc8a-134">Per contrassegnare la ricerca salvata come ricerca predefinita, selezionare **Salva come predefinita**.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-134">To mark the saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="8cc8a-135">Se si esegue una ricerca "vuota" dalla home page di Azure Data Catalog, viene eseguita la ricerca predefinita.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-135">If you perform an “empty” search from the Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="8cc8a-136">La ricerca contrassegnata come predefinita viene anche visualizzata all'inizio dell'elenco **Ricerche salvate**.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-136">In addition, the search that's marked as the default search is displayed at the top of the **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="8cc8a-137">Ricerche salvate dall'organizzazione</span><span class="sxs-lookup"><span data-stu-id="8cc8a-137">Organizational saved searches</span></span>
<span data-ttu-id="8cc8a-138">Tutti gli utenti dell'organizzazione possono salvare le ricerche per usarle a livello personale.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="8cc8a-139">Anche gli amministratori dei dati del catalogo possono salvare le ricerche per tutti gli utenti all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-139">Data Catalog administrators can also save searches for all users within the organization.</span></span> <span data-ttu-id="8cc8a-140">Quando gli amministratori salvano una ricerca, viene visualizzata l'opzione **Condividere all'interno dell'azienda**.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-140">When administrators save a search, they're presented with a **Share within the company** option.</span></span> <span data-ttu-id="8cc8a-141">Se si seleziona questa opzione, la ricerca salvata viene condivisa con tutti gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-141">Selecting this option shares the saved search for all users in the organization.</span></span>

 ![Ricerche salvate dall'organizzazione](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="8cc8a-143">Risorse di dati aggiunte</span><span class="sxs-lookup"><span data-stu-id="8cc8a-143">Pinned data assets</span></span>
<span data-ttu-id="8cc8a-144">Con le ricerche salvate, è possibile salvare e usare di nuovo le definizioni di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="8cc8a-145">Gli asset di dati restituiti dalle ricerche possono cambiare nel tempo perché cambiano i contenuti del catalogo.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-145">The data assets that are returned by the searches might change over time as the contents of the catalog change.</span></span> <span data-ttu-id="8cc8a-146">Quando si aggiungono asset di dati, è possibile identificare esplicitamente asset di dati specifici per semplificarne l'accesso senza dovere usare una ricerca.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-146">When you pin data assets, you can explicitly identify specific data assets to make them easier to access without needing to use a search.</span></span>

<span data-ttu-id="8cc8a-147">L'aggiunta di un asset di dati è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="8cc8a-148">Per inserire l'asset di dati nell'elenco di elementi aggiunti, è sufficiente fare clic sull'icona **aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-148">To add the data asset to your pinned list, you simply click the **pin** icon.</span></span> <span data-ttu-id="8cc8a-149">L'icona viene visualizzata nell'angolo del riquadro dell'asset nella visualizzazione affiancata e nella colonna all'estrema sinistra della visualizzazione elenco nel portale di Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-149">The icon is displayed in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span></span>

![Icona aggiungi dell'asset di dati](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="8cc8a-151">Anche la rimozione di un asset di dati è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="8cc8a-152">È sufficiente fare clic sull'icona **rimuovi** per disattivare l'impostazione per l'asset selezionato.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-152">Simply click the **unpin** icon to toggle the setting for the selected asset.</span></span>

![Icona rimuovi dell'asset di dati](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="the-my-assets-section"></a><span data-ttu-id="8cc8a-154">Sezione Asset personali</span><span class="sxs-lookup"><span data-stu-id="8cc8a-154">The My Assets section</span></span>
<span data-ttu-id="8cc8a-155">La home page del portale di Data Catalog include una sezione **Asset personali** che visualizza le risorse di interesse dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-155">The Data Catalog portal home page includes a **My Assets** section that displays assets of interest to the current user.</span></span> <span data-ttu-id="8cc8a-156">Questa sezione include sia le risorse aggiunte che le ricerche salvate.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-156">This section includes both pinned assets and saved searches.</span></span>

![Sezione Asset personali nella home page](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="8cc8a-158">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="8cc8a-158">Summary</span></span>
<span data-ttu-id="8cc8a-159">Azure Data Catalog offre funzionalità che semplificano l'individuazione delle origini dati necessarie, in modo che tutti i membri dell'organizzazione possano dedicare meno tempo alla ricerca dei dati e concentrarsi invece sull'uso dei dati.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-159">Azure Data Catalog provides capabilities that make it easier to discover the data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="8cc8a-160">Le ricerche salvate e gli asset di dati aggiunti si basano su queste funzionalità di base, in modo che gli utenti possano identificare con facilità le origini dati con cui lavorano ripetutamente.</span><span class="sxs-lookup"><span data-stu-id="8cc8a-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
