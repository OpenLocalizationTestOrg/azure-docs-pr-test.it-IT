---
title: aaaInstall aggiornamento 4 nel dispositivo StorSimple | Documenti Microsoft
description: Viene illustrato come tooinstall StorSimple 8000 Series aggiornamento 4 sul dispositivo serie StorSimple 8000.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/30/2017
ms.author: alkohli
ms.openlocfilehash: 62c0ae94afdbb1027d3075962afa04d49fd1f60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>Installare l'aggiornamento 4 nel dispositivo StorSimple

## <a name="overview"></a>Panoramica

In questa esercitazione viene illustrato come tooinstall aggiornamento 4 in un dispositivo StorSimple in esecuzione una versione precedente di software tramite hello portale di Azure classico e utilizzando il metodo di aggiornamento rapido hello. metodo di aggiornamento rapido Hello viene utilizzato quando un gateway è configurato su un'interfaccia di rete diverse da DATA 0 del dispositivo StorSimple hello e si sta tentando di tooupdate da una versione del software pre-aggiornamento 1.

L'aggiornamento 4 include software per dispositivi, firmware USM, firmware e driver LSI, Storport e Spaceport, aggiornamenti di sicurezza del sistema operativo e una serie di altri aggiornamenti del sistema operativo.  il software di dispositivo Hello, al firmware USM, Spaceport, Storport e altri aggiornamenti del sistema operativo sono gli aggiornamenti non comportano interruzioni del servizio. gli aggiornamenti non comportano interruzioni del servizio o regolare Hello possono essere applicati tramite hello portale di Azure classico o metodo hotfix hello. aggiornamenti del firmware di Hello disco sono gli aggiornamenti che possono causare interruzioni e possono essere applicati solo tramite il metodo di hotfix hello utilizzando l'interfaccia di Windows PowerShell hello del dispositivo hello. 

