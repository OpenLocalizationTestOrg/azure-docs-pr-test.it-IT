---
title: Panoramica di Microsoft Azure StorSimple Data Manager | Documentazione Microsoft
description: L'articolo fornisce una panoramica del servizio StorSimple Data Manager (anteprima privata)
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
ms.openlocfilehash: aedb44610fe57055851538b9dbdb810e66e58d73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="82492-103">Panoramica di StorSimple Data Manager (anteprima privata)</span><span class="sxs-lookup"><span data-stu-id="82492-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="82492-104">Overview</span><span class="sxs-lookup"><span data-stu-id="82492-104">Overview</span></span>

<span data-ttu-id="82492-105">Microsoft Azure StorSimple è una soluzione di archiviazione cloud ibrida che risolve le complessità dei dati non strutturati comunemente associate alle condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="82492-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses the complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="82492-106">StorSimple usa l'archiviazione cloud come un'estensione della soluzione locale e organizza automaticamente i dati in livelli tra archiviazione locale e archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="82492-106">StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="82492-107">La protezione integrata dei dati, con snapshot locali e cloud, elimina la necessità di un'infrastruttura di archiviazione complessa.</span><span class="sxs-lookup"><span data-stu-id="82492-107">Integrated data protection, with local and cloud snapshots, eliminates the need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="82492-108">L'archiviazione e il ripristino di emergenza sono inoltre perfettamente integrati con il cloud che funge da posizione esterna.</span><span class="sxs-lookup"><span data-stu-id="82492-108">Archival and disaster recovery is also seamless with the cloud acting as an offsite location.</span></span>

<span data-ttu-id="82492-109">Il servizio di trasformazione dati, illustrato nel presente documento, consente di accedere facilmente ai dati di StorSimple nel cloud.</span><span class="sxs-lookup"><span data-stu-id="82492-109">The data transformation service that we are introducing in this document, allows you to seamlessly access the StorSimple data in the cloud.</span></span> <span data-ttu-id="82492-110">Questo servizio fornisce API per estrarre dati da StorSimple e presentarli ad altri servizi di Azure in formati facilmente utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="82492-110">This service provides APIs to extract data from StorSimple and present it to other Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="82492-111">I formati supportati nell'anteprima sono BLOB di Azure e asset di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="82492-111">The formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="82492-112">Questa trasformazione consente di associare facilmente servizi quali Servizi multimediali di Azure, Azure HDInsight, Azure Machine Learning e Ricerca di Azure per l'uso dei dati sul dispositivo locale StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="82492-112">This transformation enables you to easily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search to operate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="82492-113">Di seguito viene presentato un diagramma a blocchi di alto livello illustrativo.</span><span class="sxs-lookup"><span data-stu-id="82492-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagramma di alto livello](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="82492-115">Nel documento viene spiegato come iscriversi per un'anteprima privata di questo servizio.</span><span class="sxs-lookup"><span data-stu-id="82492-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="82492-116">Viene inoltre descritto come usare il servizio per scrivere applicazioni che utilizzino dati di StorSimple e altri servizi di Azure nel cloud.</span><span class="sxs-lookup"><span data-stu-id="82492-116">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="82492-117">Eseguire l'iscrizione per l'anteprima di Data Manager</span><span class="sxs-lookup"><span data-stu-id="82492-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="82492-118">Prima di eseguire l'iscrizione per il servizio Data Manager, esaminare i prerequisiti seguenti.</span><span class="sxs-lookup"><span data-stu-id="82492-118">Before you sign up for the Data Manager service, review the following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="82492-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="82492-119">Prerequisites</span></span>

<span data-ttu-id="82492-120">Questo esercizio presuppone che l'utente abbia</span><span class="sxs-lookup"><span data-stu-id="82492-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="82492-121">una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="82492-121">an active Azure subscription.</span></span>
* <span data-ttu-id="82492-122">l'accesso a un dispositivo StorSimple serie 8000 registrato</span><span class="sxs-lookup"><span data-stu-id="82492-122">access to a registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="82492-123">tutte le chiavi associate con il dispositivo StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="82492-123">all the keys associated with the StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="82492-124">Iscrizione</span><span class="sxs-lookup"><span data-stu-id="82492-124">Sign up</span></span>

<span data-ttu-id="82492-125">StorSimple Data Manager è in modalità di anteprima privata.</span><span class="sxs-lookup"><span data-stu-id="82492-125">The StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="82492-126">Per iscriversi a un'anteprima privata di questo servizio, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="82492-126">Perform the following steps to sign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="82492-127">Accedere al portale di Azure con l'estensione di StorSimple Data Manager su: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="82492-127">Log into the Azure portal with the StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="82492-128">Usare le credenziali di Azure per accedere.</span><span class="sxs-lookup"><span data-stu-id="82492-128">Use your Azure credentials to log in.</span></span>

2.  <span data-ttu-id="82492-129">Fare clic sull'icona **+** per creare un servizio.</span><span class="sxs-lookup"><span data-stu-id="82492-129">Click the **+** icon to create a service.</span></span> <span data-ttu-id="82492-130">Fare clic su **Archiviazione** e scegliere **Visualizza tutto** nel pannello che si apre.</span><span class="sxs-lookup"><span data-stu-id="82492-130">Click **Storage** and then click **See All** in the blade that opens up.</span></span>

    ![Ricerca dell'icona di StorSimple Data Manager](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="82492-132">Viene visualizzata l'icona di StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="82492-132">You see the StorSimple Data Manager icon.</span></span>

    ![Selezione dell'icona di StorSimple Data Manager](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="82492-134">Fare clic sull'icona di StorSimple Data Manager, quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="82492-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="82492-135">Selezionare la sottoscrizione che si desidera abilitare per l'anteprima privata e quindi fare clic su **Sign me up!** (Esegui iscrizione)</span><span class="sxs-lookup"><span data-stu-id="82492-135">Pick the subscription that you want to enable for the private preview and then click **Sign me up!**</span></span>

    ![Esegui iscrizione](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="82492-137">Viene inviata una richiesta di iscrizione,</span><span class="sxs-lookup"><span data-stu-id="82492-137">This sends a request to onboard you.</span></span> <span data-ttu-id="82492-138">che verrà gestita non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="82492-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="82492-139">Dopo l'abilitazione della sottoscrizione, sarà possibile creare un servizio StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="82492-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="82492-140">Per accedere facilmente al servizio StorSimple Data Manager, fare clic sull'icona a stella per aggiungerlo ai Preferiti.</span><span class="sxs-lookup"><span data-stu-id="82492-140">To easily access the StorSimple Data Manager service, click the star icon to pin it to your favorites.</span></span>

    ![Accesso a StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="82492-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82492-142">Next steps</span></span>

<span data-ttu-id="82492-143">[Usare l'interfaccia utente di StorSimple Data Manager per la trasformazione dei dati](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="82492-143">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>