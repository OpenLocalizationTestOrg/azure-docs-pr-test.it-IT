---
title: aaaAMQP 1.0 in operazioni basate su richiesta-risposta Service Bus di Azure | Documenti Microsoft
description: Elenco delle operazioni basate su richiesta/risposta del bus di servizio di Microsoft Azure.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>AMQP 1.0 nel bus di servizio di Microsoft Azure: operazioni basate su richiesta/risposta

In questo argomento definisce elenco hello di operazioni di Microsoft Azure Service Bus basata su richiesta/risposta. Queste informazioni si basano su bozza di lavoro hello AMQP gestione versione 1.0.  
  
Per una Guida, protocollo AMQP 1.0 a livello di trasmissione dettagliata che illustra il Bus di servizio implementa e si basa su hello specifiche tecniche OASIS AMQP, vedere hello [AMQP 1.0 in Azure Service Bus e hub di eventi Guida protocollo](service-bus-amqp-protocol-guide.md).  
  
## <a name="concepts"></a>Concetti  
  
### <a name="entity-description"></a>Descrizione di entità  

Una descrizione dell'entità fa riferimento a un Bus di servizio tooeither [classe QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription classe](/dotnet/api/microsoft.servicebus.messaging.topicdescription), o [SubscriptionDescription classe](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) oggetto.  
  
### <a name="brokered-message"></a>Messaggio negoziato  

Rappresenta un messaggio di Service Bus, ovvero messaggio AMQP mappato tooan. mapping di Hello è definito in hello [Guida protocollo AMQP Bus di servizio](service-bus-amqp-protocol-guide.md).  
  
## <a name="attach-tooentity-management-node"></a>Collegare il nodo di gestione tooentity  

Tutte le operazioni descritte in questo documento hello seguono un modello di richiesta/risposta, sono entità tooan con ambito e richiedono l'associazione tooan nodo di gestione di entità.  
  
### <a name="create-link-for-sending-requests"></a>Creare il collegamento per l'invio delle richieste  

Crea un nodo di gestione toohello collegamento per l'invio di richieste.  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>Creare il collegamento per la ricezione delle risposte  

Crea un collegamento per la ricezione di risposte da nodo di gestione di hello.  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>Trasferire un messaggio di richiesta  

Trasferisce un messaggio di richiesta.  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>Ricevere un messaggio di risposta  

Riceve il messaggio di risposta di hello dal collegamento di risposta hello.  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
messaggio di risposta Hello è in hello seguente formato:
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>Indirizzo delle entità del bus di servizio  

L'indirizzo delle entità del bus di servizio deve essere definito come segue:  
  
|Tipo di entità|Indirizzo|Esempio|  
|-----------------|-------------|-------------|  
|coda|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|argomento|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|sottoscrizione|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>Operazioni sui messaggi  
  
### <a name="message-renew-lock"></a>Rinnovo del blocco del messaggio  

Estende il blocco di hello di un messaggio hello ora specificata nella descrizione dell'entità hello.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
 corpo del messaggio Hello richiesta deve essere costituito da una sezione di valore amqp contenente una mappa con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|matrice di UUID|Sì|Toorenew token blocco di messaggio.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo.|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito da una sezione di valore amqp contenente una mappa con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|expirations|matrice di timestamp|Sì|Messaggio di blocco token nuova scadenza toohello richiesta blocco token corrispondenti.|  
  
### <a name="peek-message"></a>Visualizzazione del messaggio  

Visualizza i messaggi senza blocco.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|long|Sì|Numero di sequenza dalla quale leggere toostart.|  
|`message-count`|int|Sì|Numero massimo di messaggi toopeek.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) se sono presenti altri messaggi<br /><br /> 0xcc (nessun contenuto) se non sono presenti altri messaggi|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|del cloud al dispositivo|elenco di mapping|Sì|Elenco di messaggi in cui ogni mapping rappresenta un messaggio.|  
  
mapping di Hello che rappresenta un messaggio deve contenere hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|message|matrice di byte|Sì|Messaggio con codifica in transito AMQP 1.0.|  
  
