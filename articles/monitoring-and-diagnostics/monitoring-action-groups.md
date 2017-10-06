---
title: aaaCreate e gestire gruppi di azioni di hello portale di Azure | Documenti Microsoft
description: Informazioni su come toocreate e gestire gruppi di azioni di hello portale di Azure.
author: anirudhcavale
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Creare e gestire gruppi di azioni di hello portale di Azure
## <a name="overview"></a>Panoramica ##
In questo articolo illustra come toocreate e gestire gruppi di azioni di hello portale di Azure.

I gruppi di azione consentono di configurare un elenco di azioni. È possibile usare questi gruppi quando si definiscono gli avvisi del log attività. Questi gruppi possono essere riutilizzati da definire, assicurando che hello stesse azioni vengono eseguite ogni volta che viene attivato l'avviso di log attività hello ogni avviso di log attività.

Un gruppo di azioni può esistere fino a too10 di ogni tipo di azione. Ogni azione è costituito da hello le proprietà seguenti:

* **Nome**: un identificatore univoco all'interno di gruppo di azioni di hello.  
* **Tipo di azione**: inviare un SMS, un messaggio di posta elettronica o chiamare un webhook.  
* **Dettagli**: hello corrispondente numero di telefono, indirizzo di posta elettronica o webhook URI.

Per informazioni su come toouse gruppi di azioni di gestione risorse di Azure modelli tooconfigure, vedere [modelli di gestione risorse di gruppo azione](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Creare un gruppo di azioni tramite hello portale di Azure ##
1. In hello [portale](https://portal.azure.com)selezionare **monitoraggio**. Hello **monitoraggio** pannello consolida tutte le impostazioni e dati in una visualizzazione monitoraggio.

    ![Hello "Monitoraggio" del servizio](./media/monitoring-action-groups/home-monitor.png)
2. In hello **log attività** selezionare **gruppi di azioni**.

    ![scheda "Gruppi di azioni" Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. Selezionare **Aggiungi gruppo di azioni**e compilare i campi di hello.

    ![comando "Aggiungi gruppo di azioni di" Hello](./media/monitoring-action-groups/add-action-group.png)
4. Immettere un nome in hello **nome del gruppo di azione** e immettere un nome in hello **nome breve** casella. nome breve Hello viene utilizzato al posto di un nome di un gruppo completo azione quando le notifiche vengono inviate utilizzando questo gruppo.

      ![la finestra di dialogo gruppo di azioni Aggiungi Hello"](./media/monitoring-action-groups/action-group-define.png)

5. Hello **sottoscrizione** casella autofills con la sottoscrizione corrente. Questa sottoscrizione è hello uno nel gruppo di azioni quali hello viene salvato.

6. Seleziona hello **gruppo di risorse** in cui azione hello gruppo viene salvato.

7. Definire un elenco di azioni fornendo i dati di ogni azione:

    a. **Nome**: immettere un identificatore univoco per questa azione.

    b. **Tipo di azione**: selezionare webhook, posta elettronica o SMS.

    c. **Dettagli**: basato sul tipo di azione hello, immettere un numero di telefono, indirizzo di posta elettronica o webhook URI.

8. Selezionare **OK** toocreate gruppo di azioni hello.

## <a name="manage-your-action-groups"></a>Gestire i gruppi di azione ##
Dopo aver creato un gruppo di azioni, è visibile in hello **gruppi di azioni** sezione di hello **monitoraggio** blade. Selezionare il gruppo di azioni hello desiderato toomanage per:

* Aggiungere, modificare o rimuovere azioni.
* Eliminare il gruppo di azioni di hello.

## <a name="next-steps"></a>Passaggi successivi ##
* Altre informazioni sul [Comportamento degli avvisi SMS](monitoring-sms-alert-behavior.md).  
* Ottenere un [informazioni dello schema di avviso webhook log attività hello](monitoring-activity-log-alerts-webhook.md).  
* Altre informazioni sulla [limitazione della frequenza](monitoring-alerts-rate-limiting.md) degli avvisi. 
* Ottenere un [panoramica degli avvisi di log attività](monitoring-overview-alerts.md)e informazioni su come tooreceive avvisi.  
* Informazioni su come troppo[configurare gli avvisi ogni volta che viene registrata una notifica di integrità del servizio](monitoring-activity-log-alerts-on-service-notifications.md).
