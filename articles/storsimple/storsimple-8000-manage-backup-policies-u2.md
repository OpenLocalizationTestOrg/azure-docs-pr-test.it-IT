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
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>Utilizzare il servizio di gestione di dispositivi StorSimple hello in Criteri di backup toomanage portale di Azure


## <a name="overview"></a>Panoramica

In questa esercitazione viene illustrato come toouse hello del servizio di gestione di dispositivi StorSimple **criteri di Backup** i processi di backup toocontrol pannello e alla conservazione dei backup per i volumi StorSimple. Viene inoltre descritto come toocomplete un backup manuale.

Quando si esegue il backup di un volume, è possibile scegliere toocreate uno snapshot locale o uno snapshot nel cloud. Se si esegue il backup di un volume aggiunto in locale, è consigliabile specificare uno snapshot nel cloud. Se si crea un numero elevato di snapshot locali di un volume aggiunto in locale e tali snapshot sono associati a un set di dati che dispone di molte varianze, si determinerà una situazione favorevole all'esaurimento rapido dello spazio locale. Se si sceglie tootake gli snapshot locali, è consigliabile richiedere meno tooback snapshot giornalieri fino allo stato più recente di hello, conservarli per un giorno e quindi eliminarli.

Quando si utilizza uno snapshot nel cloud di un volume aggiunto in locale, copiare solo hello modificato dati toohello nel cloud, in cui è deduplicato e compressi.

## <a name="hello-backup-policy-blade"></a>pannello dei criteri di Backup Hello

Hello **criteri di Backup** pannello per il dispositivo StorSimple consente toomanage i criteri di backup e di pianificazione locale e di snapshot nel cloud. Criteri di backup sono pianificazioni di backup utilizzato tooconfigure e conservazione dei backup per una raccolta di volumi. Criteri di backup consentono di tootake uno snapshot di più volumi contemporaneamente. Ciò significa che i backup hello creati da un criterio di backup sarà copie coerenti con l'arresto anomalo del sistema.

Elenco tabulare di criteri di backup Hello consente inoltre di toofilter hello criteri di backup esistenti da uno o più dei seguenti campi hello:

* **Nome criterio** : hello nome associato a criteri hello. Hello diversi tipi di criteri includono:

  * Criteri pianificati, creati esplicitamente dall'utente hello.
  * Importare i criteri che sono stati originariamente creati in hello gestione Snapshot StorSimple. Questi disponga di un tag che descrive l'host di gestione Snapshot StorSimple hello che sono stati importati criteri hello da.

  > [!NOTE]
  > Criteri di backup automatico o predefinito non sono più abilitati in fase di hello della creazione del volume.

* **Ultimo backup riuscito** : hello data e l'ora di hello ultimo backup completato che è stato creato con questo criterio.

* **Backup successivo** : hello data e l'ora di hello backup pianificato successivo che verrà avviato da questo criterio.

* **Volumi** : hello volumi associati criteri hello. Tutti i volumi di hello associati a un criterio di backup vengono raggruppati quando vengono creati i backup.

* **Le pianificazioni** : numero di pianificazioni associate al criterio di backup hello hello.

Hello utilizzato di frequente operazioni che è possibile eseguire per i criteri di backup sono:

* Aggiungere un criterio di backup
* Aggiungere o modificare una pianificazione
* Aggiungere o rimuovere un volume
* Eliminare un criterio di backup
* Creazione di un backup manuale

## <a name="add-a-backup-policy"></a>Aggiungere un criterio di backup

Aggiungere una pianificazione di criteri di backup tooautomatically i backup. Al volume creato per la prima volta non è associato alcun criterio di backup predefinito. È necessario tooadd e assegnare i dati di volume tooprotect un criterio di backup.

Eseguire i passaggi hello tooadd portale Azure un criterio di backup per il dispositivo StorSimple hello. Dopo aver aggiunto i criteri di hello, è possibile definire una pianificazione (vedere [aggiungere o modificare una pianificazione](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>Aggiungere o modificare una pianificazione

È possibile aggiungere o modificare una pianificazione che viene collegato tooan criteri di backup esistenti nel dispositivo StorSimple. Eseguire i passaggi hello tooadd portale Azure hello o modificare una pianificazione.

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>Aggiungere o rimuovere un volume

È possibile aggiungere o rimuovere un volume assegnato tooa i criteri di backup nel dispositivo StorSimple. Eseguire i passaggi hello tooadd portale Azure hello o rimozione di un volume.

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>Eliminare un criterio di backup

Eseguire i passaggi hello toodelete portale Azure un criterio di backup nel dispositivo StorSimple hello.

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Creazione di un backup manuale

Eseguire i passaggi backup (manuale) di hello toocreate portale Azure una richiesta per un singolo volume hello.

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