### <a name="schedule-message"></a>Pianificazione del messaggio  

Pianifica i messaggi.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|del cloud al dispositivo|elenco di mapping|Sì|Elenco di messaggi in cui ogni mapping rappresenta un messaggio.|  
  
mapping di Hello che rappresenta un messaggio deve contenere hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|message-id|string|Sì|`amqpMessage.Properties.MessageId` in formato stringa|  
|session-id|string|Sì|`amqpMessage.Properties.GroupId as string`|  
|partition-key|string|Sì|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|message|matrice di byte|Sì|Messaggio con codifica in transito AMQP 1.0.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo.|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito un **valore amqp** sezione contenente una mappa con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|matrice di long|Sì|Numero di sequenza dei messaggi pianificati. Numero di sequenza è toocancel utilizzato.|  
  
### <a name="cancel-scheduled-message"></a>Annullamento del messaggio pianificato  

Annulla i messaggi pianificati.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|matrice di long|Sì|Numeri di sequenza dei messaggi pianificati toocancel.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo.|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito un **valore amqp** sezione contenente una mappa con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|matrice di long|Sì|Numero di sequenza dei messaggi pianificati. Numero di sequenza è toocancel utilizzato.|  
  
## <a name="session-operations"></a>Operazioni sulle sessioni  
  
### <a name="session-renew-lock"></a>Rinnovo del blocco della sessione  

Estende il blocco di hello di un messaggio hello ora specificata nella descrizione dell'entità hello.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sì|ID sessione.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) se sono presenti altri messaggi<br /><br /> 0xcc (nessun contenuto) se non sono presenti altri messaggi|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito un **valore amqp** sezione contenente una mappa con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|expiration|timestamp|Sì|Nuova scadenza.|  
  
### <a name="peek-session-message"></a>Visualizzazione del messaggio di sessione  

Visualizza i messaggi di sessione senza blocco.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|from-sequence-number|long|Sì|Numero di sequenza dalla quale leggere toostart.|  
|message-count|int|Sì|Numero massimo di messaggi toopeek.|  
|session-id|string|Sì|ID sessione.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) se sono presenti altri messaggi<br /><br /> 0xcc (nessun contenuto) se non sono presenti altri messaggi|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito un **valore amqp** sezione contenente una mappa con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|del cloud al dispositivo|elenco di mapping|Sì|Elenco di messaggi in cui ogni mapping rappresenta un messaggio.|  
  
 mapping di Hello che rappresenta un messaggio deve contenere hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|message|matrice di byte|Sì|Messaggio con codifica in transito AMQP 1.0.|  
  
### <a name="set-session-state"></a>Impostazione dello stato della sessione  

Set di hello lo stato di una sessione.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sì|ID sessione.|  
|session-state|matrice di byte|Sì|Dati binari opachi.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
### <a name="get-session-state"></a>Recupero dello stato della sessione  

Ottiene lo stato di hello di una sessione.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sì|ID sessione.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|session-state|matrice di byte|Sì|Dati binari opachi.|  
  
### <a name="enumerate-sessions"></a>Enumerazione delle sessioni  

Enumera le sessioni per un'entità di messaggistica.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|last-updated-time|timestamp|Sì|Filtrare le sessioni di tooinclude solo dopo un determinato momento.|  
|skip|int|Sì|Numero di sessioni da ignorare.|  
|top|int|Sì|Numero massimo di sessioni.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) se sono presenti altri messaggi<br /><br /> 0xcc (nessun contenuto) se non sono presenti altri messaggi|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|skip|int|Sì|Numero di sessioni ignorate se il codice di stato è 200.|  
|sessions-ids|matrice di stringhe|Sì|Matrice di ID sessione se il codice di stato è 200.|  
  
## <a name="rule-operations"></a>Operazioni sulle regole  
  
### <a name="add-rule"></a>Aggiunta di una regola  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|Sì|Nome della regola, senza nomi di sottoscrizione e argomento.|  
|rule-description|map|Sì|Descrizione della regola, come specificato nella sezione successiva.|  
  
