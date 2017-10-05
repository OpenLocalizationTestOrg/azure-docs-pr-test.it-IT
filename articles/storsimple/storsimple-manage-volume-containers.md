---
title: Gestire i contenitori del volume di StorSimple | Microsoft Docs
description: "Viene illustrato come è possibile utilizzare la pagina di contenitori del volume di servizio StorSimple Manager per aggiungere, modificare o eliminare un contenitore del volume."
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
ms.openlocfilehash: bb55a7a4bff0fd4319de6f6ce958686ad8a4142b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="2e8a2-103">Utilizzare il servizio StorSimple Manager per gestire i contenitori di volume StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-103">Use the StorSimple Manager service to manage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="2e8a2-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2e8a2-104">Overview</span></span>
<span data-ttu-id="2e8a2-105">In questa esercitazione viene illustrato come utilizzare il servizio StorSimple Manager per creare e gestire contenitori dei volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-105">This tutorial explains how to use the StorSimple Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="2e8a2-106">Un contenitore del volume in un dispositivo StorSimple di Microsoft Azure contiene uno o più volumi che condividono l'account di archiviazione, la crittografia e le impostazioni del consumo di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="2e8a2-107">Un dispositivo può avere più contenitori del volume per tutti i volumi.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="2e8a2-108">Un contenitore del volume ha i seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="2e8a2-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="2e8a2-109">**Volumi** : i volumi StorSimple a livelli o aggiunti in locale all'interno del contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> <span data-ttu-id="2e8a2-110">Un contenitore del volume può includere fino a 256 volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-110">A volume container may contain up to 256 StorSimple volumes.</span></span>
* <span data-ttu-id="2e8a2-111">**Crittografia** : una chiave di crittografia che può essere definita per ogni contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="2e8a2-112">Questa chiave viene utilizzata per crittografare i dati inviati dal dispositivo StorSimple nel cloud.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-112">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="2e8a2-113">Una chiave a livello militare AES-256 bit viene utilizzata con la chiave immesso dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-113">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="2e8a2-114">Per proteggere i dati, è consigliabile abilitare sempre la crittografia di archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-114">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="2e8a2-115">**Account di archiviazione** : l'account di archiviazione collegato al provider di servizi di archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-115">**Storage account** – The storage account that is linked to your cloud storage service provider.</span></span> <span data-ttu-id="2e8a2-116">Tutti i volumi che risiedono in un contenitore di volumi condividono questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-116">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="2e8a2-117">È possibile scegliere un account di archiviazione da un elenco esistente o creare un nuovo account quando si crea il contenitore del volume e quindi specificare le credenziali di accesso per l'account.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-117">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="2e8a2-118">**Larghezza di banda cloud** : larghezza di banda usata dal dispositivo quando i dati dal dispositivo vengono inviati al cloud.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-118">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="2e8a2-119">È possibile applicare un controllo della larghezza di banda specificando un valore compreso tra 1 e 1000 Mbps quando si definisce questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="2e8a2-120">Se si desidera che il dispositivo usi tutti larghezza di banda disponibile, impostare questo campo su illimitata.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-120">If you want the device to consume all available bandwidth, set this field to Unlimited.</span></span> <span data-ttu-id="2e8a2-121">È inoltre possibile creare e applicare un modello di larghezza di banda per l'allocazione della larghezza di banda in base alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-121">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

![Andare alla pagina Contenitori di volumi.](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="2e8a2-123">Questa procedure seguenti viene illustrato come utilizzare quest'ultimo **contenitori del Volume** per completare le operazioni comuni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e8a2-123">This following procedures explain how to use the StorSimple **Volume containers** page to complete the following common operations:</span></span>

* <span data-ttu-id="2e8a2-124">Aggiungere un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="2e8a2-124">Add a volume container</span></span> 
* <span data-ttu-id="2e8a2-125">Modificare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="2e8a2-125">Modify a volume container</span></span> 
* <span data-ttu-id="2e8a2-126">Eliminare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="2e8a2-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="2e8a2-127">Aggiungere un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="2e8a2-127">Add a volume container</span></span>
<span data-ttu-id="2e8a2-128">Eseguire i passaggi seguenti per aggiungere un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-128">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="2e8a2-129">Modificare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="2e8a2-129">Modify a volume container</span></span>
<span data-ttu-id="2e8a2-130">Eseguire i passaggi seguenti per modificare un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-130">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="2e8a2-131">Eliminare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="2e8a2-131">Delete a volume container</span></span>
<span data-ttu-id="2e8a2-132">Un contenitore del volume ha volumi all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-132">A volume container has volumes within it.</span></span> <span data-ttu-id="2e8a2-133">Può essere eliminato solo se sono stati eliminati tutti i volumi in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-133">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="2e8a2-134">Eseguire la procedura seguente per eliminare un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="2e8a2-134">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="2e8a2-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e8a2-135">Next steps</span></span>
* <span data-ttu-id="2e8a2-136">Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="2e8a2-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="2e8a2-137">Ulteriori informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="2e8a2-137">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

