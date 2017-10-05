---
title: Gestire gli asset di dati in Azure Data Catalog | Microsoft Docs
description: "L'articolo illustra come controllare la visibilità e la proprietà degli asset di dati registrati in Azure Data Catalog."
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
ms.openlocfilehash: 8b9159b7bc4f7b2dac12d9012c6c903e75a6ac16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="6e219-103">Gestire gli asset di dati in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="6e219-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="6e219-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="6e219-104">Introduction</span></span>
<span data-ttu-id="6e219-105">Azure Data Catalog è progettato per l'individuazione delle origini dati, per poter comprendere e trovare facilmente le origini dati necessarie per eseguire analisi e prendere decisioni.</span><span class="sxs-lookup"><span data-stu-id="6e219-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span></span> <span data-ttu-id="6e219-106">Le funzionalità di individuazione fanno veramente la differenza quando tutti gli utenti hanno la possibilità di trovare e comprendere la più ampia gamma di origini dati disponibili.</span><span class="sxs-lookup"><span data-stu-id="6e219-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="6e219-107">Con questi elementi, il comportamento predefinito di Data Catalog prevede che tutte le origini dati registrate siano visibili e individuabili da tutti gli utenti del catalogo.</span><span class="sxs-lookup"><span data-stu-id="6e219-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span></span>

<span data-ttu-id="6e219-108">Data Catalog non consente di accedere ai dati stessi.</span><span class="sxs-lookup"><span data-stu-id="6e219-108">Data Catalog does not give you access to the data itself.</span></span> <span data-ttu-id="6e219-109">L'accesso ai dati è controllato dal proprietario dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="6e219-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="6e219-110">Data Catalog consente di trovare le origini dati e di visualizzare i metadati correlati alle origini registrate nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="6e219-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span></span>

