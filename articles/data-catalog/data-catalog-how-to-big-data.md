---
title: Come usare le origini dati di tipo "Big Data" | Documentazione Microsoft
description: Articolo di procedure che descrive gli schemi per usare Azure Data Catalog con origini dati di tipo Big Data, incluso l'archiviazione BLOB di Azure, Azure Data Lake e HDFS di Hadoop.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 001d80ce42f0e87276e59d70dffb75eb561d96cd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-work-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="b178c-103">Come utilizzare origini dati di tipo Big Data nel Catalogo dati di Azure</span><span class="sxs-lookup"><span data-stu-id="b178c-103">How to work with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="b178c-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="b178c-104">Introduction</span></span>
<span data-ttu-id="b178c-105">**Catalogo dati di Microsoft Azure** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali.</span><span class="sxs-lookup"><span data-stu-id="b178c-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="b178c-106">Permette agli utenti di trovare, comprendere e usare le origini dati e consente alle organizzazioni di ottenere maggior valore dalle origini dati esistenti, inclusi i Big Data.</span><span class="sxs-lookup"><span data-stu-id="b178c-106">It is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="b178c-107">**Catalogo dati di Azure** supporta la registrazione di BLOB e directory di Archiviazione BLOB di Azure, nonché file e directory HDFS di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b178c-107">**Azure Data Catalog** supports the registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="b178c-108">La natura semistrutturata di questi dati offre una grande flessibilità.</span><span class="sxs-lookup"><span data-stu-id="b178c-108">The semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="b178c-109">Per ottenere il massimo del valore dalla registrazione con **Azure Data Catalog**, gli utenti devono tuttavia considerare come sono organizzate le origini dati.</span><span class="sxs-lookup"><span data-stu-id="b178c-109">However, to get the most value from registering them with **Azure Data Catalog**, users must consider how the data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="b178c-110">Directory come set di dati logici</span><span class="sxs-lookup"><span data-stu-id="b178c-110">Directories as logical data sets</span></span>
<span data-ttu-id="b178c-111">Un modello comune per l'organizzazione delle origini dati di tipo Big Data consiste nel considerare le directory come set di dati logici.</span><span class="sxs-lookup"><span data-stu-id="b178c-111">A common pattern for organizing big data sources is to treat directories as logical data sets.</span></span> <span data-ttu-id="b178c-112">Le directory di primo livello vengono usate per definire un set di dati, mentre le sottocartelle definiscono le partizioni e i file che contengono archiviano i dati stessi.</span><span class="sxs-lookup"><span data-stu-id="b178c-112">Top-level directories are used to define a data set, while subfolders define partitions, and the files they contain store the data itself.</span></span>

<span data-ttu-id="b178c-113">Ecco un esempio di questo schema:</span><span class="sxs-lookup"><span data-stu-id="b178c-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="b178c-114">In questo esempio vehicle_maintenance_events e location_tracking_events rappresentano i set di dati logici.</span><span class="sxs-lookup"><span data-stu-id="b178c-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="b178c-115">Ognuna di queste cartelle contiene file di dati organizzati in sottocartelle per anno e mese.</span><span class="sxs-lookup"><span data-stu-id="b178c-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="b178c-116">Ogni cartella potrebbe contenere centinaia o migliaia di file.</span><span class="sxs-lookup"><span data-stu-id="b178c-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="b178c-117">In questo schema la registrazione di singoli file con **Catalogo dati di Azure** probabilmente non ha senso.</span><span class="sxs-lookup"><span data-stu-id="b178c-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="b178c-118">Registrare invece le directory che rappresentano i set di dati che sono significativi per gli utenti che utilizzano i dati.</span><span class="sxs-lookup"><span data-stu-id="b178c-118">Instead, register the directories that represent the data sets that be meaningful to the users working with the data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="b178c-119">File di dati di riferimento</span><span class="sxs-lookup"><span data-stu-id="b178c-119">Reference data files</span></span>
<span data-ttu-id="b178c-120">Uno schema complementare consiste nell'archiviare i set di dati di riferimento come singoli file.</span><span class="sxs-lookup"><span data-stu-id="b178c-120">A complementary pattern is to store reference data sets as individual files.</span></span> <span data-ttu-id="b178c-121">Questi set di dati possono essere considerati come il lato "piccolo" dei Big Data e spesso sono simili alle dimensioni in un modello di dati analitici.</span><span class="sxs-lookup"><span data-stu-id="b178c-121">These data sets may be thought of as the 'small' side of big data, and are often similar to dimensions in an analytical data model.</span></span> <span data-ttu-id="b178c-122">I file di dati di riferimento contengono record usati per fornire il contesto per la maggior parte dei file di dati archiviati altrove nell'archivio di Big Data.</span><span class="sxs-lookup"><span data-stu-id="b178c-122">Reference data files contain records that are used to provide context for the bulk of the data files stored elsewhere in the big data store.</span></span>

<span data-ttu-id="b178c-123">Ecco un esempio di questo schema:</span><span class="sxs-lookup"><span data-stu-id="b178c-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="b178c-124">Quando un analista o un data scientist utilizza i dati contenuti nelle strutture di directory più grandi, i dati in questi file di riferimento possono essere usati per fornire informazioni più dettagliate per le entità a cui viene fatto riferimento solo per nome o ID nel set di dati più grande.</span><span class="sxs-lookup"><span data-stu-id="b178c-124">When an analyst or data scientist is working with the data contained in the larger directory structures, the data in these reference files can be used to provide more detailed information for entities that are referred to only by name or ID in the larger data set.</span></span>

<span data-ttu-id="b178c-125">In questo schema può essere utile registrare i singoli file di dati di riferimento con **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="b178c-125">In this pattern, it makes sense to register the individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="b178c-126">Ogni file rappresenta un set di dati e ognuno può essere annotato ed individuato singolarmente.</span><span class="sxs-lookup"><span data-stu-id="b178c-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="b178c-127">Schemi alternativi</span><span class="sxs-lookup"><span data-stu-id="b178c-127">Alternate patterns</span></span>
<span data-ttu-id="b178c-128">Gli schemi descritti nella sezione precedente sono solo due possibili modalità di organizzazione di un archivio di Big Data, ma ogni implementazione è diversa.</span><span class="sxs-lookup"><span data-stu-id="b178c-128">The patterns described in the preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="b178c-129">Indipendentemente da come sono strutturate le origini dati, quando si registrano origini dati di tipo Big Data con **Azure Data Catalog**, concentrarsi sulla registrazione di file e directory che rappresentano i set di dati importanti per altri utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b178c-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering the files and directories that represent the data sets that are of value to others within your organization.</span></span> <span data-ttu-id="b178c-130">La registrazione di tutti i file e tutte le directory può creare confusione nel catalogo, rendendo più difficile per gli utenti trovare le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="b178c-130">Registering all files and directories can clutter the catalog, making it harder for users to find what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="b178c-131">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b178c-131">Summary</span></span>
<span data-ttu-id="b178c-132">La registrazione di origini dati con il **Catalogo dati di Azure** ne rende più semplice l'individuazione e la comprensione.</span><span class="sxs-lookup"><span data-stu-id="b178c-132">Registering data sources with **Azure Data Catalog** makes them easier to discover and understand.</span></span> <span data-ttu-id="b178c-133">La registrazione e l'annotazione dei file e delle directory di Big Data che rappresentano set di dati logici permettono agli utenti di trovare e usare le origini dati di tipo Big Data necessarie.</span><span class="sxs-lookup"><span data-stu-id="b178c-133">By registering and annotating the big data files and directories that represent logical data sets, you can help users find and use the big data sources they need.</span></span>
