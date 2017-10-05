---
title: Gestire i criteri di backup di StorSimple serie 8000 | Microsoft Docs
description: Illustra come usare il servizio Gestione dispositivi StorSimple per creare e gestire backup manuali, pianificazioni di backup e conservazione dei backup nei dispositivi StorSimple serie 8000.
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 569dbfdeb7dcd526cb5a54b487ea1bfb59b13cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-manage-backup-policies"></a><span data-ttu-id="dbf50-103">Usare il servizio Gestione dispositivi StorSimple nel portale di Azure per gestire i criteri di backup</span><span class="sxs-lookup"><span data-stu-id="dbf50-103">Use the StorSimple Device Manager service in Azure portal to manage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="dbf50-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="dbf50-104">Overview</span></span>

<span data-ttu-id="dbf50-105">Questa esercitazione illustra come usare il pannello **criteri di Backup** del servizio Gestione dispositivi StorSimple per controllare i processi di backup e le regole di conservazione dei backup per i volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dbf50-105">This tutorial explains how to use the StorSimple Device Manager service **Backup policy** blade to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="dbf50-106">Viene inoltre descritto come eseguire un backup manuale.</span><span class="sxs-lookup"><span data-stu-id="dbf50-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="dbf50-107">Quando si esegue il backup di un volume, è possibile scegliere di creare uno snapshot locale o uno snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="dbf50-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="dbf50-108">Se si esegue il backup di un volume aggiunto in locale, è consigliabile specificare uno snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="dbf50-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="dbf50-109">Se si crea un numero elevato di snapshot locali di un volume aggiunto in locale e tali snapshot sono associati a un set di dati che dispone di molte varianze, si determinerà una situazione favorevole all'esaurimento rapido dello spazio locale.</span><span class="sxs-lookup"><span data-stu-id="dbf50-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="dbf50-110">Se si sceglie di creare snapshot locali, è consigliabile creare meno snapshot giornalieri per eseguire il backup dello stato più recente, conservarli per un giorno e quindi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="dbf50-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="dbf50-111">Quando si crea uno snapshot nel cloud di un volume aggiunto in locale, copiare solo i dati modificati nel cloud, in cui è deduplicato e compresso.</span><span class="sxs-lookup"><span data-stu-id="dbf50-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span>

## <a name="the-backup-policy-blade"></a><span data-ttu-id="dbf50-112">Pannello Criteri di backup</span><span class="sxs-lookup"><span data-stu-id="dbf50-112">The Backup policy blade</span></span>

<span data-ttu-id="dbf50-113">Il pannello **Criteri di Backup** del dispositivo StorSimple consente di gestire i criteri di backup e pianificare gli snapshot in locale e nel cloud.</span><span class="sxs-lookup"><span data-stu-id="dbf50-113">The **Backup policy** blade for your StorSimple device allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="dbf50-114">I criteri di backup vengono usati per configurare le pianificazioni dei backup e la regole di conservazione dei backup per una raccolta di volumi.</span><span class="sxs-lookup"><span data-stu-id="dbf50-114">Backup policies are used to configure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="dbf50-115">I criteri di backup consentono di creare uno snapshot di più volumi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="dbf50-115">Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="dbf50-116">Questo significa che i backup creati con un criterio di backup saranno copie coerenti con l'arresto anomalo.</span><span class="sxs-lookup"><span data-stu-id="dbf50-116">This means that the backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="dbf50-117">L'elenco tabulare dei criteri di backup consente anche di filtrare i criteri di backup esistenti in base a uno o più dei seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="dbf50-117">The backup policies tabular listing also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="dbf50-118">**Nome criterio** : il nome associato al criterio.</span><span class="sxs-lookup"><span data-stu-id="dbf50-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="dbf50-119">I diversi tipi di criteri includono:</span><span class="sxs-lookup"><span data-stu-id="dbf50-119">The different types of policies include:</span></span>

  * <span data-ttu-id="dbf50-120">Criteri pianificati, vengono creati esplicitamente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="dbf50-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="dbf50-121">Criteri importati, che sono stati originariamente creati in Gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dbf50-121">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="dbf50-122">Hanno un tag che descrive l'host di gestione Snapshot StorSimple che i criteri sono stati importati da.</span><span class="sxs-lookup"><span data-stu-id="dbf50-122">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="dbf50-123">I criteri di backup automatici o predefiniti non sono più abilitati al momento della creazione del volume.</span><span class="sxs-lookup"><span data-stu-id="dbf50-123">Automatic or default backup policies are no longer enabled at the time of volume creation.</span></span>

