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
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB: importare i dati di MongoDB 

dati toomigrate da tooan MongoDB Azure Cosmos DB account per l'utilizzo con hello API per MongoDB, è necessario:

* Scaricare uno *mongoimport.exe* o *mongorestore.exe* da hello [area Download di MongoDB](https://www.mongodb.com/download-center).
* Ottenere l'[API per la stringa di connessione di MongoDB](connect-mongodb-account.md).

Se si importano dati da toouse MongoDB e un piano con hello Azure Cosmos DB, è necessario utilizzare hello [dello strumento di migrazione dei dati](import-data.md) tooimport dati.

Questa esercitazione sono trattati hello seguenti attività:

> [!div class="checklist"]
> * Recupero della stringa di connessione
> * Importazione di dati di MongoDB tramite mongoimport
> * Importazione di dati di MongoDB tramite mongorestore

## <a name="prerequisites"></a>Prerequisiti

* Aumentare la velocità effettiva: durata hello del processo di migrazione dei dati dipende dalla quantità di hello di velocità effettiva è impostare per le raccolte. Essere certi della velocità effettiva hello tooincrease per le migrazioni di dati più grande. Dopo aver completato la migrazione di hello, ridurre i costi IT toosave di velocità effettiva di hello. Per ulteriori informazioni su come aumentare la velocità effettiva in hello [portale di Azure](https://portal.azure.com), vedere [livelli di prestazioni e i piani tariffari nel database di Azure Cosmos](performance-levels.md).

* Abilitare SSL: Azure Cosmos DB ha standard e requisiti di sicurezza restrittivi. Essere tooenable che SSL quando si interagisce con l'account. le routine di Hello rest hello dell'articolo hello includono come tooenable SSL per mongoimport e mongorestore.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>Trovare le informazioni della stringa di connessione (host, porta, nome utente e password)

1. In hello [portale di Azure](https://portal.azure.com)in hello riquadro sinistro, fare clic su hello **Azure Cosmos DB** voce.
2. In hello **sottoscrizioni** riquadro, selezionare il nome dell'account.
3. In hello **stringa di connessione** pannello, fare clic su **stringa di connessione**.  
Hello destra riquadro contiene tutte le informazioni che è necessario toosuccessfully hello connettersi tooyour account.

    ![Pannello Stringa di connessione](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Importare dati toohello API per MongoDB con mongoimport

tooimport dati tooyour account Azure Cosmos DB, utilizzare hello seguente modello. Compilare *host*, *username*, e *password* con i valori hello tooyour specifici account.  

Template:

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

Esempio:  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Importare dati toohello API per MongoDB con mongorestore

toorestore dati tooyour API per conto di MongoDB, utilizzare hello dopo l'importazione dei modelli di hello tooexecute. Compilare *host*, *username*, e *password* con i valori hello tooyour specifici account.

Template:

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

Esempio:

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>Guida per una migrazione corretta

1. Creare in anticipo le raccolte e ridimensionarle:
        
    * Per impostazione predefinita, Azure Cosmos DB effettua il provisioning di una nuova raccolta MongoDB con 1.000 unità richiesta (UR). Prima di iniziare la migrazione di hello tramite mongoimport, mongorestore o mongomirror, creazione preliminare di tutte le raccolte di hello [portale di Azure](https://portal.azure.com) o da strumenti e driver di MongoDB. Se la raccolta è maggiore di 10 GB, assicurarsi che toocreate un [raccolta partizionata/partizionata](partition-data.md) con una chiave di partizione appropriato.

    * Da hello [portale di Azure](https://portal.azure.com), aumentare la velocità effettiva degli insiemi di 1.000 RUs per una raccolta di sola partizione e 2.500 RUs per una raccolta partizionata solo per la migrazione di hello. Con hello una velocità effettiva, è possibile evitare la limitazione delle richieste e la migrazione in meno tempo. Con fatturazione oraria nel database Cosmos di Azure, è possibile ridurre la velocità effettiva hello subito dopo i costi di migrazione toosave hello.

2. Calcolare hello RU ricarica per la scrittura di un singolo documento:

    a. Collegare database Azure Cosmos DB MongoDB tooyour hello MongoDB Shell. È possibile trovare istruzioni [connettersi una tooAzure applicazione MongoDB Cosmos DB](connect-mongodb-account.md).
    
    b. Eseguire un comando di inserimento di esempio utilizzando uno dei documenti di esempio da hello MongoDB Shell:
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. Eseguire ```db.runCommand({getLastRequestStatistics: 1})``` e si riceverà una risposta simile alla seguente:
     
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
        
    d. Prendere nota dei costi di hello richiesta.
    
3. Determinare la latenza di hello dal toohello macchina servizio cloud Azure Cosmos DB:
    
    a. Abilitare la registrazione dettagliata dalla Shell di MongoDB hello tramite questo comando:```setVerboseShell(true)```
    
    b. Eseguire una semplice query sul database hello: ```db.coll.find().limit(1)```. Si riceverà una risposta simile alla seguente:

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. Rimuovere il documento hello inserito prima hello migrazione tooensure non sono presenti documenti duplicati. È possibile rimuovere i documenti usando questo comando: ```db.coll.remove({})```

5. Calcolare hello approssimativo *batchSize* e *numInsertionWorkers* valori:

    * Per *batchSize*, divisione hello totale provisioning RUs da RUs hello usato dalla scrittura del singolo documento nel passaggio 3.
    
    * Se calcolato hello *batchSize* < = 24, utilizzare tale numero come il *batchSize* valore.
    
    * Se calcolato hello *batchSize* > 24, hello set *batchSize* too24 valore.
    
    * Per *numInsertionWorkers* usare questa equazione: *numInsertionWorkers = (velocità effettiva con provisioning * latenza in secondi) / (dimensioni del batch * unità richiesta utilizzate per una singola operazione di scrittura)*.
        
    |Proprietà|Valore|
    |--------|-----|
    |batchSize| 24 |
    |Unità richiesta con provisioning | 10000 |
    |Latency | 0,100 s |
    |Unità richiesta addebitate per la scrittura di 1 documento | 10 UR |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (10000 UR x 0,1 s) / (24 x 10 UR) = 4,1666*

6. Eseguire il comando di migrazione finale hello:

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>Passaggi successivi

È possibile continuare l'esercitazione successiva toohello e informazioni su come tooquery dati MongoDB tramite Azure Cosmos DB. 

> [!div class="nextstepaction"]
>[Come tooquery MongoDB dati?](../cosmos-db/tutorial-query-mongodb.md)
