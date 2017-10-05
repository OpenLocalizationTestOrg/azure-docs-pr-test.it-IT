---
title: Feed delle modifiche per le risorse HL7 FHIR in Azure Cosmos DB | Microsoft Docs
description: Informazioni su come impostare le notifiche di modifica per le cartelle cliniche dei pazienti HL7 FHIR usando le App per la logica di Azure, Azure Cosmos DB e il bus di servizio.
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
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="0dba6-104">Segnalare ai pazienti le modifiche delle cartelle cliniche HL7 FHIR utilizzando le App per la logica e Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0dba6-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="0dba6-105">Howard Edidin, Azure MVP, è stato recentemente contattato da un'organizzazione del settore di sanitario che desiderava aggiungere una nuova funzionalità al proprio portale dei pazienti.</span><span class="sxs-lookup"><span data-stu-id="0dba6-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="0dba6-106">L'organizzazione aveva bisogno di inviare notifiche ai pazienti in caso di aggiornamenti ai loro record sanitari. I pazienti dovevano anche essere in grado di iscriversi a tali aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="0dba6-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="0dba6-107">Questo articolo illustra la soluzione di notifica del feed delle modifiche creata per questa organizzazione sanitaria usando Azure Cosmos DB, le App per la logica e il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="0dba6-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="0dba6-108">Requisiti del progetto</span><span class="sxs-lookup"><span data-stu-id="0dba6-108">Project requirements</span></span>
- <span data-ttu-id="0dba6-109">I provider inviano documenti HL7 Consolidated-Clinical Document Architecture (C-CDA) in formato XML.</span><span class="sxs-lookup"><span data-stu-id="0dba6-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="0dba6-110">I documenti C-CDA comprendono sostanzialmente ogni tipo di documento clinico, incluse informazioni familiari e registri immunologici, oltre a documenti amministrati, finanziari e su flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0dba6-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="0dba6-111">I documenti C-CDA vengono convertiti in [risorse HL7 FHIR](http://hl7.org/fhir/2017Jan/resourcelist.html) in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0dba6-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="0dba6-112">I documenti di risorse FHIR modificati vengono inviati via e-mail in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0dba6-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="0dba6-113">Flusso di lavoro della soluzione</span><span class="sxs-lookup"><span data-stu-id="0dba6-113">Solution workflow</span></span> 

<span data-ttu-id="0dba6-114">A livello generale, il progetto richiedeva i seguenti passaggi del flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="0dba6-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="0dba6-115">Convertire documenti C-CDA in risorse FHIR.</span><span class="sxs-lookup"><span data-stu-id="0dba6-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="0dba6-116">Eseguire un trigger ricorrente per il polling di risorse FHIR modificate.</span><span class="sxs-lookup"><span data-stu-id="0dba6-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="0dba6-117">Chiamare un'app personalizzata, FhirNotificationApi, per connettersi ad Azure Cosmos DB ed eseguire query in merito a documenti nuovi o modificati.</span><span class="sxs-lookup"><span data-stu-id="0dba6-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="0dba6-118">Salvare la risposta nella coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="0dba6-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="0dba6-119">Effettuare il polling per i nuovi messaggi nella coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="0dba6-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="0dba6-120">Inviare notifiche e-mail ai pazienti.</span><span class="sxs-lookup"><span data-stu-id="0dba6-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="0dba6-121">Architettura della soluzione</span><span class="sxs-lookup"><span data-stu-id="0dba6-121">Solution architecture</span></span>
<span data-ttu-id="0dba6-122">Questa soluzione richiede tre App per la logica per soddisfare i requisiti precedenti e completare il flusso di lavoro della soluzione.</span><span class="sxs-lookup"><span data-stu-id="0dba6-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="0dba6-123">Le tre App per la logica sono:</span><span class="sxs-lookup"><span data-stu-id="0dba6-123">The three logic apps are:</span></span>
1. <span data-ttu-id="0dba6-124">**App HL7-FHIR-Mapping**: riceve il documento HL7 C-CDA, lo trasforma nella risorsa FHIR e lo salva in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0dba6-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="0dba6-125">**App EHR**: esegue una query nel repository FHIR di Azure Cosmos DB e salva la risposta in una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="0dba6-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="0dba6-126">Questa App per la logica usa un'[app per le API](#api-app) per recuperare i documenti nuovi e modificati.</span><span class="sxs-lookup"><span data-stu-id="0dba6-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="0dba6-127">**App per le notifiche sul processo**: invia una notifica e-mail contenente i documenti della risorsa FHIR.</span><span class="sxs-lookup"><span data-stu-id="0dba6-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![Le tre App per la logica usate in questa soluzione per la sanità HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="0dba6-129">I servizi di Azure usati nella soluzione</span><span class="sxs-lookup"><span data-stu-id="0dba6-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="0dba6-130">API DocumentDB di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0dba6-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="0dba6-131">Azure Cosmos DB è il repository per le risorse FHIR come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="0dba6-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![Account di Azure Cosmos DB utilizzato in questa esercitazione per la soluzione HL7 FHIR del settore sanitario](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="0dba6-133">App per la logica</span><span class="sxs-lookup"><span data-stu-id="0dba6-133">Logic Apps</span></span>
<span data-ttu-id="0dba6-134">Le App per la logica gestiscono il processo del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0dba6-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="0dba6-135">Gli screenshot seguenti mostrano le App per la logica create per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="0dba6-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="0dba6-136">**App HL7-FHIR-Mapping**: riceve il documento HL7 C-CDA e lo trasforma in una risorsa FHIR usando Enterprise Integration Pack per App per la logica.</span><span class="sxs-lookup"><span data-stu-id="0dba6-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="0dba6-137">Enterprise Integration Pack gestisce il mapping da C-CDA alle risorse FHIR.</span><span class="sxs-lookup"><span data-stu-id="0dba6-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![L'App per la logica usata per ricevere record sanitari HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="0dba6-139">**App EHR**: esegue una query nel repository FHIR di Azure Cosmos DB e salva la risposta in una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="0dba6-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="0dba6-140">Il codice per l'app GetNewOrModifiedFHIRDocuments è indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0dba6-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![App per la logica utilizzata per eseguire query in Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="0dba6-142">**App per le notifiche sul processo**: invia una notifica e-mail contenente i documenti della risorsa FHIR.</span><span class="sxs-lookup"><span data-stu-id="0dba6-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![L'App per la logica per inviare e-mail ai pazienti contenenti la risorsa HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="0dba6-144">Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="0dba6-144">Service Bus</span></span>
<span data-ttu-id="0dba6-145">La figura seguente mostra la coda di pazienti.</span><span class="sxs-lookup"><span data-stu-id="0dba6-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="0dba6-146">Il valore della proprietà Tag viene usato per l'oggetto dell'email.</span><span class="sxs-lookup"><span data-stu-id="0dba6-146">The Tag property value is used for the email subject.</span></span>

