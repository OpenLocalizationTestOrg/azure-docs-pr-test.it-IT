---
title: gli schemi di rilevamento per B2B aaaCustom monitoraggio - App Azure per la logica | Documenti Microsoft
description: Creare gli schemi di rilevamento personalizzato messaggi B2B toomonitor dalle transazioni nell'Account di integrazione di Azure.
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>Abilitare il rilevamento toomonitor il flusso di lavoro completata, end-to-end
È disponibile un rilevamento predefinito che è possibile abilitare per diverse parti del flusso di lavoro Business to Business, ad esempio il rilevamento dei messaggi AS2 o X12. Quando si creano flussi di lavoro che include una logica di applicazione, BizTalk Server, SQL Server o qualsiasi altro livello, è possibile abilitare il rilevamento personalizzato che registra gli eventi dalla fine di toohello hello inizio del flusso di lavoro. 

In questo argomento fornisce codice personalizzato che è possibile utilizzare nei livelli di hello all'esterno dell'app logica. 

## <a name="custom-tracking-schema"></a>Schema di rilevamento personalizzato
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| sourceType |   | Tipo di origine eseguire hello. I valori consentiti sono **Microsoft.Logic/workflows** e **custom**. Obbligatoria |
| Sorgente |   | Se il tipo di origine hello **Microsoft.Logic/workflows**, necessita di informazioni di origine hello toofollow questo schema. Se il tipo di origine hello **personalizzato**, lo schema di hello è un JToken. Obbligatoria |
| systemId | String | ID di sistema dell'app per la logica. Obbligatoria |
| runId | String | ID di esecuzione dell'app per la logica. Obbligatoria |
| operationName | String | Nome dell'operazione di hello (ad esempio, azione o trigger). Obbligatoria |
| repeatItemScopeName | String | Ripetere il nome dell'elemento se hello azione all'interno di un `foreach` / `until` ciclo. Obbligatoria |
| repeatItemIndex | Integer | Se l'azione di hello è all'interno di un `foreach` / `until` ciclo. Indica l'indice dell'elemento ripetuto di hello. Obbligatoria |
| trackingId | String | ID di traccia, messaggi hello toocorrelate. Facoltativa |
| correlationId | String | ID di correlazione, messaggi hello toocorrelate. Facoltativa |
| clientRequestId | String | Client popolarlo toocorrelate messaggi. Facoltativa |
| eventLevel |   | Livello dell'evento hello. Obbligatoria |
| eventTime |   | Ora dell'evento hello, in formato UTC AAAA-MM-DDTHH:MM:SS.00000Z. Obbligatoria |
| recordType |   | Tipo di record di rilevamento hello. Il valore consentito è **custom**. Obbligatoria |
| record |   | Tipo di record personalizzato. Il formato consentito è JToken. Obbligatoria |

## <a name="b2b-protocol-tracking-schemas"></a>Schemi di rilevamento per il protocollo B2B
Per informazioni sugli schemi di rilevamento per il protocollo B2B, vedere:
* [Schemi di rilevamento AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [Schemi di rilevamento X12](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sul [monitoraggio dei messaggi B2B](logic-apps-monitor-b2b-message.md).   
* Informazioni su [rilevamento dei messaggi B2B nel portale di Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Altre informazioni su hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).
