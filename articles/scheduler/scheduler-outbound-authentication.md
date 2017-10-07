---
title: aaaScheduler autenticazione in uscita
description: "Autenticazione in uscita dell'Utilità di pianificazione"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a>Autenticazione in uscita dell'Utilità di pianificazione
I processi dell'utilità di pianificazione potrebbe essere necessario toocall out tooservices che richiedono l'autenticazione. In questo modo, un servizio chiamato può determinare se il processo di pianificazione hello può accedere alle risorse. Alcuni di questi servizi includono altri servizi di Azure, Salesforce.com, Facebook e siti Web custom protetti.

## <a name="adding-and-removing-authentication"></a>Aggiunta e rimozione di autenticazione
Aggiunta di autenticazione tooa dell'utilità di pianificazione è semplice: aggiungere un elemento figlio JSON `authentication` toohello `request` elemento durante la creazione o l'aggiornamento del processo. I segreti passati servizio Utilità di pianificazione toohello in una richiesta PUT, PATCH o POST-come parte di hello `authentication` oggetto: non vengono mai restituiti nelle risposte. Nelle risposte, le informazioni segrete sono impostate toonull o potrebbero essere un token pubblico che rappresenta l'entità hello autenticato.

autenticazione tooremove, PUT o PATCH in modo esplicito, il processo di hello impostazione hello `authentication` toonull dell'oggetto. Nessuna proprietà di autenticazione verrà visualizzata nella risposta.

Hello supportato solo tipi di autenticazione sono attualmente hello `ClientCertificate` modello (per l'utilizzo di certificati client SSL/TLS di hello), hello `Basic` del modello (per l'autenticazione di base) e hello `ActiveDirectoryOAuth` modello (per OAuth di Active Directory autenticazione).

## <a name="request-body-for-clientcertificate-authentication"></a>Corpo della richiesta per l'autenticazione ClientCertificate
Quando si aggiunge l'autenticazione utilizzando hello `ClientCertificate` del modello, specificare i seguenti elementi aggiuntivi nel corpo della richiesta hello hello.  

| Elemento | Descrizione |
|:--- |:--- |
| *authentication (elemento padre)* |Oggetto di autenticazione per l'utilizzo di un certificato client SSL. |
| *type* |Obbligatorio. Tipo di autenticazione. Per i certificati client SSL, deve essere il valore di hello `ClientCertificate`. |
| *pfx* |Obbligatorio. Contenuto con codifica Base64 del file PFX hello. |
| *password* |Obbligatorio. File PFX hello tooaccess delle password. |

## <a name="response-body-for-clientcertificate-authentication"></a>Corpo della risposta per l'autenticazione ClientCertificate
Quando viene inviata una richiesta con informazioni di autenticazione, risposta hello contiene hello segue gli elementi correlati all'autenticazione.

| Elemento | Descrizione |
|:--- |:--- |
| *authentication (elemento padre)* |Oggetto di autenticazione per l'utilizzo di un certificato client SSL. |
| *type* |Tipo di autenticazione. Per i certificati client SSL, il valore di hello è `ClientCertificate`. |
| *certificateThumbprint* |identificazione personale Hello del certificato hello. |
| *certificateSubjectName* |Hello nome distinto del soggetto del certificato hello. |
| *certificateExpiration* |Data di scadenza Hello del certificato hello. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>Richiesta REST di esempio per l'autenticazione ClientCertificate
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>Risposta REST di esempio per l'autenticazione ClientCertificate
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a>Corpo della richiesta per l'autenticazione di Base
Quando si aggiunge l'autenticazione utilizzando hello `Basic` del modello, specificare i seguenti elementi aggiuntivi nel corpo della richiesta hello hello.

| Elemento | Descrizione |
|:--- |:--- |
| *authentication (elemento padre)* |Oggetto di autenticazione per l’utilizzo dell'autenticazione di Base. |
| *type* |Obbligatorio. Tipo di autenticazione. L'autenticazione di base, deve essere il valore di hello `Basic`. |
| *username* |Obbligatorio. Nome utente tooauthenticate. |
| *password* |Obbligatorio. Tooauthenticate password. |

## <a name="response-body-for-basic-authentication"></a>Corpo della risposta per l'autenticazione di Base
Quando viene inviata una richiesta con informazioni di autenticazione, risposta hello contiene hello segue gli elementi correlati all'autenticazione.

| Elemento | Descrizione |
|:--- |:--- |
| *authentication (elemento padre)* |Oggetto di autenticazione per l’utilizzo dell'autenticazione di Base. |
| *type* |Tipo di autenticazione. L'autenticazione di base, il valore di hello è `Basic`. |
| *username* |Hello autenticazione nome utente. |

## <a name="sample-rest-request-for-basic-authentication"></a>Richiesta REST di esempio per l'autenticazione di base
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a>Risposta REST di esempio per l'autenticazione di base
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a>Corpo della richiesta per l'autenticazione ActiveDirectoryOAuth
Quando si aggiunge l'autenticazione utilizzando hello `ActiveDirectoryOAuth` del modello, specificare i seguenti elementi aggiuntivi nel corpo della richiesta hello hello.

| Elemento | Descrizione |
|:--- |:--- |
| *authentication (elemento padre)* |Oggetto di autenticazione per l'autenticazione basata su ActiveDirectoryOAuth. |
| *type* |Obbligatorio. Tipo di autenticazione. Per l'autenticazione ActiveDirectoryOAuth, il valore di hello deve essere `ActiveDirectoryOAuth`. |
| *tenant* |Obbligatorio. Identificatore del tenant Hello per tenant hello Azure AD. |
| *audience* |Obbligatorio. Toohttps://management.core.windows.net/ è impostato. |
| *clientId* |Obbligatorio. Fornire l'identificatore hello del client per hello applicazione Azure AD. |
| *secret* |Obbligatorio. Segreto del client hello che sta richiedendo hello token. |

### <a name="determining-your-tenant-identifier"></a>Determinazione del l'identificatore del tenant
È possibile trovare l'identificatore del tenant per il tenant di Azure AD hello hello eseguendo `Get-AzureAccount` in Azure PowerShell.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>Corpo della risposta per l'autenticazione ActiveDirectoryOAuth
Quando viene inviata una richiesta con informazioni di autenticazione, risposta hello contiene hello segue gli elementi correlati all'autenticazione.

| Elemento | Descrizione |
|:--- |:--- |
| *authentication (elemento padre)* |Oggetto di autenticazione per l'autenticazione basata su ActiveDirectoryOAuth. |
| *type* |Tipo di autenticazione. Per l'autenticazione ActiveDirectoryOAuth, il valore di hello è `ActiveDirectoryOAuth`. |
| *tenant* |Identificatore del tenant Hello per tenant hello Azure AD. |
| *audience* |Toohttps://management.core.windows.net/ è impostato. |
| *clientId* |Hello identificatore client per un'applicazione hello Azure AD. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>Richiesta REST di esempio per l'autenticazione ActiveDirectoryOAuth
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>Risposta REST di esempio per l'autenticazione ActiveDirectoryOAuth
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a>Vedere anche
 [Che cos'è l'Utilità di pianificazione?](scheduler-intro.md)

 [Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure](scheduler-concepts-terms.md)

 [Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello](scheduler-get-started-portal.md)

 [Piani e fatturazione nell'utilità di pianificazione di Azure](scheduler-plans-billing.md)

 [Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure](scheduler-powershell-reference.md)

 [Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure](scheduler-high-availability-reliability.md)

 [Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure](scheduler-limits-defaults-errors.md)

