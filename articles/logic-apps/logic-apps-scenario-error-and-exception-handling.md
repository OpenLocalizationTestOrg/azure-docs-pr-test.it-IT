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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="c8fb6-103">Scenario: Gestione delle eccezioni e registrazione degli errori per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="c8fb6-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="c8fb6-104">In questo scenario viene illustrato come estendere una logica app toobetter supporto delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="c8fb6-105">È stata utilizzata una domanda di uso reale tooanswer case hello: "App per la logica di Azure supporta eccezione e la gestione degli errori?"</span><span class="sxs-lookup"><span data-stu-id="c8fb6-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="c8fb6-106">schema delle app di Azure logica corrente Hello fornisce un modello standard per le risposte di azione.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="c8fb6-107">che include le risposte per gli errori e la convalida interna restituite da un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="c8fb6-108">Panoramica su scenario e caso d'uso</span><span class="sxs-lookup"><span data-stu-id="c8fb6-108">Scenario and use case overview</span></span>

<span data-ttu-id="c8fb6-109">Ecco storia hello come caso d'uso hello per questo scenario:</span><span class="sxs-lookup"><span data-stu-id="c8fb6-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="c8fb6-110">Un'organizzazione sanitaria nota dovrà us toodevelop una soluzione di Azure che creerebbe un portale del paziente con Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="c8fb6-111">Sono necessari i record di un appuntamento toosend tra portale paziente Dynamics CRM Online hello e Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="c8fb6-112">Ci siamo richiesto hello toouse [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard per tutti i pazienti.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="c8fb6-113">progetto Hello ha due requisiti principali:</span><span class="sxs-lookup"><span data-stu-id="c8fb6-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="c8fb6-114">Un record di toolog metodo inviati da hello portale Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="c8fb6-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="c8fb6-115">Un modo tooview eventuali errori che si sono verificati all'interno del flusso di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="c8fb6-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="c8fb6-116">Per un video di alto livello su questo progetto, vedere [gruppo utente Integration](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "gruppo utente Integration").</span><span class="sxs-lookup"><span data-stu-id="c8fb6-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="c8fb6-117">Come abbiamo risolto il problema di hello</span><span class="sxs-lookup"><span data-stu-id="c8fb6-117">How we solved hello problem</span></span>

<span data-ttu-id="c8fb6-118">Abbiamo scelto [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") come repository per i record di log e di errore hello (toorecords come documenti Cosmos DB fa riferimento).</span><span class="sxs-lookup"><span data-stu-id="c8fb6-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="c8fb6-119">Poiché le app di logica di Azure dispone di un modello standard per tutte le risposte, non sono toocreate uno schema personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="c8fb6-120">È stato possibile creare un'app per le API troppo**inserire** e **Query** per i record di errore e di log.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="c8fb6-121">È inoltre possibile definire uno schema per ognuna all'interno di app per le API hello.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="c8fb6-122">Un altro requisito è stato record toopurge dopo una certa data.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="c8fb6-123">COSMOS DB è una proprietà denominata [ora tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "ora tooLive") (TTL), che ha consentito tooset un **ora tooLive** valore per ogni record o una raccolta.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="c8fb6-124">Questa funzionalità eliminate hello necessità toomanually eliminare i record nel database Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8fb6-125">toocomplete questa esercitazione, è necessario un database DB Cosmos toocreate e due raccolte (registrazione e gli errori).</span><span class="sxs-lookup"><span data-stu-id="c8fb6-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="c8fb6-126">Creare app per la logica hello</span><span class="sxs-lookup"><span data-stu-id="c8fb6-126">Create hello logic app</span></span>

<span data-ttu-id="c8fb6-127">primo passaggio Hello è toocreate hello logica app e app hello aperto nella finestra di progettazione logica App.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="c8fb6-128">In questo esempio vengono usate app per la logica padre-figlio.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="c8fb6-129">Si supponga che è già stato creato il padre di hello e verranno toocreate uno figlio logica app.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="c8fb6-130">Poiché verrà record hello toolog provengano da Dynamics CRM Online, iniziamo nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="c8fb6-131">È necessario utilizzare un **richiesta** trigger hello padre logica app attiva l'elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="c8fb6-132">Trigger dell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c8fb6-132">Logic app trigger</span></span>

<span data-ttu-id="c8fb6-133">Si sta usando un **richiesta** trigger come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c8fb6-133">We are using a **Request** trigger as shown in hello following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="c8fb6-134">Passi</span><span class="sxs-lookup"><span data-stu-id="c8fb6-134">Steps</span></span>

<span data-ttu-id="c8fb6-135">È necessario eseguire l'accesso di origine hello (request) del record paziente hello dal portale di Dynamics CRM Online hello.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="c8fb6-136">È necessario ottenere un nuovo record di appuntamento da Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="c8fb6-137">trigger Hello provenienti da CRM ci offre hello **CRM PatentId**, **tipo di record**, **nuovo o aggiornato Record** (nuovo o aggiornare un valore booleano), e  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="c8fb6-138">Hello **SalesforceId** può essere null, poiché viene utilizzato solo per un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="c8fb6-139">Record CRM hello si ottiene utilizzando hello CRM **PatientID** hello e **tipo di Record**.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="c8fb6-140">È quindi necessario tooadd l'app per le API DocumentDB **InsertLogEntry** operazione, come illustrato di seguito in Progettazione applicazione logica.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="c8fb6-141">**Inserire una voce di log**</span><span class="sxs-lookup"><span data-stu-id="c8fb6-141">**Insert log entry**</span></span>

   ![Inserire una voce di log](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="c8fb6-143">**Inserire una voce di log**</span><span class="sxs-lookup"><span data-stu-id="c8fb6-143">**Insert error entry**</span></span>

   ![Inserire una voce di log](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="c8fb6-145">**Verificare la presenza di errori nella creazione di record**</span><span class="sxs-lookup"><span data-stu-id="c8fb6-145">**Check for create record failure**</span></span>

   ![Condizione](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="c8fb6-147">Codice sorgente dell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c8fb6-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="c8fb6-148">seguono esempi Hello è solo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-148">hello following examples are samples only.</span></span> <span data-ttu-id="c8fb6-149">Poiché in questa esercitazione si basa sull'implementazione di un'ora nell'ambiente di produzione, hello valore di un **nodo di origine** potrebbe non visualizzare le proprietà correlate tooscheduling un appuntamento. ></span><span class="sxs-lookup"><span data-stu-id="c8fb6-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="c8fb6-150">Registrazione</span><span class="sxs-lookup"><span data-stu-id="c8fb6-150">Logging</span></span>

<span data-ttu-id="c8fb6-151">Hello seguendo la logica app codice di esempio viene illustrata la modalità registrazione toohandle.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="c8fb6-152">Voce di log</span><span class="sxs-lookup"><span data-stu-id="c8fb6-152">Log entry</span></span>

<span data-ttu-id="c8fb6-153">Ecco il codice sorgente di hello logica app per l'inserimento di una voce di log.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-153">Here is hello logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="c8fb6-154">Richiesta di log</span><span class="sxs-lookup"><span data-stu-id="c8fb6-154">Log request</span></span>

<span data-ttu-id="c8fb6-155">Di seguito è registrata l'app per le API toohello messaggio di richiesta di hello log.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-155">Here is hello log request message posted toohello API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="c8fb6-156">Risposta di log</span><span class="sxs-lookup"><span data-stu-id="c8fb6-156">Log response</span></span>

<span data-ttu-id="c8fb6-157">Di seguito è hello log messaggio di risposta app hello per le API.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-157">Here is hello log response message from hello API app.</span></span>

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

<span data-ttu-id="c8fb6-158">Ora esaminiamo i passaggi di gestione degli errori di hello.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="c8fb6-159">Gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="c8fb6-159">Error handling</span></span>

<span data-ttu-id="c8fb6-160">Hello logica app esempio seguente viene illustrato come è possibile implementare la gestione degli errori.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="c8fb6-161">Creare record di errore</span><span class="sxs-lookup"><span data-stu-id="c8fb6-161">Create error record</span></span>

<span data-ttu-id="c8fb6-162">Ecco il codice sorgente di hello logica app per la creazione di un record di errore.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-162">Here is hello logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="c8fb6-163">Inserire l'errore in Cosmos DB: richiesta</span><span class="sxs-lookup"><span data-stu-id="c8fb6-163">Insert error into Cosmos DB--request</span></span>

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

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="c8fb6-164">Inserire l'errore in Cosmos DB: risposta</span><span class="sxs-lookup"><span data-stu-id="c8fb6-164">Insert error into Cosmos DB--response</span></span>

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

#### <a name="salesforce-error-response"></a><span data-ttu-id="c8fb6-165">Risposta di errore di Salesforce</span><span class="sxs-lookup"><span data-stu-id="c8fb6-165">Salesforce error response</span></span>

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

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="c8fb6-166">Restituire hello risposta tooparent indietro logica app</span><span class="sxs-lookup"><span data-stu-id="c8fb6-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="c8fb6-167">Dopo avere ottenuto una risposta di hello, è possibile passare risposta hello toohello indietro padre logica app.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="c8fb6-168">App per la logica tooparent risposta restituito esito positivo</span><span class="sxs-lookup"><span data-stu-id="c8fb6-168">Return success response tooparent logic app</span></span>

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

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="c8fb6-169">Errore restituito risposta tooparent logica app</span><span class="sxs-lookup"><span data-stu-id="c8fb6-169">Return error response tooparent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="c8fb6-170">Portale e repository di Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8fb6-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="c8fb6-171">In questa soluzione sono state aggiunte funzionalità con [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="c8fb6-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="c8fb6-172">Portale di gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="c8fb6-172">Error management portal</span></span>

<span data-ttu-id="c8fb6-173">errori di hello tooview, è possibile creare un record di errore MVC web app toodisplay hello da DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="c8fb6-174">Hello **elenco**, **dettagli**, **modifica**, e **eliminare** sono incluse le operazioni nella versione corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="c8fb6-175">Operazione di modifica: Cosmos DB sostituisce l'intero documento hello.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="c8fb6-176">Hello record visualizzati in hello **elenco** e **dettaglio** le visualizzazioni sono solo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="c8fb6-177">Non si tratta di record effettivi di appuntamenti dei pazienti.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="c8fb6-178">Ecco alcuni esempi di applicazione MVC vengono descritti i dettagli creati in precedenza con hello approccio.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="c8fb6-179">Elenco di gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="c8fb6-179">Error management list</span></span>
![Elenco errori](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="c8fb6-181">Visualizzazione dei dettagli di gestione degli errori</span><span class="sxs-lookup"><span data-stu-id="c8fb6-181">Error management detail view</span></span>
![Dettagli errore](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="c8fb6-183">Portale di gestione dei log</span><span class="sxs-lookup"><span data-stu-id="c8fb6-183">Log management portal</span></span>

<span data-ttu-id="c8fb6-184">log hello tooview, è inoltre creata un'applicazione web MVC.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="c8fb6-185">Ecco alcuni esempi di applicazione MVC vengono descritti i dettagli creati in precedenza con hello approccio.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="c8fb6-186">Visualizzazione di dettagli dei log di esempio</span><span class="sxs-lookup"><span data-stu-id="c8fb6-186">Sample log detail view</span></span>
![Visualizzare i dettagli dei log](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="c8fb6-188">Dettagli dell'app per le API</span><span class="sxs-lookup"><span data-stu-id="c8fb6-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="c8fb6-189">API di gestione delle eccezioni di app per la logica</span><span class="sxs-lookup"><span data-stu-id="c8fb6-189">Logic Apps exception management API</span></span>

<span data-ttu-id="c8fb6-190">L'app per le API di gestione delle eccezioni delle App per la logica di Azure offre le funzionalità descritte di seguito, sono presenti due controller:</span><span class="sxs-lookup"><span data-stu-id="c8fb6-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="c8fb6-191">**ErrorController** inserisce un record di errore (documento) in una raccolta di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="c8fb6-192">**LogController** inserisce un record di log (documento) in una raccolta di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="c8fb6-193">Utilizzano entrambi i controller `async Task<dynamic>` operazioni, consentendo operazioni tooresolve in fase di esecuzione, affinché sia possibile creare hello schema DocumentDB nel corpo di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="c8fb6-194">Ogni documento in DocumentDB deve avere un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="c8fb6-195">Si sta usando `PatientId` e l'aggiunta di timestamp tooa Unix timestamp valore convertito (double).</span><span class="sxs-lookup"><span data-stu-id="c8fb6-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="c8fb6-196">Valore frazionario dei hello valore tooremove hello è troncato.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="c8fb6-197">È possibile visualizzare il codice sorgente hello del nostro controller Errore API [da GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="c8fb6-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="c8fb6-198">Viene chiamato hello API da un'app logica tramite hello la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="c8fb6-198">We call hello API from a logic app by using hello following syntax:</span></span>

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

<span data-ttu-id="c8fb6-199">espressione nel precedente esempio di codice cerca hello hello Hello *Create_NewPatientRecord* stato **Failed**.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="c8fb6-200">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="c8fb6-200">Summary</span></span>

* <span data-ttu-id="c8fb6-201">È possibile implementare facilmente la registrazione e la gestione degli errori in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="c8fb6-202">È possibile utilizzare DocumentDB come repository di hello per i record di log e di errore (documenti).</span><span class="sxs-lookup"><span data-stu-id="c8fb6-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="c8fb6-203">È possibile utilizzare MVC toocreate un log toodisplay portale e i record degli errori.</span><span class="sxs-lookup"><span data-stu-id="c8fb6-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="c8fb6-204">Codice sorgente</span><span class="sxs-lookup"><span data-stu-id="c8fb6-204">Source code</span></span>

<span data-ttu-id="c8fb6-205">è disponibile in questo codice di sorgente Hello per la gestione delle eccezioni App per la logica dell'applicazione API hello [repository GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API di gestione delle eccezioni di logica App").</span><span class="sxs-lookup"><span data-stu-id="c8fb6-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8fb6-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8fb6-206">Next steps</span></span>

* [<span data-ttu-id="c8fb6-207">Visualizzare altri esempi e scenari di app per la logica</span><span class="sxs-lookup"><span data-stu-id="c8fb6-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="c8fb6-208">Informazioni sul monitoraggio delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="c8fb6-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="c8fb6-209">Creare modelli di distribuzione automatizzati per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="c8fb6-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