![La coda del bus di servizio usata in questa esercitazione HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="0dba6-148">App per le API</span><span class="sxs-lookup"><span data-stu-id="0dba6-148">API app</span></span>
<span data-ttu-id="0dba6-149">Un'app per le API si connette ad Azure Cosmos DB ed esegue query per documenti FHIR nuovi o modificati in base al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="0dba6-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="0dba6-150">Questa applicazione dispone di un controller, **FhirNotificationApi** con una unica operazione **GetNewOrModifiedFhirDocuments**, vedere l'[origine di app per le API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="0dba6-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="0dba6-151">Viene utilizzata la classe [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) dell'API DocumentDB .NET di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0dba6-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="0dba6-152">Per altre informazioni, vedere l'[articolo sul feed delle modifiche](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="0dba6-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="0dba6-153">Operazione GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="0dba6-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="0dba6-154">**Input**</span><span class="sxs-lookup"><span data-stu-id="0dba6-154">**Inputs**</span></span>
- <span data-ttu-id="0dba6-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="0dba6-155">DatabaseId</span></span>
- <span data-ttu-id="0dba6-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="0dba6-156">CollectionId</span></span>
- <span data-ttu-id="0dba6-157">Nome del tipo di risorsa HL7 FHIR</span><span class="sxs-lookup"><span data-stu-id="0dba6-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="0dba6-158">Valore booleano: Avvia dall'inizio</span><span class="sxs-lookup"><span data-stu-id="0dba6-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="0dba6-159">Int: Numero di documenti restituiti</span><span class="sxs-lookup"><span data-stu-id="0dba6-159">Int: Number of documents returned</span></span>

<span data-ttu-id="0dba6-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="0dba6-160">**Outputs**</span></span>
- <span data-ttu-id="0dba6-161">Operazione riuscita: Codice di stato: 200, Risposta: Elenco di documenti (matrice JSON)</span><span class="sxs-lookup"><span data-stu-id="0dba6-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="0dba6-162">Errore: Codice di stato: 404, Risposta: "No Documents found for '*resource name'* Resource Type" (Nessun documento trovato per il tipo di risorsa "nome risorsa")</span><span class="sxs-lookup"><span data-stu-id="0dba6-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="0dba6-163">**Origine per l'app per le API**</span><span class="sxs-lookup"><span data-stu-id="0dba6-163">**Source for the API app**</span></span>

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
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
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

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="0dba6-164">Test di FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="0dba6-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="0dba6-165">Nell'immagine seguente viene illustrato l'uso di Swagger per testare [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="0dba6-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![Il file Swagger utilizzato per testare l'app per le API](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="0dba6-167">Dashboard del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0dba6-167">Azure portal dashboard</span></span>

<span data-ttu-id="0dba6-168">L'immagine seguente mostra tutti i servizi di Azure per questa soluzione in esecuzione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0dba6-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![Il portale di Azure con tutti i servizi usati in questa esercitazione HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="0dba6-170">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0dba6-170">Summary</span></span>

- <span data-ttu-id="0dba6-171">Si è appreso che Azure Cosmos DB dispone di supporto nativo per le notifiche per documenti nuovi o modificati, con notevole facilità d'uso.</span><span class="sxs-lookup"><span data-stu-id="0dba6-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="0dba6-172">Sfruttando le App per la logica è possibile creare flussi di lavoro senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="0dba6-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="0dba6-173">Uso delle code del bus di servizio di Azure per gestire la distribuzione dei documenti HL7 FHIR.</span><span class="sxs-lookup"><span data-stu-id="0dba6-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dba6-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0dba6-174">Next steps</span></span>
<span data-ttu-id="0dba6-175">Per altre informazioni su Azure Cosmos DB, vedere la [relativa home page](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="0dba6-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="0dba6-176">Per altre informazioni sulle App per la logica, vedere [App per la logica](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="0dba6-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


