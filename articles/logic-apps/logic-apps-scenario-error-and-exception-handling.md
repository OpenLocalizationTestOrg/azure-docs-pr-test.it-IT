---
title: Scenario di gestione delle eccezioni e registrazione degli errori - App per la logica di Azure | Microsoft Docs
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
ms.openlocfilehash: 044de27c75da93c95609110d2b73336c42f746fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="321b0-103">Scenario: Gestione delle eccezioni e registrazione degli errori per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="321b0-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="321b0-104">Questo scenario descrive come è possibile estendere un'app per la logica per supportare al meglio la gestione delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="321b0-104">This scenario describes how you can extend a logic app to better support exception handling.</span></span> <span data-ttu-id="321b0-105">Si tratta di un caso d'uso reale che risponde alla domanda "Le app per la logica di Azure supportano la gestione di errori ed eccezioni?".</span><span class="sxs-lookup"><span data-stu-id="321b0-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="321b0-106">Lo schema corrente delle app per la logica di Azure offre un modello standard per le risposte alle azioni,</span><span class="sxs-lookup"><span data-stu-id="321b0-106">The current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="321b0-107">che include le risposte per gli errori e la convalida interna restituite da un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="321b0-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="321b0-108">Panoramica su scenario e caso d'uso</span><span class="sxs-lookup"><span data-stu-id="321b0-108">Scenario and use case overview</span></span>

<span data-ttu-id="321b0-109">Questa è la storia riportata nel caso d'uso per lo scenario:</span><span class="sxs-lookup"><span data-stu-id="321b0-109">Here's the story as the use case for this scenario:</span></span> 

<span data-ttu-id="321b0-110">Una nota organizzazione sanitaria ha richiesto lo sviluppo di una soluzione di Azure per creare un portale per i pazienti con Microsoft Dynamics CRM Online,</span><span class="sxs-lookup"><span data-stu-id="321b0-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="321b0-111">con invio dei record degli appuntamenti tra il portale per i pazienti Dynamics CRM Online e Salesforce.</span><span class="sxs-lookup"><span data-stu-id="321b0-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="321b0-112">È stato richiesto di usare lo standard [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) per tutti i record dei pazienti.</span><span class="sxs-lookup"><span data-stu-id="321b0-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="321b0-113">Il progetto prevedeva due requisiti principali:</span><span class="sxs-lookup"><span data-stu-id="321b0-113">The project had two major requirements:</span></span>  

* <span data-ttu-id="321b0-114">Un metodo per registrare i record inviati dal portale Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="321b0-114">A method to log records sent from the Dynamics CRM Online portal</span></span>
* <span data-ttu-id="321b0-115">Un modo per visualizzare gli eventuali errori verificatisi nel flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="321b0-115">A way to view any errors that occurred within the workflow</span></span>

