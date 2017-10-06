---
title: "gli avvisi del registro attività aaaCreate | Documenti Microsoft"
description: "Ricevere una notifica tramite posta elettronica, SMS e webhook quando si verificano determinati eventi nel registro attività hello."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>Creare avvisi del log attività

## <a name="overview"></a>Panoramica
Gli avvisi del registro attività sono avvisi che attiverà quando viene generato un nuovo evento del log di attività che corrisponde alle condizioni di hello specificate nell'avviso di hello. Si tratta di risorse di Azure e possono essere create usando un modello di Azure Resource Manager. Sono inoltre può essere creati, aggiornati o eliminati nel portale di Azure hello. In questo articolo vengono presentati i concetti di base hello gli avvisi del registro attività. Viene quindi visualizzato come toouse hello tooset portale Azure backup di un avviso per eventi del registro attività.

In genere, si creano gli avvisi del registro attività tooreceive notifiche quando:

* Modifiche specifiche sulle risorse di sottoscrizione di Azure, risorse o gruppi di risorse tooparticular spesso con ambito. Ad esempio, è consigliabile una notifica quando viene eliminata una macchina virtuale in myProductionResourceGroup toobe. In alternativa, è possibile toobe riceve una notifica se eventuali nuovi ruoli assegnati tooa utente nella sottoscrizione.
* Si verifica un evento di integrità del servizio. Gli eventi di integrità servizio includono la notifica di eventi imprevisti e gli eventi di manutenzione che si applicano tooresources nella sottoscrizione.

In entrambi i casi, un avviso di log attività consente di monitorare solo per gli eventi nella sottoscrizione hello in cui hello viene creato l'avviso.

È possibile configurare un avviso di log attività in base a qualsiasi proprietà di primo livello nell'oggetto JSON hello per un evento di registro attività. Tuttavia, portale hello Mostra opzioni più comuni di hello:

