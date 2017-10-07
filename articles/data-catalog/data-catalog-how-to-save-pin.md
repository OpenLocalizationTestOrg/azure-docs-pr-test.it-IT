---
title: aaaSave ricerche e pin asset di dati in Azure Data Catalog | Documenti Microsoft
description: "Come tooarticle evidenziazione funzionalità in Azure Data Catalog per il salvataggio delle origini dati e gli asset di dati per un uso successivo."
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
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="7d44a-103">Salvare le ricerche e aggiungere gli asset di dati in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="7d44a-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="7d44a-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="7d44a-104">Introduction</span></span>
<span data-ttu-id="7d44a-105">Azure Data Catalog fornisce le funzionalità per l'individuazione delle origini dati.</span><span class="sxs-lookup"><span data-stu-id="7d44a-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="7d44a-106">Rapidamente, è possibile cercare e filtrare le origini dati del catalogo toolocate hello e comprendere lo scopo previsto, rendendo più semplice toofind hello destra dei dati per il processo di hello in questione.</span><span class="sxs-lookup"><span data-stu-id="7d44a-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="7d44a-107">Ma cosa accade se è necessario tooregularly funzionano con hello stesso dati?</span><span class="sxs-lookup"><span data-stu-id="7d44a-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="7d44a-108">E cosa accade se altri utenti contribuiscono regolarmente il toohello knowledge stesse origini dati nel catalogo di hello?</span><span class="sxs-lookup"><span data-stu-id="7d44a-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="7d44a-109">In queste situazioni, verificato il problema toorepeatedly hello stesso ricerche possono risultare inefficiente.</span><span class="sxs-lookup"><span data-stu-id="7d44a-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="7d44a-110">In questi casi possono essere d'aiuto gli asset delle ricerche salvate e dei dati aggiunti.</span><span class="sxs-lookup"><span data-stu-id="7d44a-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="7d44a-111">Ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="7d44a-111">Saved searches</span></span>
<span data-ttu-id="7d44a-112">Una ricerca salvata di Data Catalog è una definizione di ricerca riutilizzabile per singolo utente.</span><span class="sxs-lookup"><span data-stu-id="7d44a-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="7d44a-113">È possibile definire una ricerca, inclusi termini di ricerca, tag e altri filtri e quindi salvarli.</span><span class="sxs-lookup"><span data-stu-id="7d44a-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="7d44a-114">È possibile eseguire nuovamente la definizione di ricerca salvata hello tooreturn successive tutte le risorse di dati corrispondenti ai criteri di ricerca.</span><span class="sxs-lookup"><span data-stu-id="7d44a-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="7d44a-115">Creare una ricerca salvata</span><span class="sxs-lookup"><span data-stu-id="7d44a-115">Create a saved search</span></span>
<span data-ttu-id="7d44a-116">toocreate una ricerca salvata, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7d44a-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="7d44a-117">Nel portale di Azure Data Catalog, hello hello **ricerca corrente** finestra, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="7d44a-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![Collegamento Salva nelle impostazioni di Ricerca corrente](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="7d44a-119">Immettere i criteri di ricerca hello che desidera tooreuse e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="7d44a-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![Nome della ricerca salvato nelle impostazioni di Ricerca corrente](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="7d44a-121">Quando richiesto, immettere un nome per la ricerca salvata hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="7d44a-122">Scegliere un nome significativo e che descrive l'asset di dati hello che verranno restituiti dalla ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="7d44a-123">Gestire le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="7d44a-123">Manage saved searches</span></span>
<span data-ttu-id="7d44a-124">Dopo aver salvato le ricerche di uno o più, un **ricerche salvate** opzione viene visualizzata di sotto di hello **ricerca corrente** casella.</span><span class="sxs-lookup"><span data-stu-id="7d44a-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="7d44a-125">Quando viene espanso l'elenco di hello, vengono visualizzate tutte le ricerche salvate.</span><span class="sxs-lookup"><span data-stu-id="7d44a-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![Elenco di ricerche salvate](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="7d44a-127">Eseguire una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="7d44a-127">Do any of hello following:</span></span>

* <span data-ttu-id="7d44a-128">tooexecute una ricerca, selezionare una ricerca salvata nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="7d44a-129">tooview un elenco di opzioni di gestione per una ricerca salvata, fare clic su hello il nome successivo toohello ricerca sulla freccia verso il basso.</span><span class="sxs-lookup"><span data-stu-id="7d44a-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![Opzioni per la gestione delle ricerche salvate](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="7d44a-131">Selezionare un nuovo nome per la ricerca salvata hello tooenter **rinominare**.</span><span class="sxs-lookup"><span data-stu-id="7d44a-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="7d44a-132">definizione di ricerca Hello non viene modificata.</span><span class="sxs-lookup"><span data-stu-id="7d44a-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="7d44a-133">ricerca di tooremove hello salvato dall'elenco, selezionare **eliminare**, quindi confermare l'eliminazione di hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="7d44a-134">ricerca di hello salvato toomark come ricerca predefinito, selezionare **Salva come predefinito**.</span><span class="sxs-lookup"><span data-stu-id="7d44a-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="7d44a-135">Se si esegue una ricerca di "vuota" dalla home page di hello Azure Data Catalog, viene eseguita la ricerca del valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="7d44a-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="7d44a-136">Inoltre, hello ricerca che è contrassegnato come ricerca predefinita hello viene visualizzato nella parte superiore di hello di hello **ricerche salvate** elenco.</span><span class="sxs-lookup"><span data-stu-id="7d44a-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="7d44a-137">Ricerche salvate dall'organizzazione</span><span class="sxs-lookup"><span data-stu-id="7d44a-137">Organizational saved searches</span></span>
<span data-ttu-id="7d44a-138">Tutti gli utenti dell'organizzazione possono salvare le ricerche per usarle a livello personale.</span><span class="sxs-lookup"><span data-stu-id="7d44a-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="7d44a-139">Gli amministratori del catalogo dati è inoltre possono salvare le ricerche per tutti gli utenti all'interno dell'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="7d44a-140">Quando gli amministratori di salvino una ricerca, essi vengono presentati con un **condivisione all'interno della società hello** opzione.</span><span class="sxs-lookup"><span data-stu-id="7d44a-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="7d44a-141">Se si seleziona questo hello condivisioni opzione salvato cercare tutti gli utenti nell'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![Ricerche salvate dall'organizzazione](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="7d44a-143">Risorse di dati aggiunte</span><span class="sxs-lookup"><span data-stu-id="7d44a-143">Pinned data assets</span></span>
<span data-ttu-id="7d44a-144">Con le ricerche salvate, è possibile salvare e usare di nuovo le definizioni di ricerca.</span><span class="sxs-lookup"><span data-stu-id="7d44a-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="7d44a-145">Asset di dati Hello restituite da ricerche hello potrebbe cambiare nel tempo come contenuto di hello di modifica di catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="7d44a-146">Quando si aggiunge l'asset di dati, è possibile identificare in modo esplicito dati specifici asset toomake li tooaccess più semplice senza la necessità di toouse una ricerca.</span><span class="sxs-lookup"><span data-stu-id="7d44a-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="7d44a-147">L'aggiunta di un asset di dati è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="7d44a-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="7d44a-148">elenco di tooadd hello dati asset tooyour bloccato, sufficiente fare clic su hello **pin** icona.</span><span class="sxs-lookup"><span data-stu-id="7d44a-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="7d44a-149">icona Hello viene visualizzata nell'angolo hello di hello asset riquadro nella visualizzazione affiancata hello e nella colonna più a sinistra di hello nella visualizzazione elenco hello nel portale di Azure Data Catalog hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![icona della puntina Hello asset di dati](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="7d44a-151">Anche la rimozione di un asset di dati è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="7d44a-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="7d44a-152">Fare semplicemente clic hello **sbloccare** impostazione hello tootoggle di icona per la risorsa selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="7d44a-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![icona Sblocca asset di dati Hello](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="7d44a-154">Hello sezione risorse personali</span><span class="sxs-lookup"><span data-stu-id="7d44a-154">hello My Assets section</span></span>
<span data-ttu-id="7d44a-155">Hello catalogo dati home page del portale include un **asset My** sezione che visualizza l'attività dell'utente corrente toohello di interesse.</span><span class="sxs-lookup"><span data-stu-id="7d44a-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="7d44a-156">Questa sezione include sia le risorse aggiunte che le ricerche salvate.</span><span class="sxs-lookup"><span data-stu-id="7d44a-156">This section includes both pinned assets and saved searches.</span></span>

![sezione delle risorse personali nella home page di hello Hello](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="7d44a-158">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7d44a-158">Summary</span></span>
<span data-ttu-id="7d44a-159">Azure Data Catalog offre funzionalità che rendono più semplice toodiscover hello le origini dati che è necessario, pertanto tutti i membri dell'organizzazione possono ridurre il tempo per dati e più tempo di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="7d44a-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="7d44a-160">Le ricerche salvate e gli asset di dati aggiunti si basano su queste funzionalità di base, in modo che gli utenti possano identificare con facilità le origini dati con cui lavorano ripetutamente.</span><span class="sxs-lookup"><span data-stu-id="7d44a-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