> [!TIP]
> <span data-ttu-id="321b0-116">Per un video dettagliato su questo progetto, andare alla pagina di [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span><span class="sxs-lookup"><span data-stu-id="321b0-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-the-problem"></a><span data-ttu-id="321b0-117">Come è stato risolto il problema</span><span class="sxs-lookup"><span data-stu-id="321b0-117">How we solved the problem</span></span>

<span data-ttu-id="321b0-118">Come repository per i record di log e di errore è stato scelto [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB"), in cui i record sono definiti documenti.</span><span class="sxs-lookup"><span data-stu-id="321b0-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for the log and error records (Cosmos DB refers to records as documents).</span></span> <span data-ttu-id="321b0-119">Dato che le app per la logica di Azure includono un modello standard per tutte le risposte, non è stato necessario creare uno schema personalizzato.</span><span class="sxs-lookup"><span data-stu-id="321b0-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span></span> <span data-ttu-id="321b0-120">È stato possibile creare un'app per le API per l'**inserimento** e la **query** per i record di errore e di log.</span><span class="sxs-lookup"><span data-stu-id="321b0-120">We could create an API app to **Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="321b0-121">È stato anche possibile definire uno schema per ognuno all'interno dell'app per le API.</span><span class="sxs-lookup"><span data-stu-id="321b0-121">We could also define a schema for each within the API app.</span></span>  

<span data-ttu-id="321b0-122">Un altro requisito era ripulire i record dopo una certa data.</span><span class="sxs-lookup"><span data-stu-id="321b0-122">Another requirement was to purge records after a certain date.</span></span> <span data-ttu-id="321b0-123">Cosmos DB include una proprietà denominata [durata (TTL)](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "durata (TTL)") che ha consentito di impostare un valore di **durata (TTL)** per ogni record o raccolta.</span><span class="sxs-lookup"><span data-stu-id="321b0-123">Cosmos DB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span></span> <span data-ttu-id="321b0-124">Questa funzionalità ha evitato di dover eliminare manualmente i record in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="321b0-124">This capability eliminated the need to manually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="321b0-125">Per completare questa esercitazione, è necessario creare un database Cosmos DB e due raccolte, per la registrazione e gli errori.</span><span class="sxs-lookup"><span data-stu-id="321b0-125">To complete this tutorial, you need to create a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-the-logic-app"></a><span data-ttu-id="321b0-126">Creare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="321b0-126">Create the logic app</span></span>

<span data-ttu-id="321b0-127">Il primo passaggio consiste nel creare l'app per la logica e aprirla nella finestra di progettazione di app per la logica.</span><span class="sxs-lookup"><span data-stu-id="321b0-127">The first step is to create the logic app and open the app in Logic App Designer.</span></span> <span data-ttu-id="321b0-128">In questo esempio vengono usate app per la logica padre-figlio.</span><span class="sxs-lookup"><span data-stu-id="321b0-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="321b0-129">Partendo dal presupposto di aver già creato l'elemento padre, si procederà alla creazione di un'app per la logica figlio.</span><span class="sxs-lookup"><span data-stu-id="321b0-129">Let's assume that we have already created the parent and are going to create one child logic app.</span></span>

<span data-ttu-id="321b0-130">Dato che si prevede di registrare il record proveniente da Dynamics CRM Online, si inizierà dal principio.</span><span class="sxs-lookup"><span data-stu-id="321b0-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span></span> <span data-ttu-id="321b0-131">È necessario usare un trigger di **richiesta**, perché l'app per la logica padre attiva questo elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="321b0-131">We must use a **Request** trigger because the parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="321b0-132">Trigger dell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="321b0-132">Logic app trigger</span></span>

<span data-ttu-id="321b0-133">Viene usato un trigger di **richiesta** come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="321b0-133">We are using a **Request** trigger as shown in the following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="321b0-134">Passi</span><span class="sxs-lookup"><span data-stu-id="321b0-134">Steps</span></span>

<span data-ttu-id="321b0-135">È necessario registrare l'origine (richiesta) del record del paziente dal portale Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="321b0-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="321b0-136">È necessario ottenere un nuovo record di appuntamento da Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="321b0-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="321b0-137">Il trigger proveniente da CRM fornisce il **PatientID CRM**, il **tipo di record**, un **valore booleano new o update** che indica un record nuovo o aggiornato e **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="321b0-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="321b0-138">**SalesforceId** può essere Null perché viene usato solo per un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="321b0-138">The **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="321b0-139">Per ottenere il record CRM si userà il **PatientID** di CRM e il **tipo di record**.</span><span class="sxs-lookup"><span data-stu-id="321b0-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span></span>

2. <span data-ttu-id="321b0-140">È quindi necessario aggiungere l'operazione **InsertLogEntry** dell'app per le API DocumentDB, come illustrato qui in Progettazione app per la logica.</span><span class="sxs-lookup"><span data-stu-id="321b0-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="321b0-141">**Inserire una voce di log**</span><span class="sxs-lookup"><span data-stu-id="321b0-141">**Insert log entry**</span></span>

   ![Inserire una voce di log](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="321b0-143">**Inserire una voce di log**</span><span class="sxs-lookup"><span data-stu-id="321b0-143">**Insert error entry**</span></span>

   ![Inserire una voce di log](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="321b0-145">**Verificare la presenza di errori nella creazione di record**</span><span class="sxs-lookup"><span data-stu-id="321b0-145">**Check for create record failure**</span></span>

   ![Condizione](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="321b0-147">Codice sorgente dell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="321b0-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="321b0-148">Quelli riportati di seguito sono solo esempi.</span><span class="sxs-lookup"><span data-stu-id="321b0-148">The following examples are samples only.</span></span> <span data-ttu-id="321b0-149">Dato che l'esercitazione è basata su un'implementazione attualmente in produzione, il valore di un **nodo di origine** potrebbe non mostrare le proprietà correlate alla pianificazione di un appuntamento.></span><span class="sxs-lookup"><span data-stu-id="321b0-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="321b0-150">Registrazione</span><span class="sxs-lookup"><span data-stu-id="321b0-150">Logging</span></span>

<span data-ttu-id="321b0-151">L'esempio di codice dell'app per la logica seguente illustra come gestire la registrazione.</span><span class="sxs-lookup"><span data-stu-id="321b0-151">The following logic app code sample shows how to handle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="321b0-152">Voce di log</span><span class="sxs-lookup"><span data-stu-id="321b0-152">Log entry</span></span>

<span data-ttu-id="321b0-153">Questo è il codice sorgente dell'app per la logica per l'inserimento di una voce di log.</span><span class="sxs-lookup"><span data-stu-id="321b0-153">Here is the logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="321b0-154">Richiesta di log</span><span class="sxs-lookup"><span data-stu-id="321b0-154">Log request</span></span>

<span data-ttu-id="321b0-155">Questo è il messaggio di richiesta di log inviato all'app per le API.</span><span class="sxs-lookup"><span data-stu-id="321b0-155">Here is the log request message posted to the API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="321b0-156">Risposta di log</span><span class="sxs-lookup"><span data-stu-id="321b0-156">Log response</span></span>

<span data-ttu-id="321b0-157">Questo è il messaggio di risposta di log proveniente dall'app per le API.</span><span class="sxs-lookup"><span data-stu-id="321b0-157">Here is the log response message from the API app.</span></span>

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

<span data-ttu-id="321b0-158">Verranno ora esaminati i passaggi della gestione degli errori.</span><span class="sxs-lookup"><span data-stu-id="321b0-158">Now let's look at the error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="321b0-159">Gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="321b0-159">Error handling</span></span>

<span data-ttu-id="321b0-160">L'esempio di codice di app per la logica seguente illustra come è possibile implementare la gestione degli errori.</span><span class="sxs-lookup"><span data-stu-id="321b0-160">The following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="321b0-161">Creare record di errore</span><span class="sxs-lookup"><span data-stu-id="321b0-161">Create error record</span></span>

<span data-ttu-id="321b0-162">Questo è il codice sorgente dell'app per la logica per la creazione di un record di errore.</span><span class="sxs-lookup"><span data-stu-id="321b0-162">Here is the logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="321b0-163">Inserire l'errore in Cosmos DB: richiesta</span><span class="sxs-lookup"><span data-stu-id="321b0-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="321b0-164">Inserire l'errore in Cosmos DB: risposta</span><span class="sxs-lookup"><span data-stu-id="321b0-164">Insert error into Cosmos DB--response</span></span>

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
        "body": "CRM failed to complete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
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

#### <a name="salesforce-error-response"></a><span data-ttu-id="321b0-165">Risposta di errore di Salesforce</span><span class="sxs-lookup"><span data-stu-id="321b0-165">Salesforce error response</span></span>

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
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-the-response-back-to-parent-logic-app"></a><span data-ttu-id="321b0-166">Restituire la risposta all'app per la logica padre</span><span class="sxs-lookup"><span data-stu-id="321b0-166">Return the response back to parent logic app</span></span>

<span data-ttu-id="321b0-167">Dopo aver ottenuto la risposta, è possibile trasmetterla all'app per la logica padre.</span><span class="sxs-lookup"><span data-stu-id="321b0-167">After you get the response, you can pass the response back to the parent logic app.</span></span>

#### <a name="return-success-response-to-parent-logic-app"></a><span data-ttu-id="321b0-168">Restituire la risposta di esito positivo all'app per la logica padre</span><span class="sxs-lookup"><span data-stu-id="321b0-168">Return success response to parent logic app</span></span>

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

#### <a name="return-error-response-to-parent-logic-app"></a><span data-ttu-id="321b0-169">Restituire la risposta di errore all'app per la logica padre</span><span class="sxs-lookup"><span data-stu-id="321b0-169">Return error response to parent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="321b0-170">Portale e repository di Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="321b0-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="321b0-171">In questa soluzione sono state aggiunte funzionalità con [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="321b0-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="321b0-172">Portale di gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="321b0-172">Error management portal</span></span>

<span data-ttu-id="321b0-173">Per consultare gli errori, è possibile creare un'app Web MVC per visualizzare i record di errore da Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="321b0-173">To view the errors, you can create an MVC web app to display the error records from Cosmos DB.</span></span> <span data-ttu-id="321b0-174">Nella versione corrente sono incluse operazioni di tipo **Elenco**, **Dettagli**, **Modifica** ed **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="321b0-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span></span>

> [!NOTE]
> <span data-ttu-id="321b0-175">Con l'operazione di modifica, Cosmos DB sostituisce l'intero documento.</span><span class="sxs-lookup"><span data-stu-id="321b0-175">Edit operation: Cosmos DB replaces the entire document.</span></span> <span data-ttu-id="321b0-176">I record contenuti nelle visualizzazioni **elenco** e **dettagli** sono solo esempi.</span><span class="sxs-lookup"><span data-stu-id="321b0-176">The records shown in the **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="321b0-177">Non si tratta di record effettivi di appuntamenti dei pazienti.</span><span class="sxs-lookup"><span data-stu-id="321b0-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="321b0-178">Questi sono esempi dei dettagli dell'app MVC creati con l'approccio precedentemente descritto.</span><span class="sxs-lookup"><span data-stu-id="321b0-178">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="321b0-179">Elenco di gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="321b0-179">Error management list</span></span>
![Elenco errori](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="321b0-181">Visualizzazione dei dettagli di gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="321b0-181">Error management detail view</span></span>
![Dettagli errore](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="321b0-183">Portale di gestione dei log</span><span class="sxs-lookup"><span data-stu-id="321b0-183">Log management portal</span></span>

<span data-ttu-id="321b0-184">È stata creata un'app Web MVC anche per visualizzare i log.</span><span class="sxs-lookup"><span data-stu-id="321b0-184">To view the logs, we also created an MVC web app.</span></span> <span data-ttu-id="321b0-185">Questi sono esempi dei dettagli dell'app MVC creati con l'approccio precedentemente descritto.</span><span class="sxs-lookup"><span data-stu-id="321b0-185">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="321b0-186">Visualizzazione di dettagli dei log di esempio</span><span class="sxs-lookup"><span data-stu-id="321b0-186">Sample log detail view</span></span>
![Visualizzare i dettagli dei log](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="321b0-188">Dettagli dell'app per le API</span><span class="sxs-lookup"><span data-stu-id="321b0-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="321b0-189">API di gestione delle eccezioni di app per la logica</span><span class="sxs-lookup"><span data-stu-id="321b0-189">Logic Apps exception management API</span></span>

<span data-ttu-id="321b0-190">L'app per le API di gestione delle eccezioni delle App per la logica di Azure offre le funzionalità descritte di seguito, sono presenti due controller:</span><span class="sxs-lookup"><span data-stu-id="321b0-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="321b0-191">**ErrorController** inserisce un record di errore (documento) in una raccolta di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="321b0-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="321b0-192">**LogController** inserisce un record di log (documento) in una raccolta di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="321b0-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="321b0-193">Entrambi i controller usano operazioni `async Task<dynamic>`, che consentono la risoluzione in fase di runtime, per poter creare lo schema di DocumentDB nel corpo dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="321b0-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span></span> 
> 

<span data-ttu-id="321b0-194">Ogni documento in DocumentDB deve avere un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="321b0-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="321b0-195">Viene usato `PatientId` e viene aggiunto un timestamp che sarà convertito in un valore di timestamp Unix (double).</span><span class="sxs-lookup"><span data-stu-id="321b0-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span></span> <span data-ttu-id="321b0-196">Il valore viene troncato per rimuovere il valore frazionario.</span><span class="sxs-lookup"><span data-stu-id="321b0-196">We truncate the value to remove the fractional value.</span></span>

<span data-ttu-id="321b0-197">È possibile visualizzare il codice sorgente dell'API del controller degli errori [da GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="321b0-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="321b0-198">L'API viene chiamata da un'app per la logica usando la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="321b0-198">We call the API from a logic app by using the following syntax:</span></span>

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

<span data-ttu-id="321b0-199">L'espressione nell'esempio di codice precedente verifica la presenza dello stato **Non riuscito** di *Create_NewPatientRecord*.</span><span class="sxs-lookup"><span data-stu-id="321b0-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="321b0-200">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="321b0-200">Summary</span></span>

* <span data-ttu-id="321b0-201">È possibile implementare facilmente la registrazione e la gestione degli errori in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="321b0-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="321b0-202">È possibile usare DocumentDB come repository per i record di log e di errore (documenti).</span><span class="sxs-lookup"><span data-stu-id="321b0-202">You can use DocumentDB as the repository for log and error records (documents).</span></span>
* <span data-ttu-id="321b0-203">È possibile usare MVC per creare un portale per la visualizzazione dei record di log e di errore.</span><span class="sxs-lookup"><span data-stu-id="321b0-203">You can use MVC to create a portal to display log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="321b0-204">Codice sorgente</span><span class="sxs-lookup"><span data-stu-id="321b0-204">Source code</span></span>

<span data-ttu-id="321b0-205">Il codice sorgente dell'applicazione per le API di gestione delle eccezioni di app per la logica è disponibile in questo [repository GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API di gestione delle eccezioni dell'app per la logica").</span><span class="sxs-lookup"><span data-stu-id="321b0-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="321b0-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="321b0-206">Next steps</span></span>

* [<span data-ttu-id="321b0-207">Visualizzare altri esempi e scenari di app per la logica</span><span class="sxs-lookup"><span data-stu-id="321b0-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="321b0-208">Informazioni sul monitoraggio delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="321b0-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="321b0-209">Creare modelli di distribuzione automatizzati per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="321b0-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
