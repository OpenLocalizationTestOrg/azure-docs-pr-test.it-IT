---
title: dispositivo di Microsoft Azure StorSimple 8100 aaaInstall | Documenti Microsoft
description: Viene descritto come toounpack, montaggio rack e cablare il dispositivo StorSimple 8100 prima di distribuire e configurare il software di hello.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6098a01e-c031-488a-a8d7-0b607ce665e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 76b94e57318b6c25dc3333ae73edc9e4752b7d1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8100-device"></a>Disimballaggio, montaggio su rack e cablaggio del dispositivo StorSimple 8100
## <a name="overview"></a>Panoramica
Il dispositivo Microsoft Azure StorSimple 8100 è un dispositivo a singolo enclosure montato su rack. In questa esercitazione viene illustrato come cavo toounpack e montaggio in rack hardware dei dispositivi StorSimple 8100 hello prima di configurare e distribuire il dispositivo di StorSimple hello.

## <a name="unpack-your-storsimple-8100-device"></a>Disimballare il dispositivo StorSimple 8100
Hello passaggi seguenti offrono chiare e istruzioni dettagliate su come toounpack il dispositivo di archiviazione StorSimple 8100. Questo dispositivo viene fornito in una singola confezione.

### <a name="prepare-toounpack-your-device"></a>Preparare il dispositivo di toounpack
Prima di Disimballare il dispositivo, verificare le seguenti informazioni hello.

![Icona di avviso](./media/storsimple-safety/IC740879.png)![icona peso elevato](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png)**AVVISO**

1. Assicurarsi di disporre di due persone toomanage disponibili hello spessore enclosure hello se si sta gestendo manualmente. Un'enclosure completamente configurata può pesare backup too32 kg (70 lb.).
2. Posizionare la casella di hello su una superficie piana.

Eseguire quindi hello seguendo i passaggi toounpack il dispositivo.

#### <a name="toounpack-your-device"></a>toounpack del dispositivo
1. Controllare la casella di hello e hello in schiuma per schiacciamenti, tagli, guasti provocati dall'acqua o altri danni evidenti. Se la casella di hello o creazione di pacchetti è gravemente danneggiato, non aprire casella hello. . [Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) toohelp si valuta se il dispositivo di hello è funzioni correttamente.
2. Decomprimere casella hello. Hello seguente immagine Mostra hello decompresso di dispositivo StorSimple.
   
     ![Disimballare il dispositivo di archiviazione](./media/storsimple-8100-hardware-installation/HCSUnpackyour2Udevice.png)
   
    **Dispositivo di archiviazione disimballato**
   
   | Etichetta | Descrizione |
   | --- | --- |
   |   1 |Scatola |
   |   2 |Protezione inferiore |
   |   3 |Dispositivo |
   |   4 |Protezione superiore |
   |   5 |Scatola accessori |
3. Una volta hello scatola, verificare di disporre di:
   
   * 1 Dispositivo a singolo enclosure
   * 2 cavi di alimentazione
   * 1 cavo Ethernet incrociato
   * 2 cavi console seriali
   * 1 convertitore seriale-USB per l'accesso seriale
   * 1 cacciavite T10 tamper-proof
   * 4 schede da QSFP a SFP+ da usare con interfacce di rete 10 GbE
   * 1 kit per il montaggio in rack (2 guide laterali con componenti di montaggio)
   * Guida introduttiva
     
     Se non si dispone delle hello elementi sopra elencati, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).

passaggio successivo Hello è toorack montaggio del dispositivo.

## <a name="rack-mount-your-storsimple-8100-device"></a>Montare su rack il dispositivo StorSimple 8100
Seguire hello successivi passaggi tooinstall il dispositivo di archiviazione StorSimple 8100 in un rack standard da 19 pollici con anteriori e posteriori. il dispositivo StorSimple 8100 Hello contiene un'unica enclosure principale.

installazione di Hello è costituita da più passaggi, ognuno dei quali è descritto nelle procedure hello.

> [!IMPORTANT]
> I dispositivi StorSimple devono essere montati su rack per il corretto funzionamento.
> 
> 

