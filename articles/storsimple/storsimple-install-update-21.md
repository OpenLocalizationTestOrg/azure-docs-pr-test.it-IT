---
title: aaaInstall aggiornamento 2.2 nel dispositivo StorSimple | Documenti Microsoft
description: Viene illustrato come tooinstall StorSimple 8000 Series aggiornamento 2.2 sul dispositivo serie StorSimple 8000.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 047c7a4b-73d0-45ea-8d51-c54d71871392
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2016
ms.author: alkohli
ms.openlocfilehash: cedb83ce42bc6bb81a4e43345da3f25b71036d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>Installare l'aggiornamento 2.2 nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come tooinstall aggiornamento 2.2 in un dispositivo StorSimple in esecuzione una versione precedente di software tramite hello portale di Azure classico e utilizzando il metodo di aggiornamento rapido hello. metodo di aggiornamento rapido Hello viene utilizzato quando un gateway è configurato su un'interfaccia di rete diverse da DATA 0 del dispositivo StorSimple hello e si sta tentando di tooupdate da una versione del software pre-aggiornamento 1.

L'aggiornamento 2.2 comprende gli aggiornamento del software del dispositivo, iSCSI e WMI. Se l'aggiornamento dalla versione 2.1, solo l'aggiornamento del software hello dispositivo sarà necessario toobe applicato. Se l'aggiornamento da una versione 2 di pre-aggiornamento, sarà anche necessario tooapply LSI driver, Spaceport, Storport e aggiornamenti del firmware del disco. Hello software del dispositivo, WMI, iSCSI, i driver LSI, Spaceport e Storport correzioni sono aggiornamenti non comportano interruzioni del servizio e possono essere applicate tramite hello portale di Azure classico. aggiornamenti del firmware di Hello disco sono gli aggiornamenti che possono causare interruzioni e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo hello. 

> [!IMPORTANT]
> * Un set di controlli preliminari su automatici e manuali, vengono effettuati toohello precedente installazione toodetermine hello integrità del dispositivo in termini di connettività di rete e di stato dell'hardware. Questi controlli preliminari vengono eseguiti solo se si applicano gli aggiornamenti di hello dal portale di Azure classico hello.
> * Si consiglia di installare software hello e aggiornamenti di driver tramite hello portale di Azure classico. Interfaccia di Windows PowerShell toohello del dispositivo hello (tooinstall aggiornamenti) devono essere inviate solo se si verifica un errore di controllo pre-aggiornamento gateway hello nel portale di hello. A seconda che si sta aggiornando dalla versione di hello, hello aggiornamenti possono richiedere tooinstall 1.5-2,5 ore. gli aggiornamenti in modalità manutenzione Hello devono essere installati tramite l'interfaccia di Windows PowerShell hello del dispositivo hello. Dal momento che si tratta di aggiornamenti problematici, comporteranno un periodo di inattività per il dispositivo.
> * Se in esecuzione hello facoltativo StorSimple Snapshot Manager, assicurarsi di aver aggiornato il dispositivo di hello Snapshot Manager versione 2.2 tooUpdate tooupdating precedente.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-hello-azure-classic-portal"></a>Installare l'aggiornamento 2.2 tramite hello portale di Azure classico
Eseguire hello seguendo i passaggi tooupdate dispositivo troppo[2.2 aggiornamento](storsimple-update21-release-notes.md).

