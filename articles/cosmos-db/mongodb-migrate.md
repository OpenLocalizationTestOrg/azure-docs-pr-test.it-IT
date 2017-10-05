---
title: Usare mongoimport e mongorestore con l'API di Azure Cosmos DB per MongoDB | Microsoft Docs
description: Informazioni su come usare mongoimport e mongorestore per importare dati in un account dell'API per MongoDB
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
ms.openlocfilehash: 1555f13c3ea88b61be0ea240b51218b83f6f9724
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="986fe-104">Azure Cosmos DB: importare i dati di MongoDB</span><span class="sxs-lookup"><span data-stu-id="986fe-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="986fe-105">Per eseguire la migrazione di dati da MongoDB in un account Azure Cosmos DB per l'uso con l'API di MongoDB, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="986fe-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span></span>

* <span data-ttu-id="986fe-106">Scaricare *mongoimport.exe* o *mongorestore.exe* dall'[area download MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="986fe-106">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="986fe-107">Ottenere l'[API per la stringa di connessione di MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="986fe-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="986fe-108">Se si importano dati da MongoDB e si prevede di usarli con Azure Cosmos DB, è necessario usare lo [strumento di migrazione dei dati](import-data.md) per importare i dati.</span><span class="sxs-lookup"><span data-stu-id="986fe-108">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB, you should use the [Data Migration tool](import-data.md) to import data.</span></span>

<span data-ttu-id="986fe-109">Questa esercitazione illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="986fe-109">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="986fe-110">Recupero della stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="986fe-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="986fe-111">Importazione di dati di MongoDB tramite mongoimport</span><span class="sxs-lookup"><span data-stu-id="986fe-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="986fe-112">Importazione di dati di MongoDB tramite mongorestore</span><span class="sxs-lookup"><span data-stu-id="986fe-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="986fe-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="986fe-113">Prerequisites</span></span>

* <span data-ttu-id="986fe-114">Aumentare la velocità effettiva: la durata della migrazione dei dati dipende dalla quantità di velocità effettiva configurata per le raccolte.</span><span class="sxs-lookup"><span data-stu-id="986fe-114">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span></span> <span data-ttu-id="986fe-115">Assicurarsi di aumentare la velocità effettiva per le migrazioni dei dati di dimensioni più grandi.</span><span class="sxs-lookup"><span data-stu-id="986fe-115">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="986fe-116">Dopo avere completato la migrazione, diminuire la velocità effettiva per ridurre i costi.</span><span class="sxs-lookup"><span data-stu-id="986fe-116">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="986fe-117">Per altre informazioni sull'aumento della velocità effettiva nel [portale di Azure](https://portal.azure.com), vedere [Livelli di prestazioni e piani tariffari in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="986fe-117">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="986fe-118">Abilitare SSL: Azure Cosmos DB ha standard e requisiti di sicurezza restrittivi.</span><span class="sxs-lookup"><span data-stu-id="986fe-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="986fe-119">Assicurarsi di abilitare SSL quando si interagisce con l'account.</span><span class="sxs-lookup"><span data-stu-id="986fe-119">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="986fe-120">Le procedure seguenti illustrano come abilitare SSL per mongoimport e mongorestore.</span><span class="sxs-lookup"><span data-stu-id="986fe-120">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="986fe-121">Trovare le informazioni della stringa di connessione (host, porta, nome utente e password)</span><span class="sxs-lookup"><span data-stu-id="986fe-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="986fe-122">Nel riquadro sinistro del [portale di Azure](https://portal.azure.com) fare clic sulla voce **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="986fe-122">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="986fe-123">Nel riquadro **Sottoscrizioni** selezionare il nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="986fe-123">In the **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="986fe-124">Nel pannello **Stringa di connessione** fare clic su **Stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="986fe-124">In the **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="986fe-125">Il riquadro destro contiene tutte le informazioni necessarie per connettersi correttamente all'account.</span><span class="sxs-lookup"><span data-stu-id="986fe-125">The right pane contains all the information that you need to successfully connect to your account.</span></span>

    ![Pannello Stringa di connessione](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-to-the-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="986fe-127">Eseguire l'importazione di dati nell'API per MongoDB con mongoimport</span><span class="sxs-lookup"><span data-stu-id="986fe-127">Import data to the API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="986fe-128">Per importare dati nell'account Azure Cosmos DB, usare il modello seguente.</span><span class="sxs-lookup"><span data-stu-id="986fe-128">To import data to your Azure Cosmos DB account, use the following template.</span></span> <span data-ttu-id="986fe-129">Per *host*, *username* e *password* inserire i valori specifici dell'account.</span><span class="sxs-lookup"><span data-stu-id="986fe-129">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="986fe-130">Template:</span><span class="sxs-lookup"><span data-stu-id="986fe-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="986fe-131">Esempio:</span><span class="sxs-lookup"><span data-stu-id="986fe-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-to-the-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="986fe-132">Eseguire l'importazione di dati nell'API per MongoDB con mongorestore</span><span class="sxs-lookup"><span data-stu-id="986fe-132">Import data to the API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="986fe-133">Per ripristinare i dati nell'API per l'account MongoDB, usare il modello seguente per eseguire l'importazione.</span><span class="sxs-lookup"><span data-stu-id="986fe-133">To restore data to your API for MongoDB account, use the following template to execute the import.</span></span> <span data-ttu-id="986fe-134">Per *host*, *username* e *password* inserire i valori specifici dell'account.</span><span class="sxs-lookup"><span data-stu-id="986fe-134">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>

<span data-ttu-id="986fe-135">Template:</span><span class="sxs-lookup"><span data-stu-id="986fe-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="986fe-136">Esempio:</span><span class="sxs-lookup"><span data-stu-id="986fe-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="986fe-137">Guida per una migrazione corretta</span><span class="sxs-lookup"><span data-stu-id="986fe-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="986fe-138">Creare in anticipo le raccolte e ridimensionarle:</span><span class="sxs-lookup"><span data-stu-id="986fe-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="986fe-139">Per impostazione predefinita, Azure Cosmos DB effettua il provisioning di una nuova raccolta MongoDB con 1.000 unità richiesta (UR).</span><span class="sxs-lookup"><span data-stu-id="986fe-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="986fe-140">Prima di iniziare la migrazione tramite mongoimport, mongorestore o mongomirror, creare tutte le raccolte dal [portale di Azure](https://portal.azure.com) o da strumenti e driver di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="986fe-140">Before you start the migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="986fe-141">Se le dimensioni della raccolta superano 10 GB, assicurarsi di creare una [raccolta partizionata](partition-data.md) con una chiave di partizione appropriata.</span><span class="sxs-lookup"><span data-stu-id="986fe-141">If your collection is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="986fe-142">Dal [portale di Azure](https://portal.azure.com) aumentare la velocità effettiva delle raccolte da 1.000 unità richiesta per una raccolta a partizione singola e da 2.500 unità richiesta per una raccolta partizionata al solo scopo di migrazione.</span><span class="sxs-lookup"><span data-stu-id="986fe-142">From the [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for the migration.</span></span> <span data-ttu-id="986fe-143">Con una velocità effettiva più elevata, è possibile evitare la limitazione e completare più rapidamente la migrazione.</span><span class="sxs-lookup"><span data-stu-id="986fe-143">With the higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="986fe-144">Con la fatturazione oraria in Azure Cosmos DB, è possibile ridurre la velocità effettiva immediatamente dopo la migrazione per ridurre i costi.</span><span class="sxs-lookup"><span data-stu-id="986fe-144">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span></span>

2. <span data-ttu-id="986fe-145">Calcolare l'addebito approssimativo delle unità richiesta per la scrittura di un singolo documento:</span><span class="sxs-lookup"><span data-stu-id="986fe-145">Calculate the approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="986fe-146">a.</span><span class="sxs-lookup"><span data-stu-id="986fe-146">a.</span></span> <span data-ttu-id="986fe-147">Connettersi al database Azure Cosmos DB MongoDB dalla shell di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="986fe-147">Connect to your Azure Cosmos DB MongoDB database from the MongoDB Shell.</span></span> <span data-ttu-id="986fe-148">È possibile trovare istruzioni in [Connettere un'applicazione MongoDB ad Azure Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="986fe-148">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="986fe-149">b.</span><span class="sxs-lookup"><span data-stu-id="986fe-149">b.</span></span> <span data-ttu-id="986fe-150">Eseguire un comando di inserimento di esempio usando uno dei documenti di esempio dalla shell di MongoDB:</span><span class="sxs-lookup"><span data-stu-id="986fe-150">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="986fe-151">c.</span><span class="sxs-lookup"><span data-stu-id="986fe-151">c.</span></span> <span data-ttu-id="986fe-152">Eseguire ```db.runCommand({getLastRequestStatistics: 1})``` e si riceverà una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="986fe-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="986fe-153">d.</span><span class="sxs-lookup"><span data-stu-id="986fe-153">d.</span></span> <span data-ttu-id="986fe-154">Prendere nota dell'addebito della richiesta.</span><span class="sxs-lookup"><span data-stu-id="986fe-154">Take note of the request charge.</span></span>
    
3. <span data-ttu-id="986fe-155">Determinare la latenza dal proprio computer al servizio cloud Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="986fe-155">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="986fe-156">a.</span><span class="sxs-lookup"><span data-stu-id="986fe-156">a.</span></span> <span data-ttu-id="986fe-157">Abilitare la registrazione dettagliata dalla shell di MongoDB usando questo comando: ```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="986fe-157">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="986fe-158">b.</span><span class="sxs-lookup"><span data-stu-id="986fe-158">b.</span></span> <span data-ttu-id="986fe-159">Eseguire una semplice query sul database: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="986fe-159">Run a simple query against the database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="986fe-160">Si riceverà una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="986fe-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="986fe-161">Rimuovere il documento inserito prima della migrazione per verificare che non siano presenti documenti duplicati.</span><span class="sxs-lookup"><span data-stu-id="986fe-161">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span></span> <span data-ttu-id="986fe-162">È possibile rimuovere i documenti usando questo comando: ```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="986fe-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="986fe-163">Calcolare i valori *batchSize* e *numInsertionWorkers* approssimativi:</span><span class="sxs-lookup"><span data-stu-id="986fe-163">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="986fe-164">Per *batchSize* dividere le unità richiesta totali di cui è stato effettuato il provisioning per le unità richiesta consumate dalla scrittura di un singolo documento nel passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="986fe-164">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="986fe-165">Se la dimensione calcolata *batchSize* <= 24, usare questo numero come valore di *batchSize*.</span><span class="sxs-lookup"><span data-stu-id="986fe-165">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="986fe-166">Se la dimensione calcolata *batchSize* > 24, impostare il valore di *batchSize* su 24.</span><span class="sxs-lookup"><span data-stu-id="986fe-166">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span></span>
    
    * <span data-ttu-id="986fe-167">Per *numInsertionWorkers* usare questa equazione: *numInsertionWorkers = (velocità effettiva con provisioning * latenza in secondi) / (dimensioni del batch * unità richiesta utilizzate per una singola operazione di scrittura)*.</span><span class="sxs-lookup"><span data-stu-id="986fe-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="986fe-168">Proprietà</span><span class="sxs-lookup"><span data-stu-id="986fe-168">Property</span></span>|<span data-ttu-id="986fe-169">Valore</span><span class="sxs-lookup"><span data-stu-id="986fe-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="986fe-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="986fe-170">batchSize</span></span>| <span data-ttu-id="986fe-171">24</span><span class="sxs-lookup"><span data-stu-id="986fe-171">24</span></span> |
    |<span data-ttu-id="986fe-172">Unità richiesta con provisioning</span><span class="sxs-lookup"><span data-stu-id="986fe-172">RUs provisioned</span></span> | <span data-ttu-id="986fe-173">10000</span><span class="sxs-lookup"><span data-stu-id="986fe-173">10000</span></span> |
    |<span data-ttu-id="986fe-174">Latency</span><span class="sxs-lookup"><span data-stu-id="986fe-174">Latency</span></span> | <span data-ttu-id="986fe-175">0,100 s</span><span class="sxs-lookup"><span data-stu-id="986fe-175">0.100 s</span></span> |
    |<span data-ttu-id="986fe-176">Unità richiesta addebitate per la scrittura di 1 documento</span><span class="sxs-lookup"><span data-stu-id="986fe-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="986fe-177">10 UR</span><span class="sxs-lookup"><span data-stu-id="986fe-177">10 RUs</span></span> |
    |<span data-ttu-id="986fe-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="986fe-178">numInsertionWorkers</span></span> | <span data-ttu-id="986fe-179">?</span><span class="sxs-lookup"><span data-stu-id="986fe-179">?</span></span> |
    
    <span data-ttu-id="986fe-180">*numInsertionWorkers = (10000 UR x 0,1 s) / (24 x 10 UR) = 4,1666*</span><span class="sxs-lookup"><span data-stu-id="986fe-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="986fe-181">Eseguire il comando di migrazione finale:</span><span class="sxs-lookup"><span data-stu-id="986fe-181">Run the final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="986fe-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="986fe-182">Next steps</span></span>

<span data-ttu-id="986fe-183">È possibile passare all'esercitazione successiva per ottenere informazioni su come eseguire query sui dati di MongoDB tramite Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="986fe-183">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="986fe-184">Procedura per l'esecuzione di query sui dati di MongoDB</span><span class="sxs-lookup"><span data-stu-id="986fe-184">How to query MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