### <a name="prepare-hello-site"></a>Preparare il sito hello
Hello dispositivo deve essere installato in un rack standard da 19 pollici con montanti anteriori e posteriori. Utilizzare hello seguente tooprepare procedure per l'installazione in rack.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>sito hello tooprepare per l'installazione in rack
1. Assicurarsi che il dispositivo hello viene posizionato in modo sicuro su una, stabile e piana superficie di lavoro (o simile).
2. Verificare che il sito di hello in cui si intende tooset backup dispone di alimentazione CA standard da un'origine indipendente o un'unità di distribuzione di alimentazione (PDU) rack con la potenza di una gruppo di continuità (UPS) di fornire.
3. Verificare che sia disponibile in rack hello in cui si intende dispositivo hello toomount tale slot uno 2U.

![Icona di avviso](./media/storsimple-safety/IC740879.png)![icona peso elevato](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png)**AVVISO**

Assicurarsi di disporre di peso hello di due persone toomanage disponibili se si sta gestendo il programma di installazione di hello dispositivo manualmente. Un'enclosure completamente configurata può pesare backup too32 kg (70 lb.).

### <a name="rack-prerequisites"></a>Prerequisiti del rack
enclosure 8100 Hello è progettato per l'installazione in un rack da 19 pollici standard CAB con:

* Profondità minima di 27,84 pollici dal rack post toopost.
* Peso massimo di 32 kg per il dispositivo hello
* Contropressione massima di 5 Pascal (corrispondente alla pressione esercitata da una colonna di acqua di 0,5 mm).

### <a name="rack-mounting-rail-kit"></a>Kit per il montaggio su rack
Per l'utilizzo con armadio rack da 19 pollici hello viene fornito un set di guide di montaggio. le sbarre Hello sono stati testati peso massimo dell'enclosure di hello toohandle. Le guide anche consentiranno l'installazione di più enclosure senza alcuna perdita di spazio nel rack hello.

#### <a name="tooinstall-hello-device-on-hello-rails"></a>dispositivo hello tooinstall Guide hello
1. Eseguire questo passaggio solo se non ci sono guide interne installate sul dispositivo. Guide interna hello in genere, vengono installati nella factory hello. Se non sono installati Guide, quindi installare hello slitte delle guide destra e sinistra toohello i lati del telaio dell'enclosure hello. Tali slitte vengono fissate a ciascun lato con sei viti metriche. toohelp con orientamento, sbarra hello slitte delle guide sono contrassegnate **LH-Front** e **RH-Front**, e di fine hello apposta parte posteriore di hello dell'enclosure hello è un affusolata.<br/>
   
    ![Collegamento sbarra diapositive tooenclosure chassis](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)

    **Collegamento sbarra interna diapositive toohello i lati dell'enclosure hello**
   
    Etichetta | Descrizione
    ----- | -----------
    1     | Viti con testa a bottone M 3X4
    2     | Guide dello chassis

