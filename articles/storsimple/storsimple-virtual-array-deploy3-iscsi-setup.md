---
title: programma di installazione server iSCSI Azure StorSimple Virtual Array aaaMicrosoft | Documenti Microsoft
description: Descrive come registrare il server iSCSI StorSimple tooperform la configurazione iniziale e completare l'installazione di dispositivo.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>Distribuire l'array virtuale StorSimple: configurarlo come server iSCSI tramite il portale di Azure

![flusso del processo di installazione di iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>Panoramica

In questa esercitazione di distribuzione applica toohello Microsoft Azure StorSimple Virtual Array. In questa esercitazione viene descritto come la configurazione iniziale hello tooperform, registrare il server iSCSI StorSimple, l'installazione dispositivo completa hello e quindi creare, montare, inizializzare e formattare i volumi l'Array virtuale StorSimple configurato come server iSCSI. 

procedure Hello descritte qui richiedere circa 30 minuti too1 ora toocomplete. informazioni Hello pubblicate in questo articolo si applicano solo tooStorSimple array virtuale.

## <a name="setup-prerequisites"></a>Prerequisiti di installazione

Prima di configurare e installare l'array virtuale StorSimple, si deve:

* Si è eseguito il provisioning di un array virtuale e tooit come descritto in [distribuire StorSimple Virtual Array - effettuare il provisioning di un array virtuale in Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) o [distribuire StorSimple Virtual Array - effettuare il provisioning di un array virtuale in VMware ](storsimple-virtual-array-deploy2-provision-vmware.md).
* È una chiave di registrazione hello dal servizio di gestione di dispositivi StorSimple creato toomanage gli array virtuale StorSimple hello. Per ulteriori informazioni, vedere **passaggio 2: chiave di registrazione del servizio Get hello** in [il Array virtuale StorSimple distribuire - preparare portale hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
* Se si tratta di hello secondo o successive array virtuale che si sta registrando con un servizio di gestione di dispositivi StorSimple esistente, è necessario disporre di chiave di crittografia di hello servizio dati. Questa chiave è stata generata quando il primo dispositivo hello è stato registrato correttamente con questo servizio. Se si è persa la chiave, vedere **chiave DEK del servizio Get hello** in [utilizzare hello tooadminister dell'interfaccia utente Web l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).

## <a name="step-by-step-setup"></a>Installazione passo per passo

Utilizzare hello seguito tooset istruzioni dettagliate e configurare l'Array virtuale StorSimple:

* [Passaggio 1: Completare web locale hello il programma di installazione dell'interfaccia utente e registrare il dispositivo](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [Passaggio 2: Hello completa necessaria l'installazione di dispositivo](#step-2-complete-the-required-device-setup)
* [Passaggio 3: Aggiungere un volume](#step-3-add-a-volume)
* [Passaggio 4: Montare, inizializzare e formattare un volume](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Passaggio 1: Completare web locale hello il programma di installazione dell'interfaccia utente e registrare il dispositivo

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete hello il programma di installazione e registrare il dispositivo di hello

1. Aprire una finestra del browser. tooconnect toohello web tipo dell'interfaccia utente:
   
    `https://<ip-address of network interface>`
   
    Utilizzare l'URL di connessione di hello annotate nel passaggio precedente hello. Verrà visualizzato un errore di notifica che si è verificato un problema con il certificato di sicurezza del sito Web di hello. Fare clic su **pagina web di continuazione toothis**.
   
    ![errore di certificato di sicurezza](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. Interfaccia utente del dispositivo virtuale come web di accesso toohello **StorSimpleAdmin**. Immettere una password amministratore del dispositivo hello che è stata modificata nel passaggio 3: dispositivo virtuale di avvio hello in [distribuire StorSimple Virtual Array - effettuare il provisioning di un dispositivo virtuale in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) o [il Array virtuale StorSimple distribuire - Eseguire il provisioning di un dispositivo virtuale in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
    ![Pagina di accesso](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. Verrà visualizzata toohello **Home** pagina. Questa pagina vengono descritti hello varie impostazioni necessarie tooconfigure e registrare il dispositivo virtuale con il servizio di gestione di dispositivi StorSimple hello di hello. Si noti che hello **le impostazioni di rete**, **le impostazioni del proxy Web**, e **impostazioni** sono facoltativi. Hello solo le impostazioni richieste sono **le impostazioni del dispositivo** e **impostazioni Cloud**.
   
    ![Home page](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. In hello **le impostazioni di rete** pagina **interfacce di rete**, dati 0 verranno configurati automaticamente per l'utente. Ogni interfaccia di rete viene impostato per impostazione predefinita tooget un indirizzo IP automaticamente (DHCP). Quindi, un indirizzo IP, una subnet e un gateway vengono assegnati automaticamente (sia per IPv4 che per IPv6).
   
    Quando si pianifica toodeploy dispositivo come un server iSCSI (archiviazione a blocchi tooprovision), è consigliabile disabilitare hello **ottenere automaticamente l'indirizzo IP** opzione e configurare gli indirizzi IP statici.
   
    ![Pagina Impostazioni di rete](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    Se si aggiunge più di un'interfaccia di rete durante il provisioning del dispositivo hello hello, è possibile configurare in seguito. Si noti che è possibile configurare l'interfaccia di rete come solo IPv4 o come IPv4 e IPv6. Le configurazioni solo IPv6 non sono supportate.
5. I server DNS sono necessari perché vengono utilizzate quando il dispositivo tenta toocommunicate con il provider di servizi di archiviazione cloud o tooresolve il dispositivo in base al nome se è configurato come un file server. In hello **le impostazioni di rete** pagina hello **server DNS**:
   
   1. Un server DNS primario e secondario viene configurato automaticamente. Se si sceglie tooconfigure gli indirizzi IP statici, è possibile specificare server DNS. Per una disponibilità elevata, si consiglia di configurare un server DNS primario e uno secondario.
   2. Fare clic su **Apply**. Verranno applicate e convalidare le impostazioni di rete hello.
6. In hello **le impostazioni del dispositivo** pagina:
   
   1. Assegnare un univoco **nome** tooyour dispositivo. Questo nome può avere da 1 a 15 caratteri e contenere lettere, numeri e trattini.
   2. Fare clic su hello **server iSCSI** icona ![icona server iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) per hello **tipo** del dispositivo che si sta creando. Un server iSCSI consente l'archiviazione a blocchi tooprovision.
   3. Specificare se si desidera questo toobe dispositivi appartenenti a un dominio. Se il dispositivo è un server iSCSI, quindi aggiungere il dominio di hello è facoltativo. Se si decide di join toonot dominio tooa server iSCSI, fare clic su **applica**, attendere toobe impostazioni hello applicato e quindi procedere toohello successivo.
      
       Se si desidera toojoin hello dispositivo tooa dominio. Immettere un **nome di dominio**, quindi fare clic su **Applica**.
      
      > [!NOTE]
      > Se l'unione di dominio tooa server iSCSI, verificare che l'array virtuale sia nella propria unità organizzativa (OU) per Microsoft Azure Active Directory e non oggetti Criteri di gruppo (GPO) sono tooit applicato.
      > 
      > 
   4. Viene visualizzata una finestra di dialogo. Immettere le credenziali di dominio nel formato specificato hello. Fare clic sull'icona di controllo hello ![icona del segno di spunta](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). le credenziali di dominio Hello verranno verificate. Si verrà visualizzato un messaggio di errore se credenziali hello non sono corrette.
      
       ![credentials](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. Fare clic su **Apply**. Verranno applicate e convalidare le impostazioni del dispositivo hello.
7. Configurare il server proxy Web (facoltativo). Sebbene la configurazione del proxy Web sia facoltativa, tenere presente che se si utilizza un proxy Web, è possibile configurarlo solo qui.
   
    ![configurare il proxy Web](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    In hello **proxy Web** pagina:
   
   1. Alimentatore hello **URL proxy Web** nel formato: *http://host-IP indirizzo* o *FDQN:Port numero*. Notare che gli URL HTTPS non sono supportati.
   2. Specificare **Autenticazione** come **Basic** o **Nessuna**.
   3. Se si utilizza l'autenticazione, è necessario anche tooprovide un **Username** e **Password**.
   4. Fare clic su **Apply**. Verrà convalidare e applicare impostazioni del proxy web hello configurato.
8. (Facoltativo) configurare le impostazioni di ora hello per il dispositivo, ad esempio fuso orario e hello server NTP primario e secondario. I server NTP sono obbligatori in quanto il dispositivo deve sincronizzare l'ora e consentire l'autenticazione con i provider del servizio cloud.
   
    ![Impostazioni ora](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    In hello **impostazioni** pagina:
   
   1. Dall'elenco a discesa hello, selezionare hello **fuso orario** basati su hello posizione geografica in cui hello dispositivo viene distribuito. fuso orario di Hello predefinito per il dispositivo è PST. Il dispositivo utilizzerà questo fuso orario per tutte le operazioni pianificate.
   2. Specificare un **server NTP primario** per il dispositivo o accettare il valore predefinito hello di time.windows.com. Verificare che la rete consenta toopass traffico NTP dal toohello datacenter Internet.
   3. Facoltativamente, specificare un **Server NTP secondario** per il dispositivo.
   4. Fare clic su **Apply**. Questa operazione convalidare e applicherà le impostazioni dell'ora hello configurato.
9. Configurare le impostazioni di cloud hello per il dispositivo. In questo passaggio verrà completare la configurazione locale hello e quindi registrare il dispositivo hello con il servizio di gestione di dispositivi StorSimple.
   
   1. Immettere hello **chiave di registrazione del servizio** ottenuti **passaggio 2: chiave di registrazione del servizio Get hello** in [il Array virtuale StorSimple distribuire - preparare hello portale](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
   2. Se questo non è primo dispositivo hello che si sta registrando con questo servizio, sarà necessario hello tooprovide **chiave DEK del servizio**. Questa chiave è necessaria con hello registrazione tooregister chiave ulteriori dispositivi del servizio con il servizio di gestione di dispositivi StorSimple hello. Per ulteriori informazioni, vedere troppo[chiave DEK del servizio Get hello](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) locale interfaccia utente web.
   3. Fare clic su **Register**. Dispositivo hello verrà riavviato. Potrebbe essere necessario toowait 2-3 minuti prima periferica hello viene registrata correttamente. Dopo aver riavviato il dispositivo di hello, si accederà sign toohello nella pagina.
      
      ![Registrare il dispositivo](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. Restituire toohello portale di Azure.
11. Passare toohello **dispositivi** pannello del servizio. Se si dispone di molte risorse, fare clic su **Tutte le risorse**, selezionare il nome del servizio (ricercarlo se necessario), quindi fare clic su **Dispositivi**.
12. In hello **dispositivi** pannello, verificare che il dispositivo hello connesso toohello servizio esaminando lo stato di hello. deve essere stato del dispositivo Hello **pronto tooset backup**.
    
    ![Registrare il dispositivo](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>Passaggio 2: Configurare il dispositivo hello come server iSCSI

Eseguire i passaggi hello toocomplete portale Azure hello necessario dispositivo installazione hello.

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>dispositivo hello tooconfigure come server iSCSI

1. Quindi indirizzata troppo e servizio di gestione di dispositivi StorSimple tooyour**gestione > dispositivi**. In hello **dispositivi** pannello, al dispositivo hello selezionare appena creato. Il dispositivo viene visualizzato come **pronto tooset backup**.
   
    ![Configurare il dispositivo come server iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. Fare clic su dispositivo hello e verrà visualizzato un messaggio di intestazione che indica che il dispositivo hello è toosetup pronto.
   
    ![Configurare il dispositivo come server iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. Fare clic su **configura** hello dispositivo barra dei comandi. Verrà visualizzata hello **configura** blade. In hello **configura** pannello hello seguenti:
   
   * nome del server iSCSI Hello viene popolato automaticamente.
   * Assicurarsi che la crittografia di archiviazione cloud hello è impostata troppo**abilitato**. In questo modo si garantisce che i dati di hello inviati dal cloud di hello dispositivo toohello sono crittografati.
   * Specificare una chiave di 32 caratteri e registrarla in un'app di gestione delle chiavi per riferimento futuro.
   * Selezionare un toobe di account di archiviazione utilizzato con il dispositivo. In questa sottoscrizione, è possibile selezionare un account di archiviazione esistente oppure è possibile fare clic su **Aggiungi** toochoose un account da un'altra sottoscrizione.
     
     ![Configurare il dispositivo come server iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. Fare clic su **configura** toocomplete impostazione server iSCSI hello.
   
    ![Configurare il dispositivo come server iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. Si riceverà una notifica che la creazione del server iSCSI hello è in corso. Dopo la creazione del server iSCSI hello, hello **dispositivi** pannello viene aggiornato e stato della periferica corrispondente hello **Online**.
   
    ![Configurare il dispositivo come server iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>Passaggio 3: Aggiungere un volume

1. In hello **dispositivi** pannello, al dispositivo hello selezionare appena configurato come server iSCSI. Fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **aggiungere volume**. È anche possibile fare clic su **+ Aggiungi volume** hello barra dei comandi. Verrà visualizzata hello **aggiungere volume** blade.
   
    ![Aggiungere un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. In hello **aggiungere volume** pannello hello seguenti:
   
   * In hello **nome Volume** immettere un nome univoco per il volume. nome Hello deve essere una stringa che contiene 3 too127 caratteri.
   * In hello **tipo** elenco a discesa specificare se toocreate un **a livelli** o **aggiunto in locale** volume. Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni di livello superiore, selezionare **Volume** **aggiunto in locale**. Per tutti gli altri dati, selezionare **Volume** **a livelli**.
   * In hello **capacità** specificare dimensioni di hello del volume hello. Un volume a livelli deve essere compreso tra 500 GB e 5 TB e un volume aggiunto in locale deve essere compreso tra 50 e 500 GB.
     
     Un volume aggiunto in locale stati sottoposti a thick provisioning e garantisce che i dati primari hello volume hello resta nel dispositivo hello e non spill toohello cloud.
     
     Un volume a livelli in hello invece il thin provisioning. Quando si crea un volume a livelli, viene eseguito il provisioning di circa il 10% di spazio hello a livello locale hello e 90% dello spazio di hello è disponibile nel cloud hello. Ad esempio, se è stato eseguito il provisioning di un volume di 1 TB, 100 GB si troverà nello spazio locale hello e 900 GB verrebbe utilizzato nel cloud hello hello quando i livelli dati. Ciò a sua volta implica che se si esaurisce tutto lo spazio locale hello sul dispositivo hello, è possibile eseguire il provisioning una condivisione a livelli (poiché non sarà disponibile il 10% hello).
     
     ![Aggiungere un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * Fare clic su **connesso host**, selezionare un accesso controllo record (ACR) corrispondente toohello iniziatore iSCSI che desidera tooconnect toothis volume e quindi fare clic su **selezionare**. <br><br> 
3. tooadd un nuovo host connessi, fare clic su **Aggiungi nuovo**, immettere un nome per l'host di hello e relativo iSCSI nome qualificato e quindi fare clic su **Aggiungi**. Se non si dispone di hello IQN, andare troppo[appendice a: ottenere hello nome qualificato iSCSI di un host Windows Server](#appendix-a-get-the-iqn-of-a-windows-server-host).
   
      ![Aggiungere un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. Al termine della configurazione del volume, fare clic su **OK**. Verrà creato un volume con hello specificato le impostazioni e verrà visualizzata una notifica. Per impostazione predefinita, il monitoraggio e backup verrà abilitate per il volume di hello.
   
     ![Aggiungere un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. tooconfirm che hello volume è stato creato correttamente, andare toohello **volumi** blade. Verrà visualizzato il volume di hello elencato.
   
   ![Aggiungere un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>Passaggio 4: Montare, inizializzare e formattare un volume

Eseguire hello seguendo i passaggi toomount, inizializzare e formattare i volumi StorSimple su un host Windows Server.

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inizializzare e formattare un volume

1. Aprire hello **iniziatore iSCSI** app sul server appropriato hello.
2. In hello **iniziatore iSCSI-proprietà** finestra hello **individuazione** scheda, fare clic su **individua portale**.
   
    ![Individua portale](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. In hello **individua portale destinazione** nella finestra di dialogo specificare hello di indirizzo IP dell'interfaccia di rete abilitata per iSCSI e quindi fare clic su **OK**.
   
    ![Indirizzo IP](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. In hello **iniziatore iSCSI-proprietà** finestra hello **destinazioni** , individuare hello **individuati destinazioni**. (Ogni volume è una destinazione individuata.) stato del dispositivo Hello dovrebbe essere visualizzato come **inattivo**.
   
    ![destinazioni individuate](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. Selezionare un dispositivo di destinazione e quindi fare clic su **Connetti**. Dopo che hello dispositivo è connesso, lo stato di hello deve modificare troppo**connesso**. (Per ulteriori informazioni sull'uso dell'iniziatore iSCSI Microsoft di hello, vedere [installazione e configurazione iniziatore iSCSI Microsoft][1].
   
    ![selezionare il dispositivo di destinazione](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. Nell'host di Windows, premere tasto Logo Windows hello + X e quindi fare clic su **eseguire**.
7. In hello **eseguire** della finestra di dialogo tipo **Diskmgmt.msc**. Fare clic su **OK**, hello e **Gestione disco** verrà visualizzata la finestra di dialogo. riquadro di destra Hello mostrerà volumi hello sull'host.
8. In hello **Gestione disco** finestra hello volumi montati vengono visualizzati come mostrato nella seguente figura hello. Mouse sul volume hello individuato (fare clic su nome hello del disco), quindi fare clic su **Online**.
   
    ![Gestione disco](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. Fare clic con il pulsante destro del mouse e selezionare **Inizializza disco**.
   
    ![inizializzare disco 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. Nella finestra di dialogo hello selezionare tooinitialize dischi hello e quindi fare clic su **OK**.
    
    ![inizializzare disco 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. Avvia Creazione guidata nuovo Volume semplice Hello. Selezionare una dimensione disco e quindi fare clic su **Avanti**.
    
    ![procedura guidata nuovo volume 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. Assegnare un volume toohello lettera di unità e quindi fare clic su **Avanti**.
    
    ![procedura guidata nuovo volume 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. Immettere hello parametri tooformat hello volume. **In Windows Server, è supportato solo NTFS.** Impostare too64K dimensioni unità di hello allocazione. Specificare un'etichetta per il volume. È una procedura consigliata per il nome di volume del toobe toohello identici che si è specificato nella matrice virtuale StorSimple. Fare clic su **Avanti**.
    
    ![procedura guidata nuovo volume 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. Controllare i valori hello per il volume e quindi fare clic su **fine**.
    
    ![procedura guidata nuovo volume 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    Hello volumi vengono visualizzati come **Online** su hello **Gestione disco** pagina.
    
    ![volumi online](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toouse hello interfaccia utente web locale troppo[amministrare l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>Appendice a: hello Get nome qualificato iSCSI di un host Windows Server

Eseguire i seguenti passaggi tooget hello iSCSI hello nome qualificato di un host Windows che esegue Windows Server 2012.

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>hello tooget nome IQN dell'host di Windows

1. Avviare l'iniziatore iSCSI Microsoft di hello nell'host di Windows.
2. In hello **iniziatore iSCSI-proprietà** finestra hello **configurazione** , selezionare e copiare la stringa hello hello **nome iniziatore** campo.
   
    ![Proprietà iniziatore iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. Salvare la stringa.

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



