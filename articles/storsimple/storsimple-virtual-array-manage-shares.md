---
title: condivide Array virtuale StorSimple aaaManage | Documenti Microsoft
description: Gestione di dispositivi StorSimple hello descrive e illustra come toouse, condivisioni toomanage l'Array virtuale StorSimple.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a>Utilizzare condivisioni toomanage del servizio gestione di dispositivi StorSimple hello in hello Array virtuale StorSimple

## <a name="overview"></a>Panoramica

In questa esercitazione viene illustrato come toouse hello toocreate servizio di gestione di dispositivi StorSimple e gestire condivisioni nell'Array virtuale StorSimple.

servizio di gestione di dispositivi StorSimple Hello è un'estensione in hello portale di Azure che consente di gestire la soluzione StorSimple da una singola interfaccia web. In aggiunta toomanaging condivisioni e volumi, è possibile utilizzare tooview servizio di gestione di dispositivi StorSimple hello e gestire i dispositivi, visualizzare gli avvisi, gestire criteri di backup e gestire catalogo di backup hello.

## <a name="share-types"></a>Tipi di condivisione

Le condivisioni StorSimple possono essere:

* **Aggiunto in locale**: dati in tali condivisioni rimane nella matrice hello in qualsiasi momento e non lo spill toohello cloud.
* **A più livelli**: toohello cloud possono lo spill dei dati in tali condivisioni. Quando si crea una condivisione a livelli, viene eseguito il provisioning di circa il 10% di spazio hello a livello locale hello e 90% dello spazio di hello è disponibile nel cloud hello. Ad esempio, se è stato eseguito il provisioning di una condivisione di 1 TB, 100 GB si troverà nello spazio locale hello e 900 GB verrebbe utilizzato nel cloud hello hello quando i livelli dati. A sua volta, ciò implica che se si esaurisce tutto lo spazio locale hello sul dispositivo hello, è Impossibile eseguire il provisioning una condivisione a livelli (poiché hello 10% è necessario in hello locale livello non sarà disponibile).

### <a name="provisioned-capacity"></a>Capacità con provisioning

Fare riferimento toohello per la capacità massima di provisioning per ogni tipo di condivisione nella tabella seguente.

| **Identificatore limite** | **Limite** |
| --- | --- |
| Dimensione minima di una condivisione a livelli |500 GB |
| Dimensione massima di una condivisione a livelli |20 TB |
| Dimensione minima di una condivisione aggiunta in locale |50 GB |
| Dimensione massima di una condivisione aggiunta in locale |2 TB |

## <a name="hello-shares-blade"></a>Pannello condivisioni Hello

Hello **condivisioni** menu del Pannello di riepilogo del servizio StorSimple Visualizza elenco hello delle quote di archiviazione in una matrice specificata di StorSimple e consente toomanage li.