2. Associare sbarra left outer hello e destra outer assembly toohello verticali dell'armadio rack. Hello supporti sono contrassegnati con **LH**, **RH**, e **questo lato backup** tooguide tramite hello correggere orientamento.
3. Individuare i perni hello in hello anteriore e posteriore di assembly sbarra hello. Estendere hello sbarra toofit tra hello montanti del rack e inserire il PIN hello anteriore hello e rack posteriore post verticale fori. Assicurarsi che l'assembly sbarra hello sia livello.
4. Utilizzare due membri hello fornito viti metriche toosecure hello sbarra assembly toohello rack verticale. Usare una vite per hello anteriore e una sul retro hello.
5. Ripetere questi passaggi per hello altro gruppo Guida.<br/>
   
     ![Collegamento toorack diapositive sbarra CAB](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Collegamento esterno sbarra assembly toohello rack**
   
   | Etichetta | Descrizione |
   | --- | --- |
   |   1 |Vite di fissaggio |
   |   2 |Montante rack anteriore con fori quadrati |
   |   3 |Perni di posizionamento della guida sinistra (parte anteriore) |
   |   4 |Vite di fissaggio |
   |   5 |Perni di posizionamento della guida sinistra (parte posteriore) |

### <a name="mounting-hello-device-in-hello-rack"></a>Montaggio hello dispositivo nel rack hello
Usando hello guide appena installate, eseguire hello seguendo i passaggi toomount hello dispositivo rack hello.

#### <a name="toomount-hello-device"></a>dispositivo hello toomount
1. Con un Assistente, sollevare hello enclosure e allinearla alle guide rack hello.
2. Inserire delicatamente dispositivo hello in Guide hello e quindi eseguire il push dispositivo hello completamente in rack hello CAB.<br/>
   
    ![Inserimento del dispositivo nel rack hello](./media/storsimple-8100-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Montaggio hello dispositivo nel rack hello**
3. Rimuovere hello sinistra e destra anteriore copriflangia estraendo caps hello disponibile. copriflangia Hello semplicemente bloccata su hello flange.
4. Fissare l'enclosure di hello in rack hello con l'installazione uno fornito vite a croce in ciascuna flangia, sinistra e destra.
5. Installare hello copriflangia premendoli nella posizione e li allineamento sul posto.<br/>
   
     ![Installazione dei copriflangia](./media/storsimple-8100-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Installazione dei copriflangia hello**
   
   | Etichetta | Descrizione |
   | --- | --- |
   |   1 |Vite di fissaggio dell'enclosure |

passaggio successivo Hello è toocable del dispositivo per l'alimentazione, rete e accesso seriale.

## <a name="cable-your-storsimple-8100-device"></a>Cablare il dispositivo StorSimple 8100
Hello procedure seguenti illustrano come toocable il dispositivo StorSimple 8100 per l'alimentazione, rete e porte seriali.

### <a name="prerequisites"></a>Prerequisiti
Prima di iniziare hello cablaggio del dispositivo, è necessario:

* Il dispositivo di archiviazione, interamente disimballato e montato in rack.
* 2 cavi di alimentazione inclusi con il dispositivo
* Accesso too2 unità Power Distribution (scelta consigliata).
* Cavi di rete
* Cavi seriali forniti
* Convertitore seriale-USB con driver di hello appropriato installato sul PC (se necessario)
* 4 schede da QSFP a SFP fornite da usare con interfacce di rete 10 GbE
* [Hardware supportati per le interfacce di rete GbE hello 10 nel dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="power-cabling"></a>Cablaggio di alimentazione
Il dispositivo include moduli PCM (Power and Cooling Modules) Entrambi i PCM devono essere installati e connesso toodifferent power origini tooensure la disponibilità elevata.

Eseguire hello seguendo i passaggi toocable il dispositivo per l'alimentazione.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

### <a name="network-cabling"></a>Cablaggio di rete
Il dispositivo non è una configurazione attivo-standby: in qualsiasi momento, un modulo controller è attivo e l'elaborazione di tutte le operazioni su disco e rete mentre hello altro modulo controller in standby. Se un controller non riesce, controller in standby hello viene attivata immediatamente e continua tutte le operazioni su disco e rete hello.

toosupport il failover del controller ridondante, è necessario toocable il dispositivo di rete come descritto in hello alla procedura seguente.

#### <a name="toocable-for-network-connection"></a>toocable per la connessione di rete
1. Il dispositivo è dotato di sei interfacce di rete su ciascun controller: quattro porte Ethernet da 1 Gbps e due da 10 Gbps. Identificare hello diversi dati porte nel hello backplane del dispositivo.
   
    ![Backplane del dispositivo 8100](./media/storsimple-8100-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Parte posteriore dispositivo di hello con porte dati**
   
   | Etichetta | Description |
   | --- | --- |
   |   0,1,4,5 |Interfacce di rete da 1 GbE |
   |   2,3 |Interfacce di rete da 10 GbE |
   |   6 |Porte seriali |
2. Vedere hello seguente diagramma di cablaggio di rete. (configurazione di rete minima di hello è indicata da linee blu continue. La configurazione aggiuntiva richiesta per una disponibilità elevata e prestazioni ottimali è indicata da linee tratteggiate.

    ![Cablare il dispositivo 2U per la rete](./media/storsimple-8100-hardware-installation/HCSCableYour2UDeviceforNetwork.png)

    **Cablaggio di rete per il dispositivo**

   |Etichetta | Descrizione |
   |----- | ----------- |
   | A    | LAN con accesso a Internet |
   | B    | Controller 0 |
   | C    | PCM 0 |
   | D    | Controller 1 |
   | E    | PCM 1 |
   | F, G | Hosts |
   | 0-5  | Interfacce di rete |



Quando il cablaggio dispositivo hello, richiede la configurazione minima di hello:

* Almeno due interfacce di rete connesse in ogni controller, di cui una per l'accesso al cloud e l'altra per iSCSI. DATA 0, la porta è automaticamente abilitata e configurata mediante la console seriale del dispositivo hello hello Hello. Oltre a DATA 0, un'altra porta dati che deve anche toobe configurato tramite hello portale di Azure classico. In questo caso, la connessione dati 0 porta toohello rete LAN principale (rete con accesso a Internet). Hello altri dati porte possono essere connesso segmento di tooSAN/iSCSI LAN (VLAN) della rete hello, in base al ruolo hello previsto.
* Interfacce identiche su ogni toohello controller connessi stessa rete tooensure disponibilità se si verifica un failover del controller. Ad esempio, se si sceglie tooconnect DATA 0 e DATA 3 di uno dei controller hello, è necessario tooconnect hello corrispondente DATA 0 e DATA 3 su hello altro controller.

Da tenere presente per prestazioni e disponibilità elevate:

* Se possibile, configurare in ogni controller una coppia di interfacce di rete per l'accesso al cloud (1 GbE) e un'altra coppia per iSCSI (10 GbE consigliati).
* Se possibile, connettersi interfacce di rete da ogni disponibilità di controller tootwo diversi commutatori tooensure contro un malfunzionamento dell'interruttore. Hello illustrata hello due da 10 GbE interfacce di rete, DATA 2 e DATA 3, da ogni controller connessi tootwo diversi commutatori.

Per ulteriori informazioni, vedere toohello **interfacce di rete** in hello [requisiti di disponibilità elevata per il dispositivo StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Se si utilizza ricetrasmettitori SFP + con le interfacce di rete 10 GbE, utilizzare hello fornito QSFP-SFP + schede. Per ulteriori informazioni, visitare troppo[hardware supportato per le interfacce di rete GbE hello 10 nel dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Cablaggio della porta seriale
Eseguire hello seguendo i passaggi toocable la porta seriale.

#### <a name="toocable-for-serial-connection"></a>toocable per la connessione seriale
1. Il dispositivo è dotato di una porta seriale su ogni controller, identificata da un'icona a forma di chiave inglese. Vedere l'illustrazione toohello in hello [cavi di rete](#network-cabling) sezione toolocate hello porte seriali hello backplane del dispositivo.
2. Identificare hello controller attivo sul backplane del dispositivo. Un LED blu lampeggiante indica che tale controller hello è attivo.
3. Usare i cavi seriali di hello fornito (se necessario, il convertitore hello USB-seriale per il portatile) e connettere la console o il computer (con dispositivo toohello emulazione di terminale) toohello porta seriale del controller attivo hello.
4. Installare i driver seriali-USB hello (forniti con il dispositivo hello) nel computer.
5. Configurare la connessione seriale hello come segue: 115.200 baud, 8 bit di dati, 1 bit di stop, nessuna parità e controllo di flusso impostare tooNone.
6. Verificare che hello connessione funzioni premendo INVIO nella finestra di console hello. Deve comparire un menu della console seriale.

> [!NOTE]
> **Gestione Lights-Out**: quando hello dispositivo è installato in un Data Center remoto o in una sala macchine con accesso limitato, assicurarsi che i controller di hello seriali tooboth siano sempre connessi tooa interruttore della console seriale o ad apparecchiature simili. In questo modo, sono possibili operazioni di supporto e controllo remoto fuori banda in caso di interruzione della connessione di rete o malfunzionamenti imprevisti.
> 
> 

Il dispositivo è ora collegato per l'alimentazione, l'accesso di rete e quello seriale. passaggio successivo Hello tooconfigure hello software e distribuire il dispositivo.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come troppo[distribuire e configurare il dispositivo StorSimple locale](storsimple-deployment-walkthrough-u2.md).

