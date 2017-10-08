---
title: aaaInstall aggiornamento 1.2 nel dispositivo StorSimple | Documenti Microsoft
description: Viene illustrato come tooinstall StorSimple 8000 Series aggiornamento 1.2 sul dispositivo serie StorSimple 8000.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>Installare l'aggiornamento 1.2 nel dispositivo StorSimple serie 8000
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come tooinstall aggiornare 1.2 in un dispositivo StorSimple che è in esecuzione un software versione preliminare tooUpdate 1. esercitazione Hello riguarda anche hello sono necessari altri passaggi per l'aggiornamento di hello quando un gateway è configurato su un'interfaccia di rete diverse da DATA 0 del dispositivo StorSimple hello.

L'aggiornamento 1.2 include aggiornamenti del software del dispositivo, aggiornamenti del driver LSI e aggiornamenti del firmware del disco. Hello software e aggiornamenti di driver LSI sono gli aggiornamenti non comportano interruzioni del servizio e possono essere applicati tramite hello portale di Azure classico. aggiornamenti del firmware di Hello disco sono gli aggiornamenti che possono causare interruzioni e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo hello.

In base alla versione eseguita dal dispositivo, è possibile determinare se verrà applicato l'aggiornamento 1.2. È possibile controllare versione software hello del dispositivo passando toohello **riepilogo rapido** sezione del dispositivo **Dashboard**.

</br>

| Se è in esecuzione la versione del software... | Che cosa avviene nel portale di hello? |
| --- | --- |
| Versione - GA |Se è in esecuzione la versione finale (GA), non applicare questo aggiornamento. . [Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) tooupdate il dispositivo. |
| Aggiornamento 0.1 |Il portale applica l'aggiornamento 1.2. |
| Aggiornamento 0.2 |Il portale applica l'aggiornamento 1.2. |
| Aggiornamento 0.3 |Il portale applica l'aggiornamento 1.2. |
| Aggiornamento 1 |Questo aggiornamento non sarà disponibile. |
| Aggiornamento 1.1 |Questo aggiornamento non sarà disponibile. |

</br>

