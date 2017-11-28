---
title: aaaManage ai contenitori dei volumi StorSimple nel dispositivo serie StorSimple 8000 hello | Documenti Microsoft
description: Viene illustrato come usare hello gestione di dispositivi StorSimple contenitori dei volumi servizio pagina tooadd, modificare o eliminare un contenitore del volume.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="7f00c-103">Utilizzare i contenitori dei volumi StorSimple servizio toomanage hello dispositivo StorSimple Manager</span><span class="sxs-lookup"><span data-stu-id="7f00c-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="7f00c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7f00c-104">Overview</span></span>
<span data-ttu-id="7f00c-105">In questa esercitazione viene illustrato come toouse hello toocreate servizio di gestione di dispositivi StorSimple e gestire i contenitori di volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7f00c-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="7f00c-106">Un contenitore del volume in un dispositivo StorSimple di Microsoft Azure contiene uno o più volumi che condividono l'account di archiviazione, la crittografia e le impostazioni del consumo di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="7f00c-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="7f00c-107">Un dispositivo può avere più contenitori del volume per tutti i volumi.</span><span class="sxs-lookup"><span data-stu-id="7f00c-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="7f00c-108">Un contenitore di volumi sono hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f00c-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="7f00c-109">**Volumi** : hello a livelli o aggiunto in locale i volumi StorSimple di cui sono contenuti all'interno del contenitore di volume hello.</span><span class="sxs-lookup"><span data-stu-id="7f00c-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="7f00c-110">**Crittografia** : una chiave di crittografia che può essere definita per ogni contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="7f00c-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="7f00c-111">Questa chiave viene usata per crittografare i dati di hello inviata da cloud toohello dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7f00c-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="7f00c-112">Una chiave di livello militare AES a 256 bit viene utilizzata con la chiave immessa dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="7f00c-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="7f00c-113">toosecure dei dati, è consigliabile abilitare sempre la crittografia dell'archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="7f00c-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="7f00c-114">**Account di archiviazione** : hello account di archiviazione Azure che sono utilizzati toostore hello dati.</span><span class="sxs-lookup"><span data-stu-id="7f00c-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="7f00c-115">Tutti i volumi di hello che risiedono in un contenitore di volumi condividono questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7f00c-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="7f00c-116">È possibile scegliere un account di archiviazione da un elenco esistente o creare un nuovo account quando si crea il contenitore di volumi hello e quindi specificare le credenziali di accesso hello per tale account.</span><span class="sxs-lookup"><span data-stu-id="7f00c-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="7f00c-117">**Larghezza di banda cloud** : hello della larghezza di banda usata dal dispositivo hello per hello dati dal dispositivo hello inviati toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="7f00c-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="7f00c-118">È possibile applicare un controllo della larghezza di banda specificando un valore compreso tra 1 e 1.000 Mbps quando si crea questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="7f00c-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="7f00c-119">Se si desidera hello dispositivo tooconsume tutti disponibile della larghezza di banda, impostare questo campo troppo**Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="7f00c-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="7f00c-120">È anche possibile creare e applicare una larghezza di banda modello tooallocate della larghezza di banda basato su pianificazione.</span><span class="sxs-lookup"><span data-stu-id="7f00c-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="7f00c-121">Hello procedure seguenti illustrano come toouse hello StorSimple **contenitori di volumi** hello toocomplete pannello operazioni comuni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f00c-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="7f00c-122">Aggiungere un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="7f00c-122">Add a volume container</span></span>
* <span data-ttu-id="7f00c-123">Modificare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="7f00c-123">Modify a volume container</span></span>
* <span data-ttu-id="7f00c-124">Eliminare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="7f00c-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="7f00c-125">Aggiungere un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="7f00c-125">Add a volume container</span></span>
<span data-ttu-id="7f00c-126">Eseguire hello seguendo i passaggi tooadd un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="7f00c-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="7f00c-127">Modificare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="7f00c-127">Modify a volume container</span></span>
<span data-ttu-id="7f00c-128">Eseguire hello seguendo i passaggi toomodify un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="7f00c-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="7f00c-129">Eliminare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="7f00c-129">Delete a volume container</span></span>
<span data-ttu-id="7f00c-130">Un contenitore del volume ha volumi all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="7f00c-130">A volume container has volumes within it.</span></span> <span data-ttu-id="7f00c-131">Può essere eliminato solo se tutti i volumi di hello in esso contenuti sono stati eliminati.</span><span class="sxs-lookup"><span data-stu-id="7f00c-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="7f00c-132">Eseguire hello seguendo i passaggi toodelete un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="7f00c-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="7f00c-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f00c-133">Next steps</span></span>
* <span data-ttu-id="7f00c-134">Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="7f00c-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="7f00c-135">Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7f00c-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

