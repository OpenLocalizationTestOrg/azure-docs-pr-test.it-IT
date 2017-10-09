---
title: le credenziali dell'account di archiviazione StorSimple Virtual Array aaaManage | Documenti Microsoft
description: "Viene illustrato come è possibile utilizzare hello tooadd pagina Configura dispositivo StorSimple Manager, modificare, eliminare o le chiavi di sicurezza ruota hello per le credenziali dell'account di archiviazione associati hello Array virtuale StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>Utilizzare Gestione periferiche di StorSimple toomanage credenziali di account di archiviazione per Array virtuale StorSimple

## <a name="overview"></a>Panoramica
Hello **configurazione** sezione del Pannello di servizio di gestione di dispositivi StorSimple hello della matrice virtuale StorSimple presenta parametri del servizio globale hello che possono essere creati in hello servizio StorSimple Manager. Questi parametri possono essere applicati tooall hello dispositivi toohello servizio connesso e includono:

* Credenziali dell'account di archiviazione
* Record di controllo di accesso
  
  ![Dashboard del servizio Gestione dispositivi](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

Questa esercitazione illustra come aggiungere, modificare o eliminare le credenziali dell'account di archiviazione per l'array virtuale StorSimple. informazioni di Hello in questa esercitazione si applicano solo toohello Array virtuale StorSimple. Per informazioni su come account di archiviazione toomanage serie 8000, vedere [utilizzare account di archiviazione di toomanage servizio StorSimple Manager hello](storsimple-manage-storage-accounts.md).

Account di archiviazione di credenziali contiene credenziali hello hello dispositivo tooaccess utilizza l'account di archiviazione con il provider del servizio cloud. Per gli account di archiviazione di Microsoft Azure, queste sono le credenziali quali nome dell'account hello e chiave di accesso primaria hello.

In hello **le credenziali dell'account di archiviazione** blade, account di archiviazione di tutte le credenziali create per hello fatturazione sottoscrizione vengono visualizzate in formato tabulare che contiene le seguenti informazioni hello:

* **Nome** : hello account toohello nome univoco assegnato al momento della creazione.
* **SSL abilitato** : indica se hello SSL è abilitato e la comunicazione da dispositivo a cloud è su canale sicuro hello.
  
  ![Sezione Configurazione](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

attività più comuni di Hello correlate toostorage le credenziali dell'account che possono essere eseguite su hello **le credenziali dell'account di archiviazione** blade sono:

* Aggiungere una credenziale dell'account di archiviazione
* Modificare una credenziale dell'account di archiviazione
* Eliminare una credenziale dell'account di archiviazione

## <a name="types-of-storage-account-credentials"></a>Tipi di credenziali dell'account di archiviazione
Esistono tre tipi di credenziali dell'account di archiviazione che è possibile usare con il dispositivo StorSimple.

* **Le credenziali dell'account di archiviazione generato automaticamente** : come suggerisce il nome di hello, questo tipo di credenziale dell'account di archiviazione viene generato automaticamente quando viene creato il servizio di hello. toolearn ulteriori informazioni su come viene creata la credenziale dell'account di archiviazione, vedere [creare un nuovo servizio](storsimple-virtual-array-manage-service.md#create-a-service).
* **le credenziali dell'account di archiviazione nella sottoscrizione al servizio hello** : si tratta di account di archiviazione di Azure hello credenziali associate hello stessa sottoscrizione di quella del servizio hello. toolearn ulteriori informazioni su come creare le credenziali di account di archiviazione, vedere [informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).
* **le credenziali dell'account di archiviazione all'esterno di sottoscrizione del servizio hello** : si tratta delle credenziali dell'account di archiviazione di Azure hello non sono associati al servizio e probabilmente hello era presente prima di servizio è stato creato.

## <a name="add-a-storage-account-credential"></a>Aggiungere una credenziale dell'account di archiviazione
È possibile aggiungere una configurazione del servizio di archiviazione account credenziali tooyour dispositivo StorSimple Manager fornendo univoco descrittivo accesso credenziali di nome e che sono collegati toohello account di archiviazione. È anche possibile hello l'abilitazione di un canale sicuro per la comunicazione di rete tra il cloud di dispositivo e hello toocreate modalità di hello sicura sockets layer (SSL).

È possibile creare più account per un provider del servizio cloud specificato. Mentre credenziale dell'account di archiviazione hello viene salvato, il servizio di hello tenta toocommunicate con provider di servizi cloud. credenziali di Hello e dati di accesso hello fornite vengono autenticati in questo momento. Una credenziale dell'account di archiviazione viene creata solo se hello autenticazione ha esito positivo. Se l'autenticazione di hello non riesce, viene visualizzato un messaggio di errore appropriato.

Utilizzare hello le credenziali dell'account di archiviazione di Azure tooadd le procedure seguenti:

* una credenziale dell'account di archiviazione con tooadd hello stessa sottoscrizione di Azure come servizio di Gestione periferiche hello
* una credenziale dell'account di archiviazione di Azure all'esterno di sottoscrizione del servizio di Gestione periferiche hello tooadd

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>una credenziale dell'account di archiviazione con tooadd hello stessa sottoscrizione di Azure come servizio di Gestione periferiche hello

1. Passare tooyour del servizio di Gestione periferiche, seleziona e fare doppio clic. Verrà visualizzata hello **Panoramica** blade.
2. Selezionare **le credenziali dell'account di archiviazione** all'interno di hello **configurazione** sezione.
3. Fare clic su **Aggiungi**.
4. In hello **aggiungere un account di archiviazione** pannello hello seguenti:
   
    1. Per **Sottoscrizione** selezionare **Corrente**.
    2. Specificare il nome di hello dell'account di archiviazione di Azure.
    3. Selezionare **abilitare** toocreate un canale sicuro per la comunicazione di rete tra il cloud di dispositivo e hello StorSimple. Selezionare **Disabilita** solo se si opera all'interno di un cloud privato.
    4. Fare clic su **Aggiungi**. Ricevono una notifica dopo la creazione dell'account di archiviazione hello.<br></br>
   
        ![Aggiungere le credenziali di un account di archiviazione esistente](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>una credenziale dell'account di archiviazione di Azure all'esterno di sottoscrizione del servizio di Gestione periferiche hello tooadd

1. Passare tooyour del servizio di Gestione periferiche, seleziona e fare doppio clic. Verrà visualizzata hello **Panoramica** blade.
2. Selezionare **le credenziali dell'account di archiviazione** all'interno di hello **configurazione** sezione. Elenca le credenziali di account di archiviazione esistente associate hello del servizio di gestione di dispositivi StorSimple.
3. Fare clic su **Aggiungi**.
4. In hello **aggiungere un account di archiviazione** pannello hello seguenti:
   
    1. Per **Sottoscrizione** selezionare **Altro**.
   
    2. Specificare il nome di hello delle credenziali di account di archiviazione di Azure.
   
    3. In hello **chiave di accesso di account di archiviazione** casella di testo, specificare hello chiave di accesso primaria per le credenziali di account di archiviazione di Azure. tooget questa chiave, il servizio di archiviazione di Azure toohello go, selezionare le credenziali di account di archiviazione e fare clic su **la gestione delle chiavi di account**. È ora possibile copiare la chiave di accesso primaria hello.
   
    4. tooenable SSL, fare clic su hello **abilitare** pulsante toocreate un canale sicuro per la comunicazione di rete tra cloud hello e di servizio di gestione di dispositivi StorSimple. Fare clic su hello **disabilitare** pulsante solo se si sta operando all'interno di un cloud privato.
   
    5. Fare clic su **Aggiungi**. Ricevono una notifica dopo la credenziale dell'account di archiviazione hello è stato creato correttamente.

5. credenziale dell'account di archiviazione Hello appena creato viene visualizzato nel Pannello di servizio di Gestione periferiche di configurare StorSimple hello in **le credenziali dell'account di archiviazione**.
   
    ![Aggiungere una credenziale dell'account di archiviazione all'esterno di hello sottoscrizione al servizio Gestione dispositivi](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>Modificare una credenziale dell'account di archiviazione
È possibile modificare una credenziale dell'account di archiviazione usata dal dispositivo. Se si modifica una credenziale dell'account di archiviazione che è attualmente in uso, hello campi disponibili toomodify sono la chiave di accesso hello e modalità SSL hello per le credenziali di account di archiviazione hello. È possibile specificare una nuova chiave di accesso archiviazione hello o modificare hello **Abilita modalità SSL** selezione e salvare le impostazioni di hello aggiornato.

#### <a name="tooedit-a-storage-account-credential"></a>tooedit una credenziale dell'account di archiviazione
1. Passare tooyour del servizio di Gestione periferiche, seleziona e fare doppio clic. Verrà visualizzata hello **Panoramica** blade.
2. Selezionare **le credenziali dell'account di archiviazione** all'interno di hello **configurazione** sezione. Elenca le credenziali di account di archiviazione esistente associate hello del servizio di gestione di dispositivi StorSimple.
3. Nell'elenco tabulare di hello delle credenziali di account di archiviazione, selezionare e fare doppio clic su account hello che si desidera toomodify.
4. In credenziali dell'account di archiviazione hello **proprietà** pannello hello seguenti:
   
   1. Se necessario, è possibile modificare hello **abilita SSL** la selezione della modalità.
   2. È possibile scegliere tooregenerate le chiavi di accesso delle credenziali di account di archiviazione. Per ulteriori informazioni, vedere [Rigenera chiavi dell'account di archiviazione hello](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys). Fornire hello nuova archiviazione delle credenziali chiave dell'account. Per un account di archiviazione di Azure, questa è la chiave di accesso primaria hello.
   3. Fare clic su **salvare** nella parte superiore di hello di hello **proprietà** impostazioni hello toosave di blade. aggiornamento delle impostazioni di Hello in hello **le credenziali dell'account di archiviazione** blade.
      
      ![Modificare una credenziale dell'account di archiviazione](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>Eliminare una credenziale dell'account di archiviazione
> [!IMPORTANT]
> È possibile eliminare una credenziale dell'account di archiviazione solo se non è in uso. Se una credenziale dell'account di archiviazione è in uso, si riceve una notifica.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete una credenziale dell'account di archiviazione
1. Passare tooyour del servizio di Gestione periferiche, seleziona e fare doppio clic. Verrà visualizzata hello **Panoramica** blade.
2. Selezionare **le credenziali dell'account di archiviazione** all'interno di hello **configurazione** sezione. Elenca le credenziali di account di archiviazione esistente associate hello del servizio di gestione di dispositivi StorSimple.
3. Nell'elenco tabulare di hello delle credenziali di account di archiviazione, selezionare e fare doppio clic su account hello che si desidera toodelete.
4. In credenziali dell'account di archiviazione hello **proprietà** pannello hello seguenti:
   
   1. Fare clic su **eliminare** credenziali hello toodelete.
   2. Quando viene richiesta la conferma, fare clic su **Sì** toocontinue con l'eliminazione di hello. Elenco tabulare Hello è aggiornato tooreflect hello modifiche.
      
      ![Eliminare una credenziale dell'account di archiviazione](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>Sincronizzazione delle chiavi della credenziale dell'account di archiviazione esistente
Per motivi di sicurezza, la rotazione delle chiavi è spesso un requisito nei centri dati. Un amministratore di Microsoft Azure può rigenerare o modificare chiave primaria o secondaria hello accedendo direttamente alla credenziale dell'account di archiviazione hello (tramite il servizio di archiviazione di Microsoft Azure hello). servizio di gestione di dispositivi StorSimple Hello non rileva automaticamente questa modifica.

servizio di gestione di dispositivi StorSimple tooinform hello Roc hello, è necessario del servizio di gestione di dispositivi StorSimple hello tooaccess, accesso hello archiviazione delle credenziali dell'account e quindi sincronizzare hello chiave primaria o secondaria (a seconda di quale è stata cambiata). servizio di Hello quindi Ottiene la chiave più recente di hello, consente di crittografare le chiavi di hello e invia hello crittografati dispositivo toohello chiave.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>hello di chiavi toosynchronize per le credenziali dell'account di archiviazione nella stessa sottoscrizione del servizio hello (solo Azure)
1. Nel Pannello di destinazione del servizio di hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi in hello **configurazione** fare clic su **le credenziali dell'account di archiviazione**.
2. In hello **le credenziali dell'account di archiviazione** pannello hello selezionare nell'elenco di credenziali di account di archiviazione, credenziali dell'account di archiviazione hello le cui chiavi che si desidera toosynchronize.
3. In hello **proprietà** pannello hello selezionata credenziale dell'account di archiviazione, hello seguenti:
   
    1. Fare clic su **Altro**, quindi su **Sincronizza chiave di accesso**.
   
    2. Quando viene richiesta la conferma, fare clic su **Sincronizza chiave** sincronizzazione hello toocomplete.
    
4. In hello del servizio di gestione di dispositivi StorSimple, è necessario chiave hello tooupdate che è stato modificato in precedenza nel servizio di archiviazione di Microsoft Azure hello. In hello **Sincronizza chiave dell'account di archiviazione** pannello, se la chiave di accesso primaria hello è stata cambiata (rigenerata), fare clic su primario e quindi fare clic su **Sincronizza chiave**. Se la chiave secondaria hello è stata modificata, fare clic su **secondario**, quindi fare clic su **Sincronizza chiave**.
   
    ![Sincronizzare la chiave di accesso](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[amministrare l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).

