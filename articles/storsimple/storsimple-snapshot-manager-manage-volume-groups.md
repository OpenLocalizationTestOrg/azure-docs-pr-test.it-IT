---
title: gruppi di volumi di gestione Snapshot aaaStorSimple | Documenti Microsoft
description: Viene descritto come toouse hello toocreate snap-in MMC di StorSimple Snapshot Manager e gestire gruppi di volumi.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>Utilizzare Gestione Snapshot StorSimple toocreate e gestire gruppi di volumi
## <a name="overview"></a>Panoramica
È possibile utilizzare hello **gruppi di volumi** nodo hello **ambito** riquadro tooassign volumi toovolume i gruppi, visualizzare informazioni su un gruppo di volumi, pianificare i backup e modificare gruppi di volumi.

Gruppi di volumi sono pool di volumi correlati usati tooensure che i backup siano coerenti con l'applicazione. Per altre informazioni, vedere [Volumi e gruppi di volumi](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) e [Integrazione con il servizio Copia Shadow del volume di Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).

> [!IMPORTANT]
> * Tutti i volumi in un gruppo di volumi devono provenire da un singolo provider di servizi cloud.
> * Quando si configurano i gruppi di volumi, non combinare volumi condivisi cluster (CSV) e non condivisi nello hello stesso gruppo di volumi. Gestione Snapshot StorSimple non supporta la combinazione di volumi condivisi cluster e non condivisi nello stesso snapshot di hello.

