---
title: Installare l'aggiornamento 1.2 nel dispositivo StorSimple | Microsoft Docs
description: Illustra come installare l'aggiornamento 1.2 di StorSimple serie 8000 sul dispositivo StorSimple serie 8000.
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
ms.openlocfilehash: 80ff35cc47dfc38089f4c392ef4c90baf9ccc03e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>Installare l'aggiornamento 1.2 nel dispositivo StorSimple serie 8000
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come installare l'aggiornamento 1.2 in un dispositivo StorSimple in cui è in esecuzione una versione del software prima dell'aggiornamento 1. L'esercitazione illustra anche le ulteriori procedure richieste per l'aggiornamento quando un gateway è configurato su un'interfaccia di rete diversa da DATA 0 del dispositivo StorSimple.

L'aggiornamento 1.2 include aggiornamenti del software del dispositivo, aggiornamenti del driver LSI e aggiornamenti del firmware del disco. Gli aggiornamenti del software e del driver LSI non sono problematici e possono essere applicati attraverso il portale di Azure classico. Gli aggiornamenti del firmware del disco sono problematici e possono essere applicati solo tramite l'interfaccia di Windows PowerShell del dispositivo.

In base alla versione eseguita dal dispositivo, è possibile determinare se verrà applicato l'aggiornamento 1.2. È possibile verificare la versione del software del dispositivo passando alla sezione **Riepilogo rapido** del **Dashboard** del dispositivo.

</br>

