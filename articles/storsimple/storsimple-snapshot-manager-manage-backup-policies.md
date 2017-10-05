---
title: Criteri di backup di StorSimple Snapshot Manager | Microsoft Docs
description: Viene descritto come utilizzare lo snap-in MMC di Gestione snapshot StorSimple per creare e gestire i criteri di backup che consentono di controllare i backup pianificati.
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
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a>Utilizzo di Gestione snapshot StorSimple per creare e gestire i criteri di backup
## <a name="overview"></a>Panoramica
Un criterio di backup consente di creare una pianificazione di backup dei dati del volume in locale o nel cloud. Quando si crea un criterio di backup, è inoltre possibile specificare un criterio di conservazione. (È possibile conservare un massimo di 64 snapshot). Per altre informazioni sui criteri di backup, vedere [Tipi di backup](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) nell'articolo relativo a [StorSimple serie 8000: una soluzione cloud ibrida](storsimple-overview.md).

In questa esercitazione viene illustrato come:

* Creare un criterio di backup
* Modifica di un criterio di backup
* Eliminare un criterio di backup

## <a name="create-a-backup-policy"></a>Creare un criterio di backup
Utilizzare la procedura seguente per creare un nuovo criterio di backup.

#### <a name="to-create-a-backup-policy"></a>Per creare un criterio di backup
1. Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.
2. Nel riquadro **Ambito** fare clic con il pulsante destro del mouse su **Criteri di backup**, quindi fare clic su **Crea criteri di backup**.

    ![Creare un criterio di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    Viene visualizzata la finestra di dialogo **Crea un criterio** .

    ![Creazione di un criterio - scheda Generale](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. Nella scheda **Generale** , completare le informazioni seguenti:

   1. Nella casella di testo **Nome** , digitare un nome per il criterio.
   2. Nella casella di testo **Gruppo di volumi** digitare il nome del gruppo di volumi associati ai criteri.
   3. Selezionare **Snapshot locale** o **Snapshot cloud**.
   4. Selezionare il numero di snapshot da conservare. Se si seleziona **Tutti**, verranno conservati 64 snapshot (il massimo).
4. Fare clic sulla scheda **Pianificazione** .

    ![Creazione un criterio - scheda Pianificazione](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. Nella scheda **Pianificazione** , completare le informazioni seguenti:

   1. Fare clic sulla casella di controllo **Abilita** per pianificare il backup successivo.
   2. In **Impostazioni** selezionare **Una sola volta**, **Giornaliera**, **Settimanale** o **Mensile**.
   3. Nella casella di controllo **Avvio** , fare clic sull'icona del calendario e selezionare una data di avvio.
   4. In **Impostazioni avanzate**, è possibile impostare pianificazioni ripetute facoltative e una data di fine.
   5. Fare clic su **OK**.

Dopo aver creato un criterio di backup, nel riquadro **Risultati** vengono visualizzate le informazioni seguenti:

* **Nome** : il nome del criterio di backup.
* **Tipo** : snapshot locale o cloud.
* **Gruppo di volumi** : il gruppo di volumi associato al criterio.
* **Conservazione** : il numero di snapshot conservati (il massimo è 64).
* **Creato** : la data in cui è stato creato questo criterio.
* **Abilitato**: se il criterio è attualmente attivo (**True** indica che è attivo, **False** indica che non è attivo).

## <a name="edit-a-backup-policy"></a>Modifica di un criterio di backup
Utilizzare la procedura seguente per modificare un criterio di backup esistente.

#### <a name="to-edit-a-backup-policy"></a>Per modificare un criterio di backup
1. Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.
2. Nel riquadro **Ambito** fare clic sul nodo **Criteri di backup**. Nel riquadro **Risultati** vengono visualizzati tutti i criteri di backup.
3. Fare clic con il pulsante destro del mouse sul criterio che si desidera modificare, quindi fare clic su **Modifica**.

    ![Modifica di un criterio di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Quando viene visualizzata la finestra **Crea un criterio**, apportare le modifiche, quindi fare clic su **OK**.

## <a name="delete-a-backup-policy"></a>Eliminare un criterio di backup
Utilizzare la procedura seguente per eliminare un criterio di backup.

#### <a name="to-delete-a-backup-policy"></a>Per eliminare un criterio di backup
1. Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.
2. Nel riquadro **Ambito** fare clic sul nodo **Criteri di backup**. Nel riquadro **Risultati** vengono visualizzati tutti i criteri di backup.
3. Fare clic con il pulsante destro del mouse sui criteri di backup da eliminare e quindi fare clic su **Elimina**.
4. Quando viene visualizzato il messaggio di conferma, fare clic su **Sì**.

    ![Eliminazione della conferma dei criteri di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come [Usare Gestione Snapshot StorSimple per amministrare la soluzione di StorSimple](storsimple-snapshot-manager-admin.md).
* Informazioni su come [utilizzare Gestione snapshot StorSimple per visualizzare e gestire i processi di backup](storsimple-snapshot-manager-manage-backup-jobs.md).