![Nodo Gruppi di volumi](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**Figura 1: Nodo Gruppi di volumi di StorSimple Snapshot Manager** 

Questa esercitazione illustra come usare StorSimple Snapshot Manager per:

* Visualizzare le informazioni sui gruppi di volumi
* Creare un gruppo di volumi
* Eseguire il backup di un gruppo di volumi
* Modificare un gruppo di volumi
* Eliminare un gruppo di volumi

Tutte queste azioni sono disponibili anche nel hello **azioni** riquadro.

## <a name="view-volume-groups"></a>Visualizzazione dei gruppi di volumi
Se si fa clic hello **gruppi di volumi** nodo, hello **risultati** riquadro vengono visualizzate le seguenti informazioni su ogni gruppo di volumi hello, in base alle selezioni di colonna hello apportate. (hello colonne hello **risultati** riquadro sono configurabili. Pulsante destro del mouse hello **volumi** nodo, seleziona **vista**e quindi selezionare **Aggiungi/Rimuovi colonne**.)

| Colonna risultati | Descrizione |
|:--- |:--- |
| Nome |Hello **nome** colonna contiene il nome di hello hello gruppo di volumi. |
| Applicazione |Hello **applicazioni** colonna viene visualizzato il numero di hello del writer VSS attualmente installati e in esecuzione in host Windows di hello. |
| Selezionato |Hello **selezionati** colonna Mostra il numero di hello di volumi contenuti nel gruppo di volumi hello. Zero (0) indica che nessuna applicazione è associata a volumi hello nel gruppo di volumi hello. |
| Importati |Hello **importato** colonna Mostra il numero di hello di volumi importati. Quando impostato troppo**True**, questa colonna indica che un gruppo di volumi sono stato importato da hello portale di Azure e non è stato creato in Gestione Snapshot StorSimple. |

> [!NOTE]
> Vengono inoltre visualizzati i gruppi di volumi StorSimple Snapshot Manager hello **criteri di Backup** scheda hello portale di Azure.
> 
> 

## <a name="create-a-volume-group"></a>Creare un gruppo di volumi
Utilizzare hello seguendo procedure toocreate un gruppo di volumi.

#### <a name="toocreate-a-volume-group"></a>toocreate un gruppo di volumi
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro destro **gruppi di volumi**, quindi fare clic su **Crea gruppo di volumi**.
   
    ![Crea gruppo di volumi](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    Hello **creare un gruppo di volumi** viene visualizzata la finestra di dialogo.
   
    ![Finestra di dialogo Crea un gruppo di volumi](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. Immettere hello le seguenti informazioni:
   
   1. In hello **nome** , digitare un nome univoco per il nuovo gruppo di volumi hello.
   2. In hello **applicazioni** casella, selezionare le applicazioni associate a volumi hello che verrà aggiunto il gruppo di volumi toohello.
      
       Hello **applicazioni** solo le applicazioni che usano volumi StorSimple e i writer VSS è abilitate per tali elenchi della casella. Un writer VSS è abilitato solo se tutti i volumi di hello è a conoscenza di tale writer hello sono volumi StorSimple. Se hello applicazioni casella è vuota, quindi verrà installata alcuna applicazione che usa volumi StorSimple di Azure e sono supportati i writer VSS. (Attualmente, Azure StorSimple supporta Microsoft Exchange e SQL Server). Per altre informazioni sui writer del Servizio snapshot del volume, vedere [Integrazione con il servizio Copia Shadow del volume di Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).
      
       Se si seleziona un'applicazione, vengono selezionati automaticamente tutti i volumi associati ad essa. Viceversa, se si selezionano volumi associati a un'applicazione specifica, un'applicazione hello viene selezionata automaticamente in hello **applicazioni** casella. 
   3. In hello **volumi** selezionare gruppo di volumi toohello tooadd volumi StorSimple. 
      
      * È possibile includere volumi con una o più partizioni. (I volumi con più partizioni possono essere dischi dinamici o dischi di base con più partizioni.) Un volume che contiene più partizioni viene considerato come una singola unità. Di conseguenza, se si aggiungono una sola hello partizioni tooa gruppo di volumi, hello tutte le altre partizioni vengono automaticamente aggiunti toothat volume gruppo hello stesso tempo. Dopo aver aggiunto un gruppo di volumi tooa di volume più partizioni, hello volume con più partizioni continua toobe considerati come una singola unità.
      * È possibile creare gruppi di volumi vuoto, non assegnare alcun toothem volumi. 
      * Non combinare volumi condivisi cluster (CSV) e non condivisi nello hello stesso gruppo di volumi. Gestione Snapshot StorSimple non supporta la combinazione di volumi condivisi del cluster e volumi non CSV nella hello stesso snapshot.
4. Fare clic su **OK** toosave gruppo di volumi hello.

## <a name="back-up-a-volume-group"></a>Eseguire il backup di un gruppo di volumi
Utilizzare hello seguendo procedure tooback di un gruppo di volumi.

#### <a name="tooback-up-a-volume-group"></a>tooback di un gruppo di volumi
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro espandere hello **gruppi di volumi** nodo, fare doppio clic su un nome di gruppo di volumi e quindi fare clic su **Esegui Backup**.
   
    ![Esecuzione immediata del backup del gruppo di volumi](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. In hello **Esegui Backup** nella finestra di dialogo **Snapshot locale** o **Snapshot Cloud**, quindi fare clic su **crea**.
   
    ![Finestra di dialogo Esegui backup](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. tooconfirm che hello backup è in esecuzione, espandere hello **processi** nodo e quindi fare clic su **esecuzione**. backup di Hello dovrebbe essere elencato.
5. hello tooview completamento dello snapshot, espandere hello **catalogo di Backup** nodo, espandere il nome di gruppo di hello volumi e quindi fare clic su **Snapshot locale** o **Snapshot Cloud**. verranno elencati i backup di Hello se completato in modo corretto.

## <a name="edit-a-volume-group"></a>Modificare un gruppo di volumi
Utilizzare hello seguendo procedure tooedit un gruppo di volumi.

#### <a name="tooedit-a-volume-group"></a>tooedit un gruppo di volumi
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro espandere hello **gruppi di volumi** nodo, fare doppio clic su un nome di gruppo di volumi e quindi fare clic su **modifica**.
3. Hello * * creare un gruppo di volumi * * viene visualizzata la finestra di dialogo. È possibile modificare hello **nome**, **applicazioni**, e **volumi** voci.
4. Fare clic su **OK** toosave le modifiche.

## <a name="delete-a-volume-group"></a>Eliminare un gruppo di volumi
Utilizzare hello seguendo procedure toodelete un gruppo di volumi. 

> [!WARNING]
> Questa procedura elimina anche tutti i backup di hello associati al gruppo di volumi hello.
> 
> 

#### <a name="toodelete-a-volume-group"></a>toodelete un gruppo di volumi
1. Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.
2. In hello **ambito** riquadro espandere hello **gruppi di volumi** nodo, fare doppio clic su un nome di gruppo di volumi e quindi fare clic su **eliminare**.
3. Hello **Elimina gruppo di volumi** viene visualizzata la finestra di dialogo. Tipo **conferma** in hello casella di testo e quindi fare clic su **OK**.
   
    gruppo di volumi eliminato Hello torni dall'elenco hello hello **risultati** riquadro e tutti i backup associati a tale gruppo di volumi vengono eliminati dal catalogo di backup hello.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[usare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).
* Informazioni su come troppo[toocreate StorSimple Snapshot Manager di utilizzare e gestire criteri di backup](storsimple-snapshot-manager-manage-backup-policies.md).