> [!NOTE]
> Se si desidera applicare l'aggiornamento 2 o versione successiva (comprese Update 2.1), Microsoft sarà in grado di toopull informazioni diagnostiche aggiuntive dal dispositivo hello. Di conseguenza, quando il team operativo identifica i dispositivi che si sono verificati problemi, siamo migliori informazioni toocollect forniti dal dispositivo hello e diagnosticare i problemi. Accettando Update 2 o versione successiva, ci Consenti tooprovide questo supporto attiva.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Verificare che nel dispositivo sia in esecuzione l' **aggiornamento 2.2 della serie 8000 di StorSimple (6.3.9600.17708)**. Hello **data dell'ultimo aggiornamento** deve inoltre essere modificato. 
   
   Se si sta aggiornando un tooUpdate precedente versione 2, si verifica anche che sono disponibili aggiornamenti in modalità manutenzione hello (questo messaggio potrebbe continuare toobe visualizzato per backup too24 ore dopo l'installazione di hello aggiornamenti).
   
   Gli aggiornamenti in modalità manutenzione sono aggiornamenti comportano interruzioni e causare tempi di inattività di dispositivo e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo. In alcuni casi, nel qual caso non è necessario tooinstall Aggiorna qualsiasi modalità di manutenzione quando si esegue l'aggiornamento 1.2, il firmware del disco potrebbe già essere aggiornato.
   
   Se si sta aggiornando dall'aggiornamento 2, ora il dispositivo dovrebbe essere aggiornato. È possibile ignorare i passaggi rimanenti hello.
2. Scaricare gli aggiornamenti in modalità manutenzione hello attenendosi alla procedura hello elencata in [toodownload hotfix](#to-download-hotfixes) toosearch per e scaricare KB3121899, che consente di installare gli aggiornamenti del firmware del disco (hello altri aggiornamenti devono essere già installati a questo punto).
3. Seguire i passaggi di hello elencati [installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello aggiornamenti in modalità manutenzione. 

## <a name="install-update-22-as-a-hotfix"></a>Installare l'aggiornamento 2.2 come un hotfix
Utilizzare questa procedura se si esegue il controllo gateway hello durante gli aggiornamenti di hello tooinstall tramite hello portale di Azure classico. controllo di Hello non riesce quando si dispone di un gateway assegnato tooa dati non interfaccia di rete 0 e il dispositivo è in esecuzione un software versione preliminare tooUpdate 1.

versioni di software Hello che possono essere aggiornate tramite il metodo di aggiornamento rapido hello sono:

* Aggiornamento 0.1, 0.2, 0.3
* Aggiornamento 1, 1.1, 1.2
* Aggiornamento 2, 2.1 

> [!IMPORTANT]
> * Se il dispositivo sta eseguendo una versione di rilascio (GA), contattare [supporto Microsoft](storsimple-contact-microsoft-support.md) tooassist con hello aggiornare.
> 
> 

metodo di aggiornamento rapido Hello prevede hello tre passaggi:

* Scaricare gli aggiornamenti rapidi hello da Microsoft Update Catalog hello.
* Installare e verificare gli aggiornamenti rapidi di hello modalità normale.
* Installare e verificare l'hotfix di modalità di manutenzione hello (solo durante l'aggiornamento da pre-aggiornamento software di 2).

#### <a name="download-updates-for-a-device-running-update-21-software"></a>Scaricare gli aggiornamenti per un dispositivo che esegue il software di aggiornamento 2.1
**Se il dispositivo sta eseguendo l'aggiornamento 2.1**, è necessario scaricare l'aggiornamento software per dispositivi hello solo KB3179904. Installare solo i file binari di hello preceduti da 'all-hcsmdssoftwareudpate'. Non è installato hello gli elementi di configurazione e aggiornamento dell'agente MDS hello preceduti da `all-cismdsagentupdatebundle`. Errore toodo operazione genererà un errore. Si tratta di un aggiornamento non comportano interruzioni del servizio, non verrà compromesse IO e dispositivo hello non avrà alcun tempo di inattività.

#### <a name="download-updates-for-a-device-running-update-2-software"></a>Scaricare gli aggiornamenti per un dispositivo che esegue il software di aggiornamento 2
**Se il dispositivo esegue l'aggiornamento 2**, è necessario scaricare e installare hello dopo gli aggiornamenti rapidi nel hello prescritte ordine:

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |Aggiornamento software &#42; |Regolare  <br></br>Senza interruzioni |~ 45 min. |
| 2. |KB3146621 |Pacchetto iSCSI |Regolare  <br></br>Senza interruzioni |~ 20 min. |
| 3. |KB3103616 |Pacchetto WMI |Regolare  <br></br>Senza interruzioni |~ 12 min. |

 &#42;  *Si noti, l'aggiornamento software è costituito da due file binari: l'aggiornamento software del dispositivo preceduti da `all-hcsmdssoftwareupdate` hello gli elementi di configurazione e dell'agente di Mds preceduti da `all-cismdsagentupdatebundle`. l'aggiornamento del software hello dispositivo deve essere installato prima dell'agente di Mds e ci hello. È necessario riavviare il controller attivo di hello mediante hello `Restart-HcsController` cmdlet dopo l'applicazione hello gli elementi di configurazione e aggiornamento dell'agente MDS (e prima di applicare gli aggiornamenti rimanenti hello).* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>Scaricare gli aggiornamenti per un dispositivo che esegue il software di pre-aggiornamento 2
**Se il dispositivo è in esecuzione versioni 0,2, 0,3, 1.0 e 1.1**, è necessario scaricare e installare hello LSI driver e firmware inoltre aggiornare software toohello, iSCSI e gli aggiornamenti WMI. Questo aggiornamento è già installato se si esegue l'aggiornamento 1.2 o 2. 

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |Driver e firmware LSI |Regolare  <br></br>Senza interruzioni |~ 20 min. |

<br></br>
**Se il dispositivo è in esecuzione versioni 0,2, 0,3, 1.0, 1.1 e 1.2**, è necessario scaricare e installare hello Spaceport e correzione Storport hello. Sono già installati se si sta eseguendo l'aggiornamento o 2.

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Correzione Spaceport  </br> Windows Server 2012 R2 |Regolare  <br></br>Senza interruzioni |~ 20 min. |
| 6. |KB3080728 |Correzione Storport  </br> Windows Server 2012 R2 |Regolare  <br></br>Senza interruzioni |~ 20 min. |

<br></br>
È necessario anche gli aggiornamenti del firmware di tooinstall disco. È possibile verificare se è necessario hello aggiornamenti del firmware del disco eseguendo hello `Get-HcsFirmwareVersion` cmdlet. Se si eseguono queste versioni del firmware: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, quindi non è necessario tooinstall questi aggiornamenti.

| Ordine | KB | Descrizione | Tipo di aggiornamento | Tempo dell'installazione |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |Firmware del disco |Manutenzione  <br></br>Con interruzioni |~ 30 min. |

<br></br>

> [!IMPORTANT]
> * Questo toobe esigenze procedura eseguita solo una volta tooapply 2.2 di aggiornamento. È possibile utilizzare gli aggiornamenti successivi di hello Azure tooapply portale classico.
> * Se l'aggiornamento da Update 2, tempo di installazione totale hello è too1.5 Chiudi ore.
> * Prima di utilizzare questo hello tooapply procedure aggiornamento, assicurarsi che entrambi i controller dei dispositivi hello siano online e tutti i componenti hardware hello siano integri.
> 
> 

Eseguire hello seguente toodownload passaggi e installare gli aggiornamenti rapidi hello.

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [versione Update 2.1](storsimple-update21-release-notes.md).

