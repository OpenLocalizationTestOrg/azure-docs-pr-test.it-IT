---
title: aaaUse mongoimport e mongorestore con hello Azure Cosmos DB API per MongoDB | Documenti Microsoft
description: Informazioni su come toouse mongoimport e mongorestore tooimport dati tooan API per conto di MongoDB
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="9312a-104">Azure Cosmos DB: importare i dati di MongoDB</span><span class="sxs-lookup"><span data-stu-id="9312a-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="9312a-105">dati toomigrate da tooan MongoDB Azure Cosmos DB account per l'utilizzo con hello API per MongoDB, è necessario:</span><span class="sxs-lookup"><span data-stu-id="9312a-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="9312a-106">Scaricare uno *mongoimport.exe* o *mongorestore.exe* da hello [area Download di MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="9312a-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="9312a-107">Ottenere l'[API per la stringa di connessione di MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="9312a-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="9312a-108">Se si importano dati da toouse MongoDB e un piano con hello Azure Cosmos DB, è necessario utilizzare hello [dello strumento di migrazione dei dati](import-data.md) tooimport dati.</span><span class="sxs-lookup"><span data-stu-id="9312a-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="9312a-109">Questa esercitazione sono trattati hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="9312a-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9312a-110">Recupero della stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="9312a-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="9312a-111">Importazione di dati di MongoDB tramite mongoimport</span><span class="sxs-lookup"><span data-stu-id="9312a-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="9312a-112">Importazione di dati di MongoDB tramite mongorestore</span><span class="sxs-lookup"><span data-stu-id="9312a-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9312a-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9312a-113">Prerequisites</span></span>

* <span data-ttu-id="9312a-114">Aumentare la velocità effettiva: durata hello del processo di migrazione dei dati dipende dalla quantità di hello di velocità effettiva è impostare per le raccolte.</span><span class="sxs-lookup"><span data-stu-id="9312a-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="9312a-115">Essere certi della velocità effettiva hello tooincrease per le migrazioni di dati più grande.</span><span class="sxs-lookup"><span data-stu-id="9312a-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="9312a-116">Dopo aver completato la migrazione di hello, ridurre i costi IT toosave di velocità effettiva di hello.</span><span class="sxs-lookup"><span data-stu-id="9312a-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="9312a-117">Per ulteriori informazioni su come aumentare la velocità effettiva in hello [portale di Azure](https://portal.azure.com), vedere [livelli di prestazioni e i piani tariffari nel database di Azure Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9312a-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="9312a-118">Abilitare SSL: Azure Cosmos DB ha standard e requisiti di sicurezza restrittivi.</span><span class="sxs-lookup"><span data-stu-id="9312a-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="9312a-119">Essere tooenable che SSL quando si interagisce con l'account.</span><span class="sxs-lookup"><span data-stu-id="9312a-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="9312a-120">le routine di Hello rest hello dell'articolo hello includono come tooenable SSL per mongoimport e mongorestore.</span><span class="sxs-lookup"><span data-stu-id="9312a-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="9312a-121">Trovare le informazioni della stringa di connessione (host, porta, nome utente e password)</span><span class="sxs-lookup"><span data-stu-id="9312a-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="9312a-122">In hello [portale di Azure](https://portal.azure.com)in hello riquadro sinistro, fare clic su hello **Azure Cosmos DB** voce.</span><span class="sxs-lookup"><span data-stu-id="9312a-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="9312a-123">In hello **sottoscrizioni** riquadro, selezionare il nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="9312a-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="9312a-124">In hello **stringa di connessione** pannello, fare clic su **stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="9312a-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="9312a-125">Hello destra riquadro contiene tutte le informazioni che è necessario toosuccessfully hello connettersi tooyour account.</span><span class="sxs-lookup"><span data-stu-id="9312a-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![Pannello Stringa di connessione](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="9312a-127">Importare dati toohello API per MongoDB con mongoimport</span><span class="sxs-lookup"><span data-stu-id="9312a-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="9312a-128">tooimport dati tooyour account Azure Cosmos DB, utilizzare hello seguente modello.</span><span class="sxs-lookup"><span data-stu-id="9312a-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="9312a-129">Compilare *host*, *username*, e *password* con i valori hello tooyour specifici account.</span><span class="sxs-lookup"><span data-stu-id="9312a-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="9312a-130">Template:</span><span class="sxs-lookup"><span data-stu-id="9312a-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="9312a-131">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9312a-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="9312a-132">Importare dati toohello API per MongoDB con mongorestore</span><span class="sxs-lookup"><span data-stu-id="9312a-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="9312a-133">toorestore dati tooyour API per conto di MongoDB, utilizzare hello dopo l'importazione dei modelli di hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="9312a-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="9312a-134">Compilare *host*, *username*, e *password* con i valori hello tooyour specifici account.</span><span class="sxs-lookup"><span data-stu-id="9312a-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="9312a-135">Template:</span><span class="sxs-lookup"><span data-stu-id="9312a-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="9312a-136">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9312a-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="9312a-137">Guida per una migrazione corretta</span><span class="sxs-lookup"><span data-stu-id="9312a-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="9312a-138">Creare in anticipo le raccolte e ridimensionarle:</span><span class="sxs-lookup"><span data-stu-id="9312a-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="9312a-139">Per impostazione predefinita, Azure Cosmos DB effettua il provisioning di una nuova raccolta MongoDB con 1.000 unità richiesta (UR).</span><span class="sxs-lookup"><span data-stu-id="9312a-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="9312a-140">Prima di iniziare la migrazione di hello tramite mongoimport, mongorestore o mongomirror, creazione preliminare di tutte le raccolte di hello [portale di Azure](https://portal.azure.com) o da strumenti e driver di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9312a-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="9312a-141">Se la raccolta è maggiore di 10 GB, assicurarsi che toocreate un [raccolta partizionata/partizionata](partition-data.md) con una chiave di partizione appropriato.</span><span class="sxs-lookup"><span data-stu-id="9312a-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="9312a-142">Da hello [portale di Azure](https://portal.azure.com), aumentare la velocità effettiva degli insiemi di 1.000 RUs per una raccolta di sola partizione e 2.500 RUs per una raccolta partizionata solo per la migrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="9312a-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="9312a-143">Con hello una velocità effettiva, è possibile evitare la limitazione delle richieste e la migrazione in meno tempo.</span><span class="sxs-lookup"><span data-stu-id="9312a-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="9312a-144">Con fatturazione oraria nel database Cosmos di Azure, è possibile ridurre la velocità effettiva hello subito dopo i costi di migrazione toosave hello.</span><span class="sxs-lookup"><span data-stu-id="9312a-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="9312a-145">Calcolare hello RU ricarica per la scrittura di un singolo documento:</span><span class="sxs-lookup"><span data-stu-id="9312a-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="9312a-146">a.</span><span class="sxs-lookup"><span data-stu-id="9312a-146">a.</span></span> <span data-ttu-id="9312a-147">Collegare database Azure Cosmos DB MongoDB tooyour hello MongoDB Shell.</span><span class="sxs-lookup"><span data-stu-id="9312a-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="9312a-148">È possibile trovare istruzioni [connettersi una tooAzure applicazione MongoDB Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="9312a-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="9312a-149">b.</span><span class="sxs-lookup"><span data-stu-id="9312a-149">b.</span></span> <span data-ttu-id="9312a-150">Eseguire un comando di inserimento di esempio utilizzando uno dei documenti di esempio da hello MongoDB Shell:</span><span class="sxs-lookup"><span data-stu-id="9312a-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="9312a-151">c.</span><span class="sxs-lookup"><span data-stu-id="9312a-151">c.</span></span> <span data-ttu-id="9312a-152">Eseguire ```db.runCommand({getLastRequestStatistics: 1})``` e si riceverà una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="9312a-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    <span data-ttu-id="9312a-153">d.</span><span class="sxs-lookup"><span data-stu-id="9312a-153">d.</span></span> <span data-ttu-id="9312a-154">Prendere nota dei costi di hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="9312a-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="9312a-155">Determinare la latenza di hello dal toohello macchina servizio cloud Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="9312a-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="9312a-156">a.</span><span class="sxs-lookup"><span data-stu-id="9312a-156">a.</span></span> <span data-ttu-id="9312a-157">Abilitare la registrazione dettagliata dalla Shell di MongoDB hello tramite questo comando:```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="9312a-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="9312a-158">b.</span><span class="sxs-lookup"><span data-stu-id="9312a-158">b.</span></span> <span data-ttu-id="9312a-159">Eseguire una semplice query sul database hello: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="9312a-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="9312a-160">Si riceverà una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="9312a-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="9312a-161">Rimuovere il documento hello inserito prima hello migrazione tooensure non sono presenti documenti duplicati.</span><span class="sxs-lookup"><span data-stu-id="9312a-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="9312a-162">È possibile rimuovere i documenti usando questo comando: ```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="9312a-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="9312a-163">Calcolare hello approssimativo *batchSize* e *numInsertionWorkers* valori:</span><span class="sxs-lookup"><span data-stu-id="9312a-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="9312a-164">Per *batchSize*, divisione hello totale provisioning RUs da RUs hello usato dalla scrittura del singolo documento nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="9312a-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="9312a-165">Se calcolato hello *batchSize* < = 24, utilizzare tale numero come il *batchSize* valore.</span><span class="sxs-lookup"><span data-stu-id="9312a-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="9312a-166">Se calcolato hello *batchSize* > 24, hello set *batchSize* too24 valore.</span><span class="sxs-lookup"><span data-stu-id="9312a-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="9312a-167">Per *numInsertionWorkers* usare questa equazione: *numInsertionWorkers = (velocità effettiva con provisioning * latenza in secondi) / (dimensioni del batch * unità richiesta utilizzate per una singola operazione di scrittura)*.</span><span class="sxs-lookup"><span data-stu-id="9312a-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="9312a-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9312a-168">Property</span></span>|<span data-ttu-id="9312a-169">Valore</span><span class="sxs-lookup"><span data-stu-id="9312a-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="9312a-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="9312a-170">batchSize</span></span>| <span data-ttu-id="9312a-171">24</span><span class="sxs-lookup"><span data-stu-id="9312a-171">24</span></span> |
    |<span data-ttu-id="9312a-172">Unità richiesta con provisioning</span><span class="sxs-lookup"><span data-stu-id="9312a-172">RUs provisioned</span></span> | <span data-ttu-id="9312a-173">10000</span><span class="sxs-lookup"><span data-stu-id="9312a-173">10000</span></span> |
    |<span data-ttu-id="9312a-174">Latency</span><span class="sxs-lookup"><span data-stu-id="9312a-174">Latency</span></span> | <span data-ttu-id="9312a-175">0,100 s</span><span class="sxs-lookup"><span data-stu-id="9312a-175">0.100 s</span></span> |
    |<span data-ttu-id="9312a-176">Unità richiesta addebitate per la scrittura di 1 documento</span><span class="sxs-lookup"><span data-stu-id="9312a-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="9312a-177">10 UR</span><span class="sxs-lookup"><span data-stu-id="9312a-177">10 RUs</span></span> |
    |<span data-ttu-id="9312a-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="9312a-178">numInsertionWorkers</span></span> | <span data-ttu-id="9312a-179">?</span><span class="sxs-lookup"><span data-stu-id="9312a-179">?</span></span> |
    
    <span data-ttu-id="9312a-180">*numInsertionWorkers = (10000 UR x 0,1 s) / (24 x 10 UR) = 4,1666*</span><span class="sxs-lookup"><span data-stu-id="9312a-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="9312a-181">Eseguire il comando di migrazione finale hello:</span><span class="sxs-lookup"><span data-stu-id="9312a-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="9312a-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9312a-182">Next steps</span></span>

<span data-ttu-id="9312a-183">È possibile continuare l'esercitazione successiva toohello e informazioni su come tooquery dati MongoDB tramite Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9312a-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="9312a-184">Come tooquery MongoDB dati?</span><span class="sxs-lookup"><span data-stu-id="9312a-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
