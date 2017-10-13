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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Usare MongoChef con un account Azure Cosmos DB: API per MongoDB

Per connettersi a un account dell'API Azure Cosmos DB: per MongoDB, seguire questa procedura:

* Scaricare e installare [MongoChef](http://3t.io/mongochef)
* Verificare che siano disponibili le informazioni sulla [stringa di connessione](connect-mongodb-account.md) dell'account Azure Cosmos DB: API per MongoDB

## <a name="create-the-connection-in-mongochef"></a>Creare la connessione in MongoChef
Per aggiungere l'account Azure Cosmos DB: API per MongoDB allo strumento di gestione della connessione MongoChef, seguire questa procedura.

1. Recuperare le informazioni sulla connessione di Azure Cosmos DB: API per MongoDB usando le istruzioni riportate [qui](connect-mongodb-account.md).

    ![Screenshot del pannello Stringa di connessione](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Fare clic su **Connect** (Connetti) per aprire la gestione connessioni, quindi fare clic su **New Connection** (Nuova connessione)

    ![Screenshot di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. Nella finestra **New Connection** (Nuova connessione), nella scheda **Server**, specificare l'host (nome di dominio completo) dell'account Azure Cosmos DB: API per MongoDB e la porta.

    ![Screenshot della scheda relativa al server di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. Nella finestra **New Connection** (Nuova connessione) nella scheda **Authentication** (Autenticazione) scegliere la modalità di autenticazione **Standard (MONGODB-CR or SCARM-SHA-1)** (Standard - MONGODB-CR o SCARM-SHA-1) e immettere il nome utente e la password.  Accettare il database di autenticazione predefinito (admin) o specificare un valore personalizzato.

    ![Screenshot della scheda relativa all'autenticazione di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. Nella finestra **New Connection** (Nuova connessione) nella scheda **SSL** selezionare la casella di controllo **Use SSL protocol to connect** (Usa protocollo SSL per la connessione) e quindi selezionare il pulsante di opzione **Accept server self-signed SSL certificates** (Accetta certificati SSL autofirmati server).

    ![Screenshot della scheda relativa a SSL di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Fare clic sul pulsante **Test Connection** (Test connessione) per convalidare le informazioni di connessione, quindi fare clic su **OK** per tornare alla finestra New Connection (Nuova connessione) e infine su **Save** (Salva).

    ![Screenshot della scheda relativa al test della connessione di MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a>Usare MongoChef per creare un database, una raccolta e documenti
Per creare un database, una raccolta e documenti usando MongoChef, seguire questa procedura.

1. In **Connection Manager** (Gestione connessioni) evidenziare la connessione e fare clic su **Connect** (Connetti).

    ![Screenshot di gestione connessione di MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. Fare clic con il pulsante destro del mouse sull'host, quindi scegliere **Add Database**(Aggiungi database).  Specificare un nome per il database e fare clic su **OK**.

    ![Screenshot dell'opzione di aggiunta database di MongoChef](./media/mongodb-mongochef/AddDatabase1.png)
3. Fare clic con il pulsante destro del mouse sul database, quindi scegliere **Add Collection**(Aggiungi raccolta).  Specificare un nome per la raccolta, quindi fare clic su **Create**(Crea).

    ![Screenshot dell'opzione di aggiunta raccolta di MongoChef](./media/mongodb-mongochef/AddCollection.png)
4. Selezionare la voce di menu **Collection** (Raccolta), quindi fare clic su **Add Document** (Aggiungi documento).

    ![Screenshot della voce di menu di aggiunta documento di MongoChef](./media/mongodb-mongochef/AddDocument1.png)
5. Nella finestra di dialogo Add Document (Aggiungi documento) incollare quanto segue, quindi fare clic su **Add Document**(Aggiungi documento).

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
6. Aggiungere un altro documento, questa volta con il contenuto seguente.

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
7. Eseguire una query di esempio. Cercare ad esempio famiglie con cognome 'Andersen' e restituire i campi relativi a genitori e stato.

    ![Screenshot dei risultati della query di MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Passaggi successivi
* Esaminare gli [esempi](mongodb-samples.md) di Azure Cosmos DB: API per MongoDB.
