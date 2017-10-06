---
title: aaaOverview degli avvisi di Microsoft Azure e il monitoraggio di Azure | Documenti Microsoft
description: Gli avvisi consentono di metriche delle risorse di Azure toomonitor, eventi o i registri e ricevere una notifica quando viene soddisfatta una condizione specificata.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>Cosa sono gli avvisi in Microsoft Azure?
Questo articolo descrive hello hello di diverse origini degli avvisi in Microsoft Azure, quali sono le attività per gli avvisi, i vantaggi e la modalità di avvio tooget loro utilizzo. In particolare si applica tooAzure monitoraggio, ma fornisce puntatori tooother servizi nonché degli avvisi. Gli avvisi offrono un metodo di monitoraggio in Azure che consentono di condizioni tooconfigure sui dati e diventare una notifica quando le condizioni di hello corrispondono hello dati di monitoraggio più recente.

## <a name="taxonomy-of-azure-alerts"></a>Tassonomia degli avvisi di Azure
Le condizioni seguenti hello Azure utilizza toodescribe avvisi e le relative funzioni:
* **Avviso**: una definizione di criteri (una o più regole o condizioni) che vengono attivati quando vengono soddisfatti.
* **Attiva** - hello stato quando hello viene soddisfatto i criteri definiti da un avviso.
* **Risolto** : hello stato quando hello criteri definiti da un avviso non viene più soddisfatta dopo avere precedentemente stati soddisfatti.
* **Notifica** -hello azione eseguita in base di fuori di un avviso diventa attiva.
* **Azione** -chiamata specifica inviato tooa ricevitore di una notifica (ad esempio, l'invio di un indirizzo o URL del webhook tooa di registrazione). Le notifiche possono in genere attivare più azioni.

## <a name="alerts-in-different-azure-services"></a>Avvisi in diversi servizi di Azure
Gli avvisi sono disponibili in vari servizi di monitoraggio di Azure. Per informazioni su come e quando toouse questi servizi, [, vedere l'articolo](./monitoring-overview.md). Di seguito è disponibile un riepilogo dei tipi di avviso hello in Azure:

| Service | Tipo di avviso | Servizi supportati | Descrizione |
|---|---|---|---|
| Monitoraggio di Azure | [Avvisi delle metriche](./insights-alerts-portal.md) | [Metriche supportate con Monitoraggio di Azure](./monitoring-supported-metrics.md) | Ricevere una notifica quando le metriche a livello di piattaforma soddisfano una condizione specifica (ad esempio, % della CPU in una macchina virtuale è maggiore di 90 per hello negli ultimi 5 minuti). |
| Monitoraggio di Azure | [Avvisi del log attività](./monitoring-activity-log-alerts.md) | Tutti i tipi di risorse disponibili in Azure Resource Manager | Ricevere una notifica quando un nuovo evento nel hello [Log attività Azure](./monitoring-overview-activity-logs.md) corrisponde a condizioni specifiche (ad esempio, quando si verifica un'operazione di "Eliminare VM" in myProductionResourceGroup o quando un nuovo evento di integrità del servizio con "Attivo" come viene visualizzato lo stato di Hello). |
| Application Insights | [Avvisi metrica](../application-insights/app-insights-alerts.md) | Qualsiasi applicazione instrumentata toosend dati tooApplication Insights | Ricevere una notifica quando una metrica a livello di piattaforma soddisfa una condizione specifica (ad esempio, il tempo di risposta di un server è superiore a 2 secondi). |
| Application Insights | [Avvisi di test Web](../application-insights/app-insights-monitor-web-app-availability.md) | Qualsiasi sito Web instrumentato toosend dati tooApplication Insights | Ricevere una notifica quando la disponibilità o la velocità di risposta di un sito Web è inferiore alle aspettative. |
| Log Analytics | [Avvisi di Log Analytics](../log-analytics/log-analytics-alerts.md) | Qualsiasi servizio configurato toosend dati nel Log Analitica | Ricevere una notifica quando una query di ricerca di Log Analytics sui dati di metrica e/o evento soddisfa criteri specifici. |

## <a name="alerts-on-azure-monitor-data"></a>Avvisi sui dati di Monitoraggio di Azure
Sono disponibili due tipi di avvisi al di fuori dei dati disponibili da Monitoraggio di Azure: gli avvisi metrica e gli avvisi del log attività.

* **Metrici avvisi** -questo avviso viene generato in hello valore di una specifica metrica supera una soglia che è assegnato. avviso di Hello genera una notifica quando avviso hello è "attivato" (quando viene superata la soglia hello e viene raggiunta la condizione di avviso hello), nonché quando viene "risolto" (quando hello superate nuovamente e non viene più soddisfatta la condizione hello). Per un elenco in continua crescita delle metriche disponibili supportate dal monitoraggio di Azure, vedere [l'elenco delle metriche supportate in Monitoraggio di Azure](monitoring-supported-metrics.md).
* **Avvisi del log attività**: un avviso di log in streaming si attiva quando viene generato un evento di log attività che corrisponde ai criteri di filtro assegnati. Questi avvisi sono solo uno stato, "Attivato", poiché il motore degli avvisi hello applica semplicemente hello filtro criteri tooany nuovo evento. Questi avvisi possono essere utilizzati toobecome una notifica quando si verifica un nuovo evento imprevisto di integrità del servizio o quando un utente o un'applicazione esegue un'operazione nella sottoscrizione, ad esempio, "Eliminare la macchina virtuale".

Per i dati di Log di diagnostica disponibili tramite il monitoraggio di Azure, si consiglia di dati di routing hello in Log Analitica e l'utilizzo di un avviso di Log Analitica. Hello diagramma seguente sono riepilogate origini dei dati in Monitoraggio di Azure e, a livello concettuale, come è possibile avvisare di fuori di tali dati.

![Avvisi illustrati](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Come si riceve una notifica su un avviso di Monitoraggio di Azure?
Gli avvisi di Azure nelle versioni precedenti da servizi diversi usano metodi di notifica predefiniti propri. Monitoraggio di Azure offre ora un raggruppamento di notifiche riutilizzabili chiamato gruppi di azioni. Gruppi di azioni di specificano un set di destinatari per la notifica - qualsiasi numero di indirizzi di posta elettronica, i numeri di telefono (per SMS) o URL webhook - e ogni volta che viene attivato un avviso che riferimenti hello gruppo di azioni, tutti i ricevitori ricevono la notifica. In questo modo è un raggruppamento di ricevitori (ad esempio su chiamata engineer elenco) tooreuse tra molti oggetti avviso. Solo gli avvisi del log attività prevedono l'utilizzo di gruppi di azioni al momento, ma anche molti altri tipi di avviso di Azure useranno presto i gruppi di azioni.

Gruppi di azioni di supportano la notifica inviando l'URL del webhook tooa indirizzi tooemail aggiunta e i numeri SMS. Ciò consente l'automazione e la correzione, ad esempio, usando:
    - Runbook di Automazione di Azure
    - Funzione di Azure
    - App per la logica di Azure
    - un servizio di terze parti

Gli avvisi di metrica non usano ancora i gruppi di azioni. In un singolo avviso di metrica è possibile configurare le notifiche per:
* Invia messaggio di posta elettronica notifiche toohello servizio amministratore, gli amministratori di tooco o tooadditional indirizzi di posta elettronica specificato.
* Chiamare un webhook, che consente operazioni di automazione aggiuntivi toolaunch.

## <a name="next-steps"></a>Passaggi successivi
Ottenere informazioni sulle regole degli avvisi e sulla relativa configurazione usando:

* Altre informazioni sulle [metriche](monitoring-overview-metrics.md)
* Configurare gli [avvisi sulle metriche tramite il portale di Azure](insights-alerts-portal.md)
* Configurare gli [avvisi sulle metriche con PowerShell](insights-alerts-powershell.md)
* Configurare gli [avvisi sulle metriche tramite l'interfaccia della riga di comando](insights-alerts-command-line-interface.md)
* Configurare gli [avvisi sulle metriche tramite l'API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* Altre informazioni sul [log attività](monitoring-overview-activity-logs.md)
* Configurare [gli avvisi del log attività tramite il portale di Azure](monitoring-activity-log-alerts.md)
* Configurare [gli avvisi del log attività tramite Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Hello revisione [schema webhook avvisi del registro attività](monitoring-activity-log-alerts-webhook.md)
* Altre informazioni sulle [notifiche del servizio](monitoring-service-notifications.md)
* Altre informazioni sui [gruppi di azione](monitoring-action-groups.md)
