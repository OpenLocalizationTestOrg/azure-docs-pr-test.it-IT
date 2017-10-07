---
title: aaaManage i criteri di backup di StorSimple | Documenti Microsoft
description: Viene illustrato come utilizzare toocreate servizio StorSimple Manager di hello e gestire i backup manuali, pianificazioni di backup e conservazione dei backup.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a><span data-ttu-id="1f93f-103">Utilizzare hello StorSimple Manager servizio toomanage criteri di backup (Update 2)</span><span class="sxs-lookup"><span data-stu-id="1f93f-103">Use hello StorSimple Manager service toomanage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="1f93f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1f93f-104">Overview</span></span>
<span data-ttu-id="1f93f-105">In questa esercitazione viene illustrato come toouse hello servizio StorSimple Manager **criteri di Backup** pagina toocontrol i processi di backup e conservazione dei backup per i volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1f93f-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="1f93f-106">Viene inoltre descritto come toocomplete un backup manuale.</span><span class="sxs-lookup"><span data-stu-id="1f93f-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="1f93f-107">Quando si esegue il backup di un volume, è possibile scegliere toocreate uno snapshot locale o uno snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="1f93f-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="1f93f-108">Se si esegue il backup di un volume aggiunto in locale, è consigliabile specificare uno snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="1f93f-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="1f93f-109">Se si crea un numero elevato di snapshot locali di un volume aggiunto in locale e tali snapshot sono associati a un set di dati che dispone di molte varianze, si determinerà una situazione favorevole all'esaurimento rapido dello spazio locale.</span><span class="sxs-lookup"><span data-stu-id="1f93f-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="1f93f-110">Se si sceglie tootake gli snapshot locali, è consigliabile richiedere meno tooback snapshot giornalieri fino allo stato più recente di hello, conservarli per un giorno e quindi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="1f93f-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="1f93f-111">Quando si utilizza uno snapshot nel cloud di un volume aggiunto in locale, copiare solo hello modificato dati toohello nel cloud, in cui è deduplicato e compressi.</span><span class="sxs-lookup"><span data-stu-id="1f93f-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span> 

