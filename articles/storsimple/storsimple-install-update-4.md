---
title: Installare l'aggiornamento 4 nel dispositivo StorSimple | Microsoft Docs
description: Illustra come installare l'aggiornamento 4 di StorSimple serie 8000 in un dispositivo StorSimple serie 8000.
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
ms.openlocfilehash: 7dc2f29db64218b9db17eaf555c43a7ad282ea07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>Installare l'aggiornamento 4 nel dispositivo StorSimple

## <a name="overview"></a>Panoramica

Questa esercitazione illustra come installare l'aggiornamento 4 in un dispositivo StorSimple dove è in esecuzione una versione precedente del software tramite il portale di Azure classico e usando il metodo hotfix. Il metodo hotfix è usato quando viene configurato un gateway su un'interfaccia di rete diversa da DATA 0 del dispositivo StorSimple e si sta tentando di aggiornare da una versione del software precedente all'aggiornamento 1.

L'aggiornamento 4 include software per dispositivi, firmware USM, firmware e driver LSI, Storport e Spaceport, aggiornamenti di sicurezza del sistema operativo e una serie di altri aggiornamenti del sistema operativo.  Il software per dispositivi, il firmware USM, Spaceport, Storport e altri aggiornamenti del sistema operativo non implicano interruzioni del servizio. È possibile applicare gli aggiornamenti normali o che implicano un'interruzione del servizio usando il portale di Azure classico o il metodo basato su hotfix. Gli aggiornamenti del firmware del disco sono aggiornamenti con interruzioni del servizio e possono essere applicati solo tramite il metodo hotfix usando l'interfaccia di Windows PowerShell del dispositivo. 

