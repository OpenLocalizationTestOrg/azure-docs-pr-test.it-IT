---
title: aaaConfigure MPIO per il dispositivo StorSimple | Documenti Microsoft
description: "Descrive la modalità di connessione tooa host che esegue Windows Server 2012 R2 tooconfigure Multipath i/o (MPIO) per il dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 879fd0f9-c763-4fa0-a5ba-f589a825b2df
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/03/2017
ms.author: alkohli
ms.openlocfilehash: 08cd53039b3868217c7d28e97d7c3c695c06e399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>Configurare Multipath I/O per il dispositivo StorSimple
Microsoft compilato il supporto per funzionalità di hello Multipath i/o (MPIO) in Windows Server toohelp le configurazioni SAN a disponibilità elevata, a tolleranza di errore di compilazione. MPIO utilizza componenti del percorso fisico ridondanti, schede, cavi e commutatori, toocreate percorsi logici tra server hello e dispositivo di archiviazione hello. Se si verifica un errore di componente, con conseguente errore toofail un percorso logico, la logica Multipath Usa un percorso alternativo per i/o in modo che le applicazioni possano comunque accedere ai dati. Inoltre dipende dalla configurazione MPIO possa anche migliorare le prestazioni nuovo bilanciamento del carico hello tra tutti questi percorsi. Per ulteriori informazioni, vedere [Panoramica di Multipath I/O](https://technet.microsoft.com/library/cc725907.aspx "Panoramica di Multipath I/O and features").  

MPIO deve essere configurata nel dispositivo StorSimple per hello a disponibilità elevata della soluzione StorSimple. Quando MPIO è installato nel server host che eseguono Windows Server 2012 R2, i server hello possono quindi in grado di tollerare un collegamento, rete o errori dell'interfaccia. 

MPIO è una funzionalità facoltativa in Windows Server, e non è installata per impostazione predefinita. Deve essere installata come funzionalità tramite Server Manager. Questo argomento descrive i passaggi di hello devono seguire tooinstall e utilizzo funzionalità MPIO hello in un host che eseguono Windows Server 2012 R2 e connesso tooa dispositivo fisico StorSimple.

> [!NOTE]
> **Questa procedura è valida solo per StorSimple serie 8000. La funzionalità MPIO non è attualmente supportata in un dispositivo virtuale StorSimple.**
> 
> 

È necessario toofollow questi tooconfigure passaggi MPIO nel dispositivo StorSimple:

* Passaggio 1: Installare MPIO nell'host Windows Server hello
* Passaggio 2: Configurare MPIO per volumi StorSimple
* Passaggio 3: Montare i volumi StorSimple sull'host hello
* Passaggio 4: Configurare MPIO per la disponibilità elevata e il bilanciamento del carico

Ogni hello di sopra di passaggi è illustrato in hello le sezioni seguenti.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Passaggio 1: Installare MPIO nell'host Windows Server hello
completamento di questa funzionalità nell'host Windows Server, tooinstall hello seguenti procedure.

#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO nell'host di hello
1. Aprire Server Manager nell'host Windows Server. Per impostazione predefinita, Server Manager viene avviato quando un membro del gruppo Administrators hello accede tooa computer che esegue Windows Server 2012 R2 o Windows Server 2012. Se hello Server Manager non è già aperto, fare clic su **Start > Server Manager**.
   ![Server Manager](./media/storsimple-configure-mpio-windows-server/IC740997.png)
2. Fare clic su **Server Manager > Dashboard > Aggiungi ruoli e funzionalità**. Verrà avviata hello **Aggiungi ruoli e funzionalità** procedura guidata.
   ![Aggiunta guidata ruoli e funzionalità 1](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. In hello **Aggiungi ruoli e funzionalità** guidata hello seguenti:
   
   * In hello **prima di iniziare** pagina, fare clic su **Avanti**.
   * In hello **Selezione tipo di installazione** accettare l'impostazione predefinita hello **basata su ruoli o basata su funzionalità** installazione. Fare clic su **Avanti**.![Aggiunta guidata ruoli e funzionalità 2](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   * In hello **Selezione server di destinazione** pagina, scegliere **selezionare un server dal pool di server hello**. Il server host deve essere rilevato automaticamente. Fare clic su **Avanti**.
   * In hello **Selezione ruoli server** pagina, fare clic su **Avanti**.
   * In hello **Selezione funzionalità** selezionare **Multipath i/o**, fare clic su **Avanti**.![ Aggiunta guidata ruoli e funzionalità 5](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   * In hello **Conferma selezioni per l'installazione** pagina, confermare la selezione di hello e quindi selezionare **riavvio del server di destinazione hello automaticamente se necessario**, come illustrato di seguito. Fare clic su **Installa**.![Aggiunta guidata ruoli e funzionalità 8](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   * Riceverà la notifica al termine dell'installazione di hello. Fare clic su **Chiudi** guidata hello tooclose.![ Aggiunta guidata ruoli e funzionalità 9](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Passaggio 2: Configurare MPIO per volumi StorSimple
La funzionalità MPIO deve volumi StorSimple di tooidentify toobe configurato. tooconfigure MPIO toorecognize i volumi StorSimple, eseguire hello alla procedura seguente.

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>tooconfigure MPIO per i volumi StorSimple
1. Aprire hello **configurazione MPIO**. Fare clic su **Server Manager > Dashboard > Strumenti > MPIO**.
2. In hello **proprietà MPIO** la finestra di dialogo, seleziona hello **individua percorsi multipli** scheda.
3. Selezionare **Aggiungi supporto per dispositivi iSCSI**, quindi fare clic su **Aggiungi**.  
   ![Proprietà MPIO Individua percorsi multipli](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. Riavviare il computer server hello quando richiesto.
5. In hello **proprietà MPIO** finestra di dialogo fare clic su hello **dispositivi MPIO** scheda. Fare clic su **aggiungere**.
    </br>![Proprietà MPIO Dispositivi MPIO](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. In hello **Aggiungi supporto MPIO** nella finestra di dialogo **ID Hardware del dispositivo**, immettere il numero di serie del dispositivo. È possibile ottenere il numero di serie di hello dispositivo l'accesso al servizio StorSimple Manager e quindi passando troppo**dispositivi > Dashboard**. numero di serie Hello viene visualizzato nella finestra di destra hello **Quick Glance** riquadro del dashboard del dispositivo hello.
    </br>![Aggiungi supporto MPIO](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. Riavviare il computer server hello quando richiesto.

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Passaggio 3: Montare i volumi StorSimple sull'host hello
Una volta configurata la funzionalità MPIO in Windows Server, volumi creati nel dispositivo StorSimple hello possono essere montati e possono quindi sfruttare i vantaggi di MPIO per la ridondanza. toomount un volume, eseguire hello alla procedura seguente.

#### <a name="toomount-volumes-on-hello-host"></a>volumi host hello toomount
1. Aprire hello **iniziatore iSCSI-proprietà** finestra in host Windows Server hello. Fare clic su **Server Manager > Dashboard > Strumenti > Iniziatore iSCSI**.
2. In hello **iniziatore iSCSI-proprietà** la finestra di dialogo, fare clic sulla scheda individuazione hello e quindi fare clic su **individua portale destinazione**.
3. In hello **individua portale destinazione** finestra di dialogo casella, hello seguenti:
   
   * Immettere l'indirizzo IP hello di hello porta DATA del dispositivo StorSimple (ad esempio, immettere DATA 0).
   * Fare clic su **OK** tooreturn toohello **iniziatore iSCSI-proprietà** la finestra di dialogo.
     
     > [!IMPORTANT]
     > **Se si utilizza una rete privata per le connessioni iSCSI, immettere l'indirizzo IP hello hello dati della porta di cui è connesso toohello rete privata.**
     > 
     > 
4. Ripetere i passaggi 2-3 per una seconda interfaccia di rete (ad esempio, DATA 1) sul dispositivo. Tenere presente che queste interfacce devono essere abilitate per iSCSI. ulteriori informazioni, vedere toolearn [modificare interfacce di rete](storsimple-modify-device-config.md#modify-network-interfaces).
5. Seleziona hello **destinazioni** scheda hello **iniziatore iSCSI-proprietà** la finestra di dialogo. Dovrebbe essere dispositivo StorSimple hello destinazione IQN in **destinazioni individuate**.

   ![Scheda destinazioni proprietà iniziatore iSCSI](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. Fare clic su **Connetti** tooestablish una sessione iSCSI con il dispositivo StorSimple. Oggetto **connettersi tooTarget** verrà visualizzata la finestra di dialogo.
7. In hello **connettersi tooTarget** la finestra di dialogo, seleziona hello **abilitare multi-path** casella di controllo. Fare clic su **Advanced**.
8. In hello **impostazioni avanzate** finestra di dialogo casella, hello seguenti:                                        
   
   * In hello **scheda locale** elenco a discesa, seleziona **iniziatore iSCSI Microsoft**.
   * In hello **IP iniziatore** elenco a discesa, l'indirizzo IP di hello selezionare dell'host hello.
   * In hello **portale destinazione** IP riepilogo, selezionare hello IP dell'interfaccia di dispositivo.
   * Fare clic su **OK** tooreturn toohello **iniziatore iSCSI-proprietà** la finestra di dialogo.
9. Fare clic su **Proprietà**. In hello **proprietà** la finestra di dialogo, fare clic su **Aggiungi sessione**.
10. In hello **connettersi tooTarget** la finestra di dialogo, seleziona hello **abilitare multi-path** casella di controllo. Fare clic su **Advanced**.
11. In hello **impostazioni avanzate** la finestra di dialogo:                                        
    
    * In hello **scheda locale** elenco a discesa, selezionare iniziatore iSCSI Microsoft.
    * In hello **IP iniziatore** elenco a discesa, host toohello corrispondente di hello selezionare IP indirizzo. In questo caso, ci si connette due interfacce di rete su hello dispositivo tooa singola interfaccia di rete sull'host hello. Pertanto, questa interfaccia è hello identici a quelli forniti per hello prima sessione.
    * In hello **IP portale destinazione** elenco a discesa, indirizzo IP selezionare hello hello seconda interfaccia dati abilitata sul dispositivo hello.
    * Fare clic su **OK** finestra di dialogo Proprietà iniziatore iSCSI toohello di tooreturn. È stata aggiunta una seconda destinazione toohello sessione.
12. Aprire **Gestione Computer** passando troppo**Server Manager > Dashboard > Gestione Computer**. Nel riquadro di sinistra hello, fare clic su **archiviazione > Gestione disco**. Hello volumi creati nel dispositivo StorSimple hello che sono visibili toothis host verranno visualizzato in **Gestione disco** come nuovi dischi.
13. Inizializzare il disco hello e creare un nuovo volume. Durante il processo di formattazione hello, selezionare una dimensione del blocco di 64 KB.
    ![Gestione disco](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. In **Gestione disco**, hello rapida **disco** e selezionare **proprietà**.
15. In hello modello StorSimple # # # **proprietà dispositivo disco con percorsi multipli** finestra di dialogo fare clic su hello **MPIO** scheda. ![StorSimple 8100 Multi-Path Disk DeviceProp.](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. In hello **nome DSM** fare clic su **dettagli** e verificare che i parametri di hello vengono impostati i parametri predefiniti toohello. i parametri predefiniti Hello sono:
    
    * Periodo di verifica percorso = 30
    * Numero di tentativi = 3
    * Periodo di rimozione PDO = 20
    * Intervallo tentativi = 1
    * Verifica percorso attivata = deselezionata.

> [!NOTE]
> **Non modificare i parametri predefiniti hello.**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>Passaggio 4: Configurare MPIO per la disponibilità elevata e il bilanciamento del carico
Per percorsi multipli in base a disponibilità elevata e bilanciamento del carico, più sessioni devono essere aggiunta manualmente toodeclare hello diversi percorsi disponibili. Ad esempio, se hello host dispone di due interfacce connesse dispositivo tooSAN e hello ha due tooSAN connessi di interfacce, sono necessarie quattro sessioni configurate con permutazioni di percorso corrette (solo due sessioni sarà necessario se ogni interfaccia DATA e l'interfaccia dell'host in un'altra subnet IP e non è instradabile).

**È consigliabile disporre di almeno 8 sessioni parallele attive tra il dispositivo di hello e l'applicazione host.** Ciò può essere ottenuto tramite l'abilitazione di 4 interfacce di rete nel sistema Windows Server in uso. Utilizzare le interfacce di rete fisica o virtuale interfacce tramite le tecnologie di virtualizzazione di rete a livello di hardware o sistema operativo hello nell'host Windows Server. Con hello due interfacce di rete nel dispositivo hello, questa configurazione comporta 8 sessioni attive. Questa configurazione consente di ottimizzare la velocità effettiva dispositivo e cloud hello.

> [!IMPORTANT]
> **È consigliabile non combinare interfacce di rete da 1 GbE e da 10 GbE. Se si usano due interfacce di rete, entrambe le interfacce devono essere hello stesso tipo.**

Hello procedura riportata di seguito viene descritto come le sessioni di tooadd quando un dispositivo StorSimple con due interfacce di rete è connessa tooa host con due interfacce di rete. In questo modo solo 2 sessioni sono attive. Utilizzare la stessa procedura con un dispositivo StorSimple con host connesso tooa interfacce di rete due con quattro interfacce di rete. È necessario tooconfigure 8 anziché hello 4 sessioni descritte di seguito.

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>tooconfigure MPIO per la disponibilità elevata e bilanciamento del carico
1. Eseguire un'individuazione della destinazione hello: in hello **iniziatore iSCSI-proprietà** della finestra di dialogo hello **individuazione** scheda, fare clic su **individua portale**.
2. In hello **connettersi tooTarget** finestra di dialogo immettere l'indirizzo IP hello di una delle interfacce di rete del dispositivo hello.
3. Fare clic su **OK** tooreturn toohello **iniziatore iSCSI-proprietà** la finestra di dialogo.
4. In hello **iniziatore iSCSI-proprietà** la finestra di dialogo, seleziona hello **destinazioni** scheda, evidenziare la destinazione hello individuato e quindi fare clic su **Connetti**. Hello **connettersi tooTarget** viene visualizzata la finestra di dialogo.
5. In hello **connettersi tooTarget** la finestra di dialogo:
   
   * Per impostazione predefinita hello lasciare selezionata l'impostazione della destinazione per **Aggiungi connessione** toohello elenco destinazioni preferite. In questo modo il dispositivo hello eseguito automaticamente un tentativo connessione hello toorestart ogni riavvio del computer.
   * Seleziona hello **abilitare multi-path** casella di controllo.
   * Fare clic su **Advanced**.
6. In hello **impostazioni avanzate** la finestra di dialogo:
   
   * In hello **scheda locale** elenco a discesa, seleziona **iniziatore iSCSI Microsoft**.
   * In hello **IP iniziatore** elenco a discesa, l'indirizzo IP di hello selezionare dell'host hello.
   * In hello **IP portale destinazione** elenco a discesa, selezionare hello indirizzo IP di hello dati interfaccia attivato sul dispositivo hello.
   * Fare clic su **OK** finestra di dialogo Proprietà iniziatore iSCSI toohello di tooreturn.
7. Fare clic su **proprietà**e in hello **proprietà** la finestra di dialogo, fare clic su **Aggiungi sessione**.
8. In hello **connettersi tooTarget** la finestra di dialogo, seleziona hello **abilitare multi-path** casella di controllo e quindi fare clic su **avanzate**.
9. In hello **impostazioni avanzate** la finestra di dialogo:
   
   1. In hello **scheda locale** elenco a discesa, seleziona **iniziatore iSCSI Microsoft**.
   2. In hello **IP iniziatore** elenco a discesa, selezionare hello indirizzo IP corrispondente toohello seconda interfaccia sull'host hello.
   3. In hello **IP portale destinazione** elenco a discesa, indirizzo IP selezionare hello hello seconda interfaccia dati abilitata sul dispositivo hello.
   4. Fare clic su **OK** tooreturn toohello **iniziatore iSCSI-proprietà** la finestra di dialogo. È stato aggiunto una secondo destinazione toohello sessione.
10. Ripetere destinazione toohello di passaggi da 8 a 10 tooadd altre sessioni (percorsi). Con due interfacce sull'host hello e due su dispositivo hello, è possibile aggiungere un totale di quattro sessioni.
11. Dopo aver aggiunto le sessioni di hello desiderato (percorsi), in hello **iniziatore iSCSI-proprietà** la finestra di dialogo, destinazione hello selezionare e fare clic su **proprietà**. Nella scheda sessioni hello di hello **proprietà** della finestra di dialogo Nota hello quattro identificatori di sessione che corrispondono toohello possibili permutazioni di percorso. toocancel una sessione, selezionare l'identificatore di sessione successiva tooa di hello casella di controllo e quindi fare clic su **Disconnect**.
12. tooview dispositivi presentati nelle sessioni, seleziona hello **dispositivi** hello tooconfigure scheda Criteri MPIO per un dispositivo selezionato, fare clic su **MPIO**. Hello **dettagli dispositivo** verrà visualizzata la finestra di dialogo. In hello **MPIO** scheda, è possibile selezionare hello appropriato **il criterio di bilanciamento del carico** impostazioni. È inoltre possibile visualizzare hello **Active** o **Standby** tipo di percorso.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni, vedere [utilizzando hello toomodify servizio StorSimple Manager la configurazione del dispositivo StorSimple](storsimple-modify-device-config.md).

