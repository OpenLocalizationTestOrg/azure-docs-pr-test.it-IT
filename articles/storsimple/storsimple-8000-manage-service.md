---
title: hello aaaDeploy servizio di gestione di dispositivi StorSimple in Azure | Documenti Microsoft
description: Viene illustrato come toocreate e delete hello del servizio di gestione di dispositivi StorSimple nel portale di Azure hello e descrive come toomanage hello chiave di registrazione del servizio.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Distribuire il servizio di gestione di dispositivi StorSimple hello per dispositivi della serie StorSimple 8000

## <a name="overview"></a>Panoramica

servizio di gestione di dispositivi StorSimple Hello in esecuzione in Microsoft Azure e si connette dispositivi StorSimple toomultiple. Dopo aver creato il servizio di hello, è possibile utilizzare il toomanage tutti i dispositivi che sono connesso toohello dispositivo StorSimple Manager hello del servizio da un'unica posizione centrale, riducendo così al minimo carico amministrativo.

Questa esercitazione vengono descritti i passaggi di hello necessari per hello creazione, eliminazione, la migrazione del servizio hello e la gestione di hello hello servizio chiave di registrazione. informazioni di Hello contenute in questo articolo sono applicabile solo dispositivi della serie 8000 tooStorSimple. Per ulteriori informazioni su StorSimple Virtual Array, andare troppo[distribuire un servizio di gestione di dispositivi StorSimple per l'Array virtuale StorSimple](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Creare un servizio
toocreate un servizio di gestione di dispositivi StorSimple, è necessario toohave:

* Una sottoscrizione con un contratto Enterprise Agreement
* Un account di archiviazione di Microsoft Azure attivo
* le informazioni di fatturazione che viene utilizzate per la gestione accessi Hello

Sono consentite solo le sottoscrizioni di hello con un contratto Enterprise Agreement. Le sottoscrizioni di Microsoft Sponsorship che sono state consentite nel portale di Azure classico hello non sono supportate nel portale di Azure hello. Verrà visualizzato hello segue messaggio quando si utilizza una sottoscrizione non supportata:

![Sottoscrizione non valida](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

È inoltre possibile toogenerate un account di archiviazione predefinito quando si crea il servizio di hello.

Un singolo servizio può gestire più dispositivi, ma un dispositivo non può estendersi a più servizi. Una grande organizzazione può avere più toowork di istanze di servizio con diverse sottoscrizioni, organizzazioni o anche percorsi di distribuzione. 

> [!NOTE]
> È necessario istanze separate di dispositivi della serie StorSimple 8000 toomanage servizio StorSimple Manager di dispositivi e le matrici virtuale StorSimple.

Eseguire hello seguendo i passaggi toocreate un servizio.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Per ogni servizio di gestione di dispositivi StorSimple, presenti hello gli attributi seguenti:

* **Nome** – nome hello assegnato al servizio di gestione di dispositivi StorSimple tooyour quando è stata creata. **Impossibile modificare il nome del servizio Hello dopo aver creato il servizio di hello. Questo vale anche per altre entità, ad esempio i dispositivi, volumi, contenitori di volumi e criteri di backup che non possono essere rinominati in hello portale di Azure.**
* **Stato** : hello lo stato del servizio di hello, che può essere **Active**, **creazione**, o **Online**.
* **Percorso** : hello posizione geografica in cui hello StorSimple dispositivo verrà distribuito.
* **Sottoscrizione** : hello sottoscrizione a cui è associato al servizio di fatturazione.

## <a name="move-a-service-tooazure-portal"></a>Spostare un portale del servizio tooAzure
StorSimple serie 8000 possono essere ora gestiti in hello portale di Azure. Se si dispone di un dispositivi StorSimple hello toomanage servizio esistente, è consigliabile spostare i toohello servizio portale di Azure. Dopo il 30 settembre 2017 Hello portale di Azure classico per hello servizio StorSimple Manager non è disponibile.

Hello opzione toomigrate toohello portale di Azure è disponibile in fasi. Se non viene visualizzato un portale di tooAzure toomigrate opzione ma si desidera toomove e aver esaminato impatto hello della migrazione, come documentato in hello [considerazioni per la transizione](#considerations-for-transition), è possibile [inviare una richiesta](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Considerazioni per la transizione

Esaminare l'impatto di hello della migrazione toohello nuovo portale di Azure prima di spostare il servizio di hello.

#### <a name="before-you-transition"></a>Prima di eseguire la transizione

* Nel dispositivo è installato l'aggiornamento 3.0 o versione successiva. Se il dispositivo è in esecuzione una versione precedente, installare gli aggiornamenti più recenti di hello. Per ulteriori informazioni, visitare troppo[installare l'aggiornamento 4](storsimple-8000-install-update-4.md). Se si usa un'appliance cloud StorSimple (8010/8020), creare una nuova appliance cloud con l'aggiornamento 4.0. 

* Dopo avere passato toohello nuovo portale di Azure, è possibile utilizzare il dispositivo StorSimple hello Azure toomanage portale classico.

* transizione Hello è non comportano interruzioni del servizio e nessun tempo di inattività per il dispositivo hello.

* Tutti i gestori di dispositivo StorSimple hello in hello specificato sottoscrizione viene eseguita la transizione.

#### <a name="during-hello-transition"></a>Durante la transizione hello

* È possibile gestire il dispositivo dal portale hello.
* Operazioni quali backup pianificati e suddivisione in livelli continuano toooccur.
* Non eliminare hello precedente StorSimple Device Managers mentre è in corso una transizione hello.

#### <a name="after-hello-transition"></a>Dopo la transizione hello

* Non è più, è possibile gestire i dispositivi dal portale classico hello.

* cmdlet PowerShell di Azure Service Management (ASM) di Hello esistenti non sono supportati. Aggiornare hello script toomanage i dispositivi tramite hello Azure Resource Manager.

* La configurazione di servizi e dispositivi viene mantenuta. Tutti i volumi e i backup sono anche toohello transizione portale di Azure.

### <a name="begin-transition"></a>Iniziare la transizione

Eseguire hello seguendo i passaggi tootransition il toohello servizio portale di Azure.

1. Passare tooyour del servizio StorSimple Manager esistenti nel portale classico hello.

2. Viene visualizzata una notifica che informa che il servizio di gestione di dispositivi StorSimple hello è ora disponibile nel portale di Azure hello. Si noti che in hello portale di Azure, servizio hello tooas di cui si fa riferimento il servizio di gestione di dispositivi StorSimple.

    ![Notifica della migrazione](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Assicurarsi di aver esaminato hello dettagliate sull'effettivo impatto della migrazione.
    2. Esaminare l'elenco di hello di StorSimple Manager di dispositivi che verranno spostati dal portale classico hello.

3. Fare clic su **Esegui la migrazione**. transizione Hello viene avviata e richiede pochi minuti toocomplete.

Una volta completata la transizione hello, è possibile gestire i dispositivi tramite il servizio di gestione di dispositivi StorSimple nel portale di Azure hello hello.

Nel portale di Azure hello, hello solo i dispositivi StorSimple esegue Update 3.0 e versioni successive sono supportati. i dispositivi di Hello che eseguono versioni meno recenti hanno un supporto limitato. Hello nella seguente tabella summrizes quali operazioni sono supportate nel dispositivo hello in esecuzione versios precedente tooUpdate 3.0, dopo che sono stati migrati da hello classic toohello portale di Azure.

| Operazione                                                                                                                       | Supportato      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Registrare un dispositivo                                                                                                               | Sì            |
| Configurare le impostazioni di dispositivo, ad esempio le caratteristiche generali, la rete e la sicurezza                                                                | Sì            |
| Analizzare, scaricare e installare aggiornamenti                                                                                             | Sì            |
| Disattivare un dispositivo                                                                                                               | Sì            |
| Eliminare un dispositivo                                                                                                                   | Sì            |
| Creare, modificare ed eliminare un contenitore di volumi                                                                                   | No             |
| Creare, modificare ed eliminare un volume                                                                                             | No             |
| Creare, modificare ed eliminare criteri di backup                                                                                      | No             |
| Creazione di un backup manuale                                                                                                            | No             |
| Eseguire un backup pianificato                                                                                                         | Non applicabile |
| Eseguire il ripristino da un set di backup                                                                                                        | No             |
| Dispositivo tooa clone esecuzione Update 3.0 e versioni successive <br> dispositivo di origine Hello è in esecuzione tooUpdate precedente versione 3.0.                                | Sì            |
| Clonare tooa dispositivi che eseguono versioni precedenti tooUpdate 3.0                                                                          | No             |
| Eseguire il failover del dispositivo di origine <br> (da un dispositivo esegue versione preliminare tooUpdate 3.0 tooa dispositivo che esegue Update 3.0 e versioni successive)                                                               | Sì            |
| Eseguire il failover del dispositivo di destinazione <br> (tooa dispositivo che esegue software tooUpdate precedente di versione 3.0)                                                                                   | No             |
| Cancellare un avviso                                                                                                                  | Sì            |
| Visualizzare criteri di backup, catalogo di backup, volumi, contenitori di volumi, grafici di monitoraggio, processi e avvisi creati nel portale classico | Sì            |
| Attivare e disattivare i controller dei dispositivi                                                                                              | Sì            |


## <a name="delete-a-service"></a>Eliminare un servizio

Prima di eliminare un servizio, verificare che non sia usato da dispositivi connessi. Se il servizio di hello è in uso, disattivare i dispositivi connesso hello. operazione di disattivazione Hello dividere hello connessione tra il dispositivo di hello e servizio hello, ma conservare i dati del dispositivo hello nel cloud hello.

> [!IMPORTANT]
> Dopo l'eliminazione di un servizio, operazione hello non può essere annullata. Qualsiasi dispositivo che utilizza il servizio hello deve toobe reimpostazione toofactory predefiniti prima di poter essere utilizzato con un altro servizio. In questo scenario, i dati locali di hello sul dispositivo hello, nonché la configurazione di hello, viene persa.

Eseguire hello seguendo i passaggi toodelete un servizio.

### <a name="toodelete-a-service"></a>toodelete un servizio

1. Ricerca per servizio hello desiderato toodelete. Fare clic su **risorse** icona e quindi input hello toosearch termini appropriati. Nei risultati della ricerca hello, fare clic su servizio hello da toodelete.

    ![Ricerca servizio toodelete](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Consente di procedere pannello servizio di gestione di dispositivi StorSimple toohello. Fare clic su **Elimina**.

    ![Delete service](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Fare clic su **Sì** nella notifica di conferma hello. Potrebbe richiedere alcuni minuti per hello servizio toobe eliminato.

    ![Confermare l'eliminazione](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Ottenere una chiave di registrazione del servizio hello

Dopo avere creato un servizio, è necessario tooregister dispositivo StorSimple con servizio hello. tooregister del primo dispositivo StorSimple, si sarà necessario hello chiave di registrazione del servizio. tooregister ulteriori dispositivi con un servizio StorSimple esistente, è necessario che sia la chiave di registrazione hello e hello chiave DEK del servizio (che viene generato nel primo dispositivo hello durante la registrazione). Per ulteriori informazioni sulla chiave di crittografia di hello servizio dati, vedere [sicurezza in StorSimple](storsimple-8000-security.md). È possibile ottenere la chiave di registrazione hello accedendo **chiavi** nel pannello del dispositivo StorSimple Manager.

Eseguire hello seguendo i passaggi tooget hello chiave di registrazione.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Mantenere una chiave di registrazione del servizio hello in un luogo sicuro. Sarà necessario questa chiave, nonché hello chiave DEK del servizio, tooregister ulteriori dispositivi con questo servizio. Dopo aver ottenuto una chiave di registrazione del servizio hello, è necessario configurare il dispositivo tramite hello Windows PowerShell per StorSimple interfaccia.

Per informazioni dettagliate su come toouse questa chiave, vedere registrazione [passaggio 3: configurare e registrare il dispositivo hello tramite Windows PowerShell per StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Rigenerare la chiave di registrazione del servizio hello
Se si è obbligatorio tooperform rotazione delle chiavi o se l'elenco di hello degli amministratori del servizio è stato modificato, è necessario tooregenerate una chiave di registrazione del servizio. Quando si rigenera la chiave hello, nuova chiave hello viene utilizzato solo per registrare i dispositivi successivi. i dispositivi Hello già registrati sono interessati da questo processo.

Eseguire hello seguendo i passaggi tooregenerate una chiave di registrazione del servizio.

### <a name="tooregenerate-hello-service-registration-key"></a>chiave di registrazione del servizio hello tooregenerate
1. In hello **Gestione dispositivi StorSimple** pannello andare troppo**Management &gt;**  **chiavi**.
    
    ![Pannello Chiavi](./media/storsimple-8000-manage-service/regenregkey2.png)

2. In hello **chiavi** pannello, fare clic su **rigenerare**.

    ![Fare clic su Rigenera](./media/storsimple-8000-manage-service/regenregkey3.png)
3. In hello **Rigenera chiave di registrazione** pannello revisione hello azione necessaria per la hello chiavi vengono rigenerate. Tutti i dispositivi successivi hello che sono registrati con questo servizio utilizzano nuova chiave di registrazione hello. Fare clic su **rigenerare** tooconfirm. Ricevono una notifica al termine della rigenerazione hello.

    ![Confermare la rigenerazione](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Verrà visualizzata una nuova chiave di registrazione del servizio.

5. Copiare la chiave e salvarla per registrare eventuali nuovi dispositivi con il servizio.



## <a name="change-hello-service-data-encryption-key"></a>Modifica chiave DEK del servizio hello
Le chiavi DEK del servizio sono utilizzati tooencrypt dati confidenziali, ad esempio credenziali dell'account di archiviazione, che vengono inviati dal dispositivo StorSimple toohello servizio StorSimple Manager. Sarà necessario toochange queste chiavi periodicamente se l'organizzazione IT con un criterio di rotazione delle chiavi su dispositivi di archiviazione hello. Hello il processo di modifica può essere variare leggermente a seconda se sussiste una o più dispositivi gestiti dal servizio StorSimple Manager hello. Per ulteriori informazioni, visitare troppo[StorSimple sicurezza e protezione dei dati](storsimple-8000-security.md).

Modifica hello chiave DEK del servizio sono un processo passaggio 3:

1. Utilizza script di Windows PowerShell per Gestione risorse di Azure, autorizzare una dispositivo toochange hello chiave DEK del servizio.
2. Utilizzo di Windows PowerShell per StorSimple, avviare hello servizio modifica della chiave DEK.
3. Se si dispone di più di un dispositivo StorSimple, hello chiave DEK del servizio su hello aggiornare altri dispositivi.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>Passaggio 1: Utilizzo di Windows PowerShell script tooAuthorize una dispositivo toochange hello chiave DEK del servizio
Amministratore del dispositivo hello richiede in genere, tale amministratore del servizio hello autorizzare un dispositivo toochange crittografia le chiavi del servizio. amministratore del servizio Hello autorizza quindi chiave hello toochange del dispositivo hello.

Questo passaggio viene eseguito tramite script di gestione risorse di Azure basato su hello. amministratore del servizio Hello è possibile selezionare un dispositivo idoneo toobe autorizzato. dispositivo di Hello è quindi il processo di modifica della chiave DEK del servizio autorizzato toostart hello. 

Per ulteriori informazioni sull'utilizzo di script hello, andare troppo[Authorize ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Quali dispositivi possono essere autorizzate toochange chiavi DEK del servizio?
Un dispositivo deve soddisfare i seguenti criteri prima di poter essere autorizzato tooinitiate servizio modifica della chiave DEK hello:

* dispositivo di Hello deve essere online toobe idonei per l'autorizzazione di modifica della chiave di servizio dati crittografia.
* È possibile autorizzare hello stesso dispositivo nuovamente dopo 30 minuti se la chiave hello modifica non è stato avviato.
* È possibile autorizzare un dispositivo diverso, purché modifica della chiave hello non è stata avviata dal dispositivo autorizzato in precedenza hello. Dopo che è stato autorizzato alla nuova periferica hello, dispositivo precedente hello Impossibile iniziare la modifica di hello.
* Non è possibile autorizzare un dispositivo mentre è in corso hello rollover della chiave DEK del servizio hello.
* È possibile autorizzare un dispositivo quando alcuni dispositivi hello registrati con il servizio hello hanno eseguito il rollover crittografia hello ma non per altri utenti. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Passaggio 2: Utilizzo di Windows PowerShell per StorSimple tooinitiate hello servizio modifica della chiave DEK
Questo passaggio viene eseguito in hello Windows PowerShell per StorSimple interfaccia hello autorizzato dispositivo StorSimple.

> [!NOTE]
> Alcun operazioni non possono essere eseguite nel portale di Azure del servizio StorSimple Manager hello fino al completamento di rollover della chiave hello.
> 
> 

Se si utilizza l'interfaccia di Windows PowerShell toohello hello dispositivo console seriale tooconnect, eseguire hello alla procedura seguente.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>modifica della chiave DEK del servizio tooinitiate hello
1. Selezionare l'opzione 1 toolog nella con accesso completo.
2. Al prompt dei comandi di hello, digitare:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Al termine hello cmdlet, si otterrà una nuova chiave DEK del servizio. Copiare e salvare la chiave per l'uso nel passaggio 3 di questo processo. Questa chiave verrà usata tooupdate hello tutti i dispositivi registrati con il servizio StorSimple Manager hello rimanenti.
   
   > [!NOTE]
   > Questo processo deve essere avviato entro quattro ore dall'autorizzazione di un dispositivo StorSimple.
   > 
   > 
   
   La nuova chiave viene quindi inviata toohello servizio toobe inserito tooall hello di dispositivi registrati con il servizio di hello. Un avviso verrà quindi visualizzati nel dashboard del servizio hello. servizio Hello disabiliterà tutte le operazioni di hello nei dispositivi registrato hello e amministratore del dispositivo hello sarà quindi necessario tooupdate hello chiave DEK del servizio su hello altri dispositivi. Tuttavia, hello i/o (host di invio di dati nel cloud toohello) non verranno compromesse.
   
   Se dispone di un singolo dispositivo registrato tooyour servizio, il processo di rollover hello è stato completato ed è possibile ignorare il passaggio di hello. Se si dispone di più dispositivi registrati tooyour servizio, procedere toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Passaggio 3: Aggiornare hello chiave DEK del servizio su altri dispositivi StorSimple
Se si dispone di più dispositivi registrati tooyour StorSimple Manager servizio, è necessario effettuare questi passaggi nell'interfaccia di Windows PowerShell hello del dispositivo StorSimple. chiave di Hello ottenuto nel passaggio 2 deve essere utilizzato tooupdate tutti hello rimanenti dispositivo StorSimple registrato con hello servizio StorSimple Manager.

Eseguire hello dopo la crittografia dei dati di passaggi tooupdate hello servizio nel dispositivo.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>chiave di crittografia tooupdate hello servizio dati
1. Usare Windows PowerShell per StorSimple tooconnect toohello console. Selezionare l'opzione 1 toolog nella con accesso completo.
2. Al prompt dei comandi di hello, digitare:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Fornire hello chiave DEK del servizio ottenuta nel [passaggio 2: utilizzo di Windows PowerShell per StorSimple tooinitiate hello servizio modifica della chiave DEK](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su hello [il processo di distribuzione di StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* Ulteriori informazioni sulla [gestione dell'account di archiviazione di StorSimple](storsimple-8000-manage-storage-accounts.md).
* Per ulteriori informazioni su troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).
