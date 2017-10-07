---
title: "gli avvisi del registro attività aaaReceive sulle notifiche di servizio | Documenti Microsoft"
description: Ricevere le notifiche tramite SMS, posta elettronica o webhook nel servizio di Azure.
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>Creare gli avvisi del log attività per le notifiche del servizio
## <a name="overview"></a>Panoramica
Questo articolo illustra come tooset backup log delle attività degli avvisi per le notifiche di integrità del servizio tramite hello portale di Azure.  

È possibile ricevere un avviso quando Azure invia servizio integrità notifiche tooyour sottoscrizione di Azure. È possibile configurare l'avviso hello in base a:

- classe Hello di notifica del servizio integrità (evento imprevisto, manutenzione, le informazioni e così via).
- Hello servizi interessati.
- aree di Hello interessate.
- stato Hello della notifica di hello (attivo e risolti).
- livello di Hello di notifiche di hello (errore, avviso, informativo).

È anche possibile configurare che deve essere inviato avviso hello:

- Selezionare un gruppo di azione esistente.
- Creare un nuovo gruppo di azione che può essere usato per avvisi futuri.

toolearn ulteriori informazioni sui gruppi di azioni, vedere [creare e gestire gruppi di azioni](monitoring-action-groups.md).

Per informazioni su come tooconfigure notifica relativa all'integrità del servizio avvisi utilizzando i modelli di gestione risorse di Azure, vedere [modelli di gestione risorse](monitoring-create-activity-log-alerts-with-resource-manager-template.md).

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>Creare un avviso per una notifica di integrità del servizio per un nuovo gruppo di azione utilizzando hello portale di Azure
1. In hello [portale](https://portal.azure.com)selezionare **monitoraggio**.

    ![Hello "Monitoraggio" del servizio](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. In hello **log attività** selezionare **avvisi**.

    ![Nella scheda "Avvisi" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. Selezionare **Aggiungi avviso di log attività**e compilare i campi di hello.

    ![comando "Aggiungi avviso registro attività" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. Immettere un nome in hello **nome dell'avviso log attività** e specificare un **descrizione**.

    ![finestra di dialogo "Aggiungi avviso registro attività" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. Hello **sottoscrizione** casella autofills con la sottoscrizione corrente. Questa sottoscrizione è di avviso di log attività hello toosave utilizzato. risorsa avviso Hello è toothis distribuito gli eventi di sottoscrizione e i monitoraggi nel registro attività hello relativo.

6. Seleziona hello **gruppo di risorse** in cui hello avviso risorsa sono stati creati. Gruppo di risorse hello monitorato dall'avviso hello non. In alternativa, è il gruppo di risorse hello risorse avviso hello in cui si trova.

7. In hello **categoria di eventi** , quindi selezionare **servizio integrità**. Facoltativamente, selezionare hello **servizio**, **area**, **tipo**, **stato**, e **livello** del servizio notifiche di integrità che si desidera tooreceive.

8. In **avviso tramite**selezionare hello **New** pulsante di azione di gruppo. Immettere un nome in hello **nome del gruppo di azione** e immettere un nome in hello **nome breve** casella. nome breve Hello viene fatto riferimento nelle notifiche hello che vengono inviate quando viene generato questo avviso.

9. Definire un elenco di destinatari fornendo del ricevitore hello:

    a. **Nome**: immettere il nome del destinatario hello, alias o identificatore.

    b. **Tipo di azione**: selezionare webhook, posta elettronica o SMS.

    c. **Dettagli**: basato sul tipo di azione hello scelto, immettere un numero di telefono, indirizzo di posta elettronica o webhook URI.

10. Selezionare **OK** avviso hello toocreate.

Entro pochi minuti, avviso hello è attiva e avvia tootrigger in base alle condizioni di hello specificato durante la creazione.

Per informazioni sullo schema webhook hello per gli avvisi del registro attività, vedere [Webhook per attività di Azure registra avvisi](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>gruppo di azioni Hello definito in questa procedura è riutilizzabile come un gruppo di azioni esistenti per tutte le definizioni di avviso futuri.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>Creare un avviso per una notifica di integrità del servizio per un gruppo di azioni esistenti utilizzando hello portale di Azure

1. Seguire i passaggi da 1 a 7 hello precedente sezione toocreate la notifica del servizio di integrità. 

2. In **avviso tramite**selezionare hello **esistente** pulsante di azione di gruppo. Selezionare il gruppo di azioni appropriato hello.

3. Selezionare **OK** avviso hello toocreate.

Entro pochi minuti, avviso hello è attiva e avvia tootrigger in base alle condizioni di hello specificato durante la creazione.

## <a name="manage-your-alerts"></a>Gestire gli avvisi

Dopo aver creato un avviso, è visibile in hello **avvisi** sezione di hello **monitoraggio** blade. Selezionare l'avviso di hello da toomanage per:

* Modificarlo.
* Eliminarlo.
* Disabilitare o abilitare, se si desidera tootemporarily arrestare o riprendere la ricezione di notifiche di avviso hello.

## <a name="next-steps"></a>Passaggi successivi
- Informazioni sulle [notifiche per l'integrità del servizio](monitoring-service-notifications.md).
- Informazioni sulla [limitazione della frequenza delle notifiche](monitoring-alerts-rate-limiting.md).
- Hello revisione [schema webhook avvisi del registro attività](monitoring-activity-log-alerts-webhook.md).
- Ottenere un [panoramica degli avvisi di log attività](monitoring-overview-alerts.md)e informazioni su come tooreceive avvisi. 
- Altre informazioni sui [gruppi di azione](monitoring-action-groups.md).
