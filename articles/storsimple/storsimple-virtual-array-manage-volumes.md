---
title: i volumi StorSimple Virtual Array aaaManage | Documenti Microsoft
description: Gestione di dispositivi StorSimple hello descrive e illustra come toouse volumi toomanage l'Array virtuale StorSimple.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>Utilizzare Gestione periferiche di StorSimple servizio toomanage volumi hello Array virtuale StorSimple

## <a name="overview"></a>Panoramica

In questa esercitazione viene illustrato come toouse hello toocreate servizio di gestione di dispositivi StorSimple e gestire volumi sull'Array virtuale StorSimple.

servizio di gestione di dispositivi StorSimple Hello è un'estensione in hello portale di Azure che consente di gestire la soluzione StorSimple da una singola interfaccia web. In aggiunta toomanaging condivisioni e volumi, è possibile utilizzare tooview servizio di gestione di dispositivi StorSimple hello e gestire i dispositivi, visualizzare gli avvisi, visualizzare e gestire criteri di backup e di catalogo di backup hello.

## <a name="volume-types"></a>Tipi di volume

I volumi di StorSimple possono essere:

* **Aggiunto in locale**: dati in tali volumi rimane nella matrice hello in qualsiasi momento e non lo spill toohello cloud.
* **A più livelli**: toohello cloud possono lo spill dei dati in tali volumi. Quando si crea un volume a livelli, viene eseguito il provisioning di circa il 10% di spazio hello a livello locale hello e 90% dello spazio di hello è disponibile nel cloud hello. Ad esempio, se è stato eseguito il provisioning di un volume di 1 TB, 100 GB si troverà nello spazio locale hello e 900 GB verrebbe utilizzato nel cloud hello hello quando i livelli dati. A sua volta, ciò implica che se si esaurisce tutto lo spazio locale hello sul dispositivo hello, è Impossibile eseguire il provisioning un volume a livelli (poiché hello 10% è necessario in hello locale livello non sarà disponibile).

### <a name="provisioned-capacity"></a>Capacità con provisioning
Fare riferimento toohello seguente tabella per la capacità massima di provisioning per ogni tipo di volume.

| **Identificatore limite**                                       | **Limite**     |
|------------------------------------------------------------|---------------|
| Dimensione minima di un volume a livelli                            | 500 GB        |
| Dimensione massima di un volume a livelli                            | 5 TB          |
| Dimensione minima di un volume aggiunto in locale                    | 50 GB         |
| Dimensione massima di un volume aggiunto in locale                    | 500 GB        |

## <a name="hello-volumes-blade"></a>Pannello volumi Hello
Hello **volumi** menu del Pannello di riepilogo del servizio StorSimple Visualizza elenco hello di volumi di archiviazione in una matrice specificata di StorSimple e consente toomanage li.

