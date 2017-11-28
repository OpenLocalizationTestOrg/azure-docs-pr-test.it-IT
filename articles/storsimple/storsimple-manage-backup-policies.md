---
title: aaaManage i criteri di backup di StorSimple | Documenti Microsoft
description: Viene illustrato come utilizzare toocreate servizio StorSimple Manager di hello e gestire i backup manuali, pianificazioni di backup e conservazione dei backup.
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
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="21138-103">Utilizzare criteri toomanage del servizio StorSimple Manager hello backup</span><span class="sxs-lookup"><span data-stu-id="21138-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="21138-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="21138-104">Overview</span></span>
<span data-ttu-id="21138-105">In questa esercitazione viene illustrato come toouse hello servizio StorSimple Manager **criteri di Backup** pagina toocontrol i processi di backup e conservazione dei backup per i volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21138-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="21138-106">Viene inoltre descritto come toocomplete un backup manuale.</span><span class="sxs-lookup"><span data-stu-id="21138-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="21138-107">Hello **criteri di Backup** pagina permette di toomanage criteri di backup e di pianificazione locale e di snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="21138-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="21138-108">(Criteri di backup sono pianificazioni di backup utilizzato tooconfigure e conservazione dei backup per una raccolta di volumi). Criteri di backup consentono di tootake uno snapshot di più volumi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="21138-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="21138-109">Ciò significa che i backup hello creati da un criterio di backup sarà copie coerenti con l'arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="21138-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="21138-110">Questa pagina sono elencati i criteri di backup hello, tipi, i volumi associato hello, numero hello di backup conservati e hello tooenable opzione questi criteri.</span><span class="sxs-lookup"><span data-stu-id="21138-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="21138-111">Hello **criteri di Backup** pagina consente inoltre toofilter hello criteri di backup esistenti da uno o più dei seguenti campi hello:</span><span class="sxs-lookup"><span data-stu-id="21138-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="21138-112">**Nome criterio** : hello nome associato a criteri hello.</span><span class="sxs-lookup"><span data-stu-id="21138-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="21138-113">Hello diversi tipi di criteri includono:</span><span class="sxs-lookup"><span data-stu-id="21138-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="21138-114">Criteri pianificati, creati esplicitamente dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="21138-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="21138-115">Criteri automatici che vengono creati quando il backup di hello predefinito per questa opzione di volume è stato abilitato in fase di hello della creazione del volume.</span><span class="sxs-lookup"><span data-stu-id="21138-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="21138-116">Questi criteri vengono denominati Nomevolume_default in cui il nome del Volume fa riferimento a nome toohello del volume StorSimple configurato dall'utente hello nel portale di Azure classico hello hello.</span><span class="sxs-lookup"><span data-stu-id="21138-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="21138-117">criteri automatici di Hello generano snapshot nel cloud giornalieri a partire dall'ora del dispositivo 22:30.</span><span class="sxs-lookup"><span data-stu-id="21138-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="21138-118">Importare i criteri che sono stati originariamente creati in hello gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21138-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="21138-119">Questi disponga di un tag che descrive l'host di gestione Snapshot StorSimple hello che sono stati importati criteri hello da.</span><span class="sxs-lookup"><span data-stu-id="21138-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="21138-120">**Volumi** : hello volumi associati criteri hello.</span><span class="sxs-lookup"><span data-stu-id="21138-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="21138-121">Tutti i volumi di hello associati a un criterio di backup vengono raggruppati quando vengono creati i backup.</span><span class="sxs-lookup"><span data-stu-id="21138-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="21138-122">**Ultimo backup riuscito** : hello data e l'ora di hello ultimo backup completato che è stato creato con questo criterio.</span><span class="sxs-lookup"><span data-stu-id="21138-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="21138-123">**Backup successivo** : hello data e l'ora di hello backup pianificato successivo che verrà avviato da questo criterio.</span><span class="sxs-lookup"><span data-stu-id="21138-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="21138-124">**Le pianificazioni** : numero di pianificazioni associate al criterio di backup hello hello.</span><span class="sxs-lookup"><span data-stu-id="21138-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="21138-125">Hello utilizzato di frequente operazioni che è possibile eseguire in questa pagina sono:</span><span class="sxs-lookup"><span data-stu-id="21138-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="21138-126">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="21138-126">Add a backup policy</span></span> 
* <span data-ttu-id="21138-127">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="21138-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="21138-128">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="21138-128">Delete a backup policy</span></span> 
* <span data-ttu-id="21138-129">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="21138-129">Take a manual backup</span></span> 
* <span data-ttu-id="21138-130">Creare un criterio di backup personalizzato con più volumi e pianificazioni</span><span class="sxs-lookup"><span data-stu-id="21138-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="21138-131">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="21138-131">Add a backup policy</span></span>
<span data-ttu-id="21138-132">Aggiungere una pianificazione di criteri di backup tooautomatically i backup.</span><span class="sxs-lookup"><span data-stu-id="21138-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="21138-133">Eseguire i passaggi hello Azure tooadd portale classico un criterio di backup per il dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="21138-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="21138-134">Dopo aver aggiunto i criteri di hello, è possibile definire una pianificazione (vedere [aggiungere o modificare una pianificazione](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="21138-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="21138-135">![Video disponibile](./media/storsimple-manage-backup-policies/Video_icon.png)**Video disponibile**</span><span class="sxs-lookup"><span data-stu-id="21138-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="21138-136">Fare clic su un video che illustra la modalità di toocreate locale o cloud, criteri di backup toowatch [qui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="21138-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="21138-137">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="21138-137">Add or modify a schedule</span></span>
<span data-ttu-id="21138-138">È possibile aggiungere o modificare una pianificazione che viene collegato tooan criteri di backup esistenti nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21138-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="21138-139">Eseguire i passaggi hello Azure tooadd portale classico hello o modificare una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="21138-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="21138-140">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="21138-140">Delete a backup policy</span></span>
<span data-ttu-id="21138-141">Eseguire i passaggi hello Azure toodelete portale classico un criterio di backup nel dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="21138-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="21138-142">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="21138-142">Take a manual backup</span></span>
<span data-ttu-id="21138-143">Eseguire i passaggi backup (manuale) di hello Azure toocreate portale classico una richiesta per un singolo volume hello.</span><span class="sxs-lookup"><span data-stu-id="21138-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="21138-144">Creare un criterio di backup personalizzato con più volumi e pianificazioni</span><span class="sxs-lookup"><span data-stu-id="21138-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="21138-145">Eseguire i passaggi hello Azure toocreate portale classico criteri di backup personalizzati con più volumi e pianificazioni hello.</span><span class="sxs-lookup"><span data-stu-id="21138-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="21138-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21138-146">Next steps</span></span>
<span data-ttu-id="21138-147">Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="21138-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

