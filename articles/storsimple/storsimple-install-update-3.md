---
title: aaaInstall Update 3 nel dispositivo StorSimple | Documenti Microsoft
description: Viene illustrato come tooinstall StorSimple 8000 Series Update 3 sul dispositivo serie StorSimple 8000.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a156b8919639f1c7afb0fdef3d882d40d48f1c48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a>Installare l'aggiornamento 3 nel dispositivo StorSimple serie 8000

## <a name="overview"></a>Panoramica

In questa esercitazione viene illustrato come tooinstall Update 3 in un dispositivo StorSimple in esecuzione una versione precedente di software tramite hello portale di Azure classico e utilizzando il metodo di aggiornamento rapido hello. metodo di aggiornamento rapido Hello viene utilizzato quando un gateway è configurato su un'interfaccia di rete diverse da DATA 0 del dispositivo StorSimple hello e si sta tentando di tooupdate da una versione del software pre-aggiornamento 1.

L'aggiornamento 3 include gli aggiornamenti del software della periferica, di driver e firmware LSI, di Storport e Spaceport. Se l'aggiornamento da Update 2 o versione precedente, verrà anche essere necessario tooapply iSCSI, WMI e in alcuni casi, gli aggiornamenti del firmware del disco. Hello software del dispositivo, WMI, iSCSI, i driver LSI, Spaceport e Storport correzioni sono aggiornamenti non comportano interruzioni del servizio e possono essere applicate tramite hello portale di Azure classico. aggiornamenti del firmware di Hello disco sono gli aggiornamenti che possono causare interruzioni e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo hello. 

> [!IMPORTANT]
> * Un set di controlli preliminari su automatici e manuali, vengono effettuati toohello precedente installazione toodetermine hello integrità del dispositivo in termini di connettività di rete e di stato dell'hardware. Questi controlli preliminari vengono eseguiti solo se si applicano gli aggiornamenti di hello dal portale di Azure classico hello.
> * Si consiglia di installare software hello e aggiornamenti di driver tramite hello portale di Azure classico. Interfaccia di Windows PowerShell toohello del dispositivo hello (tooinstall aggiornamenti) devono essere inviate solo se si verifica un errore di controllo pre-aggiornamento gateway hello nel portale di hello. A seconda che si sta aggiornando dalla versione di hello, hello aggiornamenti possono richiedere tooinstall 1.5-2,5 ore. gli aggiornamenti in modalità manutenzione Hello devono essere installati tramite l'interfaccia di Windows PowerShell hello del dispositivo hello. Dal momento che si tratta di aggiornamenti problematici, comporteranno un periodo di inattività per il dispositivo.
> * Se in esecuzione hello facoltativo StorSimple Snapshot Manager, assicurarsi di aver aggiornato il dispositivo di gestione Snapshot versione tooUpdate 2 precedente tooupdating hello.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-hello-azure-classic-portal"></a>Installare l'aggiornamento 3 tramite hello portale di Azure classico
Eseguire hello seguendo i passaggi tooupdate dispositivo troppo[Update 3](storsimple-update3-release-notes.md).