## <a name="hello-backup-policies-page"></a><span data-ttu-id="1f93f-112">pagina Criteri di Backup Hello</span><span class="sxs-lookup"><span data-stu-id="1f93f-112">hello Backup Policies page</span></span>
<span data-ttu-id="1f93f-113">Hello **criteri di Backup** pagina permette di toomanage criteri di backup e di pianificazione locale e di snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="1f93f-113">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="1f93f-114">(Criteri di backup sono pianificazioni di backup utilizzato tooconfigure e conservazione dei backup per una raccolta di volumi). Criteri di backup consentono di tootake uno snapshot di più volumi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="1f93f-114">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="1f93f-115">Ciò significa che i backup hello creati da un criterio di backup sarà copie coerenti con l'arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="1f93f-115">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="1f93f-116">Hello **criteri di Backup** pagina vengono elencati i criteri di backup hello, tipi, i volumi associato hello, numero hello di backup conservati e hello opzione tooenable questi criteri.</span><span class="sxs-lookup"><span data-stu-id="1f93f-116">hello **Backup Policies** page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="1f93f-117">Hello **criteri di Backup** pagina consente inoltre toofilter hello criteri di backup esistenti da uno o più dei seguenti campi hello:</span><span class="sxs-lookup"><span data-stu-id="1f93f-117">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="1f93f-118">**Nome criterio** : hello nome associato a criteri hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="1f93f-119">Hello diversi tipi di criteri includono:</span><span class="sxs-lookup"><span data-stu-id="1f93f-119">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="1f93f-120">Criteri pianificati, creati esplicitamente dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="1f93f-121">Criteri automatici che vengono creati quando il backup di hello predefinito per questa opzione di volume è stato abilitato in fase di hello della creazione del volume.</span><span class="sxs-lookup"><span data-stu-id="1f93f-121">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="1f93f-122">Questi criteri vengono denominati *VolumeName*pre_definita in *VolumeName* fa riferimento il nome di toohello del volume StorSimple configurato dall'utente hello nel portale di Azure classico hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-122">These policies are named as *VolumeName*_Default where *VolumeName* refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="1f93f-123">criteri automatici di Hello generano snapshot nel cloud giornalieri a partire dall'ora del dispositivo 22:30.</span><span class="sxs-lookup"><span data-stu-id="1f93f-123">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="1f93f-124">Importare i criteri che sono stati originariamente creati in hello gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1f93f-124">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="1f93f-125">Questi disponga di un tag che descrive l'host di gestione Snapshot StorSimple hello che sono stati importati criteri hello da.</span><span class="sxs-lookup"><span data-stu-id="1f93f-125">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="1f93f-126">**Volumi** : hello volumi associati criteri hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="1f93f-127">Tutti i volumi di hello associati a un criterio di backup vengono raggruppati quando vengono creati i backup.</span><span class="sxs-lookup"><span data-stu-id="1f93f-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="1f93f-128">**Ultimo backup riuscito** : hello data e l'ora di hello ultimo backup completato che è stato creato con questo criterio.</span><span class="sxs-lookup"><span data-stu-id="1f93f-128">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="1f93f-129">**Backup successivo** : hello data e l'ora di hello backup pianificato successivo che verrà avviato da questo criterio.</span><span class="sxs-lookup"><span data-stu-id="1f93f-129">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="1f93f-130">**Le pianificazioni** : numero di pianificazioni associate al criterio di backup hello hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-130">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="1f93f-131">Hello utilizzato di frequente operazioni che è possibile eseguire in questa pagina sono:</span><span class="sxs-lookup"><span data-stu-id="1f93f-131">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="1f93f-132">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="1f93f-132">Add a backup policy</span></span> 
* <span data-ttu-id="1f93f-133">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="1f93f-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="1f93f-134">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="1f93f-134">Delete a backup policy</span></span> 
* <span data-ttu-id="1f93f-135">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="1f93f-135">Take a manual backup</span></span> 
* <span data-ttu-id="1f93f-136">Creare un criterio di backup personalizzato con più volumi e pianificazioni</span><span class="sxs-lookup"><span data-stu-id="1f93f-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="1f93f-137">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="1f93f-137">Add a backup policy</span></span>
<span data-ttu-id="1f93f-138">Aggiungere una pianificazione di criteri di backup tooautomatically i backup.</span><span class="sxs-lookup"><span data-stu-id="1f93f-138">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="1f93f-139">Eseguire i passaggi hello Azure tooadd portale classico un criterio di backup per il dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-139">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="1f93f-140">Dopo aver aggiunto i criteri di hello, è possibile definire una pianificazione (vedere [aggiungere o modificare una pianificazione](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="1f93f-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="1f93f-141">![Video disponibile](./media/storsimple-manage-backup-policies-u2/Video_icon.png)**Video disponibile**</span><span class="sxs-lookup"><span data-stu-id="1f93f-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="1f93f-142">Fare clic su un video che illustra la modalità di toocreate locale o cloud, criteri di backup toowatch [qui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="1f93f-142">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="1f93f-143">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="1f93f-143">Add or modify a schedule</span></span>
<span data-ttu-id="1f93f-144">È possibile aggiungere o modificare una pianificazione che viene collegato tooan criteri di backup esistenti nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1f93f-144">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="1f93f-145">Eseguire i passaggi hello Azure tooadd portale classico hello o modificare una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1f93f-145">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="1f93f-146">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="1f93f-146">Delete a backup policy</span></span>
<span data-ttu-id="1f93f-147">Eseguire i passaggi hello Azure toodelete portale classico un criterio di backup nel dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-147">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="1f93f-148">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="1f93f-148">Take a manual backup</span></span>
<span data-ttu-id="1f93f-149">Eseguire i passaggi backup (manuale) di hello Azure toocreate portale classico una richiesta per un singolo volume hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-149">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="1f93f-150">Creare un criterio di backup personalizzato con più volumi e pianificazioni</span><span class="sxs-lookup"><span data-stu-id="1f93f-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="1f93f-151">Eseguire i passaggi hello Azure toocreate portale classico criteri di backup personalizzati con più volumi e pianificazioni hello.</span><span class="sxs-lookup"><span data-stu-id="1f93f-151">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="1f93f-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1f93f-152">Next steps</span></span>
<span data-ttu-id="1f93f-153">Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1f93f-153">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

