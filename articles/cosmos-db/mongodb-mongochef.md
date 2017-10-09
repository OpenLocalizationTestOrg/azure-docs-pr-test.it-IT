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
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Usare MongoChef con un account Azure Cosmos DB: API per MongoDB

tooconnect tooan DB Cosmos Azure: API per conto di MongoDB, è necessario:

* Scaricare e installare [MongoChef](http://3t.io/mongochef)
* Verificare che siano disponibili le informazioni sulla [stringa di connessione](connect-mongodb-account.md) dell'account Azure Cosmos DB: API per MongoDB

## <a name="create-hello-connection-in-mongochef"></a>Crea connessione hello in MongoChef
tooadd del database di Azure Cosmos: API per MongoDB account toohello MongoChef gestione connessione, eseguire hello alla procedura seguente.

1. Recuperare il database di Azure Cosmos: API delle informazioni di connessione di MongoDB mediante istruzioni hello [qui](connect-mongodb-account.md).

    ![Cattura di schermata del pannello stringa di connessione hello](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Fare clic su **Connetti** tooopen hello Connection Manager, quindi fare clic su **nuova connessione**

    ![Cattura di schermata della gestione connessione di hello MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. In hello **nuova connessione** finestra hello **Server** , immettere hello HOST (FQDN) del database di Azure Cosmos hello: API per la porta di account e hello MongoDB.

    ![Cattura di schermata della scheda di server manager connection MongoChef hello](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. In hello **nuova connessione** finestra hello **autenticazione** scheda, scegliere la modalità di autenticazione **Standard (MONGODB CR o SCARM-SHA-1)** e immettere nome utente hello e PASSWORD.  Accettare i database di autenticazione predefiniti hello (amministrazione) o fornire un valore personalizzato.

    ![Cattura di schermata della scheda di autenticazione hello MongoChef connection manager](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. In hello **nuova connessione** finestra hello **SSL** scheda, controllare hello **Usa SSL protocollo tooconnect** casella di controllo e hello **accetta server autofirmato SSL i certificati** pulsante di opzione.

    ![Cattura di schermata della scheda di hello MongoChef connessione gestione SSL](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Fare clic su hello **Test connessione** fare clic su informazioni di connessione hello toovalidate **OK** tooreturn toohello finestra nuova connessione e quindi fare clic su **salvare**.

    ![Cattura di schermata della finestra di hello MongoChef test connessione](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>Utilizzare MongoChef toocreate un database e raccolta documenti
toocreate un database, alla raccolta e documenti mediante MongoChef, eseguono hello alla procedura seguente.

1. In **Connection Manager**, evidenziare connessione hello e fare clic su **Connetti**.

    ![Cattura di schermata della gestione connessione di hello MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. Fare clic con il pulsante destro host hello e scegliere **Aggiungi Database**.  Specificare un nome per il database e fare clic su **OK**.

    ![Cattura di schermata dell'opzione di Database aggiungere MongoChef hello](./media/mongodb-mongochef/AddDatabase1.png)
3. Fare clic con il pulsante destro del database hello e scegliere **Aggiungi raccolta**.  Specificare un nome per la raccolta, quindi fare clic su **Create**(Crea).

    ![Cattura di schermata dell'opzione MongoChef Aggiungi raccolta hello](./media/mongodb-mongochef/AddCollection.png)
4. Fare clic su hello **raccolta** menu item, quindi fare clic su **Aggiungi documento**.

    ![Cattura di schermata della voce di menu Aggiungi documento MongoChef hello](./media/mongodb-mongochef/AddDocument1.png)
5. Nella finestra di dialogo Aggiungi documento hello, incollare l'esempio hello e quindi fare clic su **Aggiungi documento**.

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
6. Aggiungere un altro documento, questa volta con hello dopo contenuto.

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
7. Eseguire una query di esempio. Ad esempio, si consiglia di cercare famiglie con cognome hello 'Andersen' e gli elementi padre hello restituito e i campi di stato.

    ![Screenshot dei risultati della query di MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Passaggi successivi
* Esaminare gli [esempi](mongodb-samples.md) di Azure Cosmos DB: API per MongoDB.
