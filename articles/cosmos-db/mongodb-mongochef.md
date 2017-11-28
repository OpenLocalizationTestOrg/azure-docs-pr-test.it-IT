---
title: Usare MongoChef per Azure Cosmos DB | Microsoft Docs
description: 'Informazioni su come usare MongoChef con un account Azure Cosmos DB: API per MongoDB'
keywords: MongoChef
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
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="3b4f2-104">Usare MongoChef con un account Azure Cosmos DB: API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="3b4f2-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="3b4f2-105">Per connettersi a un account dell'API Azure Cosmos DB: per MongoDB, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3b4f2-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="3b4f2-106">Scaricare e installare [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="3b4f2-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="3b4f2-107">Verificare che siano disponibili le informazioni sulla [stringa di connessione](connect-mongodb-account.md) dell'account Azure Cosmos DB: API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="3b4f2-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="3b4f2-108">Creare la connessione in MongoChef</span><span class="sxs-lookup"><span data-stu-id="3b4f2-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="3b4f2-109">Per aggiungere l'account Azure Cosmos DB: API per MongoDB allo strumento di gestione della connessione MongoChef, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="3b4f2-110">Recuperare le informazioni sulla connessione di Azure Cosmos DB: API per MongoDB usando le istruzioni riportate [qui](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Screenshot del pannello Stringa di connessione](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="3b4f2-112">Fare clic su **Connect** (Connetti) per aprire la gestione connessioni, quindi fare clic su **New Connection** (Nuova connessione)</span><span class="sxs-lookup"><span data-stu-id="3b4f2-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![Screenshot di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="3b4f2-114">Nella finestra **New Connection** (Nuova connessione), nella scheda **Server**, specificare l'host (nome di dominio completo) dell'account Azure Cosmos DB: API per MongoDB e la porta.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![Screenshot della scheda relativa al server di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="3b4f2-116">Nella finestra **New Connection** (Nuova connessione) nella scheda **Authentication** (Autenticazione) scegliere la modalità di autenticazione **Standard (MONGODB-CR or SCARM-SHA-1)** (Standard - MONGODB-CR o SCARM-SHA-1) e immettere il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="3b4f2-117">Accettare il database di autenticazione predefinito (admin) o specificare un valore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![Screenshot della scheda relativa all'autenticazione di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="3b4f2-119">Nella finestra **New Connection** (Nuova connessione) nella scheda **SSL** selezionare la casella di controllo **Use SSL protocol to connect** (Usa protocollo SSL per la connessione) e quindi selezionare il pulsante di opzione **Accept server self-signed SSL certificates** (Accetta certificati SSL autofirmati server).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Screenshot della scheda relativa a SSL di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="3b4f2-121">Fare clic sul pulsante **Test Connection** (Test connessione) per convalidare le informazioni di connessione, quindi fare clic su **OK** per tornare alla finestra New Connection (Nuova connessione) e infine su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![Screenshot della scheda relativa al test della connessione di MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="3b4f2-123">Usare MongoChef per creare un database, una raccolta e documenti</span><span class="sxs-lookup"><span data-stu-id="3b4f2-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="3b4f2-124">Per creare un database, una raccolta e documenti usando MongoChef, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="3b4f2-125">In **Connection Manager** (Gestione connessioni) evidenziare la connessione e fare clic su **Connect** (Connetti).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![Screenshot di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="3b4f2-127">Fare clic con il pulsante destro del mouse sull'host, quindi scegliere **Add Database**(Aggiungi database).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="3b4f2-128">Specificare un nome per il database e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-128">Provide a database name and click **OK**.</span></span>

    ![Screenshot dell'opzione di aggiunta database di MongoChef](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="3b4f2-130">Fare clic con il pulsante destro del mouse sul database, quindi scegliere **Add Collection**(Aggiungi raccolta).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="3b4f2-131">Specificare un nome per la raccolta, quindi fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-131">Provide a collection name and click **Create**.</span></span>

    ![Screenshot dell'opzione di aggiunta raccolta di MongoChef](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="3b4f2-133">Selezionare la voce di menu **Collection** (Raccolta), quindi fare clic su **Add Document** (Aggiungi documento).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![Screenshot della voce di menu di aggiunta documento di MongoChef](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="3b4f2-135">Nella finestra di dialogo Add Document (Aggiungi documento) incollare quanto segue, quindi fare clic su **Add Document**(Aggiungi documento).</span><span class="sxs-lookup"><span data-stu-id="3b4f2-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. <span data-ttu-id="3b4f2-136">Aggiungere un altro documento, questa volta con il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-136">Add another document, this time with the following content.</span></span>

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. <span data-ttu-id="3b4f2-137">Eseguire una query di esempio.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-137">Execute a sample query.</span></span> <span data-ttu-id="3b4f2-138">Cercare ad esempio famiglie con cognome 'Andersen' e restituire i campi relativi a genitori e stato.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Screenshot dei risultati della query di MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="3b4f2-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b4f2-140">Next steps</span></span>
* <span data-ttu-id="3b4f2-141">Esaminare gli [esempi](mongodb-samples.md) di Azure Cosmos DB: API per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="3b4f2-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
