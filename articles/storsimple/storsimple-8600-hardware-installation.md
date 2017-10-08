---
title: dispositivo di Microsoft Azure StorSimple 8600 aaaInstall | Documenti Microsoft
description: Viene descritto come toounpack, montaggio rack e cablare il dispositivo StorSimple 8600 prima di distribuire e configurare il software di hello.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>Disimballaggio, montaggio su rack e cablaggio del dispositivo StorSimple 8600
## <a name="overview"></a>Panoramica
Microsoft Azure StorSimple 8600 è un dispositivo enclosure con doppio alloggiamento, costituito da un'enclosure principale e un'enclosure EBOD. In questa esercitazione viene illustrato come cavo toounpack e montaggio in rack hardware dei dispositivi StorSimple 8600 hello prima di configurare il software di StorSimple hello.

## <a name="unpack-your-storsimple-8600-device"></a>Disimballare il dispositivo StorSimple 8600
Hello passaggi seguenti offrono chiare e dettagliate su come toounpack il dispositivo di archiviazione StorSimple 8600. Il dispositivo viene fornito in due caselle, uno per l'enclosure principale hello e un altro per hello enclosure EBOD. Queste due scatole vengono poi inserite in una scatola singola.

### <a name="prepare-toounpack-your-device"></a>Preparare il dispositivo di toounpack
Prima di Disimballare il dispositivo, verificare le seguenti informazioni hello.