| Se è in esecuzione la versione del software... | Cosa accade nel portale? |
| --- | --- |
| Versione - GA |Se è in esecuzione la versione finale (GA), non applicare questo aggiornamento. Contattare il [supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per aggiornare il dispositivo. |
| Aggiornamento 0.1 |Il portale applica l'aggiornamento 1.2. |
| Aggiornamento 0.2 |Il portale applica l'aggiornamento 1.2. |
| Aggiornamento 0.3 |Il portale applica l'aggiornamento 1.2. |
| Aggiornamento 1 |Questo aggiornamento non sarà disponibile. |
| Aggiornamento 1.1 |Questo aggiornamento non sarà disponibile. |

</br>

> [!IMPORTANT]
> * L'aggiornamento 1.2 potrebbe non essere immediatamente visibile perché viene effettuata un'implementazione graduale degli aggiornamenti. Provare a cercare nuovamente l'aggiornamento dopo qualche giorno perché verrà presto reso disponibile.
> * Questo aggiornamento include una serie di controlli preliminari automatici e manuali per determinare l'integrità del dispositivo in termini di connettività di stato e di rete hardware. Questi controlli preliminari vengono eseguiti solo se si applicano gli aggiornamenti dal portale di Azure classico.
> * Si consiglia di installare gli aggiornamenti software e driver tramite il portale di Azure classico. Passare all'interfaccia di Windows PowerShell del dispositivo (per installare gli aggiornamenti) solo se il gateway di pre-aggiornamento ha esito negativo nel portale. L'installazione di tutti gli aggiornamenti, inclusi gli aggiornamenti di Windows, potrebbe richiedere fino a 5-10 ore. Gli aggiornamenti in modalità di manutenzione devono essere installati tramite l'interfaccia di Windows PowerShell del dispositivo. Dal momento che si tratta di aggiornamenti problematici, comporteranno un periodo di inattività per il dispositivo.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-the-azure-classic-portal"></a>Installare l'aggiornamento 1.2 tramite il portale di Azure classico.
Seguire questa procedura per aggiornare il dispositivo a [Aggiornamento 1.2](storsimple-update1-release-notes.md). Usare questa procedura solo se è presente un gateway configurato sull'interfaccia di rete DATA 0 sul dispositivo.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Verificare che nel dispositivo sia in esecuzione l' **aggiornamento 1.2 della serie 8000 di StorSimple (6.3.9600.17584)**. Inoltre, è necessario modificare la **data dell'ultimo aggiornamento** . Saranno anche disponibili gli aggiornamenti in modalità manutenzione. Questo messaggio potrebbe essere visualizzato fino a 24 ore dopo l’installazione degli aggiornamenti.
   
   Gli aggiornamenti in modalità manutenzione sono aggiornamenti problematici che comportano tempi di inattività del dispositivo e possono essere applicati solo tramite l'interfaccia di Windows PowerShell del dispositivo.
   
   ![Pagina di manutenzione](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Pagina Manutenzione")
2. Scaricare gli aggiornamenti in modalità manutenzione utilizzando la procedura indicata in [Scaricare gli aggiornamenti rapidi](#to-download-hotfixes) per cercare e scaricare KB3063416, che installa gli aggiornamenti del firmware del disco (gli altri aggiornamenti devono essere già installati a questo punto).
3. Seguire i passaggi elencati nella sezione [Installare e verificare gli aggiornamenti rapidi in modalità manutenzione](#to-install-and-verify-maintenance-mode-hotfixes) per installare gli aggiornamenti in modalità manutenzione.
4. Nel portale di Azure classico passare alla pagina **Manutenzione** e, nella parte inferiore della pagina, fare clic su **Cerca aggiornamenti** per verificare la presenza di eventuali aggiornamenti di Windows e quindi fare clic su **Installa aggiornamenti**. Attendere che tutti gli aggiornamenti vengano installati correttamente.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>Installare l'aggiornamento 1.2 in un dispositivo con un gateway configurato per un'interfaccia di rete non DATA 0
Usare questa procedura solo se la verifica del gateway non riesce quando si cerca di installare gli aggiornamenti tramite il portale di Azure classico. La verifica non riesce quando un gateway è assegnato a un'interfaccia di rete non DATA 0e sul dispositivo è in esecuzione una versione del software precedente all'aggiornamento 1. Se il dispositivo non dispone di un gateway su un'interfaccia di rete 0 non di dati, è possibile aggiornare il dispositivo direttamente dal portale di Azure classico. Vedere [Installare l'aggiornamento 1.2 tramite il portale di Azure classico](#install-update-1.2-via-the-azure-classic-portal).

Le versioni software che possono essere aggiornate usando questo metodo sono Aggiornamento 0.1, Aggiornamento 0.2 e Aggiornamento 0.3.

> [!IMPORTANT]
> * Se il dispositivo esegue la versione finale (GA), contattare [il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per assistenza relativa all'aggiornamento.
> * Questa procedura deve essere eseguita solo una volta per applicare l'aggiornamento 1.2. È possibile utilizzare il portale di Azure classico per applicare gli aggiornamenti successivi.
> 
> 

Se sul dispositivo è in esecuzione un software precedente all'aggiornamento 1 e ha un gateway impostato per un'interfaccia di rete diversa da DATA 0, è possibile applicare l'aggiornamento 1.2 nei due modi seguenti:

* **Opzione 1**: scaricare l'aggiornamento e applicarlo usando il cmdlet `Start-HcsHotfix` dall'interfaccia Windows PowerShell del dispositivo. Questo è il metodo consigliato. **Non usare questo metodo per applicare l’aggiornamento 1.2 se il dispositivo esegue l’aggiornamento 1.0 o 1.1.**
* **Opzione 2**: rimuovere la configurazione del gateway e installare l'aggiornamento direttamente dal portale di Azure classico.

Nelle sezioni seguenti vengono fornite istruzioni dettagliate per ciascuno di essi.

## <a name="option-1-use-windows-powershell-for-storsimple-to-apply-update-12-as-a-hotfix"></a>Opzione 1: usare Windows PowerShell per StorSimple per applicare l'aggiornamento 1.2 come hotfix
Usare questa procedura solo se si esegue l'aggiornamento 0.1, 0.2, 0.3 e se la verifica del gateway non è riuscita quando si è provato a installare gli aggiornamenti tramite il portale di Azure classico. Se si esegue la versione finale (GA), contattare il [supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per aggiornare il dispositivo.

Per installare l'Aggiornamento 1.2 come un aggiornamento rapido, è necessario scaricare e installare i seguenti aggiornamenti rapidi:

| Ordine | KB | Descrizione | Tipo di aggiornamento |
| --- | --- | --- | --- |
| 1 |KB3063418 |Aggiornamento software |Normale |
| 2 |KB3043005 |Aggiornamento del controller LSI SAS |Normale |
| 3 |KB3063416 |Firmware del disco |Manutenzione |

Prima di utilizzare questa procedura per applicare l'aggiornamento, verificare quanto segue:

* Entrambi i controller di dispositivo sono in linea.

Seguire questa procedura per applicare l'aggiornamento 1.2 **Il completamento degli aggiornamenti potrebbe richiedere circa 2 ore (circa 30 minuti per il software, 30 minuti per il driver, 45 minuti per il firmware del disco).**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-the-azure-classic-portal-to-apply-update-12-after-removing-the-gateway-configuration"></a>Opzione 2: usare il portale di Azure classico per applicare l'aggiornamento 1.2 dopo aver rimosso la configurazione del gateway
Questa procedura si applica solo ai dispositivi StorSimple che eseguono una versione del software precedente all'aggiornamento 1 e hanno un gateway impostato su un'interfaccia di rete diversa da DATA 0. È necessario deselezionare l'impostazione gateway prima di applicare l'aggiornamento.

L'aggiornamento potrebbe richiedere alcune ore. Se l'host si trovano in subnet diverse, rimuovendo la configurazione del gateway sulle interfacce iSCSI può comportare tempi di inattività. Si consiglia di configurare DATA 0 per il traffico iSCSI per ridurre il tempo di inattività.

Seguire la procedura seguente per disabilitare l'interfaccia di rete con il gateway e quindi applicare l'aggiornamento.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sulla [versione dell'aggiornamento 1.2](storsimple-update1-release-notes.md)

