---
title: aaaChange feed per le risorse di HL7 FHIR - DB Cosmos Azure | Documenti Microsoft
description: Informazioni su come tooset di modificare le notifiche per HL7 FHIR sanitari pazienti tramite app di logica di Azure, Azure Cosmos DB e Bus di servizio.
keywords: hl7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="29dce-104">Segnalare ai pazienti le modifiche delle cartelle cliniche HL7 FHIR utilizzando le App per la logica e Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29dce-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="29dce-105">Azure MVP Howard Edidin recentemente è stato contattato da un'organizzazione sanitaria che voleva tooadd nuovo funzionalità tootheir paziente portale.</span><span class="sxs-lookup"><span data-stu-id="29dce-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="29dce-106">Se necessari toosend toopatients di notifiche quando i record di integrità è stato aggiornato, e sono necessari aggiornamenti toothese toosubscribe in grado di pazienti toobe.</span><span class="sxs-lookup"><span data-stu-id="29dce-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="29dce-107">In questo articolo vengono esaminati hello Modifica notifica feed soluzione creata per questa organizzazione sanitaria usando Azure Cosmos DB, App per la logica e Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="29dce-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="29dce-108">Requisiti del progetto</span><span class="sxs-lookup"><span data-stu-id="29dce-108">Project requirements</span></span>
- <span data-ttu-id="29dce-109">I provider inviano documenti HL7 Consolidated-Clinical Document Architecture (C-CDA) in formato XML.</span><span class="sxs-lookup"><span data-stu-id="29dce-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="29dce-110">I documenti C-CDA comprendono sostanzialmente ogni tipo di documento clinico, incluse informazioni familiari e registri immunologici, oltre a documenti amministrati, finanziari e su flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="29dce-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="29dce-111">Documenti C CDA vengono convertiti troppo[HL7 FHIR risorse](http://hl7.org/fhir/2017Jan/resourcelist.html) in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="29dce-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="29dce-112">I documenti di risorse FHIR modificati vengono inviati via e-mail in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="29dce-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="29dce-113">Flusso di lavoro della soluzione</span><span class="sxs-lookup"><span data-stu-id="29dce-113">Solution workflow</span></span> 

<span data-ttu-id="29dce-114">In generale, il progetto di hello necessario hello del flusso di lavoro come segue:</span><span class="sxs-lookup"><span data-stu-id="29dce-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="29dce-115">Convertire le risorse di C CDA documenti tooFHIR.</span><span class="sxs-lookup"><span data-stu-id="29dce-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="29dce-116">Eseguire un trigger ricorrente per il polling di risorse FHIR modificate.</span><span class="sxs-lookup"><span data-stu-id="29dce-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="29dce-117">Chiamare un'app personalizzata, FhirNotificationApi, tooconnect tooAzure Cosmos DB e una query per i documenti nuovi o modificati.</span><span class="sxs-lookup"><span data-stu-id="29dce-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="29dce-118">Salvare una coda di Service Bus tootoohello risposta hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="29dce-119">Esegue il polling per nuovi messaggi nella coda di Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="29dce-120">Inviare toopatients le notifiche di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="29dce-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="29dce-121">Architettura della soluzione</span><span class="sxs-lookup"><span data-stu-id="29dce-121">Solution architecture</span></span>
<span data-ttu-id="29dce-122">Questa soluzione richiede tre hello toomeet di App per la logica sopra i requisiti e del flusso di lavoro soluzione hello completo.</span><span class="sxs-lookup"><span data-stu-id="29dce-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="29dce-123">Hello tre logica App sono:</span><span class="sxs-lookup"><span data-stu-id="29dce-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="29dce-124">**Mapping di FHIR HL7 app**: riceve hello HL7 C-CDA documento, lo trasforma toohello FHIR risorse, quindi Salva tooAzure DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="29dce-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="29dce-125">**App EHR**: query repository Azure Cosmos DB FHIR hello e Salva una coda di Service Bus tooa risposta hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="29dce-126">Questa app logica Usa un [app per le API](#api-app) tooretrieve nuove e modificate documenti.</span><span class="sxs-lookup"><span data-stu-id="29dce-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="29dce-127">**Processo notifica app**: invia una notifica di posta elettronica con i documenti della risorsa FHIR hello nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Hello tre App per la logica utilizzata in questa soluzione sanitaria FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="29dce-129">Servizi Azure utilizzati nella soluzione hello</span><span class="sxs-lookup"><span data-stu-id="29dce-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="29dce-130">API DocumentDB di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29dce-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="29dce-131">DB Cosmos Azure è il repository di hello per le risorse FHIR hello come illustrato nella seguente illustrazione hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![account di Azure Cosmos DB Hello utilizzato in questa esercitazione sanitaria FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="29dce-133">App per la logica</span><span class="sxs-lookup"><span data-stu-id="29dce-133">Logic Apps</span></span>
<span data-ttu-id="29dce-134">App per la logica di gestire il processo di flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="29dce-135">Hello schermate seguenti mostrano hello logica App creata per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="29dce-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="29dce-136">**Mapping di FHIR HL7 app**: ricevere documento HL7 C-CDA hello e trasformarlo risorsa FHIR tooan usando hello Enterprise Integration Pack per le applicazioni di logica.</span><span class="sxs-lookup"><span data-stu-id="29dce-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="29dce-137">Hello Enterprise Integration Pack gestisce il mapping da hello risorse tooFHIR C CDA hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Hello App per la logica utilizzata record sanitari di tooreceive FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="29dce-139">**App EHR**: Query repository Azure Cosmos DB FHIR hello e salvare hello risposta tooa Bus di servizio della coda.</span><span class="sxs-lookup"><span data-stu-id="29dce-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="29dce-140">codice Hello per app GetNewOrModifiedFHIRDocuments hello è inferiore.</span><span class="sxs-lookup"><span data-stu-id="29dce-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![tooquery logica App usata Hello Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="29dce-142">**Processo notifica app**: inviare una notifica di posta elettronica con i documenti di risorse FHIR hello nel corpo di hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![App per la logica che invia posta elettronica del paziente con risorse HL7 FHIR hello nel corpo di hello Hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="29dce-144">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="29dce-144">Service Bus</span></span>
<span data-ttu-id="29dce-145">Hello nella seguente figura mostra hello pazienti coda.</span><span class="sxs-lookup"><span data-stu-id="29dce-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="29dce-146">Hello valore della proprietà Tag viene utilizzato per l'oggetto messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-146">hello Tag property value is used for hello email subject.</span></span>

![Hello utilizzati in questa esercitazione HL7 FHIR coda di Service Bus](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="29dce-148">App per le API</span><span class="sxs-lookup"><span data-stu-id="29dce-148">API app</span></span>
<span data-ttu-id="29dce-149">Un'app per le API si connette tooAzure DB Cosmos e query per documenti FHIR nuovi o modificati dal tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="29dce-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="29dce-150">Questa applicazione dispone di un controller, **FhirNotificationApi** con una unica operazione **GetNewOrModifiedFhirDocuments**, vedere l'[origine di app per le API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="29dce-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="29dce-151">Si sta usando hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) classe da hello API .NET di Azure Cosmos DB DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="29dce-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="29dce-152">Per ulteriori informazioni, vedere hello [modifica feed articolo](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="29dce-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="29dce-153">Operazione GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="29dce-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="29dce-154">**Input**</span><span class="sxs-lookup"><span data-stu-id="29dce-154">**Inputs**</span></span>
- <span data-ttu-id="29dce-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="29dce-155">DatabaseId</span></span>
- <span data-ttu-id="29dce-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="29dce-156">CollectionId</span></span>
- <span data-ttu-id="29dce-157">Nome del tipo di risorsa HL7 FHIR</span><span class="sxs-lookup"><span data-stu-id="29dce-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="29dce-158">Valore booleano: Avvia dall'inizio</span><span class="sxs-lookup"><span data-stu-id="29dce-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="29dce-159">Int: Numero di documenti restituiti</span><span class="sxs-lookup"><span data-stu-id="29dce-159">Int: Number of documents returned</span></span>

<span data-ttu-id="29dce-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="29dce-160">**Outputs**</span></span>
- <span data-ttu-id="29dce-161">Operazione riuscita: Codice di stato: 200, Risposta: Elenco di documenti (matrice JSON)</span><span class="sxs-lookup"><span data-stu-id="29dce-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="29dce-162">Errore: Codice di stato: 404, Risposta: "No Documents found for '*resource name'* Resource Type" (Nessun documento trovato per il tipo di risorsa "nome risorsa")</span><span class="sxs-lookup"><span data-stu-id="29dce-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="29dce-163">**Origine per l'applicazione hello API**</span><span class="sxs-lookup"><span data-stu-id="29dce-163">**Source for hello API app**</span></span>

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="29dce-164">Test hello FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="29dce-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="29dce-165">Hello immagine riportata di seguito viene illustrato come è stato utilizzato tootootest hello swagger [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="29dce-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![file Swagger Hello utilizzato tootest hello API app](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="29dce-167">Dashboard del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="29dce-167">Azure portal dashboard</span></span>

<span data-ttu-id="29dce-168">Hello seguente immagine vengono mostrati tutti di hello servizi di Azure per questa soluzione in esecuzione in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="29dce-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![portale di Azure con tutti i servizi di hello utilizzati in questa esercitazione HL7 FHIR Hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="29dce-170">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="29dce-170">Summary</span></span>

- <span data-ttu-id="29dce-171">Si è appreso che DB Cosmos Azure dispone di supporto nativo per le notifiche per il nuovo o modificato documenti e quanto sia facile toouse.</span><span class="sxs-lookup"><span data-stu-id="29dce-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="29dce-172">Sfruttando le App per la logica è possibile creare flussi di lavoro senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="29dce-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="29dce-173">Utilizzo della distribuzione di hello toohandle code di Azure Service Bus per i documenti di HL7 FHIR hello.</span><span class="sxs-lookup"><span data-stu-id="29dce-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29dce-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="29dce-174">Next steps</span></span>
<span data-ttu-id="29dce-175">Per ulteriori informazioni su Azure Cosmos DB, vedere hello [home page di Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="29dce-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="29dce-176">Per altre informazioni sulle App per la logica, vedere [App per la logica](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="29dce-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