> [!IMPORTANT]
> * 1.2 aggiornamento potrebbe non essere visibile immediatamente perché è un'implementazione graduale dei hello aggiornamenti. Provare a cercare nuovamente l'aggiornamento dopo qualche giorno perché verrà presto reso disponibile.
> * Questo aggiornamento include un set di controlli preliminari su automatico e manuale toodetermine hello dell'integrità dei dispositivi in termini di connettività di rete e di stato dell'hardware. Questi controlli preliminari vengono eseguiti solo se si applicano gli aggiornamenti di hello dal portale di Azure classico hello.
> * Si consiglia di installare software hello e aggiornamenti di driver tramite hello portale di Azure classico. Interfaccia di Windows PowerShell toohello del dispositivo hello (tooinstall aggiornamenti) devono essere inviate solo se si verifica un errore di controllo pre-aggiornamento gateway hello nel portale di hello. gli aggiornamenti di Hello potrebbero richiedere da 5 a 10 ore tooinstall (inclusi gli aggiornamenti di Windows hello). gli aggiornamenti in modalità manutenzione Hello devono essere installati tramite l'interfaccia di Windows PowerShell hello del dispositivo hello. Dal momento che si tratta di aggiornamenti problematici, comporteranno un periodo di inattività per il dispositivo.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>Installare l'aggiornamento 1.2 tramite hello portale di Azure classico
Eseguire hello seguendo i passaggi tooupdate dispositivo troppo[aggiornamento 1.2](storsimple-update1-release-notes.md). Usare questa procedura solo se è presente un gateway configurato sull'interfaccia di rete DATA 0 sul dispositivo.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Verificare che nel dispositivo sia in esecuzione l' **aggiornamento 1.2 della serie 8000 di StorSimple (6.3.9600.17584)**. Hello **data dell'ultimo aggiornamento** deve inoltre essere modificato. Si noterà anche che sono disponibili aggiornamenti in modalità manutenzione (questo messaggio potrebbe continuare toobe visualizzato per backup too24 ore dopo l'installazione di hello aggiornamenti).
   
   Gli aggiornamenti in modalità manutenzione sono aggiornamenti comportano interruzioni e causare tempi di inattività di dispositivo e possono essere applicati solo tramite l'interfaccia di Windows PowerShell hello del dispositivo.
   
   ![Pagina di manutenzione](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Pagina Manutenzione")
2. Scaricare gli aggiornamenti in modalità manutenzione hello attenendosi alla procedura hello elencata in [toodownload hotfix](#to-download-hotfixes) toosearch per e scaricare KB3063416, che consente di installare gli aggiornamenti del firmware del disco (hello altri aggiornamenti devono essere già installati a questo punto).
3. Seguire i passaggi di hello elencati [installare e verificare l'hotfix in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello aggiornamenti in modalità manutenzione.
4. Nel portale di Azure classico hello, passare toohello **manutenzione** pagina e nella parte inferiore di hello della pagina hello, fare clic su **analisi aggiornamenti** toocheck per tutti gli aggiornamenti di Windows e quindi fare clic su **Installa aggiornamenti** . Si è finito dopo che tutti di hello gli aggiornamenti vengono installati correttamente.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>Installare l'aggiornamento 1.2 in un dispositivo con un gateway configurato per un'interfaccia di rete non DATA 0
Utilizzare questa procedura solo se si esegue il controllo gateway hello durante gli aggiornamenti di hello tooinstall tramite hello portale di Azure classico. controllo di Hello non riesce quando si dispone di un gateway assegnato tooa dati non interfaccia di rete 0 e il dispositivo è in esecuzione un software versione preliminare tooUpdate 1. Se il dispositivo non dispone di un gateway su un'interfaccia di rete, 0 non di dati, è possibile aggiornare il dispositivo direttamente dal portale di Azure classico hello. Vedere [installare l'aggiornamento 1.2 tramite hello portale di Azure classico](#install-update-1.2-via-the-azure-classic-portal).

versioni del software Hello che possono essere aggiornate con questo metodo sono Update 0,1, 0,2 aggiornamento e aggiornamento 0.3.

> [!IMPORTANT]
> * Se il dispositivo sta eseguendo una versione di rilascio (GA), contattare [supporto Microsoft](storsimple-contact-microsoft-support.md) tooassist con hello aggiornare.
> * Questo toobe esigenze procedura eseguita solo una volta tooapply 1.2 di aggiornamento. È possibile utilizzare gli aggiornamenti successivi di hello Azure tooapply portale classico.
> 
> 

Se il dispositivo è in esecuzione 1 software pre-aggiornamento e dispone di un gateway impostato per un'interfaccia di rete diverse da DATA 0, è possibile applicare l'aggiornamento 1.2 in hello modi seguenti:

* **Opzione 1**: scaricare l'aggiornamento di hello e applicarlo utilizzando hello `Start-HcsHotfix` cmdlet dall'interfaccia di Windows PowerShell hello del dispositivo hello. Si tratta di hello metodo consigliato. **Non utilizzare questo tooapply metodo 1.2 aggiornamento se il dispositivo sta eseguendo l'aggiornamento 1.0 o 1.1 di aggiornamento.**
* **Opzione 2**: hello di installazione e configurazione di gateway di hello Remove aggiornare direttamente dal portale di Azure classico hello.

Istruzioni dettagliate per ognuno di essi vengono fornite in hello le sezioni seguenti.

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>Opzione 1: Utilizzare Windows PowerShell per StorSimple tooapply aggiornamento 1.2 come hotfix
Utilizzare questa procedura solo se si esegue l'aggiornamento 0,1, 0,2, 0,3 e se il controllo del gateway non è riuscita durante il tentativo di aggiornamenti tooinstall dal portale di Azure classico hello. Se si esegue il software di versione (GA), [supporto Microsoft](storsimple-contact-microsoft-support.md) tooupdate il dispositivo.

tooinstall 1.2 Update come aggiornamento rapido, è necessario scaricare e installare i seguenti hotfix hello:

| Ordine | KB | Descrizione | Tipo di aggiornamento |
| --- | --- | --- | --- |
| 1 |KB3063418 |Aggiornamento software |Normale |
| 2 |KB3043005 |Aggiornamento del controller LSI SAS |Normale |
| 3 |KB3063416 |Firmware del disco |Manutenzione  |

Prima di utilizzare questo hello tooapply procedure aggiornamento, assicurarsi che:

* Entrambi i controller di dispositivo sono in linea.

Eseguire hello seguendo i passaggi tooapply 1.2 di aggiornamento. **Hello aggiornamenti può richiedere circa 2 ore toocomplete (circa 30 minuti per il software, 30 minuti affinché i driver, firmware del disco 45 minuti).**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>Opzione 2: Utilizzare hello Azure tooapply portale classico 1.2 aggiornamento dopo la rimozione di configurazione del gateway hello
Questa procedura si applica tooStorSimple solo i dispositivi che eseguono un tooUpdate precedente versione di software 1 e un gateway impostato su un'interfaccia di rete diverse da DATA 0. Sarà necessario aggiornamento hello del tooclear hello gateway impostazione tooapplying precedente.

aggiornamento di Hello potrebbe richiedere alcune ore toocomplete. Se l'host si trovano in subnet diverse, la rimozione di configurazione del gateway hello sulle interfacce iSCSI hello potrebbe causare tempi di inattività. Si consiglia di configurare i periodi di inattività hello tooreduce il traffico iSCSI DATA 0.

Eseguire i seguenti passaggi toodisable hello l'interfaccia di rete con gateway hello hello e quindi applicare l'aggiornamento di hello.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [versione 1.2 aggiornamento](storsimple-update1-release-notes.md).

