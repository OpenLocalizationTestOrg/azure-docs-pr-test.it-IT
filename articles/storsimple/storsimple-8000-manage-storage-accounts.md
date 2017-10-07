---
title: le credenziali dell'account di archiviazione StorSimple per i dispositivi di Microsoft Azure StorSimple 8000 series aaaManage | Documenti Microsoft
description: "Viene illustrato come è possibile utilizzare hello tooadd pagina Configura dispositivo StorSimple Manager, modificare, eliminare o le chiavi di sicurezza hello Ruota per un account di archiviazione."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a>Utilizzare le credenziali dell'account di archiviazione di toomanage servizio di gestione di dispositivi StorSimple hello

## <a name="overview"></a>Panoramica

Hello **configurazione** sezione nel Pannello di servizio di gestione di dispositivi StorSimple hello presenta tutti i parametri di servizio globale hello che possono essere creati nel servizio di gestione di dispositivi StorSimple hello. Questi parametri possono essere applicati tooall hello dispositivi toohello servizio connesso e includono:

* Credenziali dell'account di archiviazione
* Modelli di larghezza di banda 
* Record di controllo di accesso 

In questa esercitazione viene illustrato come tooadd, modificare o eliminare le credenziali dell'account di archiviazione o ruotare le chiavi di sicurezza hello per un account di archiviazione.

 ![Elenco di credenziali dell'account di archiviazione](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

Gli account di archiviazione contengono le credenziali hello hello tooaccess di StorSimple dispositivo utilizza l'account di archiviazione con il provider di servizi cloud. Per gli account di archiviazione di Microsoft Azure, queste sono le credenziali quali nome dell'account hello e chiave di accesso primaria hello. 

In hello **le credenziali dell'account di archiviazione** pannello, archiviazione di tutti gli account creati per hello fatturazione sottoscrizione vengono visualizzati in formato tabulare che contiene le seguenti informazioni hello:

* **Nome** : hello account toohello nome univoco assegnato al momento della creazione.
* **SSL abilitato** : indica se hello SSL è abilitato e la comunicazione da dispositivo a cloud è su canale sicuro hello.
* **Utilizzato da** : numero di volumi che usano l'account di archiviazione hello hello.

Hello gli account correlati toostorage attività più comuni che possono essere eseguiti sono:

* Aggiungere un account di archiviazione 
* Modificare un account di archiviazione 
* Eliminare un account di archiviazione 
* Rotazione delle chiavi degli account di archiviazione 

## <a name="types-of-storage-accounts"></a>Tipi di account di archiviazione

Esistono tre tipi di account di archiviazione che è possibile utilizzare con il dispositivo StorSimple.

* **Gli account di archiviazione generato automaticamente** : come suggerisce il nome di hello, questo tipo di account di archiviazione viene generato automaticamente quando viene creato il servizio di hello. toolearn ulteriori informazioni su come viene creato l'account di archiviazione, vedere [passaggio 1: creare un nuovo servizio](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) in [distribuire il dispositivo StorSimple locale](storsimple-8000-deployment-walkthrough-u2.md). 
* **Account di archiviazione nella sottoscrizione al servizio hello** : si tratta degli account di archiviazione di Azure hello associati hello stessa sottoscrizione di quella del servizio hello. toolearn ulteriori informazioni su come creare questi account di archiviazione, vedere [informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md). 
* **Account di archiviazione all'esterno di sottoscrizione del servizio hello** : si tratta degli account di archiviazione di Azure hello non sono associati al servizio e probabilmente hello era presente prima di servizio è stato creato.

## <a name="add-a-storage-account"></a>Aggiungere un account di archiviazione

È possibile aggiungere un account di archiviazione fornendo un univoco descrittivo accesso credenziali di nome e che sono collegati toohello account di archiviazione (provider di servizi cloud specificato hello). È anche possibile hello l'abilitazione di un canale sicuro per la comunicazione di rete tra il cloud di dispositivo e hello toocreate modalità di hello sicura sockets layer (SSL).

È possibile creare più account per un provider del servizio cloud specificato. Tenere presente, tuttavia, dopo aver creato un account di archiviazione, è possibile modificare il provider di servizi cloud hello.

Durante il salvataggio dell'account di archiviazione hello, servizio hello tenta toocommunicate con provider di servizi cloud. credenziali di Hello e dati di accesso hello fornito verrà essere autenticati in questo momento. Solo se hello autenticazione ha esito positivo, viene creato un account di archiviazione. Se l'autenticazione di hello non riesce, verrà visualizzato un messaggio di errore appropriato.

Utilizzare hello le credenziali dell'account di archiviazione di Azure tooadd le procedure seguenti:

* una credenziale dell'account di archiviazione con tooadd hello stessa sottoscrizione di Azure come servizio di Gestione periferiche hello
* una credenziale dell'account di archiviazione di Azure all'esterno di sottoscrizione del servizio di Gestione periferiche hello tooadd

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a>una credenziale dell'account di archiviazione di Azure di fuori di sottoscrizione del servizio gestione di dispositivi StorSimple hello tooadd

1. Passare tooyour servizio di gestione di dispositivi StorSimple, seleziona e fare doppio clic. Verrà visualizzata hello **Panoramica** blade.
2. Selezionare **le credenziali dell'account di archiviazione** all'interno di hello **configurazione** sezione. Elenca le credenziali di account di archiviazione esistente associate hello del servizio di gestione di dispositivi StorSimple.
3. Fare clic su **Aggiungi**.
4. In hello **aggiungere una credenziale dell'account di archiviazione** pannello hello seguenti:
   
    1. Per **Sottoscrizione** selezionare **Altro**.
   
    2. Specificare il nome di hello delle credenziali di account di archiviazione di Azure.
   
    3. In hello **chiave di accesso di account di archiviazione** casella di testo, specificare hello chiave di accesso primaria per le credenziali di account di archiviazione di Azure. tooget questa chiave, il servizio di archiviazione di Azure toohello go, selezionare le credenziali di account di archiviazione e fare clic su **la gestione delle chiavi di account**. È ora possibile copiare la chiave di accesso primaria hello.
   
    4. tooenable SSL, fare clic su hello **abilitare** pulsante toocreate un canale sicuro per la comunicazione di rete tra cloud hello e di servizio di gestione di dispositivi StorSimple. Fare clic su hello **disabilitare** pulsante solo se si sta operando all'interno di un cloud privato.
   
    5. Fare clic su **Aggiungi**. Ricevono una notifica dopo la credenziale dell'account di archiviazione hello è stato creato correttamente.

5. credenziale dell'account di archiviazione Hello appena creato viene visualizzato nel Pannello di servizio di Gestione periferiche di configurare StorSimple hello in **le credenziali dell'account di archiviazione**.
   


## <a name="edit-a-storage-account"></a>Modificare un account di archiviazione

È possibile modificare un account di archiviazione utilizzato da un contenitore di volumi. Se si modifica un account di archiviazione è attualmente in uso, hello solo campo disponibile toomodify è la chiave di accesso hello hello account di archiviazione. È possibile fornire una nuova chiave di accesso archiviazione hello e salvare le impostazioni di hello aggiornato.

#### <a name="tooedit-a-storage-account"></a>tooedit un account di archiviazione

1. Passare il servizio di gestione di dispositivi StorSimple tooyour. In hello **configurazione** fare clic su **le credenziali dell'account di archiviazione**.

    ![Credenziali dell'account di archiviazione](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. In hello **le credenziali dell'account di archiviazione** pannello, dall'elenco di hello archiviazione delle credenziali dell'account, selezionare e fare clic su uno desiderato tooedit hello. 

3. È possibile modificare hello **abilita SSL** selezione. È anche possibile fare clic su **più...**  e quindi selezionare **toorotate chiave di accesso sincronizzazione** le chiavi di accesso di account di archiviazione. Andare troppo[rotazione di account di archiviazione delle chiavi](#key-rotation-of-storage-accounts) per ulteriori informazioni su come tooperform rotazione delle chiavi. Dopo avere modificato le impostazioni di hello, fare clic su **salvare**. 

    ![Salvare le credenziali dell'account di archiviazione modificate](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. Alla richiesta di conferma fare clic su **Sì**. 

    ![Confermare le modifiche](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

le impostazioni di Hello verranno aggiornate e salvate per l'account di archiviazione. 

## <a name="delete-a-storage-account"></a>Eliminare un account di archiviazione

> [!IMPORTANT]
> È possibile eliminare un account di archiviazione solo se non viene utilizzato da un contenitore di volumi. Se un account di archiviazione è utilizzato da un contenitore di volumi, prima di eliminare il contenitore di volumi hello e quindi eliminare l'account di archiviazione hello associata.

#### <a name="toodelete-a-storage-account"></a>toodelete un account di archiviazione

1. Passare il servizio di gestione di dispositivi StorSimple tooyour. In hello **configurazione** fare clic su **le credenziali dell'account di archiviazione**.

2. Nell'elenco tabulare di hello di account di archiviazione, passare il mouse su account hello che si desidera toodelete. Menu di scelta rapida hello tooinvoke destro e fare clic su **eliminare**.

    ![Eliminare le credenziali dell'account di archiviazione](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. Quando viene richiesta la conferma, fare clic su **Sì** toocontinue con l'eliminazione di hello. Elenco tabulare Hello saranno aggiornate tooreflect hello soggetti a modifiche.

    ![Conferma dell'eliminazione](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a>Rotazione delle chiavi degli account di archiviazione

Per motivi di sicurezza, la rotazione delle chiavi è spesso un requisito nei centri dati. Ogni sottoscrizione di Microsoft Azure può essere associata a uno o più account di archiviazione. account di accesso al toothese Hello è controllato da sottoscrizione hello e chiavi di accesso per ogni account di archiviazione. 

Quando si crea un account di archiviazione, Microsoft Azure genera due chiavi di accesso di archiviazione a 512 bit utilizzati per l'autenticazione quando si accede all'account di archiviazione hello. Presenza di due chiavi di accesso di archiviazione consente chiavi hello tooregenerate senza servizio di archiviazione tooyour interruzione o del servizio di accesso toothat. chiave che è attualmente in uso Hello è hello *primario* chiave e hello chiave di backup è hello cui tooas *secondario* chiave. Una di queste due chiavi deve essere specificata quando il dispositivo StorSimple di Microsoft Azure accede al provider di servizi di archiviazione cloud.

## <a name="what-is-key-rotation"></a>Che cos'è la rotazione delle chiavi?

In genere, le applicazioni utilizzano solo uno di hello chiavi tooaccess i dati. Dopo un determinato periodo di tempo, è possibile che le applicazioni passare seconda chiave di toousing hello. Dopo avere impostato la chiave secondaria toohello di applicazioni, è possibile ritirare prima chiave hello e quindi generare una nuova chiave. L'utilizzo di due chiavi hello in questo modo consente i dati di applicazioni access toohello senza tempi di inattività.

chiavi dell'account di archiviazione Hello vengono sempre archiviate nel servizio hello in formato crittografato. Tuttavia, possono essere reimpostate mediante hello del servizio di gestione di dispositivi StorSimple. servizio di Hello può ottenere la chiave primaria di hello e chiave secondaria per tutti gli account di archiviazione nella stessa sottoscrizione, inclusi quelli creati nel servizio di archiviazione hello, nonché gli account di archiviazione predefinito hello generato hello di hello hello quando Gestione dispositivi StorSimple creazione del servizio. servizio di gestione di dispositivi StorSimple Hello otterrà sempre queste chiavi dal portale di Azure classico hello e quindi archiviarli in modo crittografato.

## <a name="rotation-workflow"></a>Flusso di lavoro di rotazione

Un amministratore di Microsoft Azure può rigenerare o modificare una chiave primaria o secondaria hello accedendo direttamente all'account di archiviazione hello (tramite il servizio di archiviazione di Microsoft Azure hello). servizio di gestione di dispositivi StorSimple Hello non rileva automaticamente questa modifica.

servizio di gestione di dispositivi StorSimple tooinform hello Roc hello, sarà necessario tooaccess servizio di gestione di dispositivi StorSimple hello, accedere hello account di archiviazione e quindi sincronizzare hello chiave primaria o secondaria (a seconda di quale è stata cambiata). servizio di Hello quindi Ottiene la chiave più recente di hello, consente di crittografare le chiavi di hello e invia hello crittografati dispositivo toohello chiave.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a>toosynchronize chiavi per gli account di archiviazione in hello stessa sottoscrizione del servizio hello 
1. Passare il servizio di gestione di dispositivi StorSimple tooyour. In hello **configurazione** fare clic su **le credenziali dell'account di archiviazione**.
2. Nell'elenco tabulare di hello di account di archiviazione, fare clic su hello uno che si desidera toomodify. 

    ![sincronizzare le chiavi](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. Fare clic su **... Ulteriori** e quindi selezionare **toorotate chiave di accesso sincronizzazione**.   

    ![sincronizzare le chiavi](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. In hello del servizio di gestione di dispositivi StorSimple, è necessario chiave hello tooupdate che è stato modificato in precedenza nel servizio di archiviazione di Microsoft Azure hello. Se la chiave di accesso primaria hello è stata cambiata (rigenerata), selezionare **primario** chiave. Se è stata modificata la chiave secondaria hello, selezionare **secondario** chiave. Fare clic su **Sincronizza chiave**.
      
      ![sincronizzare le chiavi](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

Una volta chiave hello correttamente sycnhronized si riceverà la notifica.

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize chiavi per gli account di archiviazione all'esterno di sottoscrizione del servizio hello
1. In hello **servizi** pagina, fare clic su hello **configura** scheda.
2. Fare clic su **Aggiungi/modifica account di archiviazione**.
3. Nella finestra di dialogo hello hello seguenti:
   
   1. Selezionare hello account di archiviazione con la chiave di accesso hello che si desidera tooupdate.
   2. Sarà necessario chiave di accesso di archiviazione tooupdate hello in hello del servizio di gestione di dispositivi StorSimple. In questo caso, è possibile visualizzare chiave di accesso di archiviazione hello. Immettere una nuova chiave hello in hello **Storage Account Access Key** casella. 
   3. Salvare le modifiche. La chiave di accesso dell’account di archiviazione appare aggiornata.

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-8000-security.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

