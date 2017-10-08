---
title: aaaInstall aggiornamento 5 nel dispositivo StorSimple serie 8000 | Documenti Microsoft
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
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: a832f9953e8e39408efeeed375e3afe8eee8d0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-5-on-your-storsimple-device"></a>Installare l'aggiornamento 5 nel dispositivo StorSimple

## <a name="overview"></a>Panoramica

In questa esercitazione viene illustrato come tooinstall aggiornamento 5 in un dispositivo StorSimple in esecuzione una versione precedente di software tramite hello portale di Azure e utilizzando il metodo di aggiornamento rapido hello. metodo di aggiornamento rapido Hello viene utilizzato quando un gateway è configurato su un'interfaccia di rete diverse da DATA 0 del dispositivo StorSimple hello e si sta tentando di tooupdate da una versione del software pre-aggiornamento 1.

L'aggiornamento 5 include software per dispositivi, Storport e Spaceport, aggiornamenti di sicurezza del sistema operativo e aggiornamenti del sistema operativo, oltre ad aggiornamenti del firmware del disco.  il software di dispositivo Hello, Spaceport, Storport, sicurezza e altri aggiornamenti del sistema operativo sono gli aggiornamenti non comportano interruzioni del servizio. gli aggiornamenti non comportano interruzioni del servizio o regolare Hello possono essere applicati tramite hello portale di Azure o il metodo di aggiornamento rapido hello. aggiornamenti del firmware di Hello disco sono gli aggiornamenti che possono causare interruzioni e vengono applicati quando hello dispositivo è in modalità di manutenzione tramite il metodo di hotfix hello utilizzando l'interfaccia di Windows PowerShell hello del dispositivo hello.

> [!IMPORTANT]
> * Un set di controlli preliminari su automatici e manuali, vengono effettuati toohello precedente installazione toodetermine hello integrità del dispositivo in termini di connettività di rete e di stato dell'hardware. Questi controlli preliminari vengono eseguiti solo se si applicano gli aggiornamenti di hello da hello portale di Azure.
> * Si consiglia di installare software hello e altri aggiornamenti periodici tramite hello portale di Azure. Interfaccia di Windows PowerShell toohello del dispositivo hello (tooinstall aggiornamenti) devono essere inviate solo se si verifica un errore di controllo pre-aggiornamento gateway hello nel portale di hello. A seconda che si sta aggiornando dalla versione di hello, hello aggiornamenti possono richiedere 4 ore (o versione successiva) tooinstall. gli aggiornamenti in modalità manutenzione Hello devono essere installati tramite l'interfaccia di Windows PowerShell hello del dispositivo hello. Trattandosi di aggiornamenti con interruzioni del servizio, comportano un periodo di inattività per il dispositivo.
> * Se in esecuzione hello facoltativo StorSimple Snapshot Manager, assicurarsi di aver aggiornato il dispositivo di hello Snapshot Manager versione 5 tooUpdate tooupdating precedente.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-5-via-hello-azure-portal"></a>Installare l'aggiornamento 5 tramite hello portale di Azure
Eseguire hello seguendo i passaggi tooupdate dispositivo troppo[aggiornamento 5](storsimple-update5-release-notes.md).

> [!NOTE]
> Microsoft reperisce le informazioni di diagnostica aggiuntive da dispositivo hello. Di conseguenza, quando il team operativo identifica i dispositivi che si sono verificati problemi, siamo migliori informazioni toocollect forniti dal dispositivo hello e diagnosticare i problemi.

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update5-via-portal.md)]

Verificare che nel dispositivo sia in esecuzione l'**aggiornamento 5 della serie 8000 di StorSimple (6.3.9600.17845)**. Hello **data dell'ultimo aggiornamento** deve essere modificato.

