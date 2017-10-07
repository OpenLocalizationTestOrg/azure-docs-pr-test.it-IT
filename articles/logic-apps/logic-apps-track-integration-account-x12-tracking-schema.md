---
title: gli schemi di rilevamento aaaX12 per il monitoraggio B2B - App Azure per la logica | Documenti Microsoft
description: Utilizzare X12 rilevamento dei messaggi B2B toomonitor schemi dalle transazioni nell'Account di integrazione di Azure.
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>Inizio o abilitare il rilevamento di X12 messaggi toomonitor successo, errori e le proprietà del messaggio
È possibile utilizzare questi schemi di rilevamento X12 in toohelp di account l'integrazione di Azure è monitorare le transazioni di business-to-business (B2B):

* Schema di rilevamento X12 per set di transazioni
* Schema di rilevamento X12 per acknowledgement di set di transazioni
* Schema di rilevamento X12 per interscambio
* Schema di rilevamento X12 per acknowledgement di interscambio
* Schema di rilevamento X12 per gruppi funzionali
* Schema di rilevamento X12 per acknowledgement di gruppi funzionali

## <a name="x12-transaction-set-tracking-schema"></a>Schema di rilevamento X12 per set di transazioni
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | String | Nome partner del mittente del messaggio X12. (Facoltativa) |
| receiverPartnerName | String | Nome partner del destinatario del messaggio X12. (Facoltativa) |
| senderQualifier | string | Invia il qualificatore del partner. (Obbligatoria) |
| senderIdentifier | String | Invia l'identificatore del partner. (Obbligatoria) |
| receiverQualifier | String | Riceve il qualificatore del partner. (Obbligatoria) |
| receiverIdentifier | string | Riceve l'identificatore del partner. (Obbligatoria) |
| agreementName | String | Nome di messaggi hello toowhich di accordo X12 hello vengono risolti. Facoltativa |
| direction | Enum | Direzione del flusso di messaggi hello, ricezione o trasmissione. Obbligatoria |
| interchangeControlNumber | String | Numero di controllo interscambio. (Facoltativa) |
| functionalGroupControlNumber | String | Numero di controllo funzionale. (Facoltativa) |
| transactionSetControlNumber | String | Numero di controllo set transazioni. (Facoltativa) |
| CorrelationMessageId | String | ID messaggio di correlazione. Una combinazione di {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}. (Facoltativa) |
| messageType | string | Set di transazioni o tipo di documento. (Facoltativa) |
| isMessageFailed | Boolean | Se il messaggio hello X12 non è riuscita. Obbligatoria |
| isTechnicalAcknowledgmentExpected | Boolean | Riconoscimento tecnico hello se è configurato nel contratto X12 hello. Obbligatoria |
| isFunctionalAcknowledgmentExpected | Boolean | Riconoscimento funzionale hello se è configurato nel contratto X12 hello. Obbligatoria |
| needAk2LoopForValidMessages | Boolean | Indica se il ciclo AK2 hello è obbligatorio per un messaggio valido. Obbligatoria |
| segmentsCount | Integer | Numero di segmenti nel set di transazioni X12 hello. Facoltativa |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>Schema di rilevamento X12 per acknowledgement di set di transazioni
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | String | Nome partner del mittente del messaggio X12. (Facoltativa) |
| receiverPartnerName | String | Nome partner del destinatario del messaggio X12. (Facoltativa) |
| senderQualifier | string | Invia il qualificatore del partner. (Obbligatoria) |
| senderIdentifier | String | Invia l'identificatore del partner. (Obbligatoria) |
| receiverQualifier | String | Riceve il qualificatore del partner. (Obbligatoria) |
| receiverIdentifier | string | Riceve l'identificatore del partner. (Obbligatoria) |
| agreementName | String | Nome di messaggi hello toowhich di accordo X12 hello vengono risolti. Facoltativa |
| direction | Enum | Direzione del flusso di messaggi hello, ricezione o trasmissione. Obbligatoria |
| interchangeControlNumber | String | Numero di controllo di riconoscimento funzionale hello interscambio. Valore popola solo per il lato di trasmissione hello in cui è stata ricevuta riconoscimento funzionale per hello toopartner di messaggi inviati. Facoltativa |
| functionalGroupControlNumber | String | Numero di controllo gruppo funzionale di riconoscimento funzionale hello. Valore popola solo per il lato di trasmissione hello in cui è stata ricevuta riconoscimento funzionale per hello toopartner di messaggi inviati. Facoltativa |
| isaSegment | String | Segmento ISA di messaggio hello. Valore popola solo per il lato di trasmissione hello in cui è stata ricevuta riconoscimento funzionale per hello toopartner di messaggi inviati. Facoltativa |
| gsSegment | String | Segmento GS di messaggio hello. Valore popola solo per il lato di trasmissione hello in cui è stata ricevuta riconoscimento funzionale per hello toopartner di messaggi inviati. Facoltativa |
| respondingfunctionalGroupControlNumber | String | Numero di controllo interscambio di risposta. (Facoltativa) |
| respondingFunctionalGroupId | String | Blocca l'ID gruppo funzionale, che esegue il mapping di tooAK101 nel riconoscimento hello. Facoltativa |
| respondingtransactionSetControlNumber | String | Numero di controllo set transazioni di risposta. (Facoltativa) |
| respondingTransactionSetId | String | ID, che esegue il mapping tooAK201 nel riconoscimento hello del set di transazioni risponde. Facoltativa |
| statusCode | Boolean | Codice di stato dell'acknowledgement del set di transazioni. (Obbligatoria) |
| segmentsCount | Enum | Codice di stato dell'acknowledgement. I valori consentiti sono **Accepted**, **Rejected** e **AcceptedWithErrors**. (Obbligatoria) |
| processingStatus | Enum | Stato di elaborazione di acknowledgement hello. I valori consentiti sono **Received**, **Generated** e **Sent**. (Obbligatoria) |
| CorrelationMessageId | String | ID messaggio di correlazione. Una combinazione di {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}. (Facoltativa) |
| isMessageFailed | Boolean | Se il messaggio hello X12 non è riuscita. Obbligatoria |
| ak2Segment | String | Accettazione di un set di transazioni all'interno di hello ricevuto gruppo funzionale. Facoltativa |
| ak3Segment | String | Segnala gli errori in un segmento di dati. (Facoltativa) |
| ak5Segment | String | Segnala se hello set di transazioni identificato nel segmento hello AK2 sono accettata o rifiutata e il motivo. Facoltativa |