* <span data-ttu-id="dbf50-124">**Ultimo backup completato** : la data e l'ora dell'ultimo backup riuscito è stato creato con questo criterio.</span><span class="sxs-lookup"><span data-stu-id="dbf50-124">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="dbf50-125">**Backup successivo** : data e ora del successivo backup pianificato verrà avviato da questo criterio.</span><span class="sxs-lookup"><span data-stu-id="dbf50-125">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="dbf50-126">**Volumi** – i volumi associati al criterio.</span><span class="sxs-lookup"><span data-stu-id="dbf50-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="dbf50-127">Tutti i volumi associati a un criterio di backup vengono raggruppati quando vengono creati i backup.</span><span class="sxs-lookup"><span data-stu-id="dbf50-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="dbf50-128">**Pianificazioni** – il numero di pianificazioni associate al criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="dbf50-128">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="dbf50-129">Le operazioni più comuni che è possibile eseguire con i criteri di backup sono:</span><span class="sxs-lookup"><span data-stu-id="dbf50-129">The frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="dbf50-130">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="dbf50-130">Add a backup policy</span></span>
* <span data-ttu-id="dbf50-131">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="dbf50-131">Add or modify a schedule</span></span>
* <span data-ttu-id="dbf50-132">Aggiungere o rimuovere un volume</span><span class="sxs-lookup"><span data-stu-id="dbf50-132">Add or remove a volume</span></span>
* <span data-ttu-id="dbf50-133">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="dbf50-133">Delete a backup policy</span></span>
* <span data-ttu-id="dbf50-134">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="dbf50-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="dbf50-135">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="dbf50-135">Add a backup policy</span></span>

<span data-ttu-id="dbf50-136">Aggiungere un criterio di backup per la pianificazione automatica dei backup.</span><span class="sxs-lookup"><span data-stu-id="dbf50-136">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="dbf50-137">Al volume creato per la prima volta non è associato alcun criterio di backup predefinito.</span><span class="sxs-lookup"><span data-stu-id="dbf50-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="dbf50-138">È necessario aggiungere e assegnare un criterio di backup per proteggere i dati del volume.</span><span class="sxs-lookup"><span data-stu-id="dbf50-138">You need to add and assign a backup policy to protect volume data.</span></span>

<span data-ttu-id="dbf50-139">Attenersi alla procedura seguente nel portale di Azure per aggiungere un criterio di backup per il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dbf50-139">Perform the following steps in the Azure portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="dbf50-140">Dopo aver aggiunto i criteri, è possibile definire una pianificazione (vedere [Aggiungere o modificare una pianificazione](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="dbf50-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="dbf50-141">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="dbf50-141">Add or modify a schedule</span></span>

<span data-ttu-id="dbf50-142">È possibile aggiungere o modificare una pianificazione che è collegata a un criterio di backup nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dbf50-142">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="dbf50-143">Attenersi alla procedura seguente nel portale di Azure per aggiungere o modificare una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="dbf50-143">Perform the following steps in the Azure portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="dbf50-144">Aggiungere o rimuovere un volume</span><span class="sxs-lookup"><span data-stu-id="dbf50-144">Add or remove a volume</span></span>

<span data-ttu-id="dbf50-145">È possibile aggiungere o rimuovere un volume assegnato a un criterio di backup nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dbf50-145">You can add or remove a volume assigned to a backup policy on your StorSimple device.</span></span> <span data-ttu-id="dbf50-146">Attenersi alla procedura seguente nel portale di Azure per aggiungere o rimuovere un volume.</span><span class="sxs-lookup"><span data-stu-id="dbf50-146">Perform the following steps in the Azure portal to add or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="dbf50-147">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="dbf50-147">Delete a backup policy</span></span>

<span data-ttu-id="dbf50-148">Attenersi alla procedura seguente nel portale di Azure per eliminare un criterio di backup nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dbf50-148">Perform the following steps in the Azure portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="dbf50-149">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="dbf50-149">Take a manual backup</span></span>

<span data-ttu-id="dbf50-150">Attenersi alla procedura seguente nel portale di Azure per creare un backup manuale su richiesta per un singolo volume.</span><span class="sxs-lookup"><span data-stu-id="dbf50-150">Perform the following steps in the Azure portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="dbf50-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbf50-151">Next steps</span></span>

<span data-ttu-id="dbf50-152">Altre informazioni sull'[utilizzo del servizio Gestione dispositivi StorSimple per la gestione del dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="dbf50-152">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