![Pannello Condivisioni](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

Una condivisione è costituita da una serie di attributi:

* **Nome condivisione** : un nome descrittivo che deve essere univoco e consente di identificare condivisione hello.
* **Stato** : online oppure offline. Se una condivisione è offline, gli utenti della condivisione di hello non saranno in grado di tooaccess è.
* **Tipo** – indica se la condivisione hello è **a livelli** (hello predefinito) o **aggiunto in locale**.
* **Capacità** – specifica hello quantità di dati utilizzati come toohello confrontata la quantità totale di dati che possono essere archiviati nella condivisione di hello.
* **Descrizione** – un'impostazione facoltativa che consente di descrivere condivisione hello.
* **Autorizzazioni** -hello NTFS autorizzazioni toohello condivisione può essere gestite tramite Esplora risorse.
* **Backup** : nel caso di hello Array virtuale StorSimple, tutte le condivisioni vengono abilitate automaticamente per il backup.

![Dettagli sulle condivisioni](./media/storsimple-virtual-array-manage-shares/share-details.png)

Hello seguire le istruzioni riportate in questa esercitazione tooperform di hello seguenti attività:

* Aggiungere una condivisione
* Modificare una condivisione
* Portare offline una condivisione
* Eliminare una condivisione

## <a name="add-a-share"></a>Aggiungere una condivisione

1. Pannello riepilogo servizio StorSimple hello, fare clic su **+ Aggiungi condivisione** hello barra dei comandi. Verrà visualizzata hello **Aggiungi condivisione** blade.

    ![Aggiungere la condivisione](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. In hello **Aggiungi condivisione** pannello hello seguenti:
   
    1. In hello **nome condivisione** immettere un nome univoco per la condivisione. nome Hello deve essere una stringa che contiene 3 too127 caratteri.

    2. Facoltativo **descrizione** per condivisione hello. Descrizione Hello consentirà di identificare i proprietari di condivisione hello.

    3. In hello **tipo** elenco a discesa specificare se toocreate un **a livelli** o **aggiunto in locale** condividere. Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni di livello superiore, selezionare la condivisione **Aggiunto in locale**. Per tutti gli altri dati, selezionare una condivisone **A livelli** .

    4. In hello **capacità** , specificare una dimensione di hello della condivisione hello. Una condivisione a livelli deve essere compresa tra 500 GB e 20 TB e una condivisione aggiunta in locale deve essere compresa tra 50 GB e 2 TB.

    5. In hello **impostare come predefinita per le autorizzazioni complete** campo, assegnare hello autorizzazioni toohello utente o gruppo hello che accede a questa condivisione. Specificare il nome di hello di hello utente o gruppo di utenti di hello in  _john@contoso.com_  formato. È consigliabile utilizzare un tooaccess privilegi di amministratore di utente gruppo (anziché un singolo utente) tooallow tali condivisioni. Dopo aver assegnato le autorizzazioni di hello qui, è possibile quindi utilizzare Esplora File toomodify queste autorizzazioni.
3. Al termine della configurazione della condivisione fare clic su **Crea**. Verrà creata una condivisione con hello specificato le impostazioni e verrà visualizzata una notifica. Per impostazione predefinita, il backup verrà abilitato per la condivisione di hello.
4. tooconfirm che hello condivisione è stato creato correttamente, andare toohello **condivisioni** blade. Dovrebbe essere hello condividere elencati.
   
    ![Creazione della condivisione completata](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a>Modificare una condivisione

Modificare una condivisione quando è necessario descrizione hello toochange della condivisione hello. Una volta creata la condivisione di hello, è non possibile modificare nessuna altra proprietà di condivisione.

#### <a name="toomodify-a-share"></a>toomodify una condivisione

1. Da hello **condivisioni** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello condivisione desiderato toomodify risiede.
2. **Selezionare** hello condivisione tooview hello corrente descrizione e la modifica.
3. Salvare le modifiche, fare clic su hello **salvare** barra dei comandi. Verranno applicate le impostazioni specificate e verrà visualizzata una notifica.
   
    ![ Modificare la condivisione](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a>Portare offline una condivisione

Potrebbe essere necessario tootake una condivisione non in linea durante la pianificazione toomodify o eliminarlo. Quando una condivisione è offline, non è disponibile per l'accesso in lettura/scrittura. Sarà necessario tootake hello condivisione offline nell'host di hello e sul dispositivo hello.

#### <a name="tootake-a-share-offline"></a>tootake una condivisione non in linea

1. Assicurarsi che la condivisione hello in questione non è in uso prima di portarlo offline.
2. Assumere hello condivisione matrice hello offline eseguendo hello alla procedura seguente:
   
    1. Da hello **condivisioni** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello risiede condivisione desiderato tootake offline.

    2. **Selezionare** condivisione hello e fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **portare offline**.
     
        ![Condivisione offline](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. Esaminare le informazioni di hello in hello **portare offline** pannello e confermare l'operazione di accettazione di hello. Fare clic su **portare offline** tootake della condivisione hello offline. Si noterà una notifica dell'operazione di hello in corso.

    4. tooconfirm che hello condivisione è stato eseguito correttamente non in linea, andare toohello **condivisioni** blade. Dovrebbe essere stato hello della condivisione hello come non in linea.

## <a name="delete-a-share"></a>Eliminare una condivisione

> [!IMPORTANT]
> È possibile eliminare una condivisione solo se è offline.


Completare hello seguendo i passaggi toodelete una condivisione.

#### <a name="toodelete-a-share"></a>toodelete una condivisione

1. Da hello **condivisioni** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui condivisione hello desiderato toodelete risiede.
2. **Selezionare** condivisione hello e fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **eliminare**.
   
    ![Eliminare la condivisione](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. Controllare lo stato di hello della condivisione hello desiderato toodelete. Se si desidera toodelete condivisione di hello non è offline, portarlo prima offline. Seguire i passaggi di hello in [portare offline una condivisione di](#take-a-share-offline).
4. Alla richiesta di conferma in hello **eliminare** pannello accettare conferma hello e fare clic su **eliminare**. condivisione di Hello verrà eliminata e hello **condivisioni** pannello mostra l'elenco di hello aggiornato delle azioni all'interno della matrice virtuale hello.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come troppo[clonare una condivisione di StorSimple](storsimple-virtual-array-clone.md).