![Pannello Volumi](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

Un volume è costituito da una serie di attributi:

* **Nome del volume** : un nome descrittivo che deve essere univoco e consente di identificare il volume di hello.
* **Stato** : online oppure offline. Se un volume è offline, non è visibile tooinitiators (server) che è consentito l'accesso toouse hello volume.
* **Tipo** – indica se il volume di hello è **a livelli** (hello predefinito) o **aggiunto in locale**.
* **Capacità** – specifica hello quantità di dati utilizzati come toohello confrontata la quantità totale di dati che possono essere archiviati dall'iniziatore hello (server).
* **Backup** : nel caso di hello Array virtuale StorSimple, tutti i volumi vengono abilitati automaticamente per il backup.
* **Gli host connessi** – specifica iniziatori hello (server) che sono consentiti l'accesso toothis volume.

![Dettagli sui volumi](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

Hello seguire le istruzioni riportate in questa esercitazione tooperform di hello seguenti attività:

* Aggiungere un volume
* Modificare un volume
* Portare un volume offline
* Eliminare un volume

## <a name="add-a-volume"></a>Aggiungere un volume

1. Pannello riepilogo servizio StorSimple hello, fare clic su **+ Aggiungi volume** hello barra dei comandi. Verrà visualizzata hello **aggiungere volume** blade.
   
    ![Aggiungi volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. In hello **aggiungere volume** pannello hello seguenti:
   
   * In hello **nome Volume** immettere un nome univoco per il volume. nome Hello deve essere una stringa che contiene 3 too127 caratteri.
   * In hello **tipo** elenco a discesa specificare se toocreate un **a livelli** o **aggiunto in locale** volume. Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni di livello superiore, selezionare il volume **Aggiunto in locale**. Per tutti gli altri dati, selezionare volume **A livelli**.
   * In hello **capacità** specificare dimensioni di hello del volume hello. Un volume a livelli deve essere compreso tra 500 GB e 5 TB e un volume aggiunto in locale deve essere compreso tra 50 e 500 GB.
   * * Fare clic su **connesso host**, selezionare un accesso controllo record (ACR) corrispondente toohello iniziatore iSCSI che desidera tooconnect toothis volume e quindi fare clic su **selezionare**.
3. tooadd un nuovo host connessi, fare clic su **Aggiungi nuovo**, immettere un nome per l'host di hello e relativo iSCSI nome qualificato e quindi fare clic su **Aggiungi**.
   
    ![Aggiungi volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. Al termine della configurazione del volume, fare clic su **Crea**. Verrà creato un volume con hello specificato le impostazioni e verrà visualizzata una notifica al momento della creazione ha esito positivo di hello di hello stesso. Per impostazione predefinita, il backup verrà abilitato per il volume di hello.
5. tooconfirm che hello volume è stato creato correttamente, andare toohello **volumi** blade. Verrà visualizzato il volume di hello elencato.
   
    ![Creazione del volume completata](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>Modificare un volume

Modificare un volume quando sono necessari toochange hello host che accedono a volume hello. Hello altri attributi di un volume non possono essere modificati dopo aver creato il volume di hello.

#### <a name="toomodify-a-volume"></a>toomodify un volume

1. Da hello **volumi** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello volume desiderato toomodify risiede.
2. **Selezionare** hello volume e fare clic su **connesso host** tooview hello host attualmente connesso e modificarlo tooa diversi server.
   
    ![Modificare il volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. Salvare le modifiche, fare clic su hello **salvare** barra dei comandi. Verranno applicate le impostazioni specificate e verrà visualizzata una notifica.

## <a name="take-a-volume-offline"></a>Portare un volume offline

Potrebbe essere necessario tootake un volume offline quando si pianifica toomodify o eliminarlo. Quando un volume è offline, non è disponibile per l'accesso in lettura/scrittura. Sarà necessario tootake hello volume offline nell'host di hello e sul dispositivo hello.

#### <a name="tootake-a-volume-offline"></a>tootake un volume offline

1. Assicurarsi che il volume di hello in questione non è in uso prima di portarlo offline.
2. Portare hello volume offline nell'host di hello prima. In questo modo si evita i potenziali rischi di danneggiamento dei dati nel volume hello. Per passaggi specifici, vedere toohello istruzioni per il sistema operativo host.
3. Una volta volume hello host hello è offline, adottare volume hello nella matrice hello offline eseguendo hello alla procedura seguente:
   
   * Da hello **volumi** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello risiede volume desiderato tootake offline.
   * **Selezionare** hello volume e fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **portare offline**.
     
        ![Volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * Esaminare le informazioni di hello in hello **portare offline** pannello e confermare l'operazione di accettazione di hello. Fare clic su **portare offline** tootake offline volume hello. Si noterà una notifica dell'operazione di hello in corso.
   * tooconfirm volume hello correttamente è stato portato offline, visitare toohello **volumi** blade. Si dovrebbe essere stato hello del volume di hello come offline.
     
       ![Conferma volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>Eliminare un volume

> [!IMPORTANT]
> È possibile eliminare un volume solo se è offline.
> 
> 

Completare hello seguendo i passaggi toodelete un volume.

#### <a name="toodelete-a-volume"></a>toodelete un volume

1. Da hello **volumi** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello volume desiderato toodelete risiede.
2. **Selezionare** hello volume e fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **eliminare**.
   
    ![Eliminare il volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. Controllare lo stato di hello del volume hello desiderato toodelete. Se volume hello da toodelete non è offline, le operazioni non in linea hello in primo luogo, seguenti [portare offline un volume](#take-a-volume-offline).
4. Alla richiesta di conferma in hello **eliminare** pannello accettare conferma hello e fare clic su **eliminare**. volume Hello verrà eliminata e hello **volumi** pannello verrà visualizzato l'elenco di hello aggiornato di volumi presenti array virtuale hello.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[clonare un volume StorSimple](storsimple-virtual-array-clone.md).

