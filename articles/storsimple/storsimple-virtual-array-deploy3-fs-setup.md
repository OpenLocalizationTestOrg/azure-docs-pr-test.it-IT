---
title: aaaSet di StorSimple Array virtuale file server | Documenti Microsoft
description: Questa terza esercitazione nella distribuzione di StorSimple Virtual Array indica tooset un dispositivo virtuale come file server.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>Distribuire l'array virtuale StorSimple: configurare come file server tramite il portale di Azure
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>Introduzione
Questo articolo descrive come tooperform la configurazione iniziale, registrare il server di file di StorSimple, l'installazione dispositivo completa hello e creare e collegare tooSMB condivisioni. Si tratta di hello ultimo articolo hello serie di esercitazioni per la distribuzione necessaria toocompletely distribuire l'array virtuale come un file server o server iSCSI.

processo di installazione e configurazione di Hello può richiedere circa 10 minuti toocomplete. informazioni di Hello in questo articolo si applicano solo toohello distribuzione di hello Array virtuale StorSimple. Per la distribuzione di hello di dispositivi della serie StorSimple 8000, passare a: [distribuire il dispositivo StorSimple serie 8000 esegue l'aggiornamento 2](storsimple-deployment-walkthrough-u2.md).

## <a name="setup-prerequisites"></a>Prerequisiti di installazione
Prima di configurare e installare l'array virtuale StorSimple, si deve:

* È stato effettuato il provisioning di un array virtuale e tooit connesso come descritto in dettaglio nella hello [il provisioning di un Array virtuale StorSimple in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) o [il provisioning di un Array virtuale StorSimple in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
* È una chiave di registrazione del servizio hello dal servizio di gestione di dispositivi StorSimple hello creato toomanage StorSimple Virtual Array. Per ulteriori informazioni, vedere [passaggio 2: chiave di registrazione del servizio Get hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) per Array virtuale StorSimple.
* Se si tratta di hello secondo o successive array virtuale che si sta registrando con un servizio di gestione di dispositivi StorSimple esistente, è necessario disporre di chiave di crittografia di hello servizio dati. Questa chiave è stata generata quando il primo dispositivo hello è stato registrato correttamente con questo servizio. Se si è persa la chiave, vedere [chiave DEK del servizio Get hello](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) per l'Array virtuale StorSimple.

## <a name="step-by-step-setup"></a>Installazione passo per passo
Utilizzare hello seguito tooset istruzioni dettagliate e configurare l'Array virtuale StorSimple.

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Passaggio 1: Completare web locale hello il programma di installazione dell'interfaccia utente e registrare il dispositivo
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete hello il programma di installazione e registrare il dispositivo di hello
1. Aprire una finestra del browser e connettersi toohello interfaccia utente web locale. Digitare:
   
   `https://<ip-address of network interface>`
   
   Utilizzare l'URL di connessione di hello annotate nel passaggio precedente hello. Viene visualizzato un errore che indica che si è verificato un problema con il certificato di sicurezza del sito Web di hello. Fare clic su **continuare la pagina Web toothis**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. Interfaccia utente della matrice come virtuale web di accesso toohello **StorSimpleAdmin**. Immettere una password amministratore del dispositivo hello che è stata modificata nel passaggio 3: inizio hello virtuale matrice [il provisioning di un Array virtuale StorSimple in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) o in [il provisioning di un Array virtuale StorSimple in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. Il cursore si sposterà toohello **Home** pagina. Questa pagina vengono descritti hello varie impostazioni necessarie tooconfigure e registrare hello array virtuale con il servizio di gestione di dispositivi StorSimple hello. Hello **le impostazioni di rete**, **le impostazioni del proxy Web**, e **impostazioni** sono facoltativi. Hello solo le impostazioni richieste sono **le impostazioni del dispositivo** e **impostazioni Cloud**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. In hello **le impostazioni di rete** pagina **interfacce di rete**, dati 0 verranno configurati automaticamente per l'utente. Ogni interfaccia di rete viene impostato automaticamente in base all'indirizzo IP predefinito tooget (DHCP). Di conseguenza, un indirizzo IP, una subnet e un gateway vengono assegnati automaticamente (sia per IPv4 che per IPv6).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   Se si aggiunge più di un'interfaccia di rete durante il provisioning del dispositivo hello hello, è possibile configurare in seguito. Si noti che è possibile configurare l'interfaccia di rete come solo IPv4 o come IPv4 e IPv6. Le configurazioni solo IPv6 non sono supportate.
5. Server DNS sono necessari perché vengono usate quando il dispositivo tenta toocommunicate con il provider di servizi di archiviazione cloud o tooresolve il dispositivo in base al nome quando è configurato come file server. In hello **le impostazioni di rete** pagina hello **server DNS**:
   
   1. Un server DNS primario e uno secondario vengono configurati automaticamente. Se si sceglie tooconfigure gli indirizzi IP statici, è possibile specificare server DNS. Per una disponibilità elevata, si consiglia di configurare un server DNS primario e uno secondario.
   2. Fare clic su **applica** tooapply e convalidare le impostazioni di rete hello.
6. In hello **le impostazioni del dispositivo** pagina:
   
   1. Assegnare un univoco **nome** tooyour dispositivo. Questo nome può avere da 1 a 15 caratteri e contenere lettere, numeri e trattini.
   2. Fare clic su hello **File server** icona ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) per hello **tipo** del dispositivo che si sta creando. Un file server consentirà cartelle toocreate condiviso.
   3. Il dispositivo è un file server, sarà necessario dominio tooa di toojoin hello dispositivo. Immettere un **Nome di dominio**.
   4. Fare clic su **Apply**.
7. Viene visualizzata una finestra di dialogo. Immettere le credenziali di dominio nel formato specificato hello. Fare clic sull'icona di controllo di hello. verifica delle credenziali di dominio Hello. Viene visualizzato un messaggio di errore se credenziali hello non sono corrette.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. Fare clic su **Apply**. Verranno applicate e convalidare le impostazioni del dispositivo hello.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > Assicurarsi che l'array virtuale nella propria unità organizzativa (OU) di Active Directory e non oggetti Criteri di gruppo (GPO) vengono applicati tooit o ereditate. Criteri di gruppo è possono installare applicazioni, ad esempio software antivirus in hello Array virtuale StorSimple. Installare software aggiuntivo non è supportata e potrebbe causare il danneggiamento toodata. 
   > 
   > 
9. Configurare il server proxy Web (facoltativo). Sebbene la configurazione del proxy Web sia facoltativa, tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   In hello **proxy Web** pagina:
   
   1. Alimentatore hello **URL proxy Web** nel formato: *http://&lt;-indirizzo IP dell'host o nome FDQN&gt;: il numero di porta*. Notare che gli URL HTTPS non sono supportati.
   2. Specificare **Autenticazione** come **Basic** o **Nessuna**.
   3. Se si utilizza l'autenticazione, è necessario anche tooprovide un **Username** e **Password**.
   4. Fare clic su **Apply**. Verrà convalidare e applicare impostazioni del proxy web hello configurato.
10. (Facoltativo) configurare le impostazioni di ora hello per il dispositivo, ad esempio fuso orario e hello server NTP primario e secondario. I server NTP sono obbligatori in quanto il dispositivo deve sincronizzare l'ora e consentire l'autenticazione con i provider del servizio cloud.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    In hello **impostazioni** pagina:
    
    1. Selezionare dall'elenco a discesa hello hello **fuso orario** basati su hello posizione geografica in cui hello dispositivo viene distribuito. fuso orario di Hello predefinito per il dispositivo è PST. Il dispositivo utilizzerà questo fuso orario per tutte le operazioni pianificate.
    2. Specificare un **server NTP primario** per il dispositivo o accettare il valore predefinito hello di time.windows.com. Verificare che la rete consenta toopass traffico NTP dal toohello datacenter Internet.
    3. Facoltativamente, specificare un **Server NTP secondario** per il dispositivo.
    4. Fare clic su **Apply**. Questa operazione convalidare e applicherà le impostazioni dell'ora hello configurato.
11. Configurare le impostazioni di cloud hello per il dispositivo. In questo passaggio verrà completare la configurazione locale hello e quindi registrare il dispositivo hello con il servizio di gestione di dispositivi StorSimple.
    
    1. Immettere hello **chiave di registrazione del servizio** ottenuti [passaggio 2: chiave di registrazione del servizio Get hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) per Array virtuale StorSimple.
    2. Se si tratta del primo dispositivo registrazione con questo servizio, verrà visualizzato con hello **chiave DEK del servizio**. Copiare questo codice e salvarlo in un luogo sicuro. Questa chiave è necessaria con hello registrazione tooregister chiave ulteriori dispositivi del servizio con il servizio di gestione di dispositivi StorSimple hello. 
       
       Se questo non è primo dispositivo hello che si sta registrando con questo servizio, è necessario tooprovide hello chiave DEK. Per ulteriori informazioni, vedere hello tooget [chiave DEK del servizio](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) locale interfaccia utente web.
    3. Fare clic su **Register**. Dispositivo hello verrà riavviato. Potrebbe essere necessario toowait 2-3 minuti prima periferica hello viene registrata correttamente. Dopo aver riavviato il dispositivo di hello, si accederà sign toohello nella pagina.
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. Restituire toohello portale di Azure. Andare troppo**tutte le risorse**, cercare il servizio di gestione di dispositivi StorSimple.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. In hello filtrato elenco, selezionare il servizio di gestione di dispositivi StorSimple e quindi passare troppo**gestione > dispositivi**. In hello **dispositivi** pannello, verificare che il dispositivo hello connesso servizio toohello e stato hello **pronto tooset backup**.
    
    ![Configurare un file server](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>Passaggio 2: Configurare il dispositivo hello come file server
Eseguire i passaggi hello hello [portale di Azure](https://portal.azure.com/) toocomplete hello è necessaria l'installazione di dispositivi.

#### <a name="tooconfigure-hello-device-as-file-server"></a>dispositivo hello tooconfigure come file server
1. Quindi indirizzata troppo e servizio di gestione di dispositivi StorSimple tooyour **gestione > dispositivi**. In hello **dispositivi** pannello, al dispositivo hello selezionare appena creato. Il dispositivo viene visualizzato come **pronto tooset backup**.
   
   ![Configurare un file server](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. Fare clic su dispositivo hello e verrà visualizzato un messaggio di intestazione che indica che il dispositivo hello è toosetup pronto.
   
    ![Configurare un file server](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. Fare clic su **configura** hello barra dei comandi. Verrà visualizzata hello **configura** blade. In hello **configura** pannello hello seguenti:
   
    1. nome del file server Hello viene popolato automaticamente.
    
    2. Assicurarsi che la crittografia di archiviazione cloud hello è impostata troppo**abilitato**. Questo verrà crittografare tutti i dati hello viene inviati toohello cloud. 
    
    3. Una chiave AES a 256 bit viene utilizzata con hello chiave definita dall'utente per la crittografia. Specificare una chiave di 32 caratteri e quindi eseguire nuovamente tooconfirm chiave hello è. Chiave hello record in un'applicazione di gestione delle chiavi per riferimento futuro.
    
    4. Fare clic su **Configura le impostazioni obbligatorie** delle credenziali dell'account di archiviazione toospecify toobe utilizzato con il dispositivo. Se non è configurata alcuna credenziale, fare clic su **Aggiungi nuova**. **Verificare che l'account di archiviazione hello che è utilizzare supporti i BLOB in blocchi. I BLOB di pagine non sono supportati.** Altre informazioni sui [BLOB in blocchi e i BLOB di pagine](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).
   
    ![Configurare un file server](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. In hello **aggiungere le credenziali di un account di archiviazione** pannello hello seguenti: 

    1. Scegliere la sottoscrizione corrente se l'account di archiviazione hello in hello servizio hello stessa sottoscrizione. Specificare l'altro è archiviazione hello account è di fuori di sottoscrizione del servizio hello. 
    
    2. Dall'elenco a discesa hello, scegliere un account di archiviazione esistente. 
    
    3. percorso Hello verrà popolato automaticamente in base a hello specificato account di archiviazione. 
    
    4. Abilitare SSL tooensure un canale di comunicazione di rete sicura tra il dispositivo di hello e cloud hello.
    
    5. Fare clic su **Aggiungi** tooadd questa risorsa di archiviazione delle credenziali dell'account. 
   
        ![Configurare un file server](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. Una volta credenziale dell'account di archiviazione hello viene creata correttamente, hello **configura** pannello verrà aggiornato toodisplay hello specificato le credenziali dell'account di archiviazione. Fare clic su **Configure**.
   
   ![Configurare un file server](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   Viene avviata la creazione di un file server. Una volta server file hello viene creata correttamente, si riceverà la notifica.
   
   ![Configurare un file server](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   stato del dispositivo Hello modificherà anche troppo**Online**.
   
   ![Configurare un file server](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   È possibile procedere tooadd una condivisione.

## <a name="step-3-add-a-share"></a>Passaggio 3: Aggiungere una condivisione
Eseguire i passaggi hello hello [portale di Azure](https://portal.azure.com/) toocreate una condivisione.

#### <a name="toocreate-a-share"></a>toocreate una condivisione
1. Selezionare hello file server dispositivo configurato nel passaggio precedente hello e fare clic su **...**  (o destro). Nel menu di scelta rapida hello, selezionare **Aggiungi condivisione**. In alternativa, è possibile fare clic su **+ Aggiungi condivisione** hello dispositivo barra dei comandi.
   
   ![Aggiungere una condivisione](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. Specificare hello seguendo le impostazioni di condivisione:

    1. Un nome univoco per la condivisione. nome Hello deve essere una stringa che contiene 3 too127 caratteri.
    
    2. Facoltativo **descrizione** per condivisione hello. Descrizione Hello consentirà di identificare i proprietari di condivisione hello.
    
    3. Oggetto **tipo** per condivisione hello. può essere di tipo Hello **a livelli** o **aggiunto in locale**, con livelli hello predefinito. Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni di livello superiore, selezionare la condivisione **Aggiunto in locale** . Per tutti gli altri dati, selezionare una **Condivisione a livelli** .
    Una condivisione aggiunto in locale stati sottoposti a thick provisioning e garantisce che i dati primario hello nella condivisione di hello rimangono dispositivo toohello locale e non spill toohello cloud. Una condivisione a livelli in hello invece il thin provisioning. Quando si crea una condivisione a livelli, viene eseguito il provisioning di 10% di spazio hello a livello locale hello e 90% dello spazio di hello è disponibile nel cloud hello. Ad esempio, se è stato eseguito il provisioning di un volume di 1 TB, 100 GB si troverà nello spazio locale hello e 900 GB verrebbe utilizzato nel cloud hello hello quando i livelli dati. A sua volta, ciò implica che se si esaurisce tutto lo spazio locale hello sul dispositivo hello, è possibile eseguire il provisioning una condivisione a livelli.
   
    4. In hello **impostare come predefinita per le autorizzazioni complete** campo, assegnare hello autorizzazioni toohello utente o gruppo hello che accede a questa condivisione. Specificare il nome di hello di hello utente o gruppo di utenti di hello in  *john@contoso.com*  formato. È consigliabile utilizzare un tooaccess privilegi di amministratore di utente gruppo (anziché un singolo utente) tooallow tali condivisioni. Dopo aver assegnato le autorizzazioni di hello qui, è possibile quindi utilizzare Esplora File toomodify queste autorizzazioni.
   
    5. Fare clic su **Aggiungi** condivisione hello toocreate. 
    
        ![Aggiungere una condivisione](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        Notifica che è in corso la creazione di condivisione hello.
   
        ![Aggiungere una condivisione](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Dopo aver creata la condivisione hello con hello le impostazioni specificate, hello **condivisioni** pannello aggiornerà nuova condivisione di tooreflect hello. Per impostazione predefinita, il monitoraggio e backup sono abilitati per la condivisione hello.
   
    ![Aggiungere una condivisione](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>Passaggio 4: Connettere toohello condivisione
È necessario tooconnect tooone o più condivisioni di cui è stato creato nel passaggio precedente hello. Eseguire questi passaggi sul tooyour di host connesso Server Windows Array virtuale StorSimple.

#### <a name="tooconnect-toohello-share"></a>condivisione toohello tooconnect
1. Premere ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + r. Nella finestra Esegui hello specificare hello *&#92; &#92;&lt; nome del file server&gt;*  come percorso di hello, sostituendo *nome del file server* con dispositivo hello nome è assegnato tooyour file server. Fare clic su **OK**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. Si apre Esplora file. Dovrebbe ora essere condivisioni hello in grado di toosee create come cartelle. Selezionare e fare doppio clic su un contenuto di hello tooview condivisione (cartella).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. È ora possibile aggiungere condivisioni di file toothese ed eseguire un backup.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come toouse hello interfaccia utente web locale troppo[amministrare l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).

