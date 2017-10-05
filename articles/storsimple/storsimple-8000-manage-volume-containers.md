---
title: Gestire i contenitori dei volumi StorSimple nel dispositivo StorSimple serie 8000 | Microsoft Docs
description: Viene illustrato come usare la pagina dei contenitori dei volumi del servizio Gestione dispositivi StorSimple per aggiungere, modificare o eliminare un contenitore del volume.
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
ms.openlocfilehash: 0f8e00d6d07224f56625482f339e612e68914be2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="85a03-103">Usare il servizio Gestione dispositivi StorSimple per gestire i contenitori dei volumi StorSimple</span><span class="sxs-lookup"><span data-stu-id="85a03-103">Use the StorSimple Device Manager service to manage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="85a03-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="85a03-104">Overview</span></span>
<span data-ttu-id="85a03-105">Questa esercitazione illustra come usare il servizio Gestione dispositivi StorSimple per creare e gestire contenitori dei volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="85a03-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="85a03-106">Un contenitore del volume in un dispositivo StorSimple di Microsoft Azure contiene uno o più volumi che condividono l'account di archiviazione, la crittografia e le impostazioni del consumo di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="85a03-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="85a03-107">Un dispositivo può avere più contenitori del volume per tutti i volumi.</span><span class="sxs-lookup"><span data-stu-id="85a03-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="85a03-108">Un contenitore del volume ha i seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="85a03-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="85a03-109">**Volumi** : i volumi StorSimple a livelli o aggiunti in locale all'interno del contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="85a03-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> 
* <span data-ttu-id="85a03-110">**Crittografia** : una chiave di crittografia che può essere definita per ogni contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="85a03-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="85a03-111">Questa chiave viene utilizzata per crittografare i dati inviati dal dispositivo StorSimple nel cloud.</span><span class="sxs-lookup"><span data-stu-id="85a03-111">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="85a03-112">Una chiave a livello militare AES-256 bit viene utilizzata con la chiave immesso dall'utente.</span><span class="sxs-lookup"><span data-stu-id="85a03-112">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="85a03-113">Per proteggere i dati, è consigliabile abilitare sempre la crittografia di archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="85a03-113">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="85a03-114">**Account di archiviazione**: account di archiviazione di Azure usato per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="85a03-114">**Storage account** – The Azure storage account that is used to store the data.</span></span> <span data-ttu-id="85a03-115">Tutti i volumi che risiedono in un contenitore di volumi condividono questo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="85a03-115">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="85a03-116">È possibile scegliere un account di archiviazione da un elenco esistente o creare un nuovo account quando si crea il contenitore del volume e quindi specificare le credenziali di accesso per l'account.</span><span class="sxs-lookup"><span data-stu-id="85a03-116">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="85a03-117">**Larghezza di banda cloud** : larghezza di banda usata dal dispositivo quando i dati dal dispositivo vengono inviati al cloud.</span><span class="sxs-lookup"><span data-stu-id="85a03-117">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="85a03-118">È possibile applicare un controllo della larghezza di banda specificando un valore compreso tra 1 e 1.000 Mbps quando si crea questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="85a03-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="85a03-119">Se si vuole che il dispositivo usi tutti larghezza di banda disponibile, impostare questo campo su **Illimitata**.</span><span class="sxs-lookup"><span data-stu-id="85a03-119">If you want the device to consume all available bandwidth, set this field to **Unlimited**.</span></span> <span data-ttu-id="85a03-120">È inoltre possibile creare e applicare un modello di larghezza di banda per l'allocazione della larghezza di banda in base alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="85a03-120">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

<span data-ttu-id="85a03-121">La procedura seguente illustra come usare il pannello **Contenitori dei volumi** di StorSimple per completare le operazioni comuni seguenti:</span><span class="sxs-lookup"><span data-stu-id="85a03-121">The following procedures explain how to use the StorSimple **Volume containers** blade to complete the following common operations:</span></span>

* <span data-ttu-id="85a03-122">Aggiungere un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="85a03-122">Add a volume container</span></span>
* <span data-ttu-id="85a03-123">Modificare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="85a03-123">Modify a volume container</span></span>
* <span data-ttu-id="85a03-124">Eliminare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="85a03-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="85a03-125">Aggiungere un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="85a03-125">Add a volume container</span></span>
<span data-ttu-id="85a03-126">Eseguire i passaggi seguenti per aggiungere un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="85a03-126">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="85a03-127">Modificare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="85a03-127">Modify a volume container</span></span>
<span data-ttu-id="85a03-128">Eseguire i passaggi seguenti per modificare un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="85a03-128">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="85a03-129">Eliminare un contenitore di volumi</span><span class="sxs-lookup"><span data-stu-id="85a03-129">Delete a volume container</span></span>
<span data-ttu-id="85a03-130">Un contenitore del volume ha volumi all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="85a03-130">A volume container has volumes within it.</span></span> <span data-ttu-id="85a03-131">Può essere eliminato solo se sono stati eliminati tutti i volumi in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="85a03-131">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="85a03-132">Eseguire la procedura seguente per eliminare un contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="85a03-132">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="85a03-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85a03-133">Next steps</span></span>
* <span data-ttu-id="85a03-134">Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="85a03-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="85a03-135">Altre informazioni sull'[utilizzo del servizio Gestione dispositivi StorSimple per la gestione del dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="85a03-135">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

