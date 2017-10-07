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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Segnalare ai pazienti le modifiche delle cartelle cliniche HL7 FHIR utilizzando le App per la logica e Azure Cosmos DB

Azure MVP Howard Edidin recentemente è stato contattato da un'organizzazione sanitaria che voleva tooadd nuovo funzionalità tootheir paziente portale. Se necessari toosend toopatients di notifiche quando i record di integrità è stato aggiornato, e sono necessari aggiornamenti toothese toosubscribe in grado di pazienti toobe. 

In questo articolo vengono esaminati hello Modifica notifica feed soluzione creata per questa organizzazione sanitaria usando Azure Cosmos DB, App per la logica e Bus di servizio. 

## <a name="project-requirements"></a>Requisiti del progetto
- I provider inviano documenti HL7 Consolidated-Clinical Document Architecture (C-CDA) in formato XML. I documenti C-CDA comprendono sostanzialmente ogni tipo di documento clinico, incluse informazioni familiari e registri immunologici, oltre a documenti amministrati, finanziari e su flussi di lavoro. 
- Documenti C CDA vengono convertiti troppo[HL7 FHIR risorse](http://hl7.org/fhir/2017Jan/resourcelist.html) in formato JSON.
- I documenti di risorse FHIR modificati vengono inviati via e-mail in formato JSON.

## <a name="solution-workflow"></a>Flusso di lavoro della soluzione 

In generale, il progetto di hello necessario hello del flusso di lavoro come segue: 
1. Convertire le risorse di C CDA documenti tooFHIR.
2. Eseguire un trigger ricorrente per il polling di risorse FHIR modificate. 
2. Chiamare un'app personalizzata, FhirNotificationApi, tooconnect tooAzure Cosmos DB e una query per i documenti nuovi o modificati.
3. Salvare una coda di Service Bus tootoohello risposta hello.
4. Esegue il polling per nuovi messaggi nella coda di Service Bus hello.
5. Inviare toopatients le notifiche di posta elettronica.

## <a name="solution-architecture"></a>Architettura della soluzione
Questa soluzione richiede tre hello toomeet di App per la logica sopra i requisiti e del flusso di lavoro soluzione hello completo. Hello tre logica App sono:
1. **Mapping di FHIR HL7 app**: riceve hello HL7 C-CDA documento, lo trasforma toohello FHIR risorse, quindi Salva tooAzure DB Cosmos.
2. **App EHR**: query repository Azure Cosmos DB FHIR hello e Salva una coda di Service Bus tooa risposta hello. Questa app logica Usa un [app per le API](#api-app) tooretrieve nuove e modificate documenti.
3. **Processo notifica app**: invia una notifica di posta elettronica con i documenti della risorsa FHIR hello nel corpo di hello.

![Hello tre App per la logica utilizzata in questa soluzione sanitaria FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Servizi Azure utilizzati nella soluzione hello

#### <a name="azure-cosmos-db-documentdb-api"></a>API DocumentDB di Azure Cosmos DB
DB Cosmos Azure è il repository di hello per le risorse FHIR hello come illustrato nella seguente illustrazione hello.

![account di Azure Cosmos DB Hello utilizzato in questa esercitazione sanitaria FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>App per la logica
App per la logica di gestire il processo di flusso di lavoro hello. Hello schermate seguenti mostrano hello logica App creata per questa soluzione. 


1. **Mapping di FHIR HL7 app**: ricevere documento HL7 C-CDA hello e trasformarlo risorsa FHIR tooan usando hello Enterprise Integration Pack per le applicazioni di logica. Hello Enterprise Integration Pack gestisce il mapping da hello risorse tooFHIR C CDA hello.

    ![Hello App per la logica utilizzata record sanitari di tooreceive FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **App EHR**: Query repository Azure Cosmos DB FHIR hello e salvare hello risposta tooa Bus di servizio della coda. codice Hello per app GetNewOrModifiedFHIRDocuments hello è inferiore.

    ![tooquery logica App usata Hello Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **Processo notifica app**: inviare una notifica di posta elettronica con i documenti di risorse FHIR hello nel corpo di hello.

    ![App per la logica che invia posta elettronica del paziente con risorse HL7 FHIR hello nel corpo di hello Hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Bus di servizio
Hello nella seguente figura mostra hello pazienti coda. Hello valore della proprietà Tag viene utilizzato per l'oggetto messaggio di posta elettronica hello.

![Hello utilizzati in questa esercitazione HL7 FHIR coda di Service Bus](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>App per le API
Un'app per le API si connette tooAzure DB Cosmos e query per documenti FHIR nuovi o modificati dal tipo di risorsa. Questa applicazione dispone di un controller, **FhirNotificationApi** con una unica operazione **GetNewOrModifiedFhirDocuments**, vedere l'[origine di app per le API](#api-app-source).

Si sta usando hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) classe da hello API .NET di Azure Cosmos DB DocumentDB. Per ulteriori informazioni, vedere hello [modifica feed articolo](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>Operazione GetNewOrModifiedFhirDocuments

**Input**
- DatabaseId
- CollectionId
- Nome del tipo di risorsa HL7 FHIR
- Valore booleano: Avvia dall'inizio
- Int: Numero di documenti restituiti

**Outputs**
- Operazione riuscita: Codice di stato: 200, Risposta: Elenco di documenti (matrice JSON)
- Errore: Codice di stato: 404, Risposta: "No Documents found for '*resource name'* Resource Type" (Nessun documento trovato per il tipo di risorsa "nome risorsa")

<a id="api-app-source"></a>

**Origine per l'applicazione hello API**

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

### <a name="testing-hello-fhirnotificationapi"></a>Test hello FhirNotificationApi 

Hello immagine riportata di seguito viene illustrato come è stato utilizzato tootootest hello swagger [FhirNotificationApi](#api-app-source).

![file Swagger Hello utilizzato tootest hello API app](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Dashboard del portale di Azure

Hello seguente immagine vengono mostrati tutti di hello servizi di Azure per questa soluzione in esecuzione in hello portale di Azure.

![portale di Azure con tutti i servizi di hello utilizzati in questa esercitazione HL7 FHIR Hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Riepilogo

- Si è appreso che DB Cosmos Azure dispone di supporto nativo per le notifiche per il nuovo o modificato documenti e quanto sia facile toouse. 
- Sfruttando le App per la logica è possibile creare flussi di lavoro senza scrivere codice.
- Utilizzo della distribuzione di hello toohandle code di Azure Service Bus per i documenti di HL7 FHIR hello.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su Azure Cosmos DB, vedere hello [home page di Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). Per altre informazioni sulle App per la logica, vedere [App per la logica](https://azure.microsoft.com/services/logic-apps/).