* Si noterà ora che sono disponibili aggiornamenti in modalità manutenzione hello (questo messaggio potrebbe continuare toobe visualizzato per backup too24 ore dopo l'installazione di hello aggiornamenti). Gli aggiornamenti in modalità manutenzione sono aggiornamenti comportano interruzioni e causare tempi di inattività di dispositivo e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo.

* Scaricare gli aggiornamenti in modalità manutenzione hello attenendosi alla procedura hello elencata in [toodownload hotfix](#to-download-hotfixes) toosearch per e scaricare KB4011837, che consente di installare gli aggiornamenti del firmware del disco (hello altri aggiornamenti devono essere già installati a questo punto). Seguire i passaggi di hello elencati [installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello aggiornamenti in modalità manutenzione.

## <a name="install-update-5-as-a-hotfix"></a>Installare l'aggiornamento 5 come hotfix


versioni di software Hello che possono essere aggiornate tramite il metodo di aggiornamento rapido hello sono:

* Aggiornamento 0.1, 0.2, 0.3
* Aggiornamento 1, 1.1, 1.2
* Aggiornamento 2, 2.1, 2.2
* Aggiornamento 3, 3.1
* Aggiornamento 4

> [!NOTE] 
> Hello consigliabile tooinstall metodo che Update 5 è tramite hello portale di Azure. Utilizzare questa procedura se si esegue il controllo gateway hello durante gli aggiornamenti di hello tooinstall tramite hello portale di Azure. controllo di Hello non riesce quando si dispone di un gateway assegnato tooa dati non interfaccia di rete 0 e il dispositivo è in esecuzione una versione software precedente a Update 1.

metodo di aggiornamento rapido Hello prevede hello tre passaggi:

1. Scaricare gli aggiornamenti rapidi hello da Microsoft Update Catalog hello.
2. Installare e verificare gli aggiornamenti rapidi di hello modalità normale.
3. Installare e verificare hello hotfix di modalità manutenzione.

#### <a name="download-updates-for-your-device"></a>Scaricare gli aggiornamenti per il dispositivo

È necessario scaricare e installare hello seguenti hotfix in hello prescritte ordine e hello suggerite cartelle:

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |Installare nella cartella|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4037264 |Aggiornamento software<br> Scaricare sia _HcsSfotwareUpdate.exe_ che _CisMSDAgent.exe_ |Regolare  <br></br>Senza interruzioni |~ 25 min |FirstOrderUpdate|

Se l'aggiornamento da un dispositivo che esegue l'aggiornamento 4, è necessario solo gli aggiornamenti cumulativi tooinstall hello del sistema operativo come secondo aggiornamenti degli ordini.

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |Installare nella cartella|
| --- | --- | --- | --- | --- | --- |
| 2A. |KB4025336 |Pacchetto di aggiornamenti cumulativi del sistema operativo <br> Scaricare Windows Server 2012 R2 |Regolare  <br></br>Senza interruzioni |- |SecondOrderUpdate|

Se l'installazione da un dispositivo che esegue l'aggiornamento 3 o versioni precedenti, installare hello seguente inoltre gli aggiornamenti cumulativi toohello.

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |Installare nella cartella|
| --- | --- | --- | --- | --- | --- |
| 2B. |KB4011841 <br> KB4011842 |Aggiornamenti di driver e firmware LSI <br> Aggiornamento del firmware USM (versione 3.38) |Regolare  <br></br>Senza interruzioni |~ 3 ore <br> (include 2A. + 2B. + 2 C.)|SecondOrderUpdate|
| 2C. |KB3139398 <br> KB3142030 <br> KB3108381 <br> KB3153704 <br> KB3174644 <br> KB3139914   |Pacchetto di aggiornamenti della sicurezza del sistema operativo <br> Scaricare Windows Server 2012 R2 |Regolare  <br></br>Senza interruzioni |- |SecondOrderUpdate|
| 2D. |KB3146621 <br> KB3103616 <br> KB3121261 <br> KB3123538 |Pacchetto di aggiornamenti del sistema operativo <br> Scaricare Windows Server 2012 R2 |Regolare  <br></br>Senza interruzioni |- |SecondOrderUpdate|


È necessario anche gli aggiornamenti del firmware di disco tooinstall sopra tutti gli aggiornamenti di hello nella hello tabelle precedenti. È possibile verificare se è necessario hello aggiornamenti del firmware del disco eseguendo hello `Get-HcsFirmwareVersion` cmdlet. Se si eseguono queste versioni del firmware: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N003`, `0107`, quindi non è necessario tooinstall questi aggiornamenti.

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione | Installare nella cartella|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4037263 |Firmware del disco |Manutenzione  <br></br>Con interruzioni |~ 30 min. | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Se l'aggiornamento dall'aggiornamento 4, tempo di installazione totale hello è too4 Chiudi ore.
> * Prima di utilizzare questo hello tooapply procedure aggiornamento, assicurarsi che entrambi i controller dei dispositivi hello siano online e tutti i componenti hardware hello siano integri.

Eseguire hello seguente toodownload passaggi e installare gli aggiornamenti rapidi hello.

[!INCLUDE [storsimple-install-update5-hotfix](../../includes/storsimple-install-update5-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [versione aggiornamento 5](storsimple-update5-release-notes.md).