> [!IMPORTANT]
> * Un set di controlli preliminari su automatici e manuali, vengono effettuati toohello precedente installazione toodetermine hello integrità del dispositivo in termini di connettività di rete e di stato dell'hardware. Questi controlli preliminari vengono eseguiti solo se si applicano gli aggiornamenti di hello dal portale di Azure classico hello.
> * Si consiglia di installare software hello e altri aggiornamenti periodici tramite hello portale di Azure classico. Interfaccia di Windows PowerShell toohello del dispositivo hello (tooinstall aggiornamenti) devono essere inviate solo se si verifica un errore di controllo pre-aggiornamento gateway hello nel portale di hello. A seconda che si sta aggiornando dalla versione di hello, hello aggiornamenti possono richiedere 4 ore (o versione successiva) tooinstall. anche gli aggiornamenti in modalità manutenzione Hello devono essere installati tramite l'interfaccia di Windows PowerShell hello del dispositivo hello. Dal momento che si tratta di aggiornamenti problematici, comporteranno un periodo di inattività per il dispositivo.
> * Se in esecuzione hello facoltativo StorSimple Snapshot Manager, assicurarsi di aver aggiornato il dispositivo di gestione Snapshot versione tooUpdate 4 precedenti tooupdating hello.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-classic-portal"></a>Installare l'aggiornamento 4 tramite hello portale di Azure classico
Eseguire hello seguendo i passaggi tooupdate dispositivo troppo[aggiornamento 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Se si desidera applicare l'aggiornamento 2 o versione successiva (comprese Update 2.1), Microsoft sarà in grado di toopull informazioni diagnostiche aggiuntive dal dispositivo hello. Di conseguenza, quando il team operativo identifica i dispositivi che si sono verificati problemi, siamo migliori informazioni toocollect forniti dal dispositivo hello e diagnosticare i problemi. Accettando Update 2 o versione successiva, ci Consenti tooprovide questo supporto attiva. 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Verificare che nel dispositivo sia in esecuzione l'**aggiornamento 4 della serie 8000 di StorSimple (6.3.9600.17820)**. Hello **data dell'ultimo aggiornamento** deve inoltre essere modificato. 

* Si noterà ora che sono disponibili aggiornamenti in modalità manutenzione hello (questo messaggio potrebbe continuare toobe visualizzato per backup too24 ore dopo l'installazione di hello aggiornamenti). Gli aggiornamenti in modalità manutenzione sono aggiornamenti comportano interruzioni e causare tempi di inattività di dispositivo e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo.
 
* Scaricare gli aggiornamenti in modalità manutenzione hello attenendosi alla procedura hello elencata in [toodownload hotfix](#to-download-hotfixes) toosearch per e scaricare KB4011837, che consente di installare gli aggiornamenti del firmware del disco (hello altri aggiornamenti devono essere già installati a questo punto). Seguire i passaggi di hello elencati [installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello aggiornamenti in modalità manutenzione. 

## <a name="install-update-4-as-a-hotfix"></a>Installare l'aggiornamento 4 come un hotfix
Hello consigliabile tooinstall metodo che Update 4 sia dal portale di Azure classico hello.

Utilizzare questa procedura se si esegue il controllo gateway hello durante gli aggiornamenti di hello tooinstall tramite hello portale di Azure classico. controllo di Hello non riesce quando si dispone di un gateway assegnato tooa dati non interfaccia di rete 0 e il dispositivo è in esecuzione un software versione preliminare tooUpdate 1.

versioni di software Hello che possono essere aggiornate tramite il metodo di aggiornamento rapido hello sono:

* Aggiornamento 0.1, 0.2, 0.3
* Aggiornamento 1, 1.1, 1.2
* Aggiornamento 2, 2.1, 2.2
* Aggiornamento 3, 3.1 


metodo di aggiornamento rapido Hello prevede hello tre passaggi:

1. Scaricare gli aggiornamenti rapidi hello da Microsoft Update Catalog hello.
2. Installare e verificare gli aggiornamenti rapidi di hello modalità normale.
3. Installare e verificare hello hotfix di modalità manutenzione.

#### <a name="download-updates-for-your-device"></a>Scaricare gli aggiornamenti per il dispositivo

È necessario scaricare e installare hello seguenti hotfix in hello prescritte ordine e hello suggerite cartelle:

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |Installare nella cartella|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 <br> (2 file) |Aggiornamento software del dispositivo <br> Aggiornamento dell'agente CiS/MDS |Regolare  <br></br>Senza interruzioni |~ 25 min |FirstOrderUpdate <br> _Installare l'aggiornamento software del dispositivo prima di eseguire l'aggiornamento dell'agente Cis/MDS_|
| 2A. |KB4011841 <br> KB4011842 |Aggiornamenti di driver e firmware LSI <br> Aggiornamento del firmware USM (versione 3.38) |Regolare  <br></br>Senza interruzioni |~ 3 ore <br> (include 2A. + 2B. + 2 C.)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3192392  <br> KB3153704, KB3174644 <br> KB3139914  |Pacchetto di aggiornamenti della sicurezza del sistema operativo |Regolare  <br></br>Senza interruzioni |- |SecondOrderUpdate|
| 2C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |Pacchetto di aggiornamenti del sistema operativo |Regolare  <br></br>Senza interruzioni |- |SecondOrderUpdate|

È necessario anche gli aggiornamenti del firmware di disco tooinstall sopra tutti gli aggiornamenti di hello nella hello tabelle precedenti. È possibile verificare se è necessario hello aggiornamenti del firmware del disco eseguendo hello `Get-HcsFirmwareVersion` cmdlet. Se si eseguono queste versioni del firmware: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, quindi non è necessario tooinstall questi aggiornamenti.

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione | Installare nella cartella|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4011837 |Firmware del disco |Manutenzione  <br></br>Con interruzioni |~ 30 min. | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Questo toobe esigenze procedura eseguita solo una volta tooapply aggiornamento 4. È possibile utilizzare gli aggiornamenti successivi di hello Azure tooapply portale classico.
> * Se l'aggiornamento da Update 3 o 3.1, tempo di installazione totale hello è too4 Chiudi ore.
> * Prima di utilizzare questo hello tooapply procedure aggiornamento, assicurarsi che entrambi i controller dei dispositivi hello siano online e tutti i componenti hardware hello siano integri.

Eseguire hello seguente toodownload passaggi e installare gli aggiornamenti rapidi hello.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [versione Update 4](storsimple-update4-release-notes.md).

