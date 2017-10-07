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
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a>Utilizzare hello StorSimple Manager servizio toomanage criteri di backup (Update 2)
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come toouse hello servizio StorSimple Manager **criteri di Backup** pagina toocontrol i processi di backup e conservazione dei backup per i volumi StorSimple. Viene inoltre descritto come toocomplete un backup manuale.

Quando si esegue il backup di un volume, è possibile scegliere toocreate uno snapshot locale o uno snapshot nel cloud. Se si esegue il backup di un volume aggiunto in locale, è consigliabile specificare uno snapshot nel cloud. Se si crea un numero elevato di snapshot locali di un volume aggiunto in locale e tali snapshot sono associati a un set di dati che dispone di molte varianze, si determinerà una situazione favorevole all'esaurimento rapido dello spazio locale. Se si sceglie tootake gli snapshot locali, è consigliabile richiedere meno tooback snapshot giornalieri fino allo stato più recente di hello, conservarli per un giorno e quindi eliminarli.

Quando si utilizza uno snapshot nel cloud di un volume aggiunto in locale, copiare solo hello modificato dati toohello nel cloud, in cui è deduplicato e compressi. 

## <a name="hello-backup-policies-page"></a>pagina Criteri di Backup Hello
Hello **criteri di Backup** pagina permette di toomanage criteri di backup e di pianificazione locale e di snapshot nel cloud. (Criteri di backup sono pianificazioni di backup utilizzato tooconfigure e conservazione dei backup per una raccolta di volumi). Criteri di backup consentono di tootake uno snapshot di più volumi contemporaneamente. Ciò significa che i backup hello creati da un criterio di backup sarà copie coerenti con l'arresto anomalo del sistema. Hello **criteri di Backup** pagina vengono elencati i criteri di backup hello, tipi, i volumi associato hello, numero hello di backup conservati e hello opzione tooenable questi criteri.

Hello **criteri di Backup** pagina consente inoltre toofilter hello criteri di backup esistenti da uno o più dei seguenti campi hello:

* **Nome criterio** : hello nome associato a criteri hello. Hello diversi tipi di criteri includono:
  
  * Criteri pianificati, creati esplicitamente dall'utente hello.
  * Criteri automatici che vengono creati quando il backup di hello predefinito per questa opzione di volume è stato abilitato in fase di hello della creazione del volume. Questi criteri vengono denominati *VolumeName*pre_definita in *VolumeName* fa riferimento il nome di toohello del volume StorSimple configurato dall'utente hello nel portale di Azure classico hello hello. criteri automatici di Hello generano snapshot nel cloud giornalieri a partire dall'ora del dispositivo 22:30.
  * Importare i criteri che sono stati originariamente creati in hello gestione Snapshot StorSimple. Questi disponga di un tag che descrive l'host di gestione Snapshot StorSimple hello che sono stati importati criteri hello da.
* **Volumi** : hello volumi associati criteri hello. Tutti i volumi di hello associati a un criterio di backup vengono raggruppati quando vengono creati i backup.
* **Ultimo backup riuscito** : hello data e l'ora di hello ultimo backup completato che è stato creato con questo criterio.
* **Backup successivo** : hello data e l'ora di hello backup pianificato successivo che verrà avviato da questo criterio.
* **Le pianificazioni** : numero di pianificazioni associate al criterio di backup hello hello.

Hello utilizzato di frequente operazioni che è possibile eseguire in questa pagina sono:

* Aggiungere un criterio di backup 
* Aggiungere o modificare una pianificazione 
* Eliminare un criterio di backup 
* Creazione di un backup manuale 
* Creare un criterio di backup personalizzato con più volumi e pianificazioni 

## <a name="add-a-backup-policy"></a>Aggiungere un criterio di backup
Aggiungere una pianificazione di criteri di backup tooautomatically i backup. Eseguire i passaggi hello Azure tooadd portale classico un criterio di backup per il dispositivo StorSimple hello. Dopo aver aggiunto i criteri di hello, è possibile definire una pianificazione (vedere [aggiungere o modificare una pianificazione](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

![Video disponibile](./media/storsimple-manage-backup-policies-u2/Video_icon.png)**Video disponibile**

Fare clic su un video che illustra la modalità di toocreate locale o cloud, criteri di backup toowatch [qui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Aggiungere o modificare una pianificazione
È possibile aggiungere o modificare una pianificazione che viene collegato tooan criteri di backup esistenti nel dispositivo StorSimple. Eseguire i passaggi hello Azure tooadd portale classico hello o modificare una pianificazione.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a>Eliminare un criterio di backup
Eseguire i passaggi hello Azure toodelete portale classico un criterio di backup nel dispositivo StorSimple hello.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Creazione di un backup manuale
Eseguire i passaggi backup (manuale) di hello Azure toocreate portale classico una richiesta per un singolo volume hello.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Creare un criterio di backup personalizzato con più volumi e pianificazioni
Eseguire i passaggi hello Azure toocreate portale classico criteri di backup personalizzati con più volumi e pianificazioni hello.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

