---
title: criteri di backup aaaManage StorSimple 8000 series | Documenti Microsoft
description: Viene illustrato come utilizzare toocreate servizio di gestione di dispositivi StorSimple hello e gestire i backup manuali, pianificazioni di backup e conservazione dei backup in un dispositivo StorSimple serie 8000.
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
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="c4f1d-103">Utilizzare il servizio di gestione di dispositivi StorSimple hello in Criteri di backup toomanage portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c4f1d-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="c4f1d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c4f1d-104">Overview</span></span>

<span data-ttu-id="c4f1d-105">In questa esercitazione viene illustrato come toouse hello del servizio di gestione di dispositivi StorSimple **criteri di Backup** i processi di backup toocontrol pannello e alla conservazione dei backup per i volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="c4f1d-106">Viene inoltre descritto come toocomplete un backup manuale.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="c4f1d-107">Quando si esegue il backup di un volume, è possibile scegliere toocreate uno snapshot locale o uno snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="c4f1d-108">Se si esegue il backup di un volume aggiunto in locale, è consigliabile specificare uno snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="c4f1d-109">Se si crea un numero elevato di snapshot locali di un volume aggiunto in locale e tali snapshot sono associati a un set di dati che dispone di molte varianze, si determinerà una situazione favorevole all'esaurimento rapido dello spazio locale.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="c4f1d-110">Se si sceglie tootake gli snapshot locali, è consigliabile richiedere meno tooback snapshot giornalieri fino allo stato più recente di hello, conservarli per un giorno e quindi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="c4f1d-111">Quando si utilizza uno snapshot nel cloud di un volume aggiunto in locale, copiare solo hello modificato dati toohello nel cloud, in cui è deduplicato e compressi.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="c4f1d-112">pannello dei criteri di Backup Hello</span><span class="sxs-lookup"><span data-stu-id="c4f1d-112">hello Backup policy blade</span></span>

<span data-ttu-id="c4f1d-113">Hello **criteri di Backup** pannello per il dispositivo StorSimple consente toomanage i criteri di backup e di pianificazione locale e di snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="c4f1d-114">Criteri di backup sono pianificazioni di backup utilizzato tooconfigure e conservazione dei backup per una raccolta di volumi.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="c4f1d-115">Criteri di backup consentono di tootake uno snapshot di più volumi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="c4f1d-116">Ciò significa che i backup hello creati da un criterio di backup sarà copie coerenti con l'arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="c4f1d-117">Elenco tabulare di criteri di backup Hello consente inoltre di toofilter hello criteri di backup esistenti da uno o più dei seguenti campi hello:</span><span class="sxs-lookup"><span data-stu-id="c4f1d-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="c4f1d-118">**Nome criterio** : hello nome associato a criteri hello.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="c4f1d-119">Hello diversi tipi di criteri includono:</span><span class="sxs-lookup"><span data-stu-id="c4f1d-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="c4f1d-120">Criteri pianificati, creati esplicitamente dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="c4f1d-121">Importare i criteri che sono stati originariamente creati in hello gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="c4f1d-122">Questi disponga di un tag che descrive l'host di gestione Snapshot StorSimple hello che sono stati importati criteri hello da.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c4f1d-123">Criteri di backup automatico o predefinito non sono più abilitati in fase di hello della creazione del volume.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="c4f1d-124">**Ultimo backup riuscito** : hello data e l'ora di hello ultimo backup completato che è stato creato con questo criterio.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="c4f1d-125">**Backup successivo** : hello data e l'ora di hello backup pianificato successivo che verrà avviato da questo criterio.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="c4f1d-126">**Volumi** : hello volumi associati criteri hello.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="c4f1d-127">Tutti i volumi di hello associati a un criterio di backup vengono raggruppati quando vengono creati i backup.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="c4f1d-128">**Le pianificazioni** : numero di pianificazioni associate al criterio di backup hello hello.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="c4f1d-129">Hello utilizzato di frequente operazioni che è possibile eseguire per i criteri di backup sono:</span><span class="sxs-lookup"><span data-stu-id="c4f1d-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="c4f1d-130">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="c4f1d-130">Add a backup policy</span></span>
* <span data-ttu-id="c4f1d-131">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="c4f1d-131">Add or modify a schedule</span></span>
* <span data-ttu-id="c4f1d-132">Aggiungere o rimuovere un volume</span><span class="sxs-lookup"><span data-stu-id="c4f1d-132">Add or remove a volume</span></span>
* <span data-ttu-id="c4f1d-133">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="c4f1d-133">Delete a backup policy</span></span>
* <span data-ttu-id="c4f1d-134">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="c4f1d-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="c4f1d-135">Aggiungere un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="c4f1d-135">Add a backup policy</span></span>

<span data-ttu-id="c4f1d-136">Aggiungere una pianificazione di criteri di backup tooautomatically i backup.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="c4f1d-137">Al volume creato per la prima volta non è associato alcun criterio di backup predefinito.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="c4f1d-138">È necessario tooadd e assegnare i dati di volume tooprotect un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="c4f1d-139">Eseguire i passaggi hello tooadd portale Azure un criterio di backup per il dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="c4f1d-140">Dopo aver aggiunto i criteri di hello, è possibile definire una pianificazione (vedere [aggiungere o modificare una pianificazione](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="c4f1d-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="c4f1d-141">Aggiungere o modificare una pianificazione</span><span class="sxs-lookup"><span data-stu-id="c4f1d-141">Add or modify a schedule</span></span>

<span data-ttu-id="c4f1d-142">È possibile aggiungere o modificare una pianificazione che viene collegato tooan criteri di backup esistenti nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="c4f1d-143">Eseguire i passaggi hello tooadd portale Azure hello o modificare una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="c4f1d-144">Aggiungere o rimuovere un volume</span><span class="sxs-lookup"><span data-stu-id="c4f1d-144">Add or remove a volume</span></span>

<span data-ttu-id="c4f1d-145">È possibile aggiungere o rimuovere un volume assegnato tooa i criteri di backup nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="c4f1d-146">Eseguire i passaggi hello tooadd portale Azure hello o rimozione di un volume.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="c4f1d-147">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="c4f1d-147">Delete a backup policy</span></span>

<span data-ttu-id="c4f1d-148">Eseguire i passaggi hello toodelete portale Azure un criterio di backup nel dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="c4f1d-149">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="c4f1d-149">Take a manual backup</span></span>

<span data-ttu-id="c4f1d-150">Eseguire i passaggi backup (manuale) di hello toocreate portale Azure una richiesta per un singolo volume hello.</span><span class="sxs-lookup"><span data-stu-id="c4f1d-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="c4f1d-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4f1d-151">Next steps</span></span>

<span data-ttu-id="c4f1d-152">Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c4f1d-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

