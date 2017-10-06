---
title: "aaaWhat sono le notifiche di integrità servizio | Documenti Microsoft"
description: "Le notifiche di integrità servizio consentono di che messaggi di integrità servizio tooview pubblicate da Microsoft Azure."
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>Notifiche sull'integrità del servizio
## <a name="overview"></a>Panoramica

In questo articolo viene illustrato come tramite le notifiche di integrità servizio tooview hello portale di Azure.

Le notifiche di integrità servizio consentono si tooview servizio integrità messaggi pubblicati dall'hello Azure team che potrebbero influire sul risorse hello nella sottoscrizione. Queste notifiche sono una sottoclasse dell'attività del log eventi e sono disponibili nel Pannello di log attività hello. Le notifiche di integrità del servizio possono essere utilizzabili a seconda della classe hello o informativi.

Sono disponibili sei classi di notifiche sull'integrità del servizio:  

- **Azione richiesta:** da tootime tempo potrebbe notiamo qualcosa di sospetto verificarsi nel tuo account. È possibile che sia necessario toowork con si tooremedy questo. Ti invieremo una notifica di che riporta in dettaglio le azioni di hello occorre tootake o con informazioni dettagliate sulla progettazione toocontact Azure o il supporto.  
- **Recupero assistito:** si è verificato un evento e i tecnici confermano gli effetti dell'evento ancora presenti. Team di progettazione sarà necessario toowork con l'utente direttamente toobring toorestoration i servizi.  
- **Evento imprevisto:** attualmente interessa un servizio che hanno un impatto evento uno o più risorse hello nella sottoscrizione.  
- **Manutenzione:** si tratta di una notifica per informare l'utente di un'attività di manutenzione pianificata che potrebbe influire negativamente uno o più risorse hello nella sottoscrizione.  
- **Informazioni:** da tootime tempo per l'invio di notifiche che un tooyou per comunicare su potenziali ottimizzazioni che possono aiutare a migliorare l'utilizzo di risorse.  
- **Sicurezza:** informazioni urgenti relative alla sicurezza delle soluzioni in esecuzione in Azure.

Ogni notifica del servizio di integrità trasporterà dettagli sulle risorse di tooyour hello ambito e impatto. Le informazioni includono:

Nome proprietà | Descrizione
-------- | -----------
channels | È uno dei seguenti valori hello: "Admin", "Operation"
correlationId | È in genere un GUID in formato stringa hello. Gli eventi che appartengono toohello stessa azione condividono di solito hello stesso correlationId.
eventDataId | È hello identificatore univoco di un evento
eventName | Hello titolo dell'evento hello
level | Livello dell'evento hello. Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose"
resourceProviderName | Nome del provider di risorse hello per hello interessati risorsa
resourceType| tipo di Hello della risorsa di hello interessati risorsa
subStatus | In genere il codice di stato HTTP della corrispondente chiamata REST hello hello, ma può includere anche altre stringhe che descrive uno stato secondario, ad esempio i valori comuni: OK (codice di stato HTTP: 200), creato (codice di stato HTTP: 201), accettato (codice di stato HTTP: 202), il contenuto No (HTTP Codice di stato: 204), richiesta non valida (codice di stato HTTP: 400), non è stata trovata (codice di stato HTTP: 404), dei conflitti (codice di stato HTTP: 409), errore interno del Server (codice di stato HTTP: 500), Service non disponibile (codice di stato HTTP: 503), Timeout del Gateway (codice di stato HTTP: 504).
eventTimestamp | Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente.
submissionTimestamp |   Timestamp dell'evento hello è diventato disponibile per l'esecuzione di query.
subscriptionId | sottoscrizione di Azure in cui è stato registrato questo evento di Hello
status | Stringa che descrive lo stato di hello dell'operazione di hello. Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved.
operationName | Nome dell'operazione di hello.
category | "ServiceHealth"
resourceId | Id di risorsa di hello influisce sulle risorse.
Properties.title | Hello titolo localizzato per la comunicazione. L'inglese è una lingua predefinita hello.
Properties.communication | Hello localizzata dettagli di comunicazione hello con il markup HTML. Inglese è l'impostazione predefinita di hello.
Properties.incidentType | Valori possibili: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifica l'evento imprevisto di hello che è associato questo evento. Utilizzare questo evento imprevisto di toocorrelate hello eventi tooan correlati.
Properties.impactedServices | Un escape blob JSON che descrive i servizi di hello e le aree che sono interessate da evento imprevisto di hello. Un elenco di servizi, ognuno dei quali ha un nome di servizio e un elenco delle aree interessate, ognuna con un nome di area.
Properties.defaultLanguageTitle | comunicazione Hello in inglese
Properties.defaultLanguageContent | comunicazione Hello in inglese come markup html o testo normale
Properties.stage | I valori possibili di AssistedRecovery, ActionRequired, Information, Incident, Security sono Active e Resolved. Per la manutenzione i valori possibili sono: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete
Properties.communicationId | comunicazione Hello questo evento è associato.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Visualizzare le notifiche di integrità del servizio nel portale di Azure hello
1.  In hello [portale](https://portal.azure.com), passare toohello **monitoraggio** servizio

    ![Monitorare](./media/monitoring-service-notifications/home-monitor.png)
2.  Fare clic su hello **monitoraggio** tooopen opzione backup pannello monitoraggio hello. che riunisce tutte le impostazioni e i dati di monitoraggio in un'unica vista consolidata. Viene aperto prima toohello **log attività** sezione.

3.  Fare clic sulla sezione **Notifiche del servizio**

    ![Monitorare](./media/monitoring-service-notifications/service-health-summary.png)
4.  Fare clic su qualsiasi hello voci tooview ulteriori dettagli

5. Fare clic su hello **+ Aggiungi avviso di Log attività** operazione tooreceive notifiche tooensure viene inviata una notifica per le notifiche di servizio future di questo tipo. ulteriori informazioni su configurazione degli avvisi per le notifiche di servizio toolearn [fare clic qui](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Passaggi successivi:
Ricevere [notifiche di avviso per ogni notifica sull'integrità del servizio](monitoring-activity-log-alerts-on-service-notifications.md)  
Altre informazioni sugli [avvisi del log attività](monitoring-activity-log-alerts.md)
