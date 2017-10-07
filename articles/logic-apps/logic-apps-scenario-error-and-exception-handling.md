---
title: aaaException Gestione & dello scenario di registrazione errore - App Azure per la logica | Documenti Microsoft
description: "Viene descritto un caso d'uso reale riguardo a modalità avanzate di gestione delle eccezioni e registrazione degli errori per le app per la logica di Azure"
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>Scenario: Gestione delle eccezioni e registrazione degli errori per le app per la logica

In questo scenario viene illustrato come estendere una logica app toobetter supporto delle eccezioni. È stata utilizzata una domanda di uso reale tooanswer case hello: "App per la logica di Azure supporta eccezione e la gestione degli errori?"

> [!NOTE]
> schema delle app di Azure logica corrente Hello fornisce un modello standard per le risposte di azione. che include le risposte per gli errori e la convalida interna restituite da un'app per le API.

## <a name="scenario-and-use-case-overview"></a>Panoramica su scenario e caso d'uso

Ecco storia hello come caso d'uso hello per questo scenario: 

Un'organizzazione sanitaria nota dovrà us toodevelop una soluzione di Azure che creerebbe un portale del paziente con Microsoft Dynamics CRM Online. Sono necessari i record di un appuntamento toosend tra portale paziente Dynamics CRM Online hello e Salesforce. Ci siamo richiesto hello toouse [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard per tutti i pazienti.

progetto Hello ha due requisiti principali:  

* Un record di toolog metodo inviati da hello portale Dynamics CRM Online
* Un modo tooview eventuali errori che si sono verificati all'interno del flusso di lavoro hello

> [!TIP]
> Per un video di alto livello su questo progetto, vedere [gruppo utente Integration](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "gruppo utente Integration").

## <a name="how-we-solved-hello-problem"></a>Come abbiamo risolto il problema di hello

