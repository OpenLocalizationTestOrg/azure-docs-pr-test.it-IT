---
title: aaaManage l'account di archiviazione StorSimple | Documenti Microsoft
description: "Viene illustrato come è possibile utilizzare hello tooadd pagina Configura StorSimple Manager, modificare, eliminare o le chiavi di sicurezza hello Ruota per un account di archiviazione."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a>Utilizzare toomanage servizio StorSimple Manager di hello account di archiviazione
## <a name="overview"></a>Panoramica
Hello **configura** pagina presenta tutti i parametri di servizio globale hello che possono essere creati in hello servizio StorSimple Manager. Questi parametri possono essere applicati tooall hello dispositivi toohello servizio connesso e includono:

* Account di archiviazione 
* Modelli di larghezza di banda 
* Record di controllo di accesso 

In questa esercitazione viene illustrato come utilizzare hello **configura** pagina tooadd, modificare o eliminare gli account di archiviazione o ruotare le chiavi di sicurezza hello per un account di archiviazione.

 ![Pagina Configura](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

Gli account di archiviazione contengono le credenziali hello hello tooaccess di dispositivo utilizza l'account di archiviazione con il provider del servizio cloud. Per gli account di archiviazione di Microsoft Azure, queste sono le credenziali quali nome dell'account hello e chiave di accesso primaria hello. 

In hello **configura** pagina archiviazione di tutti gli account creati per hello fatturazione sottoscrizione vengono visualizzati in formato tabulare che contiene le seguenti informazioni hello:

* **Nome** : hello account toohello nome univoco assegnato al momento della creazione.
* **SSL abilitato** : indica se hello SSL è abilitato e la comunicazione da dispositivo a cloud è su canale sicuro hello.
* **Utilizzato da** : numero di volumi che usano l'account di archiviazione hello hello.

attività più comuni di Hello correlate toostorage account che possono essere eseguite su hello **configura** sono:

* Aggiungere un account di archiviazione 
* Modificare un account di archiviazione 
* Eliminare un account di archiviazione 
* Rotazione delle chiavi degli account di archiviazione 

## <a name="types-of-storage-accounts"></a>Tipi di account di archiviazione
Esistono tre tipi di account di archiviazione che è possibile utilizzare con il dispositivo StorSimple.

* **Gli account di archiviazione generato automaticamente** : come suggerisce il nome di hello, questo tipo di account di archiviazione viene generato automaticamente quando viene creato il servizio di hello. toolearn ulteriori informazioni su come viene creato l'account di archiviazione, vedere [passaggio 1: creare un nuovo servizio](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) in [distribuire il dispositivo StorSimple locale](storsimple-deployment-walkthrough.md). 
* **Account di archiviazione nella sottoscrizione al servizio hello** : si tratta degli account di archiviazione di Azure hello associati hello stessa sottoscrizione di quella del servizio hello. toolearn ulteriori informazioni su come creare questi account di archiviazione, vedere [informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md). 
* **Account di archiviazione all'esterno di sottoscrizione del servizio hello** : si tratta degli account di archiviazione di Azure hello non sono associati al servizio e probabilmente hello era presente prima di servizio è stato creato.

## <a name="add-a-storage-account"></a>Aggiungere un account di archiviazione
È possibile aggiungere un account di archiviazione fornendo un univoco descrittivo accesso credenziali di nome e che sono collegati toohello account di archiviazione (provider di servizi cloud specificato hello). È anche possibile hello l'abilitazione di un canale sicuro per la comunicazione di rete tra il cloud di dispositivo e hello toocreate modalità di hello sicura sockets layer (SSL).

È possibile creare più account per un provider del servizio cloud specificato. Tenere presente, tuttavia, dopo aver creato un account di archiviazione, è possibile modificare il provider di servizi cloud hello.

Durante il salvataggio dell'account di archiviazione hello, servizio hello tenta toocommunicate con provider di servizi cloud. credenziali di Hello e dati di accesso hello fornito verrà essere autenticati in questo momento. Solo se hello autenticazione ha esito positivo, viene creato un account di archiviazione. Se l'autenticazione di hello non riesce, verrà visualizzato un messaggio di errore appropriato.

Gli account di archiviazione di Resource Manager creati nel portale di Azure sono supportati anche con StorSimple. Gestione risorse di account di archiviazione non verranno riportata nell'elenco a discesa hello per la selezione durante il tentativo di un contenitore di volumi, toocreate Hello hello solo archiviazione, verranno visualizzati gli account creati nel portale di Azure classico hello. Account di archiviazione di gestione risorse sarà necessario toobe aggiunti utilizzando hello procedure tooadd un account di archiviazione descritto di seguito.

> [!NOTE]
> procedura di Hello per l'aggiunta di un account di archiviazione varia in base a una versione del software StorSimple hello in uso. Impossibile verificare toofollow hello stored procedure corretta per la versione di StorSimple.
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>Modificare un account di archiviazione
È possibile modificare un account di archiviazione utilizzato da un contenitore di volumi. Se si modifica un account di archiviazione è attualmente in uso, hello solo campo disponibile toomodify è la chiave di accesso hello hello account di archiviazione. È possibile fornire una nuova chiave di accesso archiviazione hello e salvare le impostazioni di hello aggiornato.

#### <a name="tooedit-a-storage-account"></a>tooedit un account di archiviazione
1. Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul nome del servizio hello e quindi fare clic su **configura**.
2. Fare clic su **Aggiungi/modifica account di archiviazione**.
3. In hello **Aggiungi/Modifica account di archiviazione** la finestra di dialogo:
   
   1. Nell'elenco a discesa hello di **gli account di archiviazione**, scegliere un account esistente che si desidera toomodify. Questo può anche includere gli account di archiviazione hello che sono stati generati automaticamente quando il servizio di hello prima di tutto è stato creato.
   2. Se necessario, è possibile modificare hello **Abilita modalità SSL** selezione.
   3. È possibile scegliere toorotate le chiavi di accesso di account di archiviazione. Vedere [rotazione di account di archiviazione delle chiavi](#key-rotation-of-storage-accounts) per ulteriori informazioni su come tooperform rotazione delle chiavi.
   4. Fare clic sull'icona di controllo hello ![il segno di spunta](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) impostazioni hello toosave. le impostazioni di Hello verranno aggiornate in hello **configura** pagina. Fare clic su **salvare** toosave hello appena le impostazioni aggiornate.
      
      ![Modificare un account di archiviazione](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>Eliminare un account di archiviazione
> [!IMPORTANT]
> È possibile eliminare un account di archiviazione solo se non viene utilizzato da un contenitore di volumi. Se un account di archiviazione è utilizzato da un contenitore di volumi, prima di eliminare il contenitore di volumi hello e quindi eliminare l'account di archiviazione hello associata.
> 
> 

#### <a name="toodelete-a-storage-account"></a>toodelete un account di archiviazione
1. Nella pagina di destinazione del servizio StorSimple Manager hello, selezionare il servizio, fare doppio clic sul nome del servizio hello e quindi fare clic su **configura**.
2. Nell'elenco tabulare di hello di account di archiviazione, passare il mouse su account hello che si desidera toodelete.
3. Un'icona di eliminazione (**x**) verrà visualizzato nella colonna destra estrema hello per tale account di archiviazione. Fare clic su hello **x** credenziali hello toodelete di icona.
4. Quando viene richiesta la conferma, fare clic su **Sì** toocontinue con l'eliminazione di hello. Elenco tabulare Hello saranno aggiornate tooreflect hello soggetti a modifiche.

## <a name="key-rotation-of-storage-accounts"></a>Rotazione delle chiavi degli account di archiviazione
Per motivi di sicurezza, la rotazione delle chiavi è spesso un requisito nei centri dati. 

> [!NOTE]
> procedura di rotazione di informazioni e hello rotazione delle chiavi di Hello applica tooMicrosoft solo gli account di archiviazione di Azure. Se si usa un altro provider di servizi cloud, è possibile gestire le chiavi degli account di archiviazione tramite il dashboard di tale provider.
> 
> 

Ogni sottoscrizione di Microsoft Azure può essere associata a uno o più account di archiviazione. account di accesso al toothese Hello è controllato da sottoscrizione hello e chiavi di accesso per ogni account di archiviazione. 

Quando si crea un account di archiviazione, Microsoft Azure genera due chiavi di accesso di archiviazione a 512 bit utilizzati per l'autenticazione quando si accede all'account di archiviazione hello. Presenza di due chiavi di accesso di archiviazione consente chiavi hello tooregenerate senza servizio di archiviazione tooyour interruzione o del servizio di accesso toothat. chiave che è attualmente in uso Hello è hello *primario* chiave e hello chiave di backup è hello cui tooas *secondario* chiave. Una di queste due chiavi deve essere specificata quando il dispositivo StorSimple di Microsoft Azure accede al provider di servizi di archiviazione cloud.

## <a name="what-is-key-rotation"></a>Che cos'è la rotazione delle chiavi?
In genere, le applicazioni utilizzano solo uno di hello chiavi tooaccess i dati. Dopo un determinato periodo di tempo, è possibile che le applicazioni passare seconda chiave di toousing hello. Dopo avere impostato la chiave secondaria toohello di applicazioni, è possibile ritirare prima chiave hello e quindi generare una nuova chiave. L'utilizzo di due chiavi hello in questo modo consente i dati di applicazioni access toohello senza tempi di inattività.

chiavi dell'account di archiviazione Hello vengono sempre archiviate nel servizio hello in formato crittografato. Tuttavia, possono essere reimpostate mediante hello servizio StorSimple Manager. servizio di Hello può ottenere la chiave primaria di hello e chiave secondaria per tutti gli account di archiviazione nella stessa sottoscrizione, inclusi quelli creati nel servizio di archiviazione hello, nonché gli account di archiviazione predefinito hello generato hello di hello hello quando il servizio StorSimple Manager servizio di creazione. servizio StorSimple Manager Hello otterrà sempre queste chiavi dal portale di Azure classico hello e quindi archiviarli in modo crittografato.

## <a name="rotation-workflow"></a>Flusso di lavoro di rotazione
Un amministratore di Microsoft Azure può rigenerare o modificare una chiave primaria o secondaria hello accedendo direttamente all'account di archiviazione hello (tramite il servizio di archiviazione di Microsoft Azure hello). Hello servizio StorSimple Manager non rileva automaticamente questa modifica.

servizio StorSimple Manager di hello tooinform Roc hello, sarà necessario servizio StorSimple Manager di hello tooaccess, accedere hello account di archiviazione e quindi sincronizzare hello chiave primaria o secondaria (a seconda di quale è stata cambiata). servizio di Hello quindi Ottiene la chiave più recente di hello, consente di crittografare le chiavi di hello e invia hello crittografati dispositivo toohello chiave.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a>toosynchronize chiavi per gli account di archiviazione in hello stessa sottoscrizione del servizio hello (solo Azure)
1. In hello **servizi** pagina, fare clic su hello **configura** scheda.
2. Fare clic su **Aggiungi/modifica account di archiviazione**.
3. Nella finestra di dialogo hello hello seguenti:
   
   1. Selezionare hello account di archiviazione con chiave hello che si desidera toosynchronize. chiavi dell'account di archiviazione Hello vengono crittografate quando vengono visualizzati.
   2. In hello servizio StorSimple Manager, è necessario chiave hello tooupdate che è stato modificato in precedenza nel servizio di archiviazione di Microsoft Azure hello. Se la chiave di accesso primaria hello è stata cambiata (rigenerata), fare clic su **Sincronizza chiave primaria**. Se la chiave secondaria hello è stata modificata, fare clic su **Sincronizza chiave secondaria**.
      
      ![sincronizzare le chiavi](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize chiavi per gli account di archiviazione all'esterno di sottoscrizione del servizio hello
1. In hello **servizi** pagina, fare clic su hello **configura** scheda.
2. Fare clic su **Aggiungi/modifica account di archiviazione**.
3. Nella finestra di dialogo hello hello seguenti:
   
   1. Selezionare hello account di archiviazione con la chiave di accesso hello che si desidera tooupdate.
   2. Sarà necessario chiave di accesso di archiviazione tooupdate hello in hello servizio StorSimple Manager. In questo caso, è possibile visualizzare chiave di accesso di archiviazione hello. Immettere una nuova chiave hello in hello **Storage Account Access Key**casella y. 
   3. Salvare le modifiche. La chiave di accesso dell’account di archiviazione appare aggiornata.

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla [sicurezza di StorSimple](storsimple-security.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

