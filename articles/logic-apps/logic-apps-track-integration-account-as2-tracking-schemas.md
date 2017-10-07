---
title: gli schemi di rilevamento aaaAS2 per il monitoraggio B2B - App Azure per la logica | Documenti Microsoft
description: Utilizzare AS2 rilevamento dei messaggi B2B toomonitor schemi dalle transazioni nell'Account di integrazione di Azure.
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>Avviare o abilitare il rilevamento di messaggi AS2 e MDN toomonitor successo, errori e le proprietà del messaggio
È possibile utilizzare questi schemi di rilevamento AS2 in toohelp di account l'integrazione di Azure è monitorare le transazioni di business-to-business (B2B):

* Schema di rilevamento messaggi AS2
* Schema di rilevamento MDN AS2

## <a name="as2-message-tracking-schema"></a>Schema di rilevamento messaggi AS2
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | String | Nome partner del mittente del messaggio AS2. Facoltativa |
| receiverPartnerName | String | Nome partner del destinatario del messaggio AS2. Facoltativa |
| as2To | String | Nome del destinatario del messaggio AS2, dalle intestazioni hello del messaggio AS2. Obbligatoria |
| as2From | String | Nome del mittente del messaggio AS2, dalle intestazioni hello del messaggio AS2. Obbligatoria |
| agreementName | String | Nome dei messaggi di hello toowhich contratto AS2 hello vengono risolti. Facoltativa |
| direction | String | Direzione del flusso di messaggi hello, ricezione o trasmissione. Obbligatoria |
| messageId | String | ID del messaggio AS2, dalle intestazioni hello del messaggio hello AS2 (facoltativo) |
| dispositionType |String | Valore del tipo di notifica sulla ricezione del messaggio (MDN). Facoltativa |
| fileName | String | Nome di file, dall'intestazione hello del messaggio AS2. Facoltativa |
| isMessageFailed |Boolean | Se il messaggio hello AS2 non è riuscita. Obbligatoria |
| isMessageSigned | Boolean | Se è stato firmato il messaggio hello AS2. Obbligatoria |
| isMessageEncrypted | Boolean | Indica se il messaggio hello AS2 è stato crittografato. Obbligatoria |
| isMessageCompressed |Boolean | Se è stata compressa messaggio hello AS2. Obbligatoria |
| correlationMessageId | String | ID del messaggio AS2, toocorrelate messaggi MDN. Facoltativa |
| incomingHeaders |Dizionario di JToken | Dettagli dell'intestazione del messaggio AS2 in arrivo. Facoltativa |
| outgoingHeaders |Dizionario di JToken | Dettagli dell'intestazione del messaggio AS2 in uscita. Facoltativa |
| isNrrEnabled | Boolean | Utilizzare il valore predefinito se non è noto il valore di hello. Obbligatoria |
| isMdnExpected | Boolean | Utilizzare il valore predefinito se non è noto il valore di hello. Obbligatoria |
| mdnType | Enum | I valori consentiti sono **NotConfigured**, **Sync** e **Async**. Obbligatoria |

## <a name="as2-mdn-tracking-schema"></a>Schema di rilevamento MDN AS2
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | String | Nome partner del mittente del messaggio AS2. Facoltativa |
| receiverPartnerName | String | Nome partner del destinatario del messaggio AS2. Facoltativa |
| as2To | String | Nome del partner che riceve il messaggio hello AS2. Obbligatoria |
| as2From | String | Nome del partner che invia il messaggio hello AS2. Obbligatoria |
| agreementName | String | Nome dei messaggi di hello toowhich contratto AS2 hello vengono risolti. Facoltativa |
| direction |String | Direzione del flusso di messaggi hello, ricezione o trasmissione. Obbligatoria |
| messageId | String | ID del messaggio AS2. Facoltativa |
| originalMessageId |String | ID del messaggio originale AS2. Facoltativa |
| dispositionType | String | Valore del tipo di gestione MDN. Facoltativa |
| isMessageFailed |Boolean | Se il messaggio hello AS2 non è riuscita. Obbligatoria |
| isMessageSigned |Boolean | Se è stato firmato il messaggio hello AS2. Obbligatoria |
| isNrrEnabled | Boolean | Utilizzare il valore predefinito se non è noto il valore di hello. Obbligatoria |
| statusCode | Enum | I valori consentiti sono **Accepted**, **Rejected** e **AcceptedWithErrors**. Obbligatoria |
| micVerificationStatus | Enum | I valori consentiti sono **NotApplicable**, **Succeeded** e **Failed**. Obbligatoria |
| correlationMessageId | String | ID correlazione. ID di messaggi Hello originale (ID del messaggio hello per cui è configurata il MDN hello). Facoltativa |
| incomingHeaders | Dizionario di JToken | Indica i dettagli dell'intestazione del messaggio in arrivo. Facoltativa |
| outgoingHeaders |Dizionario di JToken | Indica i dettagli dell'intestazione del messaggio in uscita. Facoltativa |

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).    
* Altre informazioni sul [monitoraggio dei messaggi B2B](logic-apps-monitor-b2b-message.md).   
* Altre informazioni sugli [schemi di rilevamento B2B personalizzati](logic-apps-track-integration-account-custom-tracking-schema.md).   
* Altre informazioni sugli [schemi di rilevamento X12](logic-apps-track-integration-account-x12-tracking-schema.md).   
* Informazioni su [rilevamento dei messaggi B2B nel portale di Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
