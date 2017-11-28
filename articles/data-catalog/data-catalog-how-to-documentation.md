---
title: Come documentare le origini dati | Documentazione Microsoft
description: Articolo sulle procedure che illustra come documentare gli asset di dati in Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="660b4-103">Documentare le origini dati</span><span class="sxs-lookup"><span data-stu-id="660b4-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="660b4-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="660b4-104">Introduction</span></span>
<span data-ttu-id="660b4-105">**Microsoft Azure Data Catalog** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali.</span><span class="sxs-lookup"><span data-stu-id="660b4-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="660b4-106">In altre parole, **Azure Data Catalog** permette agli utenti di trovare, *comprendere*e usare le origini dati e consente alle organizzazioni di ottenere maggior valore dai dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="660b4-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="660b4-107">Quando un'origine dati viene registrata con **Azure Data Catalog**, i relativi metadati vengono copiati e indicizzati dal servizio, ma non è tutto.</span><span class="sxs-lookup"><span data-stu-id="660b4-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="660b4-108">**Azure Data Catalog** consente agli utenti di fornire una documentazione completa per descrivere l'utilizzo e scenari comuni per l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="660b4-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="660b4-109">L'articolo [Come annotare le origini dati](data-catalog-how-to-annotate.md)mostra come gli esperti che conoscono l'origine dati possono annotarla con tag e descrizioni.</span><span class="sxs-lookup"><span data-stu-id="660b4-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="660b4-110">Il portale di **Azure Data Catalog** include un editor di testo RTF per permettere agli utenti di documentare in modo esauriente gli asset di dati e i contenitori.</span><span class="sxs-lookup"><span data-stu-id="660b4-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="660b4-111">L'editor include la formattazione paragrafo, con intestazioni, formattazione del testo, elenchi puntati, elenchi numerati e tabelle.</span><span class="sxs-lookup"><span data-stu-id="660b4-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="660b4-112">Tag e descrizioni sono utili per inserire semplici annotazioni.</span><span class="sxs-lookup"><span data-stu-id="660b4-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="660b4-113">Tuttavia, per avere una migliore comprensione di un'origine dati e dei relativi scenari di business gli utilizzatori di dati possono rivolgersi a un esperto per una documentazione completa e dettagliata.</span><span class="sxs-lookup"><span data-stu-id="660b4-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="660b4-114">È facile documentare un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="660b4-114">It's easy to document a data source.</span></span> <span data-ttu-id="660b4-115">Selezionare un contenitore o un asset di dati e scegliere **Documentazione**.</span><span class="sxs-lookup"><span data-stu-id="660b4-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="660b4-116">Documentare gli asset di dati</span><span class="sxs-lookup"><span data-stu-id="660b4-116">Documenting data assets</span></span>
<span data-ttu-id="660b4-117">La documentazione permette di usare **Azure Data Catalog** come un repository per creare un resoconto completo degli asset di dati.</span><span class="sxs-lookup"><span data-stu-id="660b4-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="660b4-118">È possibile esplorare contenuti dettagliati che descrivono i contenitori e le tabelle.</span><span class="sxs-lookup"><span data-stu-id="660b4-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="660b4-119">Se sono già presenti contenuti in un altro repository, ad esempio SharePoint o una condivisione file, è possibile aggiungere alla documentazione degli asset collegamenti che fanno riferimento al contenuto esistente.</span><span class="sxs-lookup"><span data-stu-id="660b4-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="660b4-120">Questa funzione rende i documenti esistenti più facilmente individuabili.</span><span class="sxs-lookup"><span data-stu-id="660b4-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="660b4-121">La documentazione non è inclusa nell'indice di ricerca.</span><span class="sxs-lookup"><span data-stu-id="660b4-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="660b4-122">Il livello di documentazione va dalla descrizione delle caratteristiche e del valore di un contenitore di asset di dati alla descrizione dettagliata dello schema di tabella all'interno di un contenitore.</span><span class="sxs-lookup"><span data-stu-id="660b4-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="660b4-123">Il livello di documentazione fornito deve essere proporzionato alle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="660b4-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="660b4-124">In linea generale, ecco alcuni vantaggi e svantaggi legati alla documentazione degli asset di dati:</span><span class="sxs-lookup"><span data-stu-id="660b4-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="660b4-125">Documentare solo un contenitore: tutto il contenuto è in un'unica posizione, ma potrebbe non fornire agli utenti tutti i dettagli necessari per prendere decisioni basate su informazioni aggiornate.</span><span class="sxs-lookup"><span data-stu-id="660b4-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="660b4-126">Documentare solo le tabelle: il contenuto è specifico dell'oggetto, ma i documenti degli utenti non si trovano in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="660b4-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="660b4-127">Documentare contenitori e tabelle: è l'approccio più completo, ma potrebbe richiedere una maggiore manutenzione dei documenti.</span><span class="sxs-lookup"><span data-stu-id="660b4-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="660b4-128">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="660b4-128">Summary</span></span>
<span data-ttu-id="660b4-129">La documentazione delle origini dati con **Azure Data Catalog** permette di creare un resoconto sugli asset di dati con un livello di dettaglio basato sulle esigenze.</span><span class="sxs-lookup"><span data-stu-id="660b4-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="660b4-130">È possibile creare collegamenti a contenuti archiviati in un repository esistente che riunisce i documenti e gli asset di dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="660b4-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="660b4-131">Dopo aver trovato gli asset di dati appropriati, gli utenti hanno a disposizione un set di documentazione completo.</span><span class="sxs-lookup"><span data-stu-id="660b4-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
