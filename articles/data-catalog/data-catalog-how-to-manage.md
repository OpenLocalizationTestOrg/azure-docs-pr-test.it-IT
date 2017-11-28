---
title: aaaManage asset di dati in Azure Data Catalog | Documenti Microsoft
description: "articolo Hello evidenzia come toocontrol visibilità e la proprietà di asset di dati registrata in Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="00eb3-103">Gestire gli asset di dati in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="00eb3-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="00eb3-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="00eb3-104">Introduction</span></span>
<span data-ttu-id="00eb3-105">Azure Data Catalog è progettato per l'individuazione dell'origine dati, in modo che è possibile individuare facilmente e comprendere le origini dati hello è necessario analysis tooperform e prendere decisioni.</span><span class="sxs-lookup"><span data-stu-id="00eb3-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="00eb3-106">Queste funzionalità di individuazione verificare l'impatto maggiore sul hello quando gli utenti di trovare e comprendere più ampia gamma di hello delle origini dati disponibili.</span><span class="sxs-lookup"><span data-stu-id="00eb3-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="00eb3-107">Con questi elementi presenti, il comportamento predefinito hello del catalogo dati è per tutti i dati registrati origini toobe visibile tooand individuabili tutti gli utenti del catalogo.</span><span class="sxs-lookup"><span data-stu-id="00eb3-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="00eb3-108">Catalogo dati non consentono di accedere ai dati toohello stesso.</span><span class="sxs-lookup"><span data-stu-id="00eb3-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="00eb3-109">Accesso ai dati è controllato dal proprietario hello dell'origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="00eb3-110">Con il catalogo dati, è possibile individuare le origini dati e visualizzare i metadati hello origini toohello correlati che vengono registrate nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="00eb3-111">Potrebbero esserci delle situazioni, tuttavia, in cui devono essere solo origini dati utenti toospecific visibili, o toomembers di gruppi specifici.</span><span class="sxs-lookup"><span data-stu-id="00eb3-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="00eb3-112">In questi scenari, gli utenti possono diventare proprietari di asset di dati registrati all'interno del catalogo hello e quindi controllare la visibilità di hello degli asset hello che sono proprietari.</span><span class="sxs-lookup"><span data-stu-id="00eb3-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="00eb3-113">funzionalità di Hello descritto in questo articolo è disponibile solo nell'edizione Standard di Azure Data Catalog hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="00eb3-114">Hello edizione gratuita non fornisce funzionalità per la proprietà e per limitare la visibilità di asset di dati.</span><span class="sxs-lookup"><span data-stu-id="00eb3-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="00eb3-115">Gestire la proprietà degli asset di dati</span><span class="sxs-lookup"><span data-stu-id="00eb3-115">Manage ownership of data assets</span></span>
<span data-ttu-id="00eb3-116">Per impostazione predefinita, gli asset di dati registrati in Data Catalog sono senza proprietario.</span><span class="sxs-lookup"><span data-stu-id="00eb3-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="00eb3-117">Qualsiasi utente con il catalogo di hello tooaccess di autorizzazione può individuare e annotare queste risorse.</span><span class="sxs-lookup"><span data-stu-id="00eb3-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="00eb3-118">Gli utenti possono diventare proprietari di asset di dati senza proprietario e quindi limitare la visibilità di hello degli asset hello che sono proprietari.</span><span class="sxs-lookup"><span data-stu-id="00eb3-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="00eb3-119">Quando un asset di dati nel catalogo dati è di proprietà, solo gli utenti autorizzati dai proprietari hello possono individuare asset hello e visualizzarne i metadati e solo i proprietari di hello possono eliminare asset hello dal catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="00eb3-120">Proprietà nel catalogo dati interessa solo i metadati di hello archiviati nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="00eb3-121">La proprietà non conferisce tutte le autorizzazioni per l'origine dati sottostante hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="00eb3-122">Diventare proprietario</span><span class="sxs-lookup"><span data-stu-id="00eb3-122">Take ownership</span></span>
<span data-ttu-id="00eb3-123">Gli utenti possono diventare proprietari di asset di dati selezionando hello **Take Ownership** opzione nel portale di hello catalogo dati.</span><span class="sxs-lookup"><span data-stu-id="00eb3-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="00eb3-124">Autorizzazioni speciali non sono necessari tootake proprietà di un asset di dati senza proprietario.</span><span class="sxs-lookup"><span data-stu-id="00eb3-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="00eb3-125">Qualsiasi utente può diventare proprietario di un asset di dati senza proprietario.</span><span class="sxs-lookup"><span data-stu-id="00eb3-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="00eb3-126">Aggiungere proprietari e comproprietari</span><span class="sxs-lookup"><span data-stu-id="00eb3-126">Add owners and co-owners</span></span>
<span data-ttu-id="00eb3-127">Se un asset di dati ha già un proprietario, gli altri utenti non possono semplicemente diventare proprietari.</span><span class="sxs-lookup"><span data-stu-id="00eb3-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="00eb3-128">Devono essere aggiunti come comproprietari da un proprietario esistente.</span><span class="sxs-lookup"><span data-stu-id="00eb3-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="00eb3-129">Qualsiasi proprietario può aggiungere altri utenti o gruppi di sicurezza come comproprietari.</span><span class="sxs-lookup"><span data-stu-id="00eb3-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="00eb3-130">Si è un migliore toohave practice almeno due utenti come proprietari per qualsiasi proprietà dell'asset di dati.</span><span class="sxs-lookup"><span data-stu-id="00eb3-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="00eb3-131">Rimuovere i proprietari</span><span class="sxs-lookup"><span data-stu-id="00eb3-131">Remove owners</span></span>
<span data-ttu-id="00eb3-132">Qualsiasi proprietario di asset può rimuovere i relativi comproprietari.</span><span class="sxs-lookup"><span data-stu-id="00eb3-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="00eb3-133">Un proprietario asset rimuove aggiungersi come proprietario non è più possibile gestire asset hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="00eb3-134">Se esistono altri CO-proprietari proprietario dell'asset hello rimuove aggiungersi come proprietario, asset hello Ripristina tooan senza proprietario dello stato.</span><span class="sxs-lookup"><span data-stu-id="00eb3-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="00eb3-135">Controllare la visibilità</span><span class="sxs-lookup"><span data-stu-id="00eb3-135">Control visibility</span></span>
<span data-ttu-id="00eb3-136">Proprietari di asset di dati è possono controllare la visibilità di hello degli asset di dati hello che sono proprietari.</span><span class="sxs-lookup"><span data-stu-id="00eb3-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="00eb3-137">visibilità toorestrict come valore predefinito di hello, in cui tutti i Data Catalog, gli utenti possono individuare e visualizzare hello asset di dati, proprietario dell'asset hello può attivare o hello visibilità impostazione **Everyone** troppo**proprietari e utenti** nelle proprietà hello asset hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="00eb3-138">I proprietari possono quindi aggiungere utenti e gruppi di sicurezza specifici.</span><span class="sxs-lookup"><span data-stu-id="00eb3-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="00eb3-139">Quando possibile, devono essere assegnate le autorizzazioni di proprietà e la visibilità di asset, toosecurity gruppi e non agli utenti di tooindividual.</span><span class="sxs-lookup"><span data-stu-id="00eb3-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="00eb3-140">Amministratori del catalogo</span><span class="sxs-lookup"><span data-stu-id="00eb3-140">Catalog administrators</span></span>
<span data-ttu-id="00eb3-141">Gli amministratori del catalogo dati sono implicitamente comproprietari di tutte le risorse nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="00eb3-142">Proprietari della risorsa non è possibile rimuovere la visibilità da parte degli amministratori e gli amministratori possono gestire proprietà e la visibilità per tutti gli asset di dati nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="00eb3-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="00eb3-143">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="00eb3-143">Summary</span></span>
<span data-ttu-id="00eb3-144">Hello catalogo dati crowdsourcing modello toometadata e dati di individuazione consente a tutti i toocontribute gli utenti del catalogo e individuare.</span><span class="sxs-lookup"><span data-stu-id="00eb3-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="00eb3-145">Hello edizione Standard di catalogo dati è progettato per la gestione e la proprietà visibilità hello toolimit e l'uso di asset di dati specifico.</span><span class="sxs-lookup"><span data-stu-id="00eb3-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>
