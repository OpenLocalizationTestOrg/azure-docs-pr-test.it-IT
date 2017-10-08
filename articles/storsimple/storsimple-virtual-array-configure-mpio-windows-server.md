---
title: aaaConfigure MPIO nell'host connesso tooStorSimple Array virtuale | Documenti Microsoft
description: "Descrive la modalità di connessione tooa host che esegue Windows Server 2012 R2 tooconfigure Multipath i/o (MPIO) per l'Array virtuale StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Configurare Multipath i/o in host Windows Server per hello Array virtuale StorSimple
## <a name="overview"></a>Panoramica
In questo articolo viene descritto come applicare impostazioni di configurazione specifiche per i volumi StorSimple sola funzionalità di tooinstall Multipath i/o (MPIO) in host Windows Server e quindi verificare MPIO per i volumi StorSimple. Hello si presuppone che l'Array virtuale StorSimple 1200 con due interfacce di rete è connessa tooa host di Windows Server con due interfacce di rete. informazioni di Hello contenute in questo articolo si applicano solo toohello array virtuale. Per informazioni su dispositivi della serie StorSimple 8000, visitare troppo[configurare MPIO per StorSimple host](storsimple-configure-mpio-windows-server.md). 

funzionalità MPIO Hello in Windows Server consente di configurazioni di archiviazione a disponibilità elevata e a tolleranza di errore. MPIO utilizza componenti del percorso fisico ridondanti, schede, cavi e commutatori, toocreate percorsi logici tra server hello e dispositivo di archiviazione hello. Se si verifica un errore di componente, con conseguente errore toofail un percorso logico, la logica Multipath Usa un percorso alternativo per i/o in modo che le applicazioni possano comunque accedere ai dati. Inoltre dipende dalla configurazione MPIO possa anche migliorare le prestazioni nuovo bilanciamento del carico hello tra tutti questi percorsi. Per ulteriori informazioni, vedere [Panoramica di Multipath I/O](https://technet.microsoft.com/library/cc725907.aspx "Panoramica di Multipath I/O and features").

Per hello a disponibilità elevata della soluzione StorSimple configurare MPIO in Windows Server host connesso tooyour Array virtuale StorSimple (modello a 1200) hello. i server host Hello quindi in grado di tollerare un collegamento, rete o errori dell'interfaccia. 

È necessario toofollow questi tooconfigure passaggi MPIO: 

* Prerequisiti di configurazione
* Passaggio 1: Installare MPIO nell'host Windows Server hello
* Passaggio 2: Configurare MPIO per volumi StorSimple
* Passaggio 3: Montare i volumi StorSimple sull'host hello

Ogni hello di sopra di passaggi è illustrato in hello le sezioni seguenti.

## <a name="prerequisites"></a>Prerequisiti
Questa sezione descrive i prerequisiti di configurazione hello per host di Windows Server hello e l'array virtuale.

### <a name="on-windows-server-host"></a>Dall'host Windows Server
* Assicurarsi che l'host Windows Server abbia due interfacce di rete abilitate.

### <a name="on-storsimple-virtual-array"></a>Dall'array virtuale StorSimple
* Matrice di Hello virtuale deve essere configurato come un server iSCSI. vedere, più toolearn [impostare array virtuale come server iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md). Uno o più interfacce di rete devono essere abilitate su matrice hello.   
* interfacce di rete Hello l'array virtuale devono essere raggiungibile dall'host di Server di Windows hello.
* È necessario creare uno o più volumi sull'array virtuale StorSimple. vedere, più toolearn [aggiungere un volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) sull'Array virtuale StorSimple. In questa procedura, creata nell'array virtuale hello 3 (volumi 1 localmente bloccata e 2 a più livelli come mostrato sotto).
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>Configurazione hardware per l'array virtuale StorSimple
Hello seguente figura configurazione hardware hello per la disponibilità elevata e bilanciamento del carico percorsi multipli per l'host di Windows Server e il StorSimple Array virtuale utilizzato in questa procedura.

![Configurazione hardware di MPIO](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Come illustrato nella figura precedente hello:

* L'array virtuale StorSimple con provisioning in Hyper-V è un dispositivo attivo a nodo singolo configurato come server iSCSI.
* Sull'array sono abilitate due interfacce di rete virtuali. In hello interfaccia utente web locale della matrice virtuale, verificare che i due interfacce di rete siano abilitate passando troppo**le impostazioni di rete** come illustrato di seguito:
  
    ![Interfacce di rete abilitate su 1200](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    Gli indirizzi IPv4 hello nota di hello abilitato (Ethernet, Ethernet 2 per impostazione predefinita), interfacce di rete e salvare per un utilizzo successivo nell'host di hello.
* Sull'host Windows Server sono abilitate due interfacce di rete. Se hello connesse le interfacce per host e la matrice si trovano in hello stessa subnet, non ci saranno 4 percorsi disponibili. Questo è il caso hello in questa procedura. Tuttavia, se ogni interfaccia di rete sull'interfaccia di matrice e host hello in un'altra subnet IP (e non instradabili), quindi solo 2 i percorsi saranno disponibili.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Passaggio 1: Installare MPIO nell'host Windows Server hello
MPIO è una funzionalità facoltativa in Windows Server, e non è installata per impostazione predefinita. Deve essere installata come funzionalità tramite Server Manager. completamento di questa funzionalità nell'host Windows Server, tooinstall hello seguenti procedure.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Passaggio 2: Configurare MPIO per volumi StorSimple
La funzionalità MPIO deve volumi StorSimple di tooidentify toobe configurato. tooconfigure MPIO toorecognize i volumi StorSimple, eseguire hello alla procedura seguente.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Passaggio 3: Montare i volumi StorSimple sull'host hello
Una volta configurata la funzionalità MPIO in Windows Server, volumi creati nel array StorSimple hello possono essere montati e possono quindi sfruttare i vantaggi di MPIO per la ridondanza. toomount un volume, eseguire hello alla procedura seguente.

#### <a name="toomount-volumes-on-hello-host"></a>volumi host hello toomount
1. Aprire hello **iniziatore iSCSI-proprietà** finestra in host Windows Server hello. Andare troppo**Server Manager > Dashboard > Strumenti > iniziatore iSCSI**.
2. In hello **iniziatore iSCSI-proprietà** la finestra di dialogo, fare clic su **individuazione**, quindi fare clic su **individua portale destinazione**.
3. In hello **individua portale destinazione** finestra di dialogo casella, hello seguenti:
   
    1. Immettere l'indirizzo IP hello dell'interfaccia di rete abilitate prima hello sull'Array virtuale StorSimple. Per impostazione predefinita, si tratta dell'interfaccia **Ethernet**. 
    2. Fare clic su **OK** tooreturn toohello **iniziatore iSCSI-proprietà** la finestra di dialogo.
     
    > [!IMPORTANT]
    > Se si utilizza una rete privata per le connessioni iSCSI, immettere l'indirizzo IP hello hello dati della porta di cui è connesso toohello rete privata.
     
4. Ripetere i passaggi 2-3 per una seconda interfaccia di rete (ad esempio, Ethernet 2) sull'array. 
5. Seleziona hello **destinazioni** scheda hello **iniziatore iSCSI-proprietà** la finestra di dialogo. Nell'array virtuale ogni area di volume deve essere visualizzata come destinazione in **Destinazioni individuate**. In questo caso, potrebbero essere individuate tre destinazioni (volumi toothree corrispondente).
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. Fare clic su **Connetti** tooestablish una sessione iSCSI con l'Array virtuale StorSimple. Oggetto **connettersi tooTarget** verrà visualizzata la finestra di dialogo. Seleziona hello **abilitare multi-path** casella di controllo. Fare clic su **Advanced**.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. In hello **impostazioni avanzate** finestra di dialogo casella, hello seguenti:                                        
   
    1. In hello **scheda locale** elenco a discesa, seleziona **iniziatore iSCSI Microsoft**.
    2. In hello **IP iniziatore** elenco a discesa, l'indirizzo IP di hello selezionare dell'host hello.
    3. In hello **portale destinazione** IP riepilogo, selezionare hello IP dell'interfaccia di matrice.
    4. Fare clic su **OK** tooreturn toohello **iniziatore iSCSI-proprietà** la finestra di dialogo.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. Fare clic su **Proprietà**. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. In hello **proprietà** la finestra di dialogo, fare clic su **Aggiungi sessione**.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. In hello **connettersi tooTarget** la finestra di dialogo, seleziona hello **abilitare multi-path** casella di controllo. Fare clic su **Advanced**.
11. In hello **impostazioni avanzate** la finestra di dialogo:                                        
    
    1. In hello **scheda locale** elenco a discesa, selezionare iniziatore iSCSI Microsoft.

    2. In hello **IP iniziatore** elenco a discesa, host toohello corrispondente di hello selezionare IP indirizzo. In questo caso, ci si connette due interfacce di rete su hello matrice tooa singola interfaccia di rete sull'host hello. Pertanto, questa interfaccia è hello identici a quelli forniti per hello prima sessione.

    3. In hello **IP portale destinazione** elenco a discesa, indirizzo IP selezionare hello hello seconda interfaccia dati abilitata in una matrice di hello.

    4. Fare clic su **OK** finestra di dialogo Proprietà iniziatore iSCSI toohello di tooreturn. È stata aggiunta una seconda destinazione toohello sessione.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. Dopo aver aggiunto le sessioni di hello desiderato (percorsi), in hello **iniziatore iSCSI-proprietà** la finestra di dialogo, destinazione hello selezionare e fare clic su **proprietà**. Nella scheda sessioni hello di hello **proprietà** della finestra di dialogo Nota hello quattro identificatori di sessione che corrispondono toohello possibili permutazioni di percorso. toocancel una sessione, selezionare l'identificatore di sessione successiva tooa di hello casella di controllo e quindi fare clic su **Disconnect**.

    6. tooview dispositivi presentati nelle sessioni, seleziona hello **dispositivi** hello tooconfigure scheda Criteri MPIO per un dispositivo selezionato, fare clic su **MPIO**.

    7. Hello **dettagli** verrà visualizzata la finestra di dialogo. In hello **MPIO** scheda, è possibile selezionare hello appropriato **il criterio di bilanciamento del carico** impostazioni. È inoltre possibile visualizzare hello **Active** o **Standby** tipo di percorso.
12. Ripetere destinazione toohello di passaggi da 8 a 11 tooadd altre sessioni (percorsi). Con due interfacce sull'host hello e due su array virtuale hello, è possibile aggiungere un totale di quattro sessioni per ogni destinazione. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. Sarà necessario toorepeat questi passaggi per ogni volume (rappresentato da una destinazione).
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. Aprire **Gestione Computer** passando troppo**Server Manager > Dashboard > Gestione Computer**. Nel riquadro di sinistra hello, fare clic su **archiviazione > Gestione disco**. Hello volumi creati nel hello Array virtuale StorSimple che sono visibili toothis host verranno visualizzato in **Gestione disco** come nuovi dischi.
15. Inizializzare il disco hello e creare un nuovo volume. Durante il processo di formattazione hello, selezionare una dimensione di unità di allocazione (Australia) di 64 KB. Ripetere il processo di hello per tutti i volumi disponibili hello.
    
    ![Gestione disco](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. In **Gestione disco**, hello rapida **disco** e selezionare **proprietà**.
17. In hello **proprietà dispositivo disco con percorsi multipli** finestra di dialogo fare clic su hello **MPIO** scheda.
    
    ![Proprietà del disco](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. In hello **nome DSM** fare clic su **dettagli** e verificare che i parametri di hello vengono impostati i parametri predefiniti toohello. i parametri predefiniti Hello sono:
    
    * Periodo di verifica percorso = 30
    * Numero di tentativi = 3
    * Periodo di rimozione PDO = 20
    * Intervallo tentativi = 1
    * Verifica percorso attivata = deselezionata.
    
    > [!NOTE]
    > **Non modificare i parametri predefiniti hello.**
   
## <a name="next-steps"></a>Passaggi successivi
Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple l'Array virtuale StorSimple](storsimple-virtual-array-manager-service-administration.md).

