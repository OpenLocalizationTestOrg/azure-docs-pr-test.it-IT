---
title: "aaaGet introduzione dell'utilità di pianificazione di Azure nel portale di Azure | Documenti Microsoft"
description: "Introduzione all'Utilità di pianificazione di Azure nel portale di Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Introduzione all'Utilità di pianificazione di Azure nel portale di Azure
È facile toocreate pianificati processi nell'utilità di pianificazione di Azure. In questa esercitazione si apprenderà come toocreate un processo. Si apprenderanno anche le funzionalità di monitoraggio e gestione dell'Utilità di pianificazione.

## <a name="create-a-job"></a>Creare un processo
1. Accedi troppo[portale di Azure](https://portal.azure.com/).  
2. Fare clic su **+ nuovo** > tipo *dell'utilità di pianificazione* nella casella di ricerca hello > selezionare **dell'utilità di pianificazione** nei risultati > fare clic su **crea**.
   
    ![][marketplace-create]
3. Creiamo un processo che accede semplicemente a http://www.microsoft.com/ con una richiesta GET. In hello **dell'utilità di pianificazione** immettere hello le seguenti informazioni:
   
   1. **Nome:** `getmicrosoft`  
   2. **Sottoscrizione:** sottoscrizione di Azure   
   3. **Raccolta processi:** selezionare una raccolta di processi esistente oppure fare clic su **Crea nuovo** e immettere un nome.
4. Successivamente, nel **Impostazioni azione**, definire hello seguenti valori:
   
   1. **Tipo di azione:** ` HTTP`  
   2. **Metodo:** `GET`  
   3. **URL:** ` http://www.microsoft.com`  
      
      ![][action-settings]
5. Infine, definire una pianificazione. il processo di Hello può essere definito come processo occasionale, ma si seleziona una pianificazione ricorrenza:
   
   1. **Ricorrenza:**`Recurring`
   2. **Inizia**: data odierna
   3. **Ricorre ogni:** `12 Hours`
   4. **Termina entro**: due giorni dalla data odierna  
      
      ![][recurrence-schedule]
6. Fare clic su **Crea**

## <a name="manage-and-monitor-jobs"></a>Gestire e monitorare i processi
Dopo aver creato un processo, viene visualizzato nel dashboard di Azure principale hello. Fare clic su processo hello e un nuovo verrà visualizzata la finestra con hello seguenti schede:

1. Proprietà  
2. Impostazioni azione  
3. Pianificazione  
4. Cronologia
5. Utenti
   
   ![][job-overview]

### <a name="properties"></a>Proprietà
Queste proprietà di sola lettura descrivono i metadati di gestione di hello per il processo dell'utilità di pianificazione hello.

   ![][job-properties]

### <a name="action-settings"></a>Impostazioni azione
Facendo clic su un processo in hello **processi** schermata consente tooconfigure che del processo. Ciò consente di configurare le impostazioni avanzate, se non sono stati configurati in hello della procedura guidata di creazione rapida.

Per tutti i tipi di azione, è possibile modificare i criteri di ripetizione hello e azione di errore hello.

Per i tipi di azione del processo HTTP e HTTPS, è possibile modificare tooany metodo hello verbo HTTP consentito. È anche possibile aggiungere, eliminare o modificare intestazioni hello e le informazioni di autenticazione di base.

Per i tipi di azione della coda di archiviazione, è possibile modificare l'account di archiviazione hello, nome, token di firma di accesso condiviso della coda e corpo.

Per i tipi di azione bus di servizio, è possibile modificare lo spazio dei nomi hello, percorso coda o argomento, le impostazioni di autenticazione, il tipo di trasporto, le proprietà del messaggio e corpo del messaggio.

   ![][job-action-settings]

### <a name="schedule"></a>Pianificazione
Ciò consente di riconfigurare pianificazione hello, se si desidera pianificazione hello toochange che è stato creato in hello della procedura guidata di creazione rapida.

Si tratta di un'opportunità toobuild [pianificazioni complesse e ricorrenza avanzate nel processo](scheduler-advanced-complexity.md)

È possibile modificare la data di inizio hello e tempo, pianificazione ricorrenza e hello data di fine e l'ora (se il processo di hello è ricorrente.)

   ![][job-schedule]

### <a name="history"></a>Cronologia
Hello **cronologia** scheda vengono visualizzate le metriche selezionate per ogni esecuzione del processo nel sistema hello per processo selezionato hello. Queste metriche forniscono valori in tempo reale relativamente hello integrità dell'utilità di pianificazione:

1. Stato  
2. Dettagli  
3. Tentativi
4. Occorrenza: 1, 2, 3 e così via
5. Ora di inizio dell'esecuzione  
6. Ora di fine dell'esecuzione
   
   ![][job-history]

È possibile fare clic su una fase tooview relativo **i dettagli della cronologia**, inclusi l'intera risposta di hello per ogni esecuzione. Questa finestra di dialogo consente anche negli Appunti di toohello toocopy hello risposta.

   ![][job-history-details]

### <a name="users"></a>Utenti
Il controllo degli accessi in base al ruolo di Azure consente una gestione degli accessi specifica per l'Utilità di pianificazione di Azure. toolearn come toouse hello scheda utenti, fare riferimento troppo[gestire il controllo di accesso](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>Vedere anche
 [Che cos'è l'Utilità di pianificazione?](scheduler-intro.md)

 [Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione](scheduler-concepts-terms.md)

 [Piani e fatturazione nell'utilità di pianificazione di Azure](scheduler-plans-billing.md)

 [Come toobuild complesso pianifica e ricorrenza avanzata con utilità di pianificazione di Azure](scheduler-advanced-complexity.md)

 [Riferimento API REST dell'utilità di pianificazione](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione](scheduler-powershell-reference.md)

 [Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione](scheduler-high-availability-reliability.md)

 [Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione](scheduler-limits-defaults-errors.md)

 [Autenticazione in uscita dell'Utilità di pianificazione](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
