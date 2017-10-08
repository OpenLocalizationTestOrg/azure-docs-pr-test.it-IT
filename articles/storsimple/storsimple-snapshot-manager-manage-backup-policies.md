---
title: criteri di backup di Snapshot Manager aaaStorSimple | Documenti Microsoft
description: Viene descritto come toouse hello toocreate snap-in MMC di StorSimple Snapshot Manager e gestire i criteri di backup hello che controllano i backup pianificati.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>Utilizzare Gestione Snapshot StorSimple toocreate e gestire i criteri di backup
## <a name="overview"></a>Panoramica
Un criterio di backup crea una pianificazione per il backup dei dati del volume in locale o cloud hello. Quando si crea un criterio di backup, è inoltre possibile specificare un criterio di conservazione. (È possibile conservare un massimo di 64 snapshot). Per altre informazioni sui criteri di backup, vedere [Tipi di backup](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) nell'articolo relativo a [StorSimple serie 8000: una soluzione cloud ibrida](storsimple-overview.md).

In questa esercitazione viene illustrato come:

* Creare un criterio di backup
* Modifica di un criterio di backup
* Eliminare un criterio di backup

## <a name="create-a-backup-policy"></a>Creare un criterio di backup
Utilizzare hello seguendo procedure toocreate nuovi criteri di backup.

#### <a name="toocreate-a-backup-policy"></a>toocreate un criterio di backup
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro destro **criteri di Backup**, fare clic su **Crea criteri di Backup**.

    ![Creare un criterio di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    Hello **creare un criterio** viene visualizzata la finestra di dialogo.

    ![Creazione di un criterio - scheda Generale](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. In hello **generale** scheda, hello completa le seguenti informazioni:

   1. In hello **nome** casella di testo, digitare un nome per il criterio di hello.
   2. In hello **gruppo di volumi** casella di testo, nome del gruppo di volumi hello associata al criterio di hello hello di tipo.
   3. Selezionare **Snapshot locale** o **Snapshot cloud**.
   4. Selezionare il numero di hello di tooretain snapshot. Se si seleziona **tutti**, verranno conservati 64 snapshot (Buongiorno massimo).
4. Fare clic su hello **pianificazione** scheda.

    ![Creazione un criterio - scheda Pianificazione](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. In hello **pianificazione** scheda, hello completa le seguenti informazioni:

   1. Fare clic su hello **abilitare** backup successivo hello tooschedule di casella di controllo.
   2. In **Impostazioni** selezionare **Una sola volta**, **Giornaliera**, **Settimanale** o **Mensile**.
   3. In hello **avviare** casella di testo, fare clic sull'icona calendario hello e selezionare una data di inizio.
   4. In **Impostazioni avanzate**, è possibile impostare pianificazioni ripetute facoltative e una data di fine.
   5. Fare clic su **OK**.

Dopo aver creato un criterio di backup, le seguenti informazioni hello viene visualizzato in hello **risultati** riquadro:

* **Nome** : hello nome del criterio di backup.
* **Tipo** : snapshot locale o cloud.
* **Gruppo di volumi** : hello gruppo di volumi associato criteri hello.
* **Conservazione** : hello mantenuto il numero di snapshot; hello massimo è 64.
* **Creato** – data hello che è stato creato questo criterio.
* **Abilitato** : indica se i criteri di hello sono attualmente attivo: **True** indica che è attivo; **False** indica che non è attivo.

## <a name="edit-a-backup-policy"></a>Modifica di un criterio di backup
Utilizzare hello seguendo procedure tooedit un criterio di backup.

#### <a name="tooedit-a-backup-policy"></a>tooedit un criterio di backup
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro, fare clic su hello **criteri di Backup** nodo. Vengono visualizzati tutti i criteri di backup hello in hello **risultati** riquadro.
3. Mouse hello criterio che desidera tooedit e quindi fare clic su **modifica**.

    ![Modifica di un criterio di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Quando hello **creare un criterio** verrà visualizzata la finestra, immettere le modifiche e quindi fare clic su **OK**.

## <a name="delete-a-backup-policy"></a>Eliminare un criterio di backup
Utilizzare hello seguendo procedure toodelete un criterio di backup.

#### <a name="toodelete-a-backup-policy"></a>toodelete un criterio di backup
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro, fare clic su hello **criteri di Backup** nodo. Vengono visualizzati tutti i criteri di backup hello in hello **risultati** riquadro.
3. Fare doppio clic su hello dei criteri di backup che desidera toodelete e quindi fare clic su **eliminare**.
4. Quando viene visualizzato il messaggio di conferma di hello, fare clic su **Sì**.

    ![Eliminazione della conferma dei criteri di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[usare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).
* Informazioni su come troppo[tooview StorSimple Snapshot Manager di utilizzare e gestire i processi di backup](storsimple-snapshot-manager-manage-backup-jobs.md).
