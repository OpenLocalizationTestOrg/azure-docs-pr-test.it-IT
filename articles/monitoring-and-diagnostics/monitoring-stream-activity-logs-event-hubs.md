---
title: "aaaStream hello Log attività Azure tooEvent hub | Documenti Microsoft"
description: "Informazioni su come toostream hello tooEvent Log attività Azure hub."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Flusso hello Log attività Azure tooEvent hub
Hello [ **Log attività Azure** ](monitoring-overview-activity-logs.md) può essere trasmesso quasi in tempo reale tooany applicazione tramite l'opzione "Esporta" incorporato hello nel portale di hello o abilitando hello Id regola Bus di servizio in un profilo di Log tramite hello Cmdlet di Azure PowerShell o Azure CLI.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>Operazioni eseguibili con hello Log attività e gli hub di eventi
Ecco alcune modalità è possibile utilizzare hello funzionalità per hello Log attività di streaming:

* **Sistemi di registrazione e telemetria toothird parti del flusso** – nel tempo, gli hub di eventi di flusso diventeranno hello meccanismo toopipe il Log di attività in Siem di terze parti e soluzioni analitica di log.
* **Compilare una piattaforma di registrazione e i dati di telemetria personalizzati** : se si dispone già di una piattaforma dati di telemetria personalizzati o sono solo le compilazione uno, hello altamente scalabile di pubblicazione-sottoscrizione natura degli hub di eventi consente tooflexibly inserimento hello registro attività. [Vedere toousing di Guida di Dan Rosanova hub eventi in una piattaforma di dati di telemetria di su scala globale.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Abilitare lo streaming di hello Log attività
È possibile abilitare lo streaming di hello Log attività a livello di codice o tramite il portale di hello. In entrambi i casi, si sceglie un Namespace Bus di servizio e un criterio di accesso condiviso per tale spazio dei nomi e un Hub eventi viene creato nello spazio dei nomi quando si verifica hello primo nuovo evento di registro attività. Se non si dispone di un Namespace Bus di servizio, è necessario innanzitutto toocreate uno. Se si hanno in precedenza di flusso attività Log eventi toothis Service Bus Namespace, verrà riutilizzata hello Hub di eventi che è stato creato in precedenza. i criteri di accesso condiviso Hello definiscono hello autorizzazioni meccanismo streaming hello. Oggi, streaming hub eventi tooan richiede **Gestisci**, **inviare**, e **ascolto** autorizzazioni. È possibile creare o modificare i criteri di accesso condiviso di Service Bus Namespace nel portale classico di hello nella scheda "Configurazione" hello per le Namespace Bus di servizio. tooupdate hello Log attività log profilo tooinclude streaming, l'utente hello modifica hello deve disporre dell'autorizzazione ListKey hello tale regola di autorizzazione del Bus di servizio.

Hello service bus o evento hub dello spazio dei nomi non presenti toobe hello stessa sottoscrizione come sottoscrizione hello la creazione di log come utente di hello che configura l'impostazione di hello dispone di sottoscrizioni di tooboth accesso RBAC appropriate.

### <a name="via-azure-portal"></a>Tramite il portale di Azure
1. Passare toohello **Log attività** pannello utilizzando il menu di hello hello il lato sinistro di portale hello.
   
    ![Passare tooActivity Log nel portale](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Fare clic su hello **esportare** pulsante nella parte superiore di hello del pannello hello.
   
    ![Pulsante Esporta nel portale](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Nel pannello hello che viene visualizzata, è possibile selezionare le aree di hello per il quale si desidera toostream eventi e hello Service Bus Namespace nel quale si desidera toobe un Hub eventi creato per lo streaming di questi eventi.
   
    ![Pannello Esporta log di controllo](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Fare clic su **salvare** toosave queste impostazioni. le impostazioni di Hello sono immediatamente di essere applicati tooyour sottoscrizione.

### <a name="via-powershell-cmdlets"></a>Tramite i cmdlet di PowerShell
Se esiste già un profilo di log, è necessario innanzitutto tooremove tale profilo.

1. Utilizzare `Get-AzureRmLogProfile` tooidentify se esiste un profilo di log
2. In questo caso, utilizzare `Remove-AzureRmLogProfile` tooremove è.
3. Utilizzare `Set-AzureRmLogProfile` toocreate un profilo:

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

Hello ID regola Bus di servizio è una stringa con questo formato: {ID risorsa bus di servizio} /authorizationrules/ {nome}, ad esempio 

### <a name="via-azure-cli"></a>Tramite l'interfaccia della riga di comando di Azure
Se esiste già un profilo di log, è necessario innanzitutto tooremove tale profilo.

1. Utilizzare `azure insights logprofile list` tooidentify se esiste un profilo di log
2. In questo caso, utilizzare `azure insights logprofile delete` tooremove è.
3. Utilizzare `azure insights logprofile add` toocreate un profilo:

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

Hello ID regola Bus di servizio è una stringa con questo formato: `{service bus resource ID}/authorizationrules/{key name}`.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Come utilizzano i dati del log hello dagli hub eventi?
[schema di Hello per hello Log attività è disponibile qui](monitoring-overview-activity-logs.md). Ogni evento si trova in una matrice di BLOB JSON denominati "record".

## <a name="next-steps"></a>Passaggi successivi
* [Hello archivio account di archiviazione tooa Log attività](monitoring-archive-activity-log.md)
* [Panoramica di hello di hello Log attività di Azure](monitoring-overview-activity-logs.md)
* [Set up an alert based on an Activity Log event](insights-auditlog-to-webhook-email.md) (Configurare un avviso in base a un evento del log attività)