> [!IMPORTANT]
> * Si esegue una serie di controlli preliminari automatici e manuali prima dell'installazione per determinare l'integrità del dispositivo in termini di connettività di stato e di rete hardware. Questi controlli preliminari vengono eseguiti solo se si applicano gli aggiornamenti dal portale di Azure classico.
> * Si consiglia di installare gli aggiornamenti software e gli altri aggiornamenti normali tramite il portale di Azure classico. Passare all'interfaccia di Windows PowerShell del dispositivo (per installare gli aggiornamenti) solo se il gateway di pre-aggiornamento ha esito negativo nel portale. A seconda della versione da cui viene eseguito l'aggiornamento, l'installazione degli aggiornamenti può richiedere un minimo di 4 ore. Gli aggiornamenti in modalità di manutenzione devono essere installati anche usando l'interfaccia di Windows PowerShell del dispositivo. Dal momento che si tratta di aggiornamenti problematici, comporteranno un periodo di inattività per il dispositivo.
> * Se StorSimple Snapshot Manager facoltativo è in esecuzione, assicurarsi di avere aggiornato la versione di Snapshot Manager con l'aggiornamento 4 prima di aggiornare il dispositivo.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-the-azure-classic-portal"></a>Installare l'aggiornamento 4 tramite il portale di Azure classico
Seguire questa procedura per applicare il dispositivo l'[aggiornamento 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Se si sta applicando l'aggiornamento 2 o una versione successiva (compreso l'aggiornamento 2.1), Microsoft è in grado di estrarre le informazioni di diagnostica aggiuntive dal dispositivo. Di conseguenza, quando il team addetto alle operazioni identifica i dispositivi che presentano problemi, sono disponibili più modi di raccogliere informazioni dal dispositivo e diagnosticare i problemi. Accettando l'aggiornamento 2, si acconsente a partecipare al supporto proattivo. 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Verificare che nel dispositivo sia in esecuzione l'**aggiornamento 4 della serie 8000 di StorSimple (6.3.9600.17820)**. Inoltre, è necessario modificare la **data dell'ultimo aggiornamento** . 

* Saranno ora disponibili gli aggiornamenti in modalità manutenzione. Questo messaggio potrebbe essere visualizzato fino a 24 ore dopo l'installazione degli aggiornamenti. Gli aggiornamenti in modalità manutenzione sono aggiornamenti problematici che comportano tempi di inattività del dispositivo e possono essere applicati solo tramite l'interfaccia di Windows PowerShell del dispositivo.
 
* Scaricare gli aggiornamenti in modalità di manutenzione usando la procedura indicata in [Scaricare gli hotfix](#to-download-hotfixes) per cercare e scaricare KB4011837, che installa gli aggiornamenti del firmware del disco; gli altri aggiornamenti devono essere già installati a questo punto. Seguire i passaggi elencati nella sezione [Installare e verificare gli aggiornamenti rapidi in modalità di manutenzione](#to-install-and-verify-maintenance-mode-hotfixes) per installare gli aggiornamenti in modalità manutenzione. 

## <a name="install-update-4-as-a-hotfix"></a>Installare l'aggiornamento 4 come un hotfix
È consigliabile installare l'aggiornamento 4 usando il portale di Azure classico.

Usare questa procedura se la verifica del gateway non riesce quando si cerca di installare gli aggiornamenti tramite il portale di Azure classico. La verifica non riesce quando un gateway è assegnato a un'interfaccia di rete non DATA 0e sul dispositivo è in esecuzione una versione del software precedente all'aggiornamento 1.

Le versioni software che possono essere aggiornate usando il metodo hotfix sono:

* Aggiornamento 0.1, 0.2, 0.3
* Aggiornamento 1, 1.1, 1.2
* Aggiornamento 2, 2.1, 2.2
* Aggiornamento 3, 3.1 


Il metodo hotfix prevede i tre passaggi seguenti:

1. Scaricare gli hotfix da Microsoft Update Catalog.
2. Installare e verificare gli hotfix in modalità normale.
3. Installare e verificare l'hotfix in modalità di manutenzione.

#### <a name="download-updates-for-your-device"></a>Scaricare gli aggiornamenti per il dispositivo

È necessario scaricare e installare gli hotfix seguenti nell'ordine indicato e nelle cartelle seguenti:

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |Installare nella cartella|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 <br> (2 file) |Aggiornamento software del dispositivo <br> Aggiornamento dell'agente CiS/MDS |Regolare  <br></br>Senza interruzioni |~ 25 min |FirstOrderUpdate <br> _Installare l'aggiornamento software del dispositivo prima di eseguire l'aggiornamento dell'agente Cis/MDS_|
| 2A. |KB4011841 <br> KB4011842 |Aggiornamenti di driver e firmware LSI <br> Aggiornamento del firmware USM (versione 3.38) |Regolare  <br></br>Senza interruzioni |~ 3 ore <br> (include 2A. + 2B. + 2 C.)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3192392  <br> KB3153704, KB3174644 <br> KB3139914  |Pacchetto di aggiornamenti della sicurezza del sistema operativo |Regolare  <br></br>Senza interruzioni |- |SecondOrderUpdate|
| 2C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |Pacchetto di aggiornamenti del sistema operativo |Regolare  <br></br>Senza interruzioni |- |SecondOrderUpdate|

Potrebbe essere necessario anche installare gli aggiornamenti del firmware del disco sopra tutti gli aggiornamenti indicati nelle tabelle precedenti. È possibile verificare se sono necessari gli aggiornamenti del firmware del disco eseguendo il cmdlet `Get-HcsFirmwareVersion` . Se si stanno eseguendo le versioni del firmware `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106` non è quindi necessario installare questi aggiornamenti.

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione | Installare nella cartella|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4011837 |Firmware del disco |Manutenzione  <br></br>Con interruzioni |~ 30 min. | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Questa procedura deve essere eseguita solo una volta per applicare l'aggiornamento 4. È possibile utilizzare il portale di Azure classico per applicare gli aggiornamenti successivi.
> * Se si parte dall'aggiornamento 3 o 3.1, il tempo totale richiesto per l'installazione è di circa 4 ore.
> * Prima di usare questa procedura per applicare l'aggiornamento, assicurarsi che entrambi i controller del dispositivo siano online e che tutti i componenti hardware siano integri.

Eseguire i passaggi seguenti per scaricare e importare gli hotfix.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sulla [versione dell'aggiornamento 4](storsimple-update4-release-notes.md).

