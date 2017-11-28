---
title: Panoramica di gestione di dati di Azure StorSimple aaaMicrosoft | Documenti Microsoft
description: Viene fornita una panoramica di hello servizio StorSimple Manager di dati (anteprima privata)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="c9777-103">Panoramica di StorSimple Data Manager (anteprima privata)</span><span class="sxs-lookup"><span data-stu-id="c9777-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="c9777-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c9777-104">Overview</span></span>

<span data-ttu-id="c9777-105">Microsoft Azure StorSimple è una soluzione di archiviazione cloud ibrida che indirizzi hello complessità dei dati non strutturati generalmente associati a condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="c9777-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="c9777-106">StorSimple utilizza l'archiviazione cloud come soluzione locale di un'estensione di hello e livelli automaticamente i dati tra l'archiviazione locale hello e archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="c9777-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="c9777-107">Integrati, protezione dei dati locali e gli snapshot nel cloud, evitando hello un'infrastruttura di archiviazione ha.</span><span class="sxs-lookup"><span data-stu-id="c9777-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="c9777-108">Archiviazione e ripristino di emergenza è trasparente anche con cloud hello funge da una posizione esterna.</span><span class="sxs-lookup"><span data-stu-id="c9777-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="c9777-109">servizio di trasformazione di dati Hello Microsoft sta introducendo in questo documento consente si tooseamlessly accesso hello StorSimple dati nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="c9777-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="c9777-110">Questo servizio fornisce i dati di tooextract API da StorSimple e presentarli tooother Azure servizi nei formati che possono essere utilizzati facilmente.</span><span class="sxs-lookup"><span data-stu-id="c9777-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="c9777-111">formati di Hello è supportati in questa versione di anteprima sono BLOB di Azure e gli asset di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9777-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="c9777-112">Questa trasformazione consente si tooeasily collegare i servizi, ad esempio servizi multimediali di Azure, HDInsight di Azure, Azure Machine Learning e ricerca di Azure dati toooperate nel dispositivo StorSimple serie 8000 locale.</span><span class="sxs-lookup"><span data-stu-id="c9777-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="c9777-113">Di seguito viene presentato un diagramma a blocchi di alto livello illustrativo.</span><span class="sxs-lookup"><span data-stu-id="c9777-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagramma di alto livello](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="c9777-115">Nel documento viene spiegato come iscriversi per un'anteprima privata di questo servizio.</span><span class="sxs-lookup"><span data-stu-id="c9777-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="c9777-116">Viene inoltre illustrato come utilizzare questa applicazione di servizio toowrite che utilizzano dati di StorSimple e altri servizi di Azure nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="c9777-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="c9777-117">Eseguire l'iscrizione per l'anteprima di Data Manager</span><span class="sxs-lookup"><span data-stu-id="c9777-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="c9777-118">Prima di iscriversi per il servizio di gestione dati hello, esaminare hello seguenti prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="c9777-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c9777-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c9777-119">Prerequisites</span></span>

<span data-ttu-id="c9777-120">Questo esercizio presuppone che l'utente abbia</span><span class="sxs-lookup"><span data-stu-id="c9777-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="c9777-121">una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="c9777-121">an active Azure subscription.</span></span>
* <span data-ttu-id="c9777-122">accesso tooa registrazione dispositivo di StorSimple 8000 series</span><span class="sxs-lookup"><span data-stu-id="c9777-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="c9777-123">tutti hello chiavi associate ai dispositivi serie StorSimple 8000 hello.</span><span class="sxs-lookup"><span data-stu-id="c9777-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="c9777-124">Iscrizione</span><span class="sxs-lookup"><span data-stu-id="c9777-124">Sign up</span></span>

<span data-ttu-id="c9777-125">Hello StorSimple Data Manager è in anteprima privata.</span><span class="sxs-lookup"><span data-stu-id="c9777-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="c9777-126">Eseguire hello toosign passaggi per l'anteprima privata di questo servizio seguente:</span><span class="sxs-lookup"><span data-stu-id="c9777-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="c9777-127">Accedere a hello portale di Azure con estensione della gestione di dati di StorSimple hello in: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="c9777-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="c9777-128">Utilizzare toolog le credenziali di Azure in.</span><span class="sxs-lookup"><span data-stu-id="c9777-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="c9777-129">Fare clic su hello  **+**  toocreate icona un servizio.</span><span class="sxs-lookup"><span data-stu-id="c9777-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="c9777-130">Fare clic su **archiviazione** e quindi fare clic su **vedere tutti** nel pannello hello visualizzata.</span><span class="sxs-lookup"><span data-stu-id="c9777-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Ricerca dell'icona di StorSimple Data Manager](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="c9777-132">Viene visualizzata l'icona di gestione di dati di StorSimple di hello.</span><span class="sxs-lookup"><span data-stu-id="c9777-132">You see hello StorSimple Data Manager icon.</span></span>

    ![Selezione dell'icona di StorSimple Data Manager](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="c9777-134">Fare clic sull'icona di StorSimple Data Manager, quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c9777-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="c9777-135">Selezionare una sottoscrizione di hello che desidera tooenable per l'anteprima privata hello e quindi fare clic su **iscriversi me!**</span><span class="sxs-lookup"><span data-stu-id="c9777-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Esegui iscrizione](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="c9777-137">Consente di inviare una richiesta tooonboard è.</span><span class="sxs-lookup"><span data-stu-id="c9777-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="c9777-138">che verrà gestita non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="c9777-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="c9777-139">Dopo l'abilitazione della sottoscrizione, sarà possibile creare un servizio StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="c9777-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="c9777-140">tooeasily accedere servizio StorSimple Manager dati hello, fare clic su toopin icona a stella hello è tooyour Preferiti.</span><span class="sxs-lookup"><span data-stu-id="c9777-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Accesso a StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="c9777-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9777-142">Next steps</span></span>

<span data-ttu-id="c9777-143">[Utilizzare i dati di interfaccia utente di gestione dati di StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="c9777-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
