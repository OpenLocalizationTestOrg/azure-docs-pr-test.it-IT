---
title: aaaUse MongoChef per Azure Cosmos DB | Documenti Microsoft
description: 'Informazioni su come toouse MongoChef con un database di Azure Cosmos: API per conto di MongoDB'
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
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="499af-104">Usare MongoChef con un account Azure Cosmos DB: API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="499af-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="499af-105">tooconnect tooan DB Cosmos Azure: API per conto di MongoDB, è necessario:</span><span class="sxs-lookup"><span data-stu-id="499af-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="499af-106">Scaricare e installare [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="499af-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="499af-107">Verificare che siano disponibili le informazioni sulla [stringa di connessione](connect-mongodb-account.md) dell'account Azure Cosmos DB: API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="499af-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="499af-108">Crea connessione hello in MongoChef</span><span class="sxs-lookup"><span data-stu-id="499af-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="499af-109">tooadd del database di Azure Cosmos: API per MongoDB account toohello MongoChef gestione connessione, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="499af-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="499af-110">Recuperare il database di Azure Cosmos: API delle informazioni di connessione di MongoDB mediante istruzioni hello [qui](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="499af-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Cattura di schermata del pannello stringa di connessione hello](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="499af-112">Fare clic su **Connetti** tooopen hello Connection Manager, quindi fare clic su **nuova connessione**</span><span class="sxs-lookup"><span data-stu-id="499af-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Cattura di schermata della gestione connessione di hello MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="499af-114">In hello **nuova connessione** finestra hello **Server** , immettere hello HOST (FQDN) del database di Azure Cosmos hello: API per la porta di account e hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="499af-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Cattura di schermata della scheda di server manager connection MongoChef hello](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="499af-116">In hello **nuova connessione** finestra hello **autenticazione** scheda, scegliere la modalità di autenticazione **Standard (MONGODB CR o SCARM-SHA-1)** e immettere nome utente hello e PASSWORD.</span><span class="sxs-lookup"><span data-stu-id="499af-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="499af-117">Accettare i database di autenticazione predefiniti hello (amministrazione) o fornire un valore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="499af-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Cattura di schermata della scheda di autenticazione hello MongoChef connection manager](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="499af-119">In hello **nuova connessione** finestra hello **SSL** scheda, controllare hello **Usa SSL protocollo tooconnect** casella di controllo e hello **accetta server autofirmato SSL i certificati** pulsante di opzione.</span><span class="sxs-lookup"><span data-stu-id="499af-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Cattura di schermata della scheda di hello MongoChef connessione gestione SSL](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="499af-121">Fare clic su hello **Test connessione** fare clic su informazioni di connessione hello toovalidate **OK** tooreturn toohello finestra nuova connessione e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="499af-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Cattura di schermata della finestra di hello MongoChef test connessione](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="499af-123">Utilizzare MongoChef toocreate un database e raccolta documenti</span><span class="sxs-lookup"><span data-stu-id="499af-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="499af-124">toocreate un database, alla raccolta e documenti mediante MongoChef, eseguono hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="499af-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="499af-125">In **Connection Manager**, evidenziare connessione hello e fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="499af-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Cattura di schermata della gestione connessione di hello MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="499af-127">Fare clic con il pulsante destro host hello e scegliere **Aggiungi Database**.</span><span class="sxs-lookup"><span data-stu-id="499af-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="499af-128">Specificare un nome per il database e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="499af-128">Provide a database name and click **OK**.</span></span>

    ![Cattura di schermata dell'opzione di Database aggiungere MongoChef hello](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="499af-130">Fare clic con il pulsante destro del database hello e scegliere **Aggiungi raccolta**.</span><span class="sxs-lookup"><span data-stu-id="499af-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="499af-131">Specificare un nome per la raccolta, quindi fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="499af-131">Provide a collection name and click **Create**.</span></span>

    ![Cattura di schermata dell'opzione MongoChef Aggiungi raccolta hello](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="499af-133">Fare clic su hello **raccolta** menu item, quindi fare clic su **Aggiungi documento**.</span><span class="sxs-lookup"><span data-stu-id="499af-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Cattura di schermata della voce di menu Aggiungi documento MongoChef hello](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="499af-135">Nella finestra di dialogo Aggiungi documento hello, incollare l'esempio hello e quindi fare clic su **Aggiungi documento**.</span><span class="sxs-lookup"><span data-stu-id="499af-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="499af-136">Aggiungere un altro documento, questa volta con hello dopo contenuto.</span><span class="sxs-lookup"><span data-stu-id="499af-136">Add another document, this time with hello following content.</span></span>

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
7. <span data-ttu-id="499af-137">Eseguire una query di esempio.</span><span class="sxs-lookup"><span data-stu-id="499af-137">Execute a sample query.</span></span> <span data-ttu-id="499af-138">Ad esempio, si consiglia di cercare famiglie con cognome hello 'Andersen' e gli elementi padre hello restituito e i campi di stato.</span><span class="sxs-lookup"><span data-stu-id="499af-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Screenshot dei risultati della query di MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="499af-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="499af-140">Next steps</span></span>
* <span data-ttu-id="499af-141">Esaminare gli [esempi](mongodb-samples.md) di Azure Cosmos DB: API per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="499af-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