Hello **-descrizione della regola** mappa deve includere hello seguenti voci, in cui **filtro sql** e **filtro di correlazione** si escludono a vicenda:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|sql-filter|map|Sì|`sql-filter`, come specificato nella sezione successiva hello.|  
|correlation-filter|map|Sì|`correlation-filter`, come specificato nella sezione successiva hello.|  
|sql-rule-action|map|Sì|`sql-rule-action`, come specificato nella sezione successiva hello.|  
  
mappa di filtro sql Hello deve includere hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|expression|string|Sì|Espressione di filtro SQL.|  
  
Hello **filtro di correlazione** mappa deve includere almeno una delle seguenti voci hello:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|correlation-id|string|No||  
|message-id|string|No||  
|to|string|No||  
|reply-to|string|No||  
|label|string|No||  
|session-id|string|No||  
|reply-to-session-id|string|No||  
|content-type|string|No||  
|properties|map|No|Esegue il mapping tooService Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).|  
  
Hello **azione di regola sql** mappa deve includere hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|expression|string|Sì|Espressione di azione SQL.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
### <a name="remove-rule"></a>Rimozione di una regola  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|Sì|Nome della regola, senza nomi di sottoscrizione e argomento.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
## <a name="deferred-message-operations"></a>Operazioni sui messaggi rinviati  
  
### <a name="receive-by-sequence-number"></a>Ricezione in base al numero di sequenza  

Riceve i messaggi rinviati in base al numero di sequenza.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|matrice di long|Sì|Numeri di sequenza.|  
|receiver-settle-mode|ubyte|Sì|Modalità di **finalizzazione del ricevitore**, come indicata nella specifica di base AMQP versione 1.0.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo|  
|statusDescription|string|No|Descrizione dello stato di hello.|  
  
corpo del messaggio di risposta Hello deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|del cloud al dispositivo|elenco di mapping|Sì|Elenco di messaggi in cui ogni mapping rappresenta un messaggio.|  
  
mapping di Hello che rappresenta un messaggio deve contenere hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|lock-token|uuid|Sì|Token di blocco se il valore di `receiver-settle-mode` è 1.|  
|message|matrice di byte|Sì|Messaggio con codifica in transito AMQP 1.0.|  
  
### <a name="update-disposition-status"></a>Aggiornamento dello stato di ricezione  

Aggiorna lo stato di disposizione hello dei messaggi posticipati.  
  
#### <a name="request"></a>Richiesta  

messaggio di richiesta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|operation|string|Sì|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|No|Timeout del server per l'operazione, in millisecondi.|  
  
corpo del messaggio Hello richiesta deve essere costituito un **valore amqp** sezione contenente un **mappa** con hello seguenti voci:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|disposition-status|string|Sì|completed<br /><br /> abandoned<br /><br /> suspended|  
|lock-tokens|matrice di UUID|Sì|Lo stato di disposizione tooupdate i token del blocco del messaggio.|  
|deadletter-reason|string|No|Può essere impostato se lo stato di disposizione è troppo**sospeso**.|  
|deadletter-description|string|No|Può essere impostato se lo stato di disposizione è troppo**sospeso**.|  
|properties-to-modify|map|No|Elenco di Service Bus negoziata toomodify proprietà messaggio.|  
  
#### <a name="response"></a>Response  

messaggio di risposta Hello deve includere hello le proprietà delle applicazioni seguenti:  
  
|Chiave|Tipo di valore|Obbligatorio|Contenuti del valore|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sì|Codice di risposta HTTP [RFC2616]<br /><br /> 200 (OK) in caso di esito positivo, altro valore in caso di esito negativo|  
|statusDescription|string|No|Descrizione dello stato di hello.|

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su AMQP e Bus di servizio, visitare hello seguenti collegamenti:

* [Panoramica di AMQP per il bus di servizio]
* [Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio]
* [AMQP nel bus di servizio per Windows Server]

[Panoramica di AMQP per il bus di servizio]: service-bus-amqp-overview.md
[Supporto di AMQP 1.0 per code e argomenti partizionati del bus di servizio]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP nel bus di servizio per Windows Server]: https://msdn.microsoft.com/library/dn574799.asp