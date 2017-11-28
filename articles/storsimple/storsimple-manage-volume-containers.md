---
title: aaaManage ai contenitori dei volumi StorSimple | Documenti Microsoft
description: Viene illustrato come utilizzare hello StorSimple Manager contenitori dei volumi servizio pagina tooadd, modificare o eliminare un contenitore del volume.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="0b231-103">Usare i contenitori di volumi StorSimple toomanage servizio StorSimple Manager hello</span><span class="sxs-lookup"><span data-stu-id="0b231-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="0b231-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0b231-104">Overview</span></span>
<span data-ttu-id="0b231-105">In questa esercitazione viene illustrato come toouse hello toocreate servizio StorSimple Manager e gestire i contenitori di volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b231-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="0b231-106">Un contenitore del volume in un dispositivo StorSimple di Microsoft Azure contiene uno o più volumi che condividono l'account di archiviazione, la crittografia e le impostazioni del consumo di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="0b231-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="0b231-107">Un dispositivo può avere più contenitori del volume per tutti i volumi.</span><span class="sxs-lookup"><span data-stu-id="0b231-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="0b231-108">Un contenitore di volumi sono hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b231-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="0b231-109">**Volumi** : hello a livelli o aggiunto in locale i volumi StorSimple di cui sono contenuti all'interno del contenitore di volume hello.</span><span class="sxs-lookup"><span data-stu-id="0b231-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="0b231-110">Un contenitore del volume può contenere i volumi StorSimple too256.</span><span class="sxs-lookup"><span data-stu-id="0b231-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="0b231-111">**Crittografia** : una chiave di crittografia che può essere definita per ogni contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="0b231-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="0b231-112">Questa chiave viene usata per crittografare i dati di hello inviata da cloud toohello dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b231-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="0b231-113">Una chiave di livello militare AES a 256 bit viene utilizzata con la chiave immessa dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="0b231-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="0b231-114">toosecure dei dati, è consigliabile abilitare sempre la crittografia dell'archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="0b231-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="0b231-115">**Account di archiviazione** : hello account di archiviazione di provider di servizi di archiviazione cloud tooyour collegato.</span><span class="sxs-lookup"><span data-stu-id="0b231-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="0b231-116">Tutti i volumi di hello che risiedono in un contenitore di volumi condividono questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0b231-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="0b231-117">È possibile scegliere un account di archiviazione da un elenco esistente o creare un nuovo account quando si crea il contenitore di volumi hello e quindi specificare le credenziali di accesso hello per tale account.</span><span class="sxs-lookup"><span data-stu-id="0b231-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="0b231-118">**Larghezza di banda cloud** : hello della larghezza di banda usata dal dispositivo hello per hello dati dal dispositivo hello inviati toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="0b231-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="0b231-119">È possibile applicare un controllo della larghezza di banda specificando un valore compreso tra 1 e 1000 Mbps quando si definisce questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="0b231-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="0b231-120">Se si desidera hello dispositivo tooconsume tutti disponibile della larghezza di banda, impostare tooUnlimited questo campo.</span><span class="sxs-lookup"><span data-stu-id="0b231-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="0b231-121">È anche possibile creare e applicare una larghezza di banda modello tooallocate della larghezza di banda basato su pianificazione.</span><span class="sxs-lookup"><span data-stu-id="0b231-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![Andare alla pagina Contenitori di volumi.](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="0b231-123">Procedure riportate di seguito viene illustrato come toouse hello StorSimple **contenitori di volumi** hello toocomplete pagina operazioni comuni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b231-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="0b231-124">Aggiungere un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="0b231-124">Add a volume container</span></span> 
* <span data-ttu-id="0b231-125">Modificare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="0b231-125">Modify a volume container</span></span> 
* <span data-ttu-id="0b231-126">Eliminare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="0b231-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="0b231-127">Aggiungere un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="0b231-127">Add a volume container</span></span>
<span data-ttu-id="0b231-128">Eseguire hello seguendo i passaggi tooadd un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="0b231-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="0b231-129">Modificare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="0b231-129">Modify a volume container</span></span>
<span data-ttu-id="0b231-130">Eseguire hello seguendo i passaggi toomodify un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="0b231-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="0b231-131">Eliminare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="0b231-131">Delete a volume container</span></span>
<span data-ttu-id="0b231-132">Un contenitore del volume ha volumi all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="0b231-132">A volume container has volumes within it.</span></span> <span data-ttu-id="0b231-133">Può essere eliminato solo se tutti i volumi di hello in esso contenuti sono stati eliminati.</span><span class="sxs-lookup"><span data-stu-id="0b231-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="0b231-134">Eseguire hello seguendo i passaggi toodelete un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="0b231-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="0b231-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b231-135">Next steps</span></span>
* <span data-ttu-id="0b231-136">Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="0b231-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="0b231-137">Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0b231-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