- **Categoria**: amministrazione, integrità del servizio, scalabilità automatica e indicazione. Per ulteriori informazioni, vedere [Panoramica del log attività Azure hello](./monitoring-overview-activity-logs.md#categories-in-the-activity-log). toolearn informazioni su eventi di integrità del servizio, vedere [ricevere gli avvisi del registro attività sulle notifiche di servizio](./monitoring-activity-log-alerts-on-service-notifications.md).
- **Gruppo di risorse**
- **Risorsa**
- **Tipo di risorsa**
- **Nome dell'operazione**: nome dell'operazione di controllo di accesso basato sui ruoli Gestione risorse hello.
- **Livello**: hello a livello di gravità dell'evento hello (dettagliato, informativo, avviso, errore o critico).
- **Stato**: stato di hello dell'evento di hello, in genere avviato, non è riuscito o ha avuto esito positivo.
- **Evento avviato da**: anche noto come hello "chiamante". indirizzo di posta elettronica Hello o un identificatore di Azure Active Directory dell'utente hello che ha eseguito l'operazione di hello.

>[!NOTE]
>È necessario specificare almeno due delle hello criteri che precede l'avviso, con una categoria di hello. Non è possibile creare un avviso che viene attivato ogni volta che viene creato un evento nel log attività hello.
>
>

Quando si attiva un avviso di log di attività, utilizza un'azione gruppo toogenerate azioni o le notifiche. Un gruppo di azione è un set riutilizzabile di ricevitori di notifica, ad esempio gli indirizzi di posta elettronica, gli URL webhook o i numeri di telefono di SMS. ricevitori di Hello possono fare riferimento da più toocentralize gli avvisi e raggruppare i canali di notifica. Quando si definisce l'avviso del log di attività, sono disponibili due opzioni. È possibile:

* Usare un gruppo di azione esistente nell'avviso del log attività. 
* Creare un nuovo gruppo di azione. 

toolearn ulteriori informazioni sui gruppi di azioni, vedere [creare e gestire gruppi di azioni nel portale di Azure hello](monitoring-action-groups.md).

toolearn sulle notifiche di integrità del servizio, vedere [ricevere gli avvisi del registro attività sulle notifiche di integrità servizio](monitoring-activity-log-alerts-on-service-notifications.md).

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Creare un avviso per un evento di registro attività con un nuovo gruppo di azione utilizzando hello portale di Azure
1. In hello [portale](https://portal.azure.com)selezionare **monitoraggio**.

    ![Hello "Monitoraggio" del servizio](./media/monitoring-activity-log-alerts/home-monitor.png)
2. In hello **log attività** selezionare **avvisi**.

    ![Nella scheda "Avvisi" Hello](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. Selezionare **Aggiungi avviso di log attività**e compilare i campi di hello.

4. Immettere un nome in hello **nome dell'avviso log attività** e selezionare un **descrizione**.

    ![comando "Aggiungi avviso registro attività" Hello](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. Hello **sottoscrizione** casella autofills con la sottoscrizione corrente. Questa sottoscrizione è hello uno nel gruppo di azioni quali hello viene salvato. risorsa avviso Hello è distribuito toothis sottoscrizione e i monitoraggi log eventi dell'attività da essa.

    ![finestra di dialogo "Aggiungi avviso registro attività" Hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. Seleziona hello **gruppo di risorse** in cui hello avviso risorsa sono stati creati. Non si tratta di gruppo di risorse hello monitorato dall'avviso hello. In alternativa, è il gruppo di risorse hello risorse avviso hello in cui si trova.

7. Facoltativamente, selezionare un **categoria di eventi** toomodify hello filtri aggiuntivi che vengono visualizzati. Per gli eventi amministrativi, i filtri di hello includono **gruppo di risorse**, **risorse**, **tipo di risorsa**, **nome operazione**, **Livello**, **stato**, e **evento avviato da**. Questi valori identificano gli eventi che devono essere monitorati da questo avviso.

    >[!NOTE]
    >È necessario specificare almeno uno dei criteri che precede l'avviso hello. Non è possibile creare un avviso che viene attivato ogni volta che viene creato un evento nel log attività hello.
    >
    >

8. Immettere un nome in hello **nome del gruppo di azione** e immettere un nome in hello **nome breve** casella. nome breve Hello viene utilizzato al posto di un nome di un gruppo completo azione quando le notifiche vengono inviate utilizzando questo gruppo.

9.  Definire un elenco di azioni fornendo dell'azione hello:

    a. **Nome**: immettere il nome dell'azione di hello, alias o identificatore.

    b. **Tipo di azione**: selezionare webhook, posta elettronica o SMS.

    c. **Dettagli**: basato sul tipo di azione hello, immettere un numero di telefono, indirizzo di posta elettronica o webhook URI.

10. Selezionare **OK** avviso hello toocreate.

avviso di Hello richiede alcuni minuti toofully propagare e quindi diventare attivo. Viene attivato quando i criteri dell'avviso hello corrispondono a nuovi eventi.

Per ulteriori informazioni, vedere [informazioni schema di webhook hello utilizzato con gli avvisi del registro attività](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>gruppo di azioni Hello definito in questa procedura è riutilizzabile come un gruppo di azioni esistenti per tutte le definizioni di avviso futuri.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Creare un avviso per un evento di registro attività per un gruppo di azioni esistenti utilizzando hello portale di Azure
1. Seguire i passaggi da 1 a 7 hello precedente sezione toocreate l'avviso di log di attività.

2. In **notificare tramite**selezionare hello **esistente** pulsante di azione di gruppo. Selezionare un gruppo di azioni esistenti dall'elenco di hello.

3. Selezionare **OK** avviso hello toocreate.

avviso di Hello richiede alcuni minuti toofully propagare e quindi diventare attivo. Viene attivato quando i criteri dell'avviso hello corrispondono a nuovi eventi.

## <a name="manage-your-alerts"></a>Gestire gli avvisi

Dopo aver creato un avviso, è visibile nella sezione avvisi hello del pannello monitoraggio hello. Selezionare l'avviso di hello da toomanage per:

* Modificarlo.
* Eliminarlo.
* Disabilitare o abilitare, se si desidera tootemporarily arrestare o riprendere la ricezione di notifiche di avviso hello.

## <a name="next-steps"></a>Passaggi successivi
- Ottenere una [panoramica degli avvisi](monitoring-overview-alerts.md).
- Informazioni sulla [limitazione della frequenza delle notifiche](monitoring-alerts-rate-limiting.md).
- Hello revisione [schema webhook avvisi del registro attività](monitoring-activity-log-alerts-webhook.md).
- Altre informazioni sui [gruppi di azione](monitoring-action-groups.md).  
- Informazioni sulle [notifiche per l'integrità del servizio](monitoring-service-notifications.md).
- Creare un [attività tutte le operazioni del motore di scalabilità automatica per la sottoscrizione di avvisi toomonitor log](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Creare un [attività tutte le operazioni di scala/scalabilità di scalabilità automatica non riuscita per la sottoscrizione di avvisi toomonitor log](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
