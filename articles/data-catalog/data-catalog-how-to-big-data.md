---
title: toowork aaaHow con origini dati 'big data' | Documenti Microsoft
description: Modelli di evidenziazione come tooarticle per l'utilizzo di Azure Data Catalog con origini di dati 'big data', inclusi archiviazione Blob di Azure, Azure Data Lake e Hadoop HDFS.
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
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="c4239-103">Come origini di toowork dati di grandi dimensioni in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="c4239-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="c4239-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="c4239-104">Introduction</span></span>
<span data-ttu-id="c4239-105">**Microsoft Azure Data Catalog** è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per origini dati aziendali.</span><span class="sxs-lookup"><span data-stu-id="c4239-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="c4239-106">Si tratta di consentendo alle persone di individuare, comprendere e utilizzare origini dati e il supporto di maggior valore organizzazioni tooget dalle origini dati esistenti, inclusi i dati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="c4239-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="c4239-107">**Azure Data Catalog** supporta hello registrazione del BLOB di archiviazione BLOB di Azure e le directory, nonché i file HDFS Hadoop e directory.</span><span class="sxs-lookup"><span data-stu-id="c4239-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="c4239-108">Hello semistrutturati natura queste origini dati offre una notevole flessibilità.</span><span class="sxs-lookup"><span data-stu-id="c4239-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="c4239-109">Tuttavia, tooget hello maggior valore tramite la registrazione con **Azure Data Catalog**, gli utenti devono considerare l'organizzazione delle origini dati hello.</span><span class="sxs-lookup"><span data-stu-id="c4239-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="c4239-110">Directory come set di dati logici</span><span class="sxs-lookup"><span data-stu-id="c4239-110">Directories as logical data sets</span></span>
<span data-ttu-id="c4239-111">Un modello comune per organizzare le origini dati di grandi dimensioni è tootreat directory come set di dati logico.</span><span class="sxs-lookup"><span data-stu-id="c4239-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="c4239-112">Directory di primo livello sono toodefine utilizzato un set di dati, mentre le sottocartelle di definire le partizioni e hello che contengono dell'archivio dati hello stessi.</span><span class="sxs-lookup"><span data-stu-id="c4239-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="c4239-113">Ecco un esempio di questo schema:</span><span class="sxs-lookup"><span data-stu-id="c4239-113">An example of this pattern might be:</span></span>

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

<span data-ttu-id="c4239-114">In questo esempio vehicle_maintenance_events e location_tracking_events rappresentano i set di dati logici.</span><span class="sxs-lookup"><span data-stu-id="c4239-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="c4239-115">Ognuna di queste cartelle contiene file di dati organizzati in sottocartelle per anno e mese.</span><span class="sxs-lookup"><span data-stu-id="c4239-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="c4239-116">Ogni cartella potrebbe contenere centinaia o migliaia di file.</span><span class="sxs-lookup"><span data-stu-id="c4239-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="c4239-117">In questo schema la registrazione di singoli file con **Catalogo dati di Azure** probabilmente non ha senso.</span><span class="sxs-lookup"><span data-stu-id="c4239-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="c4239-118">In alternativa, registrare directory hello che rappresentano i set di dati di hello essere significativi toohello agli utenti che lavorano con dati hello.</span><span class="sxs-lookup"><span data-stu-id="c4239-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="c4239-119">File di dati di riferimento</span><span class="sxs-lookup"><span data-stu-id="c4239-119">Reference data files</span></span>
<span data-ttu-id="c4239-120">Un modello complementare è toostore set di dati di riferimento come singoli file.</span><span class="sxs-lookup"><span data-stu-id="c4239-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="c4239-121">Questi set di dati può essere considerati come sul lato 'small' hello dei big data e sono spesso toodimensions simili in un modello di dati analitici.</span><span class="sxs-lookup"><span data-stu-id="c4239-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="c4239-122">File di dati di riferimento contengono record di contesto utilizzate tooprovide per bulk hello hello dei file di dati archiviati in un' posizione nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="c4239-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="c4239-123">Ecco un esempio di questo schema:</span><span class="sxs-lookup"><span data-stu-id="c4239-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="c4239-124">Quando un esperto di analista o dati funziona con dati hello contenuti in strutture di directory di dimensioni maggiori hello, dati hello in questi file di riferimento possono essere utilizzato tooprovide informazioni più dettagliate per le entità che sono definita tooonly per nome o ID in dati di dimensioni maggiori di hello set.</span><span class="sxs-lookup"><span data-stu-id="c4239-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="c4239-125">In questo modello, è consigliabile memorizzarlo file di dati di riferimento individuale tooregister hello con **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="c4239-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="c4239-126">Ogni file rappresenta un set di dati e ognuno può essere annotato ed individuato singolarmente.</span><span class="sxs-lookup"><span data-stu-id="c4239-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="c4239-127">Schemi alternativi</span><span class="sxs-lookup"><span data-stu-id="c4239-127">Alternate patterns</span></span>
<span data-ttu-id="c4239-128">modelli descritti nella precedente sezione hello Hello sono solo due possibili modalità che può essere organizzato in un archivio dati di grandi dimensioni, ma ogni implementazione è diverso.</span><span class="sxs-lookup"><span data-stu-id="c4239-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="c4239-129">Indipendentemente dalla modalità le origini dati sono strutturate, durante la registrazione delle origini dati di grandi dimensioni con **Azure Data Catalog**, lo stato attivo sulla registrazione hello file e directory che rappresentano i set di dati hello di tooothers valore all'interno del organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c4239-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="c4239-130">Registrazione di tutti i file e directory possono creare confusione catalogo hello, rendendone più difficile per gli utenti toofind hanno bisogno.</span><span class="sxs-lookup"><span data-stu-id="c4239-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="c4239-131">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="c4239-131">Summary</span></span>
<span data-ttu-id="c4239-132">La registrazione delle origini dati con **Azure Data Catalog** rende più semplice toodiscover e comprendere.</span><span class="sxs-lookup"><span data-stu-id="c4239-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="c4239-133">Registrando e annotazione hello dati file e directory che rappresentano il set di dati logico, si consente agli utenti di trovare e utilizzare origini dati hello che hanno bisogno.</span><span class="sxs-lookup"><span data-stu-id="c4239-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
