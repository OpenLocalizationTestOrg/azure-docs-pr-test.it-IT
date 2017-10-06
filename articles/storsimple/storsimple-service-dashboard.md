---
title: dashboard del servizio di gestione aaaStorSimple | Documenti Microsoft
description: "Dashboard del servizio StorSimple Manager hello descrive e illustra come toouse, integrità hello toomonitor della soluzione StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>Utilizzare dashboard del servizio StorSimple Manager hello
## <a name="overview"></a>Panoramica
pagina del dashboard del servizio StorSimple Manager Hello fornisce un riepilogo di tutti i dispositivi di hello che sono connesso toohello servizio StorSimple Manager, evidenziando quelli che richiedono attenzione da parte dell'amministratore di sistema. In questa esercitazione presenta pagina dashboard hello, spiega (funzione) e del contenuto del dashboard hello e vengono descritte le attività di hello che è possibile eseguire in questa pagina.

![Dashboard del servizio](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

dashboard del servizio StorSimple Manager Hello Visualizza hello le seguenti informazioni:

* In hello **grafico** area, è possibile visualizzare le metriche pertinenti hello del grafico per i dispositivi. È possibile visualizzare hello archiviazione primaria (in locale bloccata e a livelli) usata in tutti i dispositivi di hello, così come spazio di archiviazione cloud hello utilizzati dai dispositivi in un periodo di tempo. Usare hello controlli nell'angolo superiore destro di hello di hello grafico toospecify una scala temporale di 1 settimana, 1 mese, 3 mesi o 1 anno.
* Hello **panoramica sull'utilizzo** Mostra hello archiviazione primaria che viene eseguito il provisioning e utilizzati da tutti i dispositivi toohello relativo spazio di archiviazione totale disponibile tra tutti i dispositivi. **Il provisioning** fa riferimento toohello quantità di spazio di archiviazione viene preparata e allocata per l'uso, mentre **utilizzato** fa riferimento toousage di volumi di base a quanto visualizzato dagli iniziatori hello che sono dispositivi toohello connesso.
* Hello **avvisi** area fornisce uno snapshot di tutti gli avvisi attivi hello in tutti i dispositivi di hello, raggruppati in base alla gravità dell'avviso. Fare clic sul livello di gravità hello apre hello **avvisi** pagina, con ambito tooshow tali avvisi. In hello **avvisi** pagina, è possibile fare clic su un singolo tooview avviso ulteriori dettagli su tale avviso, incluse tutte le azioni consigliate. È inoltre possibile cancellare avviso hello se hello problema è stato risolto.
* Hello **processi** area fornisce uno snapshot dei processi recenti in tutti i dispositivi connessi tooyour servizio. Sono disponibili collegamenti che è possibile utilizzare i processi attualmente in corso, quelli che non è riuscito a hello ultime 24 ore, toolook o quelli che vengono pianificati toorun in hello 24 ore successive.
* Hello **riepilogo rapido** area fornisce informazioni utili, ad esempio lo stato del servizio, il numero di dispositivi connessi toohello servizio, posizione del servizio hello e dettagli della sottoscrizione hello associata al servizio hello. È inoltre disponibile un log di operazioni di collegamento toohello. Fare clic su hello collegamento toosee un elenco di tutte le operazioni del servizio StorSimple Manager completata.

È possibile utilizzare hello StorSimple Manager servizio dashboard pagina tooinitiate hello seguenti attività:

* Consente di visualizzare o rigenerare la chiave di registrazione del servizio hello.
* Modifica hello chiave DEK del servizio.
* Consente di visualizzare i log delle operazioni hello.

## <a name="view-or-regenerate-hello-service-registration-key"></a>Consente di visualizzare o rigenerare la chiave di registrazione del servizio hello
chiave di registrazione del servizio Hello è tooregister usato un dispositivo StorSimple di Microsoft Azure con il servizio StorSimple Manager hello, in modo che hello dispositivo viene visualizzato in hello portale di Azure classico per ulteriori azioni di gestione. chiave Hello creato nel primo dispositivo hello e condivisi con rest hello dei dispositivi.

Fare clic su **chiave di registrazione** (nella parte inferiore di hello della pagina hello) apre hello **chiave di registrazione del servizio** nella finestra di dialogo in cui è possibile una copia hello corrente del servizio registrazione toohello chiave Appunti o rigenerare la chiave di registrazione del servizio hello.

Rigenerazione della chiave di hello interessano i dispositivi registrati in precedenza: interessa solo i dispositivi di hello che sono registrati con il servizio hello dopo hello chiave viene rigenerata.

Per ulteriori informazioni sulla visualizzazione e la generazione di chiavi, Vai di hello servizio registrazione troppo[chiave di registrazione del servizio Get hello](storsimple-manage-service.md#get-the-service-registration-key).

## <a name="change-hello-service-data-encryption-key"></a>Modifica chiave DEK del servizio hello
Le chiavi DEK del servizio sono utilizzati tooencrypt dati confidenziali, ad esempio credenziali dell'account di archiviazione, che vengono inviati dal dispositivo StorSimple toohello servizio StorSimple Manager. Sarà necessario toochange queste chiavi periodicamente se l'organizzazione IT con un criterio di rotazione delle chiavi su dispositivi di archiviazione hello. Hello il processo di modifica può essere variare leggermente a seconda se sussiste una o più dispositivi gestiti dal servizio StorSimple Manager hello.

Modifica hello chiave DEK del servizio sono un processo passaggio 3:

1. Utilizza hello portale di Azure classico, autorizzare una dispositivo toochange hello chiave DEK del servizio.
2. Utilizzo di Windows PowerShell per StorSimple, avviare hello servizio modifica della chiave DEK.
3. Se si dispone di più di un dispositivo StorSimple, hello chiave DEK del servizio su hello aggiornare altri dispositivi.

Hello passaggi seguenti descrivono il processo di rollover hello hello servizio dati chiave di crittografia.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>Visualizzare i registri operazioni hello
È possibile visualizzare i log delle operazioni hello facendo hello collegamento disponibile in hello **riepilogo rapido** riquadro del dashboard hello. Verrà visualizzata la pagina Gestione toohello pagina servizi, in cui è possibile filtrare e vedere hello registra servizio StorSimple Manager tooyour specifico.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[risolvere i problemi relativi a un dispositivo StorSimple](storsimple-troubleshoot-operational-device.md).
* Per ulteriori informazioni su troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

