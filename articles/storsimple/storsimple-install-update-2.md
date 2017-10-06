---
title: aaaInstall Update 2 nel dispositivo StorSimple | Documenti Microsoft
description: Viene illustrato come tooinstall aggiornamento 2 di StorSimple 8000 Series sul dispositivo serie StorSimple 8000.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Installare l'aggiornamento 2 nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come tooinstall aggiornare 2 in un dispositivo StorSimple in esecuzione una versione precedente di software tramite hello portale di Azure classico. esercitazione Hello descrive inoltre i passaggi di hello necessari per l'aggiornamento di hello quando un gateway è configurato su un'interfaccia di rete diverse da DATA 0 del dispositivo StorSimple hello e si sta tentando di tooupdate da una versione del software pre-aggiornamento 1.

L'aggiornamento 2 include aggiornamenti del software del dispositivo, aggiornamenti del driver LSI e aggiornamenti del firmware del disco. Hello dispositivo aggiornamenti software e LSI sono gli aggiornamenti non comportano interruzioni del servizio e possono essere applicati tramite hello portale di Azure classico. aggiornamenti del firmware di Hello disco sono gli aggiornamenti che possono causare interruzioni e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo hello.

> [!IMPORTANT]
> * Aggiornamento 2 potrebbe non essere visibile immediatamente perché è un'implementazione graduale dei hello aggiornamenti. Provare a cercare nuovamente l'aggiornamento dopo qualche giorno perché verrà presto reso disponibile.
> * Un set di controlli preliminari su automatici e manuali, vengono effettuati toohello precedente installazione toodetermine hello integrità del dispositivo in termini di connettività di rete e di stato dell'hardware. Questi controlli preliminari vengono eseguiti solo se si applicano gli aggiornamenti di hello dal portale di Azure classico hello.
> * Si consiglia di installare software hello e aggiornamenti di driver tramite hello portale di Azure classico. Interfaccia di Windows PowerShell toohello del dispositivo hello (tooinstall aggiornamenti) devono essere inviate solo se si verifica un errore di controllo pre-aggiornamento gateway hello nel portale di hello. gli aggiornamenti di Hello potrebbero richiedere ore 4-7 tooinstall (inclusi gli aggiornamenti di Windows hello). gli aggiornamenti in modalità manutenzione Hello devono essere installati tramite l'interfaccia di Windows PowerShell hello del dispositivo hello. Dal momento che si tratta di aggiornamenti problematici, comporteranno un periodo di inattività per il dispositivo.
> * Se in esecuzione hello facoltativo StorSimple Snapshot Manager, assicurarsi di aver aggiornato il dispositivo di gestione Snapshot versione tooUpdate 2 precedente tooupdating hello.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Installare l'aggiornamento 2 tramite hello portale di Azure classico
Eseguire hello seguendo i passaggi tooupdate dispositivo troppo[Update 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Aggiornamento 2 consente a Microsoft toopull informazioni diagnostiche aggiuntive dal dispositivo hello. Di conseguenza, quando il team operativo identifica i dispositivi che si sono verificati problemi, siamo migliori informazioni toocollect forniti dal dispositivo hello e diagnosticare i problemi. Accettando Update 2, ci Consenti tooprovide questo supporto attiva.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Verificare che nel dispositivo sia in esecuzione l'**aggiornamento 2 della serie 8000 di StorSimple (6.3.9600.17673)**. Hello **data dell'ultimo aggiornamento** deve inoltre essere modificato. Si noterà anche che sono disponibili aggiornamenti in modalità manutenzione (questo messaggio potrebbe continuare toobe visualizzato per backup too24 ore dopo l'installazione di hello aggiornamenti).
   
   Gli aggiornamenti in modalità manutenzione sono aggiornamenti comportano interruzioni e causare tempi di inattività di dispositivo e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo. In alcuni casi, nel qual caso non è necessario tooinstall Aggiorna qualsiasi modalità di manutenzione quando si esegue l'aggiornamento 1.2, il firmware del disco potrebbe già essere aggiornato.
2. Scaricare gli aggiornamenti in modalità manutenzione hello attenendosi alla procedura hello elencata in [toodownload hotfix](#to-download-hotfixes) toosearch per e scaricare KB3121899, che consente di installare gli aggiornamenti del firmware del disco (hello altri aggiornamenti devono essere già installati a questo punto).
3. Seguire i passaggi di hello elencati [installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello aggiornamenti in modalità manutenzione.

## <a name="install-update-2-as-a-hotfix"></a>Installare l'aggiornamento 2 come un hotfix
Utilizzare questa procedura se si esegue il controllo gateway hello durante gli aggiornamenti di hello tooinstall tramite hello portale di Azure classico. controllo di Hello non riesce quando si dispone di un gateway assegnato tooa dati non interfaccia di rete 0 e il dispositivo è in esecuzione un software versione preliminare tooUpdate 1.

versioni del software che possono essere aggiornate utilizzando il metodo di aggiornamento rapido hello Hello sono aggiornamento 0,1 0,2, aggiornamento e aggiornamento 0.3, aggiornamento 1, aggiornamento 1.1 e 1.2 di aggiornamento. metodo di aggiornamento rapido Hello prevede hello tre passaggi:

* Scaricare gli aggiornamenti rapidi hello da Microsoft Update Catalog hello.
* Installare e verificare gli aggiornamenti rapidi di hello modalità normale.
* Installare e verificare hello hotfix di modalità manutenzione.

tooinstall Update 2 come hotfix, è necessario scaricare e installare i seguenti hotfix hello:

| Ordine | KB | Descrizione | Tipo di aggiornamento |
| --- | --- | --- | --- |
| 1 |KB3121901 |Aggiornamento software |Normale |
| 2 |KB3121900 |Driver LSI |Normale |
| 3 |KB3080728 |Correzione Storport  </br> Windows Server 2012 R2 |Normale |
| 4 |KB3090322 |Correzione Spaceport  </br> Windows Server 2012 R2 |Normale |
| 5 |KB3121899 |Firmware del disco |Manutenzione  |

> [!IMPORTANT]
> * Se il dispositivo sta eseguendo una versione di rilascio (GA), contattare [supporto Microsoft](storsimple-contact-microsoft-support.md) tooassist con hello aggiornare.
> * Questo toobe esigenze procedura eseguita solo una volta tooapply Update 2. È possibile utilizzare gli aggiornamenti successivi di hello Azure tooapply portale classico.
> * Ogni installazione di hotfix può richiedere circa 20 minuti toocomplete. Ora di installazione totale è too2 Chiudi ore.
> * Prima di utilizzare questo hello tooapply procedure aggiornamento, assicurarsi che entrambi i controller dei dispositivi siano online e tutti i componenti hardware hello siano integri.
> 
> 

Eseguire l'aggiornamento di hello tooapply i passaggi seguenti come hotfix.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [versione 2 aggiornamento](storsimple-update2-release-notes.md).