## <a name="x12-interchange-tracking-schema"></a>Schema di rilevamento X12 per interscambio
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | String | Nome partner del mittente del messaggio X12. (Facoltativa) |
| receiverPartnerName | String | Nome partner del destinatario del messaggio X12. (Facoltativa) |
| senderQualifier | string | Invia il qualificatore del partner. (Obbligatoria) |
| senderIdentifier | String | Invia l'identificatore del partner. (Obbligatoria) |
| receiverQualifier | String | Riceve il qualificatore del partner. (Obbligatoria) |
| receiverIdentifier | string | Riceve l'identificatore del partner. (Obbligatoria) |
| agreementName | String | Nome di messaggi hello toowhich di accordo X12 hello vengono risolti. Facoltativa |
| direction | Enum | Direzione del flusso di messaggi hello, ricezione o trasmissione. Obbligatoria |
| interchangeControlNumber | String | Numero di controllo interscambio. (Facoltativa) |
| isaSegment | String | Segmento ISA del messaggio. (Facoltativa) |
| isTechnicalAcknowledgmentExpected | Boolean | Riconoscimento tecnico hello se è configurato nel contratto X12 hello. Obbligatoria |
| isMessageFailed | Boolean | Se il messaggio hello X12 non è riuscita. Obbligatoria |
| isa09 | string | Data di interscambio del documento X12. (Facoltativa) |
| isa10 | String | Ora di interscambio del documento X12. (Facoltativa) |
| isa11 | String | Identificatore standard del controllo di interscambio X12. (Facoltativa) |
| isa12 | string | Numero di versione del controllo di interscambio X12. (Facoltativa) |
| isa14 | string | È necessario l'acknowledgement X12. (Facoltativa) |
| isa15 | string | Indicatore per test o produzione. (Facoltativa) |
| isa16 | string | Separatore elementi. (Facoltativa) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>Schema di rilevamento X12 per acknowledgement di interscambio
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | String | Nome partner del mittente del messaggio X12. (Facoltativa) |
| receiverPartnerName | String | Nome partner del destinatario del messaggio X12. (Facoltativa) |
| senderQualifier | string | Invia il qualificatore del partner. (Obbligatoria) |
| senderIdentifier | String | Invia l'identificatore del partner. (Obbligatoria) |
| receiverQualifier | String | Riceve il qualificatore del partner. (Obbligatoria) |
| receiverIdentifier | string | Riceve l'identificatore del partner. (Obbligatoria) |
| agreementName | String | Nome di messaggi hello toowhich di accordo X12 hello vengono risolti. Facoltativa |
| direction | Enum | Direzione del flusso di messaggi hello, ricezione o trasmissione. Obbligatoria |
| interchangeControlNumber | String | Numero di controllo di riconoscimento tecnico hello ricevuti dal partner di interscambio. Facoltativa |
| isaSegment | String | Segmento ISA per riconoscimento tecnico hello ricevuti dal partner. Facoltativa |
| respondingInterchangeControlNumber |String | Numero di controllo di riconoscimento tecnico hello ricevuti dal partner di interscambio. Facoltativa |
| isMessageFailed | Boolean | Se il messaggio hello X12 non è riuscita. Obbligatoria |
| statusCode | Enum | Codice di stato dell'acknowledgement di interscambio. I valori consentiti sono **Accepted**, **Rejected** e **AcceptedWithErrors**. (Obbligatoria) |
| processingStatus | Enum | Stato dell'acknowledgement. I valori consentiti sono **Received**, **Generated** e **Sent**. (Obbligatoria) |
| ta102 | string | Data di interscambio. (Facoltativa) |
| ta103 | String | Ora di interscambio. (Facoltativa) |
| ta105 | string | Codice della nota di interscambio. (Facoltativa) |