Abbiamo scelto [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") come repository per i record di log e di errore hello (toorecords come documenti Cosmos DB fa riferimento). Poiché le app di logica di Azure dispone di un modello standard per tutte le risposte, non sono toocreate uno schema personalizzato. È stato possibile creare un'app per le API troppo**inserire** e **Query** per i record di errore e di log. È inoltre possibile definire uno schema per ognuna all'interno di app per le API hello.  

Un altro requisito è stato record toopurge dopo una certa data. COSMOS DB è una proprietà denominata [ora tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "ora tooLive") (TTL), che ha consentito tooset un **ora tooLive** valore per ogni record o una raccolta. Questa funzionalità eliminate hello necessità toomanually eliminare i record nel database Cosmos.

> [!IMPORTANT]
> toocomplete questa esercitazione, è necessario un database DB Cosmos toocreate e due raccolte (registrazione e gli errori).

## <a name="create-hello-logic-app"></a>Creare app per la logica hello

primo passaggio Hello è toocreate hello logica app e app hello aperto nella finestra di progettazione logica App. In questo esempio vengono usate app per la logica padre-figlio. Si supponga che è già stato creato il padre di hello e verranno toocreate uno figlio logica app.

Poiché verrà record hello toolog provengano da Dynamics CRM Online, iniziamo nella parte superiore di hello. È necessario utilizzare un **richiesta** trigger hello padre logica app attiva l'elemento figlio.

### <a name="logic-app-trigger"></a>Trigger dell'app per la logica

Si sta usando un **richiesta** trigger come illustrato nell'esempio seguente hello:

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a>Passi

È necessario eseguire l'accesso di origine hello (request) del record paziente hello dal portale di Dynamics CRM Online hello.

1. È necessario ottenere un nuovo record di appuntamento da Dynamics CRM Online.

   trigger Hello provenienti da CRM ci offre hello **CRM PatentId**, **tipo di record**, **nuovo o aggiornato Record** (nuovo o aggiornare un valore booleano), e  **SalesforceId**. Hello **SalesforceId** può essere null, poiché viene utilizzato solo per un aggiornamento.
   Record CRM hello si ottiene utilizzando hello CRM **PatientID** hello e **tipo di Record**.

2. È quindi necessario tooadd l'app per le API DocumentDB **InsertLogEntry** operazione, come illustrato di seguito in Progettazione applicazione logica.

   **Inserire una voce di log**

   ![Inserire una voce di log](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **Inserire una voce di log**

   ![Inserire una voce di log](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **Verificare la presenza di errori nella creazione di record**

   ![Condizione](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>Codice sorgente dell'app per la logica

> [!NOTE]
> seguono esempi Hello è solo gli esempi. Poiché in questa esercitazione si basa sull'implementazione di un'ora nell'ambiente di produzione, hello valore di un **nodo di origine** potrebbe non visualizzare le proprietà correlate tooscheduling un appuntamento. > 

### <a name="logging"></a>Registrazione

Hello seguendo la logica app codice di esempio viene illustrata la modalità registrazione toohandle.

#### <a name="log-entry"></a>Voce di log

Ecco il codice sorgente di hello logica app per l'inserimento di una voce di log.

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a>Richiesta di log

Di seguito è registrata l'app per le API toohello messaggio di richiesta di hello log.

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a>Risposta di log

Di seguito è hello log messaggio di risposta app hello per le API.

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

Ora esaminiamo i passaggi di gestione degli errori di hello.

### <a name="error-handling"></a>Gestione degli errori

Hello logica app esempio seguente viene illustrato come è possibile implementare la gestione degli errori.

#### <a name="create-error-record"></a>Creare record di errore

Ecco il codice sorgente di hello logica app per la creazione di un record di errore.

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a>Inserire l'errore in Cosmos DB: richiesta

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a>Inserire l'errore in Cosmos DB: risposta

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a>Risposta di errore di Salesforce

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a>Restituire hello risposta tooparent indietro logica app

Dopo avere ottenuto una risposta di hello, è possibile passare risposta hello toohello indietro padre logica app.

#### <a name="return-success-response-tooparent-logic-app"></a>App per la logica tooparent risposta restituito esito positivo

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a>Errore restituito risposta tooparent logica app

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a>Portale e repository di Cosmos DB

In questa soluzione sono state aggiunte funzionalità con [Cosmos DB](https://azure.microsoft.com/services/documentdb).

### <a name="error-management-portal"></a>Portale di gestione degli errori

errori di hello tooview, è possibile creare un record di errore MVC web app toodisplay hello da DB Cosmos. Hello **elenco**, **dettagli**, **modifica**, e **eliminare** sono incluse le operazioni nella versione corrente di hello.

> [!NOTE]
> Operazione di modifica: Cosmos DB sostituisce l'intero documento hello. Hello record visualizzati in hello **elenco** e **dettaglio** le visualizzazioni sono solo gli esempi. Non si tratta di record effettivi di appuntamenti dei pazienti.

Ecco alcuni esempi di applicazione MVC vengono descritti i dettagli creati in precedenza con hello approccio.

#### <a name="error-management-list"></a>Elenco di gestione degli errori
![Elenco errori](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>Visualizzazione dei dettagli di gestione degli errori
![Dettagli errore](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>Portale di gestione dei log

log hello tooview, è inoltre creata un'applicazione web MVC. Ecco alcuni esempi di applicazione MVC vengono descritti i dettagli creati in precedenza con hello approccio.

#### <a name="sample-log-detail-view"></a>Visualizzazione di dettagli dei log di esempio
![Visualizzare i dettagli dei log](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>Dettagli dell'app per le API

#### <a name="logic-apps-exception-management-api"></a>API di gestione delle eccezioni di app per la logica

L'app per le API di gestione delle eccezioni delle App per la logica di Azure offre le funzionalità descritte di seguito, sono presenti due controller:

* **ErrorController** inserisce un record di errore (documento) in una raccolta di DocumentDB.
* **LogController** inserisce un record di log (documento) in una raccolta di DocumentDB.

> [!TIP]
> Utilizzano entrambi i controller `async Task<dynamic>` operazioni, consentendo operazioni tooresolve in fase di esecuzione, affinché sia possibile creare hello schema DocumentDB nel corpo di hello dell'operazione di hello. 
> 

Ogni documento in DocumentDB deve avere un ID univoco. Si sta usando `PatientId` e l'aggiunta di timestamp tooa Unix timestamp valore convertito (double). Valore frazionario dei hello valore tooremove hello è troncato.

È possibile visualizzare il codice sorgente hello del nostro controller Errore API [da GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).

Viene chiamato hello API da un'app logica tramite hello la seguente sintassi:

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

espressione nel precedente esempio di codice cerca hello hello Hello *Create_NewPatientRecord* stato **Failed**.

## <a name="summary"></a>Riepilogo

* È possibile implementare facilmente la registrazione e la gestione degli errori in un'app per la logica.
* È possibile utilizzare DocumentDB come repository di hello per i record di log e di errore (documenti).
* È possibile utilizzare MVC toocreate un log toodisplay portale e i record degli errori.

### <a name="source-code"></a>Codice sorgente

è disponibile in questo codice di sorgente Hello per la gestione delle eccezioni App per la logica dell'applicazione API hello [repository GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API di gestione delle eccezioni di logica App").

## <a name="next-steps"></a>Passaggi successivi

* [Visualizzare altri esempi e scenari di app per la logica](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Informazioni sul monitoraggio delle app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Creare modelli di distribuzione automatizzati per le app per la logica](../logic-apps/logic-apps-create-deploy-template.md)
