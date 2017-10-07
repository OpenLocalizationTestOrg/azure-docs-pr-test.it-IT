---
title: comportamento di avviso aaaSMS in gruppi di azioni | Documenti Microsoft
description: Formato del messaggio SMS e risponde tooSMS messaggi toounsubscribe, ripetuta o richiedere assistenza.
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
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>Comportamento degli avvisi SMS nei gruppi di azione
## <a name="overview"></a>Panoramica ##
Gruppi di azioni consentono di tooconfigure un elenco di destinatari. Questi gruppi possono quindi essere utilizzati quando si definiscono gli avvisi del registro attività; verifica che un gruppo particolare azione riceve una notifica quando viene attivato l'avviso di log attività hello. Uno degli avvisi meccanismi supportati hello è SMS; gli avvisi di Hello supportano la comunicazione bidirezionale. Un utente può rispondere tooan avviso:

- **Annullare la sottoscrizione agli avvisi:** un utente può annullare la sottoscrizione a tutti gli avvisi SMS per tutti i gruppi di azione o per un singolo gruppo di azioni.  
- **Ripetuta tooalerts:** un utente può ripetuta tooall gli avvisi SMS per tutti i gruppi di azioni o un gruppo di azioni singolare.  
- **Richiedere assistenza:** un utente può chiedere ulteriori informazioni su hello SMS. Sarà reindirizzato toothis articolo

Questo articolo descrive il comportamento di hello degli avvisi SMS hello e hello risposta azioni hello utente può eseguire in base alle impostazioni locali di hello dell'utente hello:

## <a name="usacanada-sms-behavior"></a>Comportamento SMS per Stati Uniti e Canada
### <a name="receiving-an-sms-alert"></a>Ricezione di un avviso SMS
Un ricevitore di SMS, configurato come parte di un gruppo di azioni, riceverà un SMS quando viene generato un avviso. Hello SMS trasporterà hello le seguenti informazioni:
* ShortName del gruppo di azioni hello questo avviso è stato inviato a
- Titolo dell'avviso hello

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Annullamento della sottoscrizione agli avvisi SMS per un gruppo di azioni
Un utente può annullare la sottoscrizione SMS per gli avvisi per gruppo di un'azione risponde toohello 20873 con parole chiave hello: "DISABILITARE &lt;Shortname del gruppo di azioni&gt;".

Esempio: Un utente che desiderano toounsubscribe dagli avvisi per un gruppo di azioni con shortname hello "Azure", viene inviato un toohello SMS 20873 indicante "DISABILITARE Azure"

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Annullamento della sottoscrizione agli avvisi SMS per tutti i gruppi di azioni
Un utente può annullare la sottoscrizione tutti gli avvisi SMS per tutti i gruppi di azione risponde toohello 20873 con uno qualsiasi di hello parole chiave seguenti:
* STOP

Esempio: Un utente che desiderano toounsubscribe da tutti gli avvisi SMS per tutti i gruppi di azioni, viene inviato un toohello SMS 20873 indicante "STOP"

>[!NOTE]
>Se un utente ha annullato la sottoscrizione da SMS avvisi, ma viene quindi aggiunto tooa azione al gruppo precedente. si verrà ricevere gli avvisi SMS per il nuovo gruppo di azioni, ma rimangono annullate da tutti i gruppi di azione precedente.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>Ripetere la sottoscrizione tooSMS gli avvisi per un gruppo di azioni
Un utente può ripetuta tooSMS per gli avvisi per gruppo di un'azione da risponde toohello 20873 con parole chiave hello: "abilitare &lt;Shortname del gruppo di azioni&gt;".

Esempio: Un utente che desiderano tooalerts tooresubscribe per un gruppo di azioni con shortname hello "Azure", viene inviato un toohello SMS 20873 indicante "Abilitare Azure"

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>Ripetere la sottoscrizione tooSMS gli avvisi per tutti i gruppi di azioni
Un utente può ripetuta tooall SMS per gli avvisi per tutti i gruppi di azioni da risponde toohello 20873 con uno qualsiasi di hello parole chiave seguenti:

* START

Esempio: Un utente che desiderano toounsubscribe da tutti gli avvisi SMS per tutti i gruppi di azioni, viene inviato un toohello SMS 20873 indicante "START"

### <a name="requesting-help-via-sms"></a>Richiesta di assistenza tramite SMS
Un utente può chiedere per ulteriori informazioni su hello SMS ricevuti da risponde toohello 20873 con una delle seguenti parole chiave hello:
* HELP

Verrà inviata una risposta toohello utente con un articolo toothis di collegamento.

## <a name="next-steps"></a>Passaggi successivi
Ottenere un [panoramica degli avvisi di log attività](monitoring-overview-alerts.md) e informazioni su come viene generato un avviso di tooget  
Altre informazioni sulla [limitazione della frequenza degli SMS](monitoring-alerts-rate-limiting.md)  
Altre informazioni sui [gruppi di azioni](monitoring-action-groups.md)