## <a name="x12-functional-group-tracking-schema"></a>Schema di rilevamento X12 per gruppi funzionali
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | String | Nome partner del mittente del messaggio X12. (Facoltativa) |
| receiverPartnerName | String | Nome partner del destinatario del messaggio X12. (Facoltativa) |
| senderQualifier | string | Invia il qualificatore del partner. (Obbligatoria) |
| senderIdentifier | String | Invia l'identificatore del partner. (Obbligatoria) |
| receiverQualifier | String | Riceve il qualificatore del partner. (Obbligatoria) |
| receiverIdentifier | string | Riceve l'identificatore del partner. (Obbligatoria) |
| agreementName | String | Nome di messaggi hello toowhich di accordo X12 hello vengono risolti. Facoltativa |
| direction | Enum | Direzione del flusso di messaggi hello, ricezione o trasmissione. Obbligatoria |
| interchangeControlNumber | String | Numero di controllo interscambio. (Facoltativa) |
| functionalGroupControlNumber | String | Numero di controllo funzionale. (Facoltativa) |
| gsSegment | String | Segmento GS del messaggio. (Facoltativa) |
| isTechnicalAcknowledgmentExpected | Boolean | Riconoscimento tecnico hello se è configurato nel contratto X12 hello. Obbligatoria |
| isFunctionalAcknowledgmentExpected | Boolean | Riconoscimento funzionale hello se è configurato nel contratto X12 hello. Obbligatoria |
| isMessageFailed | Boolean | Se il messaggio hello X12 non è riuscita. Obbligatoria|
| gs01 | String | Codice identificatore funzionale. (Facoltativa) |
| gs02 | String | Codice del mittente dell'applicazione. (Facoltativa) |
| gs03 | String | Codice del ricevitore dell'applicazione. (Facoltativa) |
| gs04 | String | Data del gruppo funzionale. (Facoltativa) |
| gs05 | string | Ora del gruppo funzionale. (Facoltativa) |
| gs07 | string | Codice agenzia responsabile. (Facoltativa) |
| gs08 | String | Codice identificatore versione/rilascio/settore. (Facoltativa) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>Schema di rilevamento X12 per acknowledgement di gruppi funzionali
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | String | Nome partner del mittente del messaggio X12. (Facoltativa) |
| receiverPartnerName | String | Nome partner del destinatario del messaggio X12. (Facoltativa) |
| senderQualifier | string | Invia il qualificatore del partner. (Obbligatoria) |
| senderIdentifier | String | Invia l'identificatore del partner. (Obbligatoria) |
| receiverQualifier | String | Riceve il qualificatore del partner. (Obbligatoria) |
| receiverIdentifier | string | Riceve l'identificatore del partner. (Obbligatoria) |
| agreementName | String | Nome di messaggi hello toowhich di accordo X12 hello vengono risolti. Facoltativa |
| direction | Enum | Direzione del flusso di messaggi hello, ricezione o trasmissione. Obbligatoria |
| interchangeControlNumber | String | Numero di controllo interscambio popola per hello lato di trasmissione quando viene ricevuto un riconoscimento tecnico dai partner. Facoltativa |
| functionalGroupControlNumber | String | Numero di controllo gruppo funzionale di riconoscimento tecnico hello, che popola per hello lato di trasmissione quando viene ricevuto un riconoscimento tecnico dai partner. Facoltativa |
| isaSegment | String | Come il numero di controllo interscambio, ma viene popolato solo in casi specifici. (Facoltativa) |
| gsSegment | String | Come il numero di controllo gruppo funzionale, ma viene popolato solo in casi specifici. (Facoltativa) |
| respondingfunctionalGroupControlNumber | String | Numero di controllo di gruppo funzionale originale hello. Facoltativa |
| respondingFunctionalGroupId | String | Esegue il mapping tooAK101 in hello riconoscimento funzionale ID del gruppo. Facoltativa |
| isMessageFailed | Boolean | Se il messaggio hello X12 non è riuscita. Obbligatoria |
| statusCode | Enum | Codice di stato dell'acknowledgement. I valori consentiti sono **Accepted**, **Rejected** e **AcceptedWithErrors**. (Obbligatoria) |
| processingStatus | Enum | Stato di elaborazione di acknowledgement hello. I valori consentiti sono **Received**, **Generated** e **Sent**. (Obbligatoria) |
| ak903 | string | Numero di set transazioni ricevuti. (Facoltativa) |
| ak904 | String | Numero di set di transazioni accettati nel gruppo funzionale identificato hello. Facoltativa |
| ak9Segment | String | Se il gruppo funzionale hello identificato nel segmento hello AK1 è accettato o rifiutato e perché. Facoltativa |

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sul [monitoraggio dei messaggi B2B](logic-apps-monitor-b2b-message.md).
* Altre informazioni sugli [schemi di rilevamento AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md).
* Altre informazioni sugli [schemi di rilevamento B2B personalizzati](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md).
* Informazioni su [rilevamento dei messaggi B2B nel portale di Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Altre informazioni su hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).  