<span data-ttu-id="6e219-111">In alcune situazioni tuttavia le origini dati devono essere visibili solo a utenti specifici o ai membri di gruppi specifici.</span><span class="sxs-lookup"><span data-stu-id="6e219-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="6e219-112">In tali scenari gli utenti possono acquisire la proprietà di asset di dati registrati nel catalogo e quindi di controllare la visibilità degli asset di cui sono proprietari.</span><span class="sxs-lookup"><span data-stu-id="6e219-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="6e219-113">Le funzionalità descritte in questo articolo sono disponibili solo nell'edizione Standard di Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="6e219-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="6e219-114">L'edizione gratuita non offre funzionalità relative alla proprietà e alla limitazione della visibilità di asset di dati.</span><span class="sxs-lookup"><span data-stu-id="6e219-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="6e219-115">Gestire la proprietà degli asset di dati</span><span class="sxs-lookup"><span data-stu-id="6e219-115">Manage ownership of data assets</span></span>
<span data-ttu-id="6e219-116">Per impostazione predefinita, gli asset di dati registrati in Data Catalog sono senza proprietario.</span><span class="sxs-lookup"><span data-stu-id="6e219-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="6e219-117">Qualsiasi utente con l'autorizzazione necessaria per accedere al catalogo può trovare e annotare questi asset.</span><span class="sxs-lookup"><span data-stu-id="6e219-117">Any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="6e219-118">Gli utenti possono acquisire la proprietà di asset di dati senza proprietario e quindi limitarne la visibilità.</span><span class="sxs-lookup"><span data-stu-id="6e219-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="6e219-119">Quando un asset di dati in Data Catalog ha dei proprietari, solo gli utenti autorizzati dai proprietari possono trovare l'asset e visualizzarne i metadati e solo i proprietari possono eliminare l'asset dal catalogo.</span><span class="sxs-lookup"><span data-stu-id="6e219-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="6e219-120">In Data Catalog la proprietà interessa unicamente i metadati archiviati nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="6e219-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span></span> <span data-ttu-id="6e219-121">La proprietà non conferisce autorizzazioni per l'origine dati sottostante.</span><span class="sxs-lookup"><span data-stu-id="6e219-121">Ownership does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="6e219-122">Diventare proprietario</span><span class="sxs-lookup"><span data-stu-id="6e219-122">Take ownership</span></span>
<span data-ttu-id="6e219-123">Per acquisire la proprietà di asset di dati, gli utenti possono selezionare l'opzione **Diventa proprietario** nel portale di Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="6e219-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span></span> <span data-ttu-id="6e219-124">Non sono necessarie speciali autorizzazioni per diventare proprietario di un asset di dati senza proprietario.</span><span class="sxs-lookup"><span data-stu-id="6e219-124">No special permissions are required to take ownership of an unowned data asset.</span></span> <span data-ttu-id="6e219-125">Qualsiasi utente può diventare proprietario di un asset di dati senza proprietario.</span><span class="sxs-lookup"><span data-stu-id="6e219-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="6e219-126">Aggiungere proprietari e comproprietari</span><span class="sxs-lookup"><span data-stu-id="6e219-126">Add owners and co-owners</span></span>
<span data-ttu-id="6e219-127">Se un asset di dati ha già un proprietario, gli altri utenti non possono semplicemente diventare proprietari.</span><span class="sxs-lookup"><span data-stu-id="6e219-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="6e219-128">Devono essere aggiunti come comproprietari da un proprietario esistente.</span><span class="sxs-lookup"><span data-stu-id="6e219-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="6e219-129">Qualsiasi proprietario può aggiungere altri utenti o gruppi di sicurezza come comproprietari.</span><span class="sxs-lookup"><span data-stu-id="6e219-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="6e219-130">È consigliabile che ogni asset di dati con proprietari abbia almeno due proprietari.</span><span class="sxs-lookup"><span data-stu-id="6e219-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="6e219-131">Rimuovere i proprietari</span><span class="sxs-lookup"><span data-stu-id="6e219-131">Remove owners</span></span>
<span data-ttu-id="6e219-132">Qualsiasi proprietario di asset può rimuovere i relativi comproprietari.</span><span class="sxs-lookup"><span data-stu-id="6e219-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="6e219-133">Un proprietario di un asset che rimuove se stesso come proprietario, non potrà più gestire l'asset.</span><span class="sxs-lookup"><span data-stu-id="6e219-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span></span> <span data-ttu-id="6e219-134">Se il proprietario di un asset rimuove se stesso come proprietario e non esistono altri comproprietari, l'asset torna allo stato senza proprietario.</span><span class="sxs-lookup"><span data-stu-id="6e219-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="6e219-135">Controllare la visibilità</span><span class="sxs-lookup"><span data-stu-id="6e219-135">Control visibility</span></span>
<span data-ttu-id="6e219-136">La visibilità degli asset di dati è controllata dai relativi proprietari.</span><span class="sxs-lookup"><span data-stu-id="6e219-136">Data-asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="6e219-137">Per limitare la visibilità come impostazione predefinita, in cui tutti gli utenti di Data Catalog possono trovare e visualizzare l'asset di dati, il proprietario dell'asset può alternare l'impostazione di visibilità tra **Tutti** e **Proprietario e questi utenti** nelle proprietà dell'asset.</span><span class="sxs-lookup"><span data-stu-id="6e219-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span></span> <span data-ttu-id="6e219-138">I proprietari possono quindi aggiungere utenti e gruppi di sicurezza specifici.</span><span class="sxs-lookup"><span data-stu-id="6e219-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="6e219-139">Quando è possibile, la proprietà dell'asset e le autorizzazioni di visibilità devono essere assegnate a gruppi di sicurezza e non a singoli utenti.</span><span class="sxs-lookup"><span data-stu-id="6e219-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="6e219-140">Amministratori del catalogo</span><span class="sxs-lookup"><span data-stu-id="6e219-140">Catalog administrators</span></span>
<span data-ttu-id="6e219-141">Gli amministratori di Data Catalog sono implicitamente comproprietari di tutti gli asset nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="6e219-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span></span> <span data-ttu-id="6e219-142">I proprietari di asset non possono rimuovere la visibilità dagli amministratori, che possono gestire la proprietà e la visibilità per tutti gli asset di dati nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="6e219-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="6e219-143">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="6e219-143">Summary</span></span>
<span data-ttu-id="6e219-144">Il modello di crowdsourcing di Data Catalog per l'individuazione di asset di dati e metadati consente a tutti gli utenti del catalogo di contribuire all'individuazione.</span><span class="sxs-lookup"><span data-stu-id="6e219-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span></span> <span data-ttu-id="6e219-145">L'edizione Standard di Data Catalog è progettata per la proprietà e la gestione per poter limitare la visibilità e l'uso di asset di dati specifici.</span><span class="sxs-lookup"><span data-stu-id="6e219-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span></span>
