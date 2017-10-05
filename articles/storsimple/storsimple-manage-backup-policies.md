---
title: Gestire i criteri di backup di StorSimple | Microsoft Docs
description: "Viene illustrato come è possibile utilizzare il servizio StorSimple Manager per creare e gestire backup manuali, pianificazioni di backup e conservazione dei backup."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: c1e9d5d0450bab5d371aafb40fd7c5920d39dfdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies"></a><span data-ttu-id="83a68-103">Per gestire i criteri di backup, è possibile usare il servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="83a68-103">Use the StorSimple Manager service to manage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="83a68-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="83a68-104">Overview</span></span>
<span data-ttu-id="83a68-105">In questa esercitazione viene illustrato come utilizzare il servizio StorSimple Manager **criteri di Backup** pagina per controllare i processi di backup e memorizzazione dei backup per i volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="83a68-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="83a68-106">Viene inoltre descritto come eseguire un backup manuale.</span><span class="sxs-lookup"><span data-stu-id="83a68-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="83a68-107">Il **criteri di Backup** pagina consente di gestire i criteri di backup e pianificare locale e gli snapshot cloud.</span><span class="sxs-lookup"><span data-stu-id="83a68-107">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="83a68-108">(Criteri di backup vengono utilizzati per configurare pianificazioni di backup e memorizzazione dei backup per un insieme di volumi). I criteri di backup consentono di creare uno snapshot di più volumi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="83a68-108">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="83a68-109">Questo significa che i backup creati con un criterio di backup saranno copie coerenti con l'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="83a68-109">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="83a68-110">Questa pagina vengono elencati i criteri di backup, i relativi tipi, i volumi associati, il numero di backup conservati e l'opzione per abilitare questi criteri.</span><span class="sxs-lookup"><span data-stu-id="83a68-110">This page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="83a68-111">Il **criteri di Backup** pagina consente inoltre di filtrare i criteri di backup esistenti da una o più dei seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="83a68-111">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="83a68-112">**Nome criterio** : il nome associato al criterio.</span><span class="sxs-lookup"><span data-stu-id="83a68-112">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="83a68-113">I diversi tipi di criteri includono:</span><span class="sxs-lookup"><span data-stu-id="83a68-113">The different types of policies include:</span></span>
  
  * <span data-ttu-id="83a68-114">Criteri pianificati, vengono creati esplicitamente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="83a68-114">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="83a68-115">Criteri automatici, che vengono creati quando il backup predefinito per questa opzione è stato abilitato al momento della creazione del volume.</span><span class="sxs-lookup"><span data-stu-id="83a68-115">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="83a68-116">Questi criteri sono denominati VolumeName_Default dove nome Volume si riferisce al nome del volume StorSimple configurato dall'utente nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="83a68-116">These policies are named as VolumeName_Default where Volume name refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="83a68-117">I criteri automatici generare gli snapshot cloud giornalieri a partire da 22:30 ora del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="83a68-117">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="83a68-118">Criteri importati, che sono stati originariamente creati in Gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="83a68-118">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="83a68-119">Hanno un tag che descrive l'host di gestione Snapshot StorSimple che i criteri sono stati importati da.</span><span class="sxs-lookup"><span data-stu-id="83a68-119">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="83a68-120">**Volumi** – i volumi associati al criterio.</span><span class="sxs-lookup"><span data-stu-id="83a68-120">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="83a68-121">Tutti i volumi associati a un criterio di backup vengono raggruppati quando vengono creati i backup.</span><span class="sxs-lookup"><span data-stu-id="83a68-121">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="83a68-122">**Ultimo backup completato** : la data e l'ora dell'ultimo backup riuscito è stato creato con questo criterio.</span><span class="sxs-lookup"><span data-stu-id="83a68-122">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="83a68-123">**Backup successivo** : data e ora del successivo backup pianificato verrà avviato da questo criterio.</span><span class="sxs-lookup"><span data-stu-id="83a68-123">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="83a68-124">**Pianificazioni** – il numero di pianificazioni associate al criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="83a68-124">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="83a68-125">Le operazioni utilizzate di frequente che è possibile eseguire da questa pagina sono:</span><span class="sxs-lookup"><span data-stu-id="83a68-125">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="83a68-126">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="83a68-126">Add a backup policy</span></span> 
* <span data-ttu-id="83a68-127">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="83a68-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="83a68-128">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="83a68-128">Delete a backup policy</span></span> 
* <span data-ttu-id="83a68-129">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="83a68-129">Take a manual backup</span></span> 
* <span data-ttu-id="83a68-130">Creare un criterio di backup personalizzato con più volumi e pianificazioni</span><span class="sxs-lookup"><span data-stu-id="83a68-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="83a68-131">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="83a68-131">Add a backup policy</span></span>
<span data-ttu-id="83a68-132">Aggiungere un criterio di backup per la pianificazione automatica dei backup.</span><span class="sxs-lookup"><span data-stu-id="83a68-132">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="83a68-133">Eseguire i passaggi seguenti nel portale di Azure classico per aggiungere un criterio di backup per il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="83a68-133">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="83a68-134">Dopo aver aggiunto i criteri, è possibile definire una pianificazione (vedere [Aggiungere o modificare una pianificazione](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="83a68-134">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="83a68-135">![Video disponibile](./media/storsimple-manage-backup-policies/Video_icon.png) **Video disponibile**</span><span class="sxs-lookup"><span data-stu-id="83a68-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="83a68-136">Per guardare un video che illustra come creare un criterio di backup cloud o locale, fare clic [qui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="83a68-136">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="83a68-137">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="83a68-137">Add or modify a schedule</span></span>
<span data-ttu-id="83a68-138">È possibile aggiungere o modificare una pianificazione che è collegata a un criterio di backup nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="83a68-138">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="83a68-139">Eseguire i passaggi seguenti nel portale di Azure classico per aggiungere o modificare un backup pianificato.</span><span class="sxs-lookup"><span data-stu-id="83a68-139">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="83a68-140">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="83a68-140">Delete a backup policy</span></span>
<span data-ttu-id="83a68-141">Eseguire i passaggi seguenti nel portale di Azure classico per eliminare un criterio di backup nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="83a68-141">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="83a68-142">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="83a68-142">Take a manual backup</span></span>
<span data-ttu-id="83a68-143">Eseguire i passaggi seguenti nel portale di Azure classico per creare un backup manuale su richiesta per un singolo volume.</span><span class="sxs-lookup"><span data-stu-id="83a68-143">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="83a68-144">Creare un criterio di backup personalizzato con più volumi e pianificazioni</span><span class="sxs-lookup"><span data-stu-id="83a68-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="83a68-145">Eseguire i passaggi seguenti nel portale di Azure classico per creare un criterio di backup personalizzato che dispone di più volumi e pianificazioni.</span><span class="sxs-lookup"><span data-stu-id="83a68-145">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="83a68-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83a68-146">Next steps</span></span>
<span data-ttu-id="83a68-147">Ulteriori informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="83a68-147">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

