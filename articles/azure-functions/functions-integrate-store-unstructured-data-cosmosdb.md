---
title: aaaStore dati non strutturati tramite le funzioni di Azure e Cosmos DB
description: Archiviare dati non strutturati tramite Funzioni di Azure e Cosmos DB
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, Cosmos DB, calcolo dinamico, architettura senza server
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a><span data-ttu-id="2c206-104">Archiviare dati non strutturati tramite Funzioni di Azure e Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2c206-104">Store unstructured data using Azure Functions and Cosmos DB</span></span>

<span data-ttu-id="2c206-105">[Azure DB Cosmos](https://azure.microsoft.com/services/cosmos-db/) è un ottimo modo toostore non strutturati e i dati JSON.</span><span class="sxs-lookup"><span data-stu-id="2c206-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way toostore unstructured and JSON data.</span></span> <span data-ttu-id="2c206-106">Insieme a Funzioni di Azure, Cosmos DB semplifica e velocizza l'archiviazione dei dati con una quantità minore di codice rispetto a quella necessaria per l'archiviazione dei dati in un database relazionale.</span><span class="sxs-lookup"><span data-stu-id="2c206-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

<span data-ttu-id="2c206-107">Nelle funzioni di Azure, le associazioni di input e outpue forniscono dati di servizio tooexternal tooconnect una modalità dichiarativa dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="2c206-107">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="2c206-108">In questo argomento, informazioni su come tooupdate un esistente c# funzione tooadd un'associazione di output che archivia i dati non strutturati in un documento DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2c206-108">In this topic, learn how tooupdate an existing C# function tooadd an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="2c206-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2c206-110">Prerequisites</span></span>

<span data-ttu-id="2c206-111">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="2c206-111">toocomplete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="2c206-112">Aggiungere un binding di output</span><span class="sxs-lookup"><span data-stu-id="2c206-112">Add an output binding</span></span>

1. <span data-ttu-id="2c206-113">Espandere sia l'app per le funzioni sia la funzione.</span><span class="sxs-lookup"><span data-stu-id="2c206-113">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="2c206-114">Selezionare **integrazione** e **+ nuovo Output**, ovvero hello in alto a destra della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2c206-114">Select **Integrate** and **+ New Output**, which is at hello top right of hello page.</span></span> <span data-ttu-id="2c206-115">Scegliere **Azure Cosmos DB**, quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2c206-115">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![Aggiungere un binding di output di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="2c206-117">Hello utilizzare **output Azure Cosmos DB** impostazioni come specificato nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="2c206-117">Use hello **Azure Cosmos DB output** settings as specified in hello table:</span></span> 

    ![Configurare il binding di output di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="2c206-119">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2c206-119">Setting</span></span>      | <span data-ttu-id="2c206-120">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="2c206-120">Suggested value</span></span>  | <span data-ttu-id="2c206-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2c206-121">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="2c206-122">**Nome del parametro del documento**</span><span class="sxs-lookup"><span data-stu-id="2c206-122">**Document parameter name**</span></span> | <span data-ttu-id="2c206-123">taskDocument</span><span class="sxs-lookup"><span data-stu-id="2c206-123">taskDocument</span></span> | <span data-ttu-id="2c206-124">Nome che fa riferimento a oggetto DB Cosmos toohello nel codice.</span><span class="sxs-lookup"><span data-stu-id="2c206-124">Name that refers toohello Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="2c206-125">**Database name** (Nome database)</span><span class="sxs-lookup"><span data-stu-id="2c206-125">**Database name**</span></span> | <span data-ttu-id="2c206-126">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="2c206-126">taskDatabase</span></span> | <span data-ttu-id="2c206-127">Nome del database toosave documenti.</span><span class="sxs-lookup"><span data-stu-id="2c206-127">Name of database toosave documents.</span></span> |
    | <span data-ttu-id="2c206-128">**Nome raccolta**</span><span class="sxs-lookup"><span data-stu-id="2c206-128">**Collection name**</span></span> | <span data-ttu-id="2c206-129">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="2c206-129">TaskCollection</span></span> | <span data-ttu-id="2c206-130">Nome della raccolta di database di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c206-130">Name of collection of Cosmos DB databases.</span></span> |
    | <span data-ttu-id="2c206-131">**Se true, Crea raccolta e il database DB Cosmos hello**</span><span class="sxs-lookup"><span data-stu-id="2c206-131">**If true, creates hello Cosmos DB database and collection**</span></span> | <span data-ttu-id="2c206-132">Selezionato</span><span class="sxs-lookup"><span data-stu-id="2c206-132">Checked</span></span> | <span data-ttu-id="2c206-133">raccolta di Hello non esiste già, quindi crearla.</span><span class="sxs-lookup"><span data-stu-id="2c206-133">hello collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="2c206-134">Selezionare **New** toohello Avanti **connessione documento Cosmos DB** etichetta, quindi selezionare **+ Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="2c206-134">Select **New** next toohello **Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="2c206-135">Hello utilizzare **nuovo account** impostazioni come specificato nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="2c206-135">Use hello **New account** settings as specified in hello table:</span></span> 

    ![Configurare la connessione di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="2c206-137">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2c206-137">Setting</span></span>      | <span data-ttu-id="2c206-138">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="2c206-138">Suggested value</span></span>  | <span data-ttu-id="2c206-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2c206-139">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="2c206-140">**ID**</span><span class="sxs-lookup"><span data-stu-id="2c206-140">**ID**</span></span> | <span data-ttu-id="2c206-141">Nome del database</span><span class="sxs-lookup"><span data-stu-id="2c206-141">Name of database</span></span> | <span data-ttu-id="2c206-142">ID univoco per il database DB Cosmos hello</span><span class="sxs-lookup"><span data-stu-id="2c206-142">Unique ID for hello Cosmos DB database</span></span>  |
    | <span data-ttu-id="2c206-143">**API**</span><span class="sxs-lookup"><span data-stu-id="2c206-143">**API**</span></span> | <span data-ttu-id="2c206-144">SQL (DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="2c206-144">SQL (DocumentDB)</span></span> | <span data-ttu-id="2c206-145">Selezionare l'API di database documento hello.</span><span class="sxs-lookup"><span data-stu-id="2c206-145">Select hello document database API.</span></span>  |
    | <span data-ttu-id="2c206-146">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="2c206-146">**Subscription**</span></span> | <span data-ttu-id="2c206-147">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="2c206-147">Azure Subscription</span></span> | <span data-ttu-id="2c206-148">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="2c206-148">Azure Subscription</span></span>  |
    | <span data-ttu-id="2c206-149">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="2c206-149">**Resource Group**</span></span> | <span data-ttu-id="2c206-150">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2c206-150">myResourceGroup</span></span> |  <span data-ttu-id="2c206-151">Usare gruppo di risorse esistente hello che contiene l'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="2c206-151">Use hello existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="2c206-152">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="2c206-152">**Location**</span></span>  | <span data-ttu-id="2c206-153">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="2c206-153">WestEurope</span></span> | <span data-ttu-id="2c206-154">Selezionare una posizione accanto tooeither l'app di funzione o tooother App che usano hello documenti archiviati.</span><span class="sxs-lookup"><span data-stu-id="2c206-154">Select a location near tooeither your function app or tooother apps that use hello stored documents.</span></span>  |

6. <span data-ttu-id="2c206-155">Fare clic su **OK** database hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2c206-155">Click **OK** toocreate hello database.</span></span> <span data-ttu-id="2c206-156">Potrebbe richiedere alcuni database di hello toocreate minuti.</span><span class="sxs-lookup"><span data-stu-id="2c206-156">It may take a few minutes toocreate hello database.</span></span> <span data-ttu-id="2c206-157">Dopo aver creato il database di hello, stringa di connessione database hello è archiviato come un'impostazione di app di funzione.</span><span class="sxs-lookup"><span data-stu-id="2c206-157">After hello database is created, hello database connection string is stored as a function app setting.</span></span> <span data-ttu-id="2c206-158">nome Hello di questa impostazione di app viene inserita nella **connessione ad account Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="2c206-158">hello name of this app setting is inserted in **Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="2c206-159">Dopo aver impostata la stringa di connessione hello, selezionare **salvare** associazione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2c206-159">After hello connection string is set, select **Save** toocreate hello binding.</span></span>

## <a name="update-hello-function-code"></a><span data-ttu-id="2c206-160">Aggiornare il codice di funzione hello</span><span class="sxs-lookup"><span data-stu-id="2c206-160">Update hello function code</span></span>

<span data-ttu-id="2c206-161">Sostituire hello c# funzione codice esistente con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="2c206-161">Replace hello existing C# function code with hello following code:</span></span>

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
<span data-ttu-id="2c206-162">In questo esempio di codice legge hello richiesta HTTP le stringhe di query e li assegna toofields in hello `taskDocument` oggetto.</span><span class="sxs-lookup"><span data-stu-id="2c206-162">This code sample reads hello HTTP Request query strings and assigns them toofields in hello `taskDocument` object.</span></span> <span data-ttu-id="2c206-163">Hello `taskDocument` associazione invia dati dell'oggetto hello da questo toobe di parametro di associazione archiviati nel database di hello documento associato.</span><span class="sxs-lookup"><span data-stu-id="2c206-163">hello `taskDocument` binding sends hello object data from this binding parameter toobe stored in hello bound document database.</span></span> <span data-ttu-id="2c206-164">database Hello viene creata la prima esecuzione funzione hello di hello.</span><span class="sxs-lookup"><span data-stu-id="2c206-164">hello database is created hello first time hello function runs.</span></span>

## <a name="test-hello-function-and-database"></a><span data-ttu-id="2c206-165">Funzione hello test e database</span><span class="sxs-lookup"><span data-stu-id="2c206-165">Test hello function and database</span></span>

1. <span data-ttu-id="2c206-166">Finestra di destra hello espandere e selezionare **Test**.</span><span class="sxs-lookup"><span data-stu-id="2c206-166">Expand hello right window and select **Test**.</span></span> <span data-ttu-id="2c206-167">In **Query**, fare clic su **+ Aggiungi parametro** e aggiungere hello seguente stringa di query toohello parametri:</span><span class="sxs-lookup"><span data-stu-id="2c206-167">Under **Query**, click **+ Add parameter** and add hello following parameters toohello query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="2c206-168">Fare clic su **Esegui** e verificare che venga restituito uno stato 200.</span><span class="sxs-lookup"><span data-stu-id="2c206-168">Click **Run** and verify that a 200 status is returned.</span></span>

    ![Configurare il binding di output di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="2c206-170">Hello il lato sinistro di hello portale di Azure, espandere barra delle icone hello tipo `cosmos` in hello ricerca campo e selezionare **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="2c206-170">On hello left side of hello Azure portal, expand hello icon bar, type `cosmos` in hello search field, and select **Azure Cosmos DB**.</span></span>

    ![Cercare hello servizio Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="2c206-172">Database selezionare hello è stato creato, quindi selezionare **Esplora dati**.</span><span class="sxs-lookup"><span data-stu-id="2c206-172">Select hello database you created, then select **Data Explorer**.</span></span> <span data-ttu-id="2c206-173">Espandere hello **raccolte** nodi, selezionare nuovo documento hello e verificare che il documento hello contiene i valori di stringa di query, con alcuni metadati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="2c206-173">Expand hello **Collections** nodes, select hello new document, and confirm that hello document contains your query string values, along with some additional metadata.</span></span> 

    ![Verificare la voce di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="2c206-175">È stato aggiunto correttamente un trigger HTTP tooyour di associazione che contiene dati non strutturati in un database DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2c206-175">You have successfully added a binding tooyour HTTP trigger that stores unstructured data in a Cosmos DB database.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="2c206-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c206-176">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="2c206-177">Per ulteriori informazioni sul binding tooa DB Cosmos database, vedere [associazioni Azure funzioni Cosmos DB](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="2c206-177">For more information about binding tooa Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>