> [!NOTE]
> Se si desidera applicare l'aggiornamento 2 o versione successiva (comprese Update 2.1), Microsoft sarà in grado di toopull informazioni diagnostiche aggiuntive dal dispositivo hello. Di conseguenza, quando il team operativo identifica i dispositivi che si sono verificati problemi, siamo migliori informazioni toocollect forniti dal dispositivo hello e diagnosticare i problemi. Accettando Update 2 o versione successiva, ci Consenti tooprovide questo supporto attiva.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Verificare che nel dispositivo sia in esecuzione l' **aggiornamento 3 della serie 8000 di StorSimple (6.3.9600.17759)**. Hello **data dell'ultimo aggiornamento** deve inoltre essere modificato. 
   - Se si sta aggiornando un tooUpdate precedente versione 2, si verifica anche che sono disponibili aggiornamenti in modalità manutenzione hello (questo messaggio potrebbe continuare toobe visualizzato per backup too24 ore dopo l'installazione di hello aggiornamenti).
     Gli aggiornamenti in modalità manutenzione sono aggiornamenti comportano interruzioni e causare tempi di inattività di dispositivo e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo. In alcuni casi, nel qual caso non è necessario tooinstall Aggiorna qualsiasi modalità di manutenzione quando si esegue l'aggiornamento 1.2, il firmware del disco potrebbe già essere aggiornato.
   - Se si parte dall'aggiornamento 2 o versione successiva, ora il dispositivo dovrebbe essere aggiornato. È possibile ignorare il passaggio di hello.

Scaricare gli aggiornamenti in modalità manutenzione hello attenendosi alla procedura hello elencata in [toodownload hotfix](#to-download-hotfixes) toosearch per e scaricare KB3121899, che consente di installare gli aggiornamenti del firmware del disco (hello altri aggiornamenti devono essere già installati a questo punto). Seguire i passaggi di hello elencati [installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello aggiornamenti in modalità manutenzione. 

## <a name="install-update-3-as-a-hotfix"></a>Installare l'aggiornamento 3 come un hotfix
Utilizzare questa procedura se si esegue il controllo gateway hello durante gli aggiornamenti di hello tooinstall tramite hello portale di Azure classico. controllo di Hello non riesce quando si dispone di un gateway assegnato tooa dati non interfaccia di rete 0 e il dispositivo è in esecuzione un software versione preliminare tooUpdate 1.

versioni di software Hello che possono essere aggiornate tramite il metodo di aggiornamento rapido hello sono:

* Aggiornamento 0.1, 0.2, 0.3
* Aggiornamento 1, 1.1, 1.2
* Aggiornamento 2, 2.1, 2.2 

> [!IMPORTANT]
> * Se il dispositivo sta eseguendo una versione di rilascio (GA), contattare [supporto Microsoft](storsimple-contact-microsoft-support.md) tooassist con hello aggiornare.
> 
> 

metodo di aggiornamento rapido Hello prevede hello tre passaggi:

1. Scaricare gli aggiornamenti rapidi hello da Microsoft Update Catalog hello.
2. Installare e verificare gli aggiornamenti rapidi di hello modalità normale.
3. Installare e verificare l'hotfix di modalità di manutenzione hello (solo durante l'aggiornamento da pre-aggiornamento software di 2).

#### <a name="download-updates-for-your-device"></a>Scaricare gli aggiornamenti per il dispositivo
**Se il dispositivo è in esecuzione Update 2.1 o 2.2**, è necessario scaricare e installare hello dopo gli aggiornamenti rapidi nel hello prescritte ordine:

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |
| --- | --- | --- | --- | --- |
| 1. |KB3186843 |Aggiornamento software &#42; |Regolare  <br></br>Senza interruzioni |~ 45 min. |
| 2. |KB3186859 |Driver e firmware LSI |Regolare  <br></br>Senza interruzioni |~ 20 min. |
| 3. |KB3121261 |Correzione Storport e Spaceport  </br> Windows Server 2012 R2 |Regolare  <br></br>Senza interruzioni |~ 20 min. |

&#42;  *Nota che gli aggiornamenti software hello è costituito da due file binari: l'aggiornamento software del dispositivo preceduti da `all-hcsmdssoftwareupdate` hello gli elementi di configurazione e dell'agente di Mds preceduti da `all-cismdsagentupdatebundle`. l'aggiornamento del software hello dispositivo deve essere installato prima hello gli elementi di configurazione e Mds agente. È necessario riavviare il controller attivo di hello mediante hello `Restart-HcsController` cmdlet dopo l'applicazione hello gli elementi di configurazione e aggiornamento dell'agente di Mds (e prima di applicare gli aggiornamenti rimanenti hello).* 

**Se il dispositivo sta eseguendo l'aggiornamento 0,1, 0,2, 0,3, 1.0, 1.1, 1.2 o 2.0**, è necessario scaricare e installare i seguenti hotfix nel software dei driver LSI toohello aggiunta hello e (Buongiorno illustrato nella tabella precedente), gli aggiornamenti del firmware in hello prescritte ordine:

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |
| --- | --- | --- | --- | --- |
| 4. |KB3146621 |Pacchetto iSCSI |Regolare  <br></br>Senza interruzioni |~ 20 min. |
| 5. |KB3103616 |Pacchetto WMI |Regolare  <br></br>Senza interruzioni |~ 12 min. |

<br></br>

**Se il dispositivo è in esecuzione versioni 0,2, 0,3, 1.0, 1.1 e 1.2**, è necessario anche gli aggiornamenti del firmware di disco tooinstall sopra tutti gli aggiornamenti di hello nella hello tabelle precedenti. È possibile verificare se è necessario hello aggiornamenti del firmware del disco eseguendo hello `Get-HcsFirmwareVersion` cmdlet. Se si eseguono queste versioni del firmware: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, quindi non è necessario tooinstall questi aggiornamenti.

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |
| --- | --- | --- | --- | --- |
| 6. |KB3121899 |Firmware del disco |Manutenzione  <br></br>Con interruzioni |~ 30 min. |

<br></br>

> [!IMPORTANT]
> * Questo toobe esigenze procedura eseguita solo una volta tooapply Update 3. È possibile utilizzare gli aggiornamenti successivi di hello Azure tooapply portale classico.
> * Se l'aggiornamento dall'aggiornamento 2.2, il tempo di installazione totale hello è too1.1 Chiudi ore.
> * Prima di utilizzare questo hello tooapply procedure aggiornamento, assicurarsi che entrambi i controller dei dispositivi hello siano online e tutti i componenti hardware hello siano integri.
> 
> 

Eseguire hello seguente toodownload passaggi e installare gli aggiornamenti rapidi hello.

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [Update 3 release](storsimple-update3-release-notes.md).