![Icona di avviso](./media/storsimple-safety/IC740879.png)![icona peso elevato](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **AVVISO**

1. Assicurarsi di disporre di due persone toomanage disponibili hello spessore dispositivo hello se si sta gestendo manualmente. Un'enclosure completamente configurata può pesare backup too32 kg (70 lb.).
2. Posizionare la casella di hello su una superficie piana.

Eseguire quindi hello seguendo i passaggi toounpack il dispositivo.

#### <a name="toounpack-your-device"></a>toounpack del dispositivo
1. Controllare la casella di hello e hello in schiuma per schiacciamenti, tagli, guasti provocati dall'acqua o altri danni evidenti. Se la casella di hello o creazione di pacchetti è gravemente danneggiato, non aprire casella hello. . [Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) toohelp si valuta se il dispositivo di hello è funzioni correttamente.
2. Aprire hello outer dialogo e quindi estrarre due caselle hello corrispondente tooprimary e l'enclosure EBOD. È ora possibile decomprimere hello primario e l'enclosure EBOD. Hello seguente illustrazione mostra hello decompresso di una delle enclosure hello.
   
    ![Disimballare il dispositivo di archiviazione](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **Dispositivo di archiviazione disimballato**
   
   | Etichetta | Descrizione |
   | --- | --- |
   |   1 |Scatola |
   |   2 |Cavi SAS (nel vassoio cavi e accessori) |
   |   3 |Protezione inferiore |
   |   4 |Dispositivo |
   |   5 |Protezione superiore |
   |   6 |Scatola accessori |
3. Dopo aver decompresso caselle hello due, assicurarsi di disporre di:
   
   * 1 enclosure principale (hello enclosure principale ed EBOD sono confezionate separatamente)
   * 1 enclosure EBOD
   * 4 cavi di alimentazione, 2 in ciascuna scatola
   * 2 cavi SAS (enclosure tooEBOD per tooconnect hello enclosure principale)
   * 1 cavo Ethernet incrociato
   * 2 cavi console seriali
   * 1 convertitore seriale-USB per l'accesso seriale
   * 4 schede da QSFP a SFP da usare con interfacce di rete 10 GbE
   * 2 rack Kit di montaggio (4 Guide laterali con montaggio, 2 per hello enclosure principale ed EBOD), 1 in ciascuna casella
   * Guida introduttiva
     
     Se non si dispone delle hello elementi sopra elencati, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).  

passaggio successivo Hello è toorack montaggio del dispositivo.

## <a name="rack-mount-your-storsimple-8600-device"></a>Montare su rack il dispositivo StorSimple 8600
Seguire hello successivi passaggi tooinstall il dispositivo di archiviazione StorSimple 8600 in un rack standard da 19 pollici con anteriori e posteriori. Il dispositivo è costituito da due enclosure, una principale e una EBOD, Entrambi questi necessario toobe montate su rack.

installazione di Hello è costituita da più passaggi, ognuno dei quali è descritto nelle procedure hello.

> [!IMPORTANT]
> I dispositivi StorSimple devono essere montati su rack per il corretto funzionamento.
> 
> 

### <a name="site-preparation"></a>Operazioni preliminari
Hello enclosure devono essere installate in un rack standard da 19 pollici con montanti anteriori e posteriori. Utilizzare hello seguente tooprepare procedure per l'installazione in rack.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>sito hello tooprepare per l'installazione in rack
1. Verificare che tale hello primario e l'enclosure EBOD sono in sospeso in modo sicuro in un'area di lavoro, stabile e piana (o simile).
2. Verificare di tale sito hello in cui si intende tooset backup ha AC standard alimentazione da un'origine indipendente o un'unità di distribuzione dell'alimentazione (PDU) rack con un gruppo di continuità (UPS).
3. Assicurarsi che sia disponibile nel rack hello in cui si intendono enclosure hello toomount slot uno 4U (2 X 2U).

![Icona di avviso](./media/storsimple-safety/IC740879.png)![icona peso elevato](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **AVVISO**

 Assicurarsi di disporre di peso hello di due persone toomanage disponibili se si sta gestendo il programma di installazione di hello dispositivo manualmente. Un'enclosure completamente configurata può pesare backup too32 kg (70 lb.).

### <a name="rack-prerequisites"></a>Prerequisiti del rack
Hello enclosure sono progettate per l'installazione in un rack da 19 pollici standard CAB con:

* Profondità minima di 27,84 pollici dal rack post toopost
* Peso massimo di 32 kg per il dispositivo hello
* Contropressione massima di 5 Pascal (corrispondente alla pressione esercitata da una colonna di acqua di 0,5 mm)

### <a name="rack-mounting-rail-kit"></a>Kit per il montaggio su rack
Viene fornito un set di guide di montaggio per l'utilizzo con armadio rack da 19 pollici hello. le sbarre Hello sono stati testati peso massimo dell'enclosure di hello toohandle. Le guide è possibile installare altre enclosure senza occupare spazio all'interno di rack hello anche. Installare prima l'enclosure EBOD hello.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>hello tooinstall enclosure EBOD in Guide hello
1. Eseguire questo passaggio solo se non ci sono guide interne installate sul dispositivo. Guide interna hello in genere, vengono installati nella factory hello. Se non sono installati Guide, quindi installare hello slitte delle guide destra e sinistra toohello i lati del telaio dell'enclosure hello. Tali slitte vengono fissate a ciascun lato con sei viti metriche. toohelp con orientamento, sbarra hello slitte delle guide sono contrassegnate **LH-Front** e **RH-Front**, e di fine hello apposta parte posteriore di hello dell'enclosure hello è un affusolata.
   
    ![Collegamento sbarra diapositive tooenclosure chassis](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **Collegamento sbarra diapositive toohello i lati dell'enclosure hello**
   
   | Etichetta | Descrizione |
   | --- | --- |
   |  1 |Viti con testa a bottone M 3X4 |
   |  2 |Guide dello chassis |
2. Collegare Guida sinistra hello e destra assembly toohello verticali dell'armadio rack. Hello supporti sono contrassegnati con **LH**, **RH**, e **questo lato backup** tooguide tramite un corretto orientamento.
3. Individuare i perni hello in hello anteriore e posteriore di assembly sbarra hello. Estendere hello sbarra toofit tra hello montanti del rack e inserire il PIN hello hello post anteriore e posteriore rack verticale fori. Assicurarsi che l'assembly sbarra hello sia livello.
4. Proteggere hello rack toohello di assembly sbarra verticali membri utilizzando due delle viti metriche hello forniti. Usare una vite per hello anteriore e una sul retro hello.
5. Ripetere questi passaggi per hello altro gruppo Guida.
   
     ![Collegamento toorack diapositive sbarra CAB](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Collegamento sbarra assembly toohello rack**
   
   | Etichetta | Descrizione |
   | --- | --- |
   |   1 |Vite di fissaggio |
   |   2 |Montante rack anteriore con fori quadrati |
   |   3 |Perni di posizionamento della guida sinistra (parte anteriore) |
   |   4 |Vite di fissaggio |
   |   5 |Perni di posizionamento della guida sinistra (parte posteriore) |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Montaggio dell'enclosure EBOD hello in rack hello
Usando hello guide appena installate, eseguire hello seguente enclosure EBOD di passaggi toomount hello in rack hello.

#### <a name="toomount-hello-ebod-enclosure"></a>hello toomount enclosure EBOD
1. Con un Assistente, sollevare hello enclosure e allinearla alle guide rack hello.
2. Inserire delicatamente enclosure hello in Guide hello e quindi inserirlo completamente rack hello CAB.
   
    ![Inserimento del dispositivo nel rack hello](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Montaggio hello enclosure nel rack hello**
3. Rimuovere hello sinistra e destra anteriore copriflangia estraendo caps hello disponibile. copriflangia Hello semplicemente bloccata su hello flange.
4. Fissare enclosure hello in rack hello con l'installazione uno fornito vite a croce in ciascuna flangia, sinistra e destra.
5. Installare hello copriflangia premendoli nella posizione e tali blocchi in posizione.
   
     ![Installazione dei copriflangia](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Installazione dei copriflangia hello**
   
   | Etichetta | Descrizione |
   | --- | --- |
   |   1 |Vite di fissaggio dell'enclosure |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Montare l'enclosure principale hello rack hello
Dopo aver completato il montaggio dell'enclosure EBOD hello, sarà necessario enclosure principale di hello toomount seguente hello stessi passaggi.

> [!NOTE]
> * È possibile toohave alcuni slot vuoti in hello rack tra hello primario e hello EBOD.
> * Utilizzare hello fornito 2M SAS cavo tooconnect hello enclosure principale toohello EBOD enclosure.
> * Non sono presenti vincoli nella posizione relativa di hello di hello head unità toohello EBOD unità di misura. Pertanto, enclosure principale hello può essere inserita in slot superiore hello e l'enclosure EBOD hello sotto, o viceversa.
> 
> 

passaggio successivo Hello è toocable del dispositivo per l'alimentazione, rete e accesso seriale.

## <a name="cable-your-storsimple-8600-device"></a>Cablare il dispositivo StorSimple 8600
Hello procedure seguenti illustrano come toocable del dispositivo 8600 di StorSimple per l'alimentazione, rete e porte seriali.

### <a name="prerequisites"></a>Prerequisiti
Prima di iniziare toocable il dispositivo, è necessario:

* L'enclosure principale e l'enclosure EBOD hello, completamente disimballate
* 4 cavi di alimentazione (2 ogni hello primario e hello enclosure EBOD) forniti con il dispositivo
* 2 cavi SAS forniti con hello di hello dispositivo tooconnect enclosure principale toohello di enclosure EBOD
* Unità di distribuzione accesso too2 alimentazione (PDU) (scelta consigliata)
* Cavi di rete
* Cavi seriali forniti
* Convertitore seriale-USB con driver di hello appropriato installato sul PC (se necessario)
* 4 schede da QSFP a SFP fornite da usare con interfacce di rete 10 GbE
* [Hardware supportati per le interfacce di rete GbE hello 10 nel dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>SAS e i cavi di alimentazione
Il dispositivo è costituito da un'enclosure principale e un'enclosure EBOD. Questa operazione richiede hello unità toobe cablate insieme per la connettività SAS Serial Attached SCSI () e l'alimentazione.

Quando si imposta questo dispositivo per hello prima volta, eseguire hello del cablaggio SAS innanzitutto e passaggi hello quindi completo per il collegamento all'alimentazione.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>Cablaggio di rete
Il dispositivo sia in una configurazione attivo-standby: in qualsiasi momento, un modulo controller è attivo e l'elaborazione di tutte le operazioni su disco e rete mentre hello altro modulo controller in standby. Se si verifica un errore nel controller, controller in standby hello immediatamente attiva e continua a tutte le operazioni su disco e rete hello.

toosupport il failover del controller ridondante, è necessario che il dispositivo di rete come illustrato nella procedura hello toocable.

#### <a name="toocable-for-network-connection"></a>toocable per la connessione di rete
1. Il dispositivo è dotato di sei interfacce di rete su ciascun controller: quattro porte Ethernet da 1 Gbps e due da 10 Gbps. Fare riferimento toohello seguendo porte dati hello di illustrazione tooidentify hello backplane del dispositivo.
   
     ![Backplane del dispositivo 8600](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Parte posteriore del dispositivo con le porte dati hello**
   
   | Etichetta | Description |
   | --- | --- |
   |   0,1,4,5 |Interfacce di rete da 1 GbE |
   |   2,3 |Interfacce di rete da 10 GbE |
   |   6 |Porte seriali |
2. Vedere hello seguente diagramma di cablaggio di rete. (configurazione di rete minima di hello è indicata da linee blu continue. Per una disponibilità elevata e prestazioni ottimali, la configurazione aggiuntiva richiesta è indicata da linee tratteggiate.

![Cablare il dispositivo 4U per la rete](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**Cablaggio di rete per il dispositivo**

| Etichetta | Descrizione |
| --- | --- |
| A |LAN con accesso a Internet |
| B |Controller 0 |
| C |PCM 0 |
| D |Controller 1 |
| E |PCM 1 |
| F |Controller 0 EBOD |
| G |Controller 1 EBOD |
| H,I |Host (ad esempio, file server) |
| 0-5 |Interfacce di rete |
| 6 |Enclosure principale |
| 7 |Chassis EBOD |

Quando il cablaggio dispositivo hello, richiede la configurazione minima di hello:

* Almeno due interfacce di rete connesse in ogni controller, di cui una per l'accesso al cloud e l'altra per iSCSI. DATA 0, la porta è automaticamente abilitata e configurata mediante la console seriale del dispositivo hello hello Hello. Oltre a DATA 0, un'altra porta dati che deve anche toobe configurato tramite hello portale di Azure classico. In questo caso, la connessione dati 0 porta toohello rete LAN principale (rete con accesso a Internet). Hello altri dati porte possono essere connesso segmento di tooSAN/iSCSI LAN (VLAN) della rete hello, in base al ruolo hello previsto.
* Interfacce identiche su ogni toohello controller connessi stessa rete tooensure disponibilità se si verifica un failover del controller. Ad esempio, se si sceglie tooconnect DATA 0 e DATA 3 di uno dei controller hello, è necessario tooconnect hello corrispondente DATA 0 e DATA 3 su hello altro controller.

Da tenere presente per prestazioni e disponibilità elevate:

* Se possibile, configurare in ogni controller una coppia di interfacce di rete per l'accesso al cloud (1 GbE) e un'altra coppia per iSCSI (10 GbE consigliati).
* Se possibile, connettersi interfacce di rete da ogni disponibilità di controller tootwo diversi commutatori tooensure contro un malfunzionamento dell'interruttore. Hello illustrata hello due da 10 GbE interfacce di rete, DATA 2 e DATA 3, da ogni controller connessi tootwo diversi commutatori. Per ulteriori informazioni, vedere toohello **interfacce di rete** in hello [requisiti di disponibilità elevata per il dispositivo StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Se si utilizza ricetrasmettitori SFP + con le interfacce di rete 10 GbE, utilizzare hello fornito QSFP-SFP + schede. Per ulteriori informazioni, visitare troppo[hardware supportato per le interfacce di rete GbE hello 10 nel dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Cablaggio della porta seriale
Eseguire hello seguendo i passaggi toocable la porta seriale.

#### <a name="toocable-for-serial-connection"></a>toocable per la connessione seriale
1. Il dispositivo è dotato di una porta seriale su ogni controller, identificata da un'icona a forma di chiave inglese. porte seriali hello toolocate, fare riferimento toohello illustrazione porte dati hello in hello parte posteriore del dispositivo.
2. Identificare hello controller attivo sul backplane del dispositivo. Un LED blu lampeggiante indica che tale controller hello è attivo.
3. Utilizzare hello fornito il cavo seriale (se necessario, il convertitore hello USB-seriale per il portatile) e connettere la console o il computer (con dispositivo di emulazione di terminale toohello) toohello porta seriale del controller attivo hello.
4. Installare i driver seriali-USB hello (forniti con il dispositivo hello) nel computer.
5. Configurare la connessione seriale hello come segue:
   
   * 115.200 baud
   * 8 bit di dati
   * 1 bit di stop
   * Nessuna parità
   * Controllo di flusso è stato impostato troppo**nessuno**
6. Verificare che hello connessione funzioni premendo INVIO nella finestra di console hello. Deve comparire un menu della console seriale.

> [!NOTE]
> **Gestione Lights-Out:** quando hello dispositivo è installato in un Data Center remoto o in una sala macchine con accesso limitato, assicurarsi che i controller di hello seriali tooboth siano sempre connessi tooa interruttore della console seriale o ad apparecchiature simili. In questo modo, sono possibili operazioni di supporto e controllo remoto fuori banda in caso di interruzione della connessione di rete o malfunzionamenti imprevisti.
> 
> 

È stata completata cablaggio del dispositivo per l'alimentazione, l'accesso alla rete, e seriale connection.hello successivo è un software di hello tooconfigure sul dispositivo.

## <a name="next-steps"></a>Passaggi successivi
Si è pronti a questo punto troppo[distribuire e configurare il dispositivo StorSimple locale](storsimple-deployment-walkthrough-u2.md).

