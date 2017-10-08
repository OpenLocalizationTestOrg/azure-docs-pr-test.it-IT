---
title: dispositivo di StorSimple 8000 tootroubleshoot strumento aaaDiagnostics | Documenti Microsoft
description: "Modalità del dispositivo StorSimple hello descrive e illustra come toouse Windows PowerShell per StorSimple toochange hello modalità del dispositivo."
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>Utilizzare hello lo strumento di diagnostica StorSimple tootroubleshoot 8000 series problemi dei dispositivi

## <a name="overview"></a>Panoramica

lo strumento di diagnostica StorSimple Hello individua problemi correlati toosystem, prestazioni, rete e lo stato di componenti hardware per un dispositivo StorSimple. strumento di diagnostica Hello può essere utilizzato in scenari diversi. Questi scenari includono la pianificazione del carico di lavoro, la distribuzione di un dispositivo StorSimple, valutare l'ambiente di rete hello e determinare le prestazioni di un dispositivo operativo hello. In questo articolo viene fornita una panoramica dello strumento di diagnostica hello e viene descritto come utilizzare lo strumento hello con un dispositivo StorSimple.

lo strumento di diagnostica Hello viene usata principalmente per i dispositivi locali serie StorSimple 8000 (8100 e 8600).

## <a name="run-diagnostics-tool"></a>Eseguire lo strumento di diagnostica

Questo strumento può essere eseguito tramite l'interfaccia di Windows PowerShell hello del dispositivo StorSimple. Esistono due modi tooaccess hello interfaccia locale del dispositivo:

* [Console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
* [Accedere in remoto lo strumento hello tramite hello Windows PowerShell per StorSimple](storsimple-remote-connect.md).

In questo articolo si presuppone che si è connessi toohello console seriale del dispositivo tramite PuTTY.

#### <a name="toorun-hello-diagnostics-tool"></a>strumento di diagnostica hello toorun

Dopo avere connesso toohello interfaccia di Windows PowerShell del dispositivo hello, eseguire hello seguendo i passaggi toorun hello cmdlet.
1. Accedere alla procedura seguente hello in console seriale del dispositivo toohello [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).

2. Digitare hello comando seguente:

    `Invoke-HcsDiagnostics`

    Se non è stato specificato il parametro di ambito hello, hello cmdlet esegue tutti i test diagnostici hello. I test riguardano il sistema, l'integrità dei componenti hardware, la rete e le prestazioni. 
    
    toorun solo un test specifico, specificare il parametro di ambito hello. Ad esempio, toorun solo hello test di rete, tipo

    `Invoke-HcsDiagnostics -Scope Network`

3. Selezionare e copiare l'output di hello dal hello PuTTY finestra in un file di testo per un'ulteriore analisi.

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>Strumento di diagnostica di scenari toouse hello

Utilizzare hello diagnostica strumento tootroubleshoot hello rete, le prestazioni, sistema e hardware integrità del sistema hello. Di seguito sono riportati alcuni scenari possibili:

* **Dispositivo offline**: il dispositivo StorSimple serie 8000 è offline. Tuttavia, dall'interfaccia di Windows PowerShell hello, ci risulta che entrambi i controller hello siano in esecuzione.
    * È possibile utilizzare questo strumento toothen determinare lo stato di rete hello.
         
         > [!NOTE]
         > Non utilizzare questo tooassess prestazioni e le impostazioni di rete in un dispositivo prima della registrazione hello (o la configurazione tramite installazione guidata). Un indirizzo IP valido assegnato toohello dispositivo durante la registrazione e installazione guidata. In un dispositivo non registrato è possibile eseguire questo cmdlet per valutare il sistema e l'integrità dell'hardware. Usare il parametro di ambito hello, ad esempio:
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **Problemi dei dispositivi permanenti** -si verificano problemi di dispositivo che sembrano toopersist. Ad esempio, la registrazione ha esito negativo. Si può anche essere problemi dispositivo dopo dispositivo hello è operativo e registrati correttamente per un periodo di tempo.
    * In tal caso, è possibile usare lo strumento di diagnostica per risolvere i problemi prima di inviare una richiesta di servizio al supporto tecnico Microsoft. Ti consigliamo di eseguire l'output di hello strumento e acquisizione di questo strumento. È quindi possibile fornire questo output tooSupport tooexpedite la risoluzione dei problemi.
    * In caso di problemi relativi ai componenti hardware o ai cluster, è necessario inviare una richiesta di supporto.

* **Prestazioni ridotte del dispositivo**: il dispositivo StorSimple è lento.
    * In questo caso, è possibile eseguire questo cmdlet con tooperformance set di parametri di ambito. Analizzare l'output di hello. È possibile ottenere il cloud hello latenze di lettura / scrittura. Hello utilizzare segnalato latenze come destinazione raggiungibile massimo, fattore in un certo overhead per l'elaborazione dati interna hello e quindi distribuire i carichi di lavoro hello nel sistema hello. Per ulteriori informazioni, visitare troppo[utilizzare le prestazioni del dispositivo hello rete test tootroubleshoot](#network-test).


## <a name="diagnostics-test-and-sample-outputs"></a>Test di diagnostica e output di esempio

### <a name="hardware-test"></a>Test dell'hardware

Questo test determina lo stato di hello di componenti hardware hello, al firmware USM hello e firmware del disco hello in esecuzione nel sistema.

* componenti hardware Hello segnalati sono i componenti di tale test hello non riuscito o non sono presenti nel sistema hello.
* versioni del firmware del disco e del firmware Hello USM vengono segnalate per Controller 0, 1 Controller, hello e i componenti condivisi nel sistema. Per un elenco completo dei componenti hardware, vedere:

    * [Componenti nello chassis principale](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [Componenti nello chassis EBOD](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> Se il test dell'hardware hello segnala problemi dei componenti, [log in una richiesta di servizio con il supporto Microsoft](storsimple-contact-microsoft-support.md).

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>Output di esempio del test dell'hardware per un dispositivo 8100

Di seguito è riportato un output di esempio per un dispositivo StorSimple 8100. Nel dispositivo di modello 8100 hello, hello enclosure EBOD non è presente. Di conseguenza, non vengono segnalati i componenti del controller EBOD hello.

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>Test del sistema

Questo test segnala le informazioni di sistema hello, hello gli aggiornamenti disponibili, informazioni sul cluster hello e informazioni hello del servizio per il dispositivo.

* informazioni di sistema Hello includono il modello di hello, numero di serie del dispositivo, fuso orario, lo stato del controller e versione del software dettagliate hello in esecuzione sul sistema hello. hello toounderstand vari parametri di sistema segnalato come output di hello, andare troppo[interpretazione delle informazioni di sistema](#appendix-interpreting-system-information).

* disponibilità di aggiornamenti Hello segnala se sono disponibili le modalità normali e di manutenzione di hello e i relativi nomi di pacchetto associati. Se `RegularUpdates` e `MaintenanceModeUpdates` sono `false`, ciò indica che non sono disponibili aggiornamenti di hello. e il dispositivo è già aggiornato.
* informazioni sul cluster Hello contiene informazioni di hello sui vari componenti logici di tutti i gruppi di cluster HCS hello e i relativi stati rispettivi. Se viene visualizzato un gruppo di cluster non in linea in questa sezione del report hello, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).
* informazioni sul servizio Hello include nomi di hello e gli stati di hello tutti HCS e gli elementi di configurazione servizi in esecuzione sul dispositivo. Queste informazioni sono utili per hello supporto Microsoft nella risoluzione dei problemi di dispositivo hello.

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>Output di esempio del test del sistema per un dispositivo 8100

Di seguito è riportato un esempio di output di hello sistema esecuzione dei test in un dispositivo 8100.

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>Test della rete

Questo test consente di verificare lo stato di hello di interfacce di rete hello, porte, DNS e NTP connettività del server, SSL certificato, le credenziali dell'account di archiviazione, i server di aggiornamento toohello connettività e connettività proxy web nel dispositivo StorSimple.

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>Esempio di output del test della rete quando è abilitata solo l'interfaccia di rete DATA0

Di seguito è riportato un esempio di output del dispositivo 8100 hello. È possibile vedere nell'output di hello che:
* Solo le interfacce di rete DATA0 e DATA1 sono abilitate e configurate.
* 2-5 di dati non sono abilitati nel portale di hello.
* configurazione del server DNS Hello è valida e hello dispositivo possa connettersi attraverso il server DNS hello.
* è inoltre Hello connettività del server NTP.
* Le porte 80 e 443 sono aperte, ma la porta 9354 è bloccata. In base a hello [requisiti di sistema di rete](storsimple-system-requirements.md), tooopen questa porta è necessaria per la comunicazione di hello service bus.
* certificazione SSL Hello è valido.
* account di archiviazione toohello è possibile connettere il dispositivo di Hello: _myss8000storageacct_.
* i server tooUpdate connettività Hello è valido.
* Hello web proxy non è configurato su questo dispositivo.

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>Esempio di output del test della rete quando sono abilitate le interfacce di rete DATA0 e DATA1

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>Test delle prestazioni

Questo test indica prestazioni cloud hello tramite latenze di lettura / scrittura hello cloud per il dispositivo. Questo strumento può essere utilizzato tooestablish una linea di base delle prestazioni di cloud hello che è possibile ottenere con StorSimple. Hello strumento report hello massimo delle prestazioni (scenario migliore per le latenze di lettura / scrittura) che è possibile ottenere per la connessione.

Come strumento hello segnala le massime prestazioni ottenibili hello, possiamo utilizzare hello segnalato le latenze di lettura / scrittura quando si distribuiscono le destinazioni hello carichi di lavoro.

test di Hello simula le dimensioni di blob hello associate a tipi di volume diversa hello sul dispositivo hello. I normali volumi a livelli e i backup dei volumi aggiunti in locale usano dimensioni del BLOB pari a 64 KB. I volumi a livelli con l'opzione di archiviazione selezionata usano dimensioni del BLOB pari a 512 KB. Se il dispositivo dispone di volumi aggiunti in locale e a più livelli è configurato, solo hello test corrispondente too64 KB blob di dimensioni dei dati viene eseguita.

toouse questo strumento, eseguire hello alla procedura seguente:

1.  Creare prima di tutto una combinazione di volumi a livelli e volumi a livelli con l'opzione di archiviazione selezionata. Questa operazione assicura che lo strumento hello esegue i test di hello per 64 KB e 512 KB dimensioni blob.

2. Dopo aver creato e configurato i volumi di hello, eseguire i cmdlet di hello. Digitare:

    `Invoke-HcsDiagnostics -Scope Performance`

3. Prendere nota della latenza di lettura / scrittura hello segnalati dallo strumento hello. Questo test può richiedere diversi minuti toorun prima che riporti i risultati di hello.

4. Se le latenze connessione hello sono tutti in hello intervallo previsto, quindi hello latenze segnalate dallo strumento hello utilizzabili come destinazione raggiungibile massimo quando si distribuiscono i carichi di lavoro di hello. Tenere conto dell'overhead per l'elaborazione dei dati interna.

    Se le latenze di lettura / scrittura hello segnalati lo strumento di diagnostica hello sono elevati:

    1. Configurare l'archiviazione Analitica per i servizi blob e analizzare hello output toounderstand hello latenze per hello account di archiviazione di Azure. Per istruzioni dettagliate, vedere troppo[abilitare e configurare archiviazione Analitica](../storage/common/storage-enable-and-view-metrics.md). Se le latenze sono anche numeri toohello elevata e comparabili ricevuto da hello lo strumento di diagnostica di StorSimple, è necessario toolog una richiesta di servizio con l'archiviazione di Azure.

    2. Se le latenze account di archiviazione hello sono basse, contattare il tooinvestigate di amministratore di rete problemi di latenza della rete.

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>Output di esempio del test delle prestazioni per un dispositivo 8100

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>Appendice: interpretazione delle informazioni sul sistema

Di seguito è riportata una tabella che descrive quale hello per eseguire il mapping di diversi parametri di Windows PowerShell nelle informazioni di sistema hello. 

| Parametro di PowerShell    | Descrizione  |
|-------------------------|------------------|
| ID istanza             | Ogni controller è associato a un identificatore univoco o un GUID.|
| Nome                    | nome descrittivo di Hello del dispositivo hello in base alla configurazione hello portale di Azure durante la distribuzione del dispositivo. nome descrittivo predefinito Hello è hello numero di serie del dispositivo. |
| Modello                   | modello di Hello del dispositivo StorSimple 8000 series. è possibile modello Hello 8100 o 8600.|
| SerialNumber            | numero di serie Hello è assegnato alla factory hello e 15 caratteri. Ad esempio, 8600-SHX0991003G44HT indica quanto segue:<br> 8600: è un modello di dispositivo hello.<br>SHX – è hello di produzione del sito.<br> 0991003: prodotto specifico. <br> G44HT-hello ultimi 5 cifre vengono incrementati toocreate i numeri di serie univoco. Questo potrebbe non essere un insieme sequenziale.|
| TimeZone                | Hello fuso orario del dispositivo come configurato nella hello portale di Azure durante la distribuzione del dispositivo.|
| CurrentController       | controller Hello che si è connessi toothrough interfaccia di Windows PowerShell hello del dispositivo StorSimple.|
| ActiveController        | controller Hello che è attivo sul dispositivo e controlla tutte le operazioni di rete e disco hello. Può trattarsi del Controller 0 o del Controller 1.  |
| Controller0Status       | stato di Hello del Controller 0 sul dispositivo. lo stato del controller Hello può essere normale, in modalità di ripristino o non è raggiungibile.|
| Controller1Status       | Hello lo stato del Controller 1 nel dispositivo.  lo stato del controller Hello può essere normale, in modalità di ripristino o non è raggiungibile.|
| SystemMode              | Hello stato generale del dispositivo StorSimple. stato del dispositivo Hello può essere normale, manutenzione, o non autorizzato (corrisponde toodeactivated in hello portale di Azure).|
| FriendlySoftwareVersion | stringa descrittivo Hello corrispondente toohello versione software del dispositivo. Per un sistema che esegue l'aggiornamento 4, versione del software descrittivo hello sarebbe StorSimple 8000 Series Update 4.0.|
| HcsSoftwareVersion      | versione del software HCS Hello in esecuzione sul dispositivo. Ad esempio, hello HCS software versione corrispondente tooStorSimple 8000 Series Update 4.0 è 6.3.9600.17820. |
| ApiVersion              | versione del software Hello dell'API di Windows PowerShell del dispositivo HCS hello hello.|
| VhdVersion              | versione del software Hello dell'immagine del factory hello hello dispositivo è stata fornita con. Se si reimpostano le impostazioni predefinite del dispositivo toofactory, esegue questa versione del software.|
| OSVersion               | versione del sistema operativo di Windows Server hello in esecuzione sul dispositivo hello software Hello. Windows Server 2012 R2 corrispondente too6.3.9600 hello è basata sul dispositivo StorSimple Hello.|
| CisAgentVersion         | versione di Hello per l'agente di elementi di configurazione in esecuzione sul dispositivo StorSimple. Questo agente consente di comunicare con il servizio StorSimple Manager hello in esecuzione in Azure.|
| MdsAgentVersion         | Hello versione corrispondente toohello Mds agente in esecuzione nel dispositivo StorSimple. Questo agente sposta dati toohello monitoraggio e diagnostica del servizio (MDS).|
| Lsisas2Version          | Hello driver versione corrispondente toohello LSI nel dispositivo StorSimple.|
| Capacity                | capacità totale di Hello del dispositivo hello in byte.|
| RemoteManagementMode    | Indica se il dispositivo hello può essere gestito in modalità remota tramite l'interfaccia di Windows PowerShell. |
| FipsMode                | Indica se il dispositivo viene abilitata la modalità di hello United States elaborazione Standard FIPS (Federal Information). standard di Hello FIPS 140 definisce gli algoritmi di crittografia approvati per l'utilizzo dai sistemi di computer governo federale US per la protezione dei dati sensibili hello. Per i dispositivi che eseguono l'aggiornamento 4 o versione successiva, la modalità FIPS è abilitata per impostazione predefinita. |

## <a name="next-steps"></a>Passaggi successivi

* Informazioni su hello [sintassi del cmdlet Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).

* Per ulteriori informazioni su troppo[risolvere i problemi di distribuzione](storsimple-troubleshoot-deployment.md) nel dispositivo StorSimple.
