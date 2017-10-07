---
title: stringa di connessione aaaMongoDB per un account Azure Cosmos DB | Documenti Microsoft
description: Informazioni su come tooconnect il tooan app MongoDB Azure Cosmos DB account utilizzando una stringa di connessione di MongoDB.
keywords: stringa di connessione mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>Connettersi a un tooAzure applicazione MongoDB Cosmos DB
Informazioni su come tooconnect il tooan app MongoDB Azure Cosmos DB account utilizzando una stringa di connessione di MongoDB. È quindi possibile utilizzare un database di Azure Cosmos DB come dati hello archiviare per l'app di MongoDB. 

In questa esercitazione fornisce due metodi tooretrieve informazioni della stringa di connessione:

- [metodo di avvio rapido di Hello](#QuickstartConnection), per l'utilizzo con i driver .NET, Node.js, MongoDB Shell, Java e Python
- [il metodo di stringhe di connessione personalizzata Hello](#GetCustomConnection), per l'uso con altri driver

## <a name="prerequisites"></a>Prerequisiti

- Un account Azure. Se non si ha un account Azure, creare un [account Azure gratuito](https://azure.microsoft.com/free/) ora. 
- Account Azure Cosmos DB. Per istruzioni, vedere [compilare un'app web API MongoDB con .NET e hello Azure portal](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Ottenere stringa di connessione hello MongoDB con avvio rapido hello
1. In un browser Internet, accedi toohello [portale di Azure](https://portal.azure.com).
2. In hello **Azure Cosmos DB** pannello selezionare hello API per conto di MongoDB. 
3. Nel riquadro di sinistra hello del Pannello di hello account, fare clic su **avvio rapido**. 
4. Scegliere la piattaforma (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**). Se il driver o lo strumento non compare nell'elenco, ricordare che altri frammenti di codice di connessione vengono continuamente documentati. Commentare di seguito si desidera toosee. toolearn modalità di lettura, la connessione di toocraft [ottenere informazioni sulla stringa di connessione dell'account hello](#GetCustomConnection).
5. Copiare e incollare il frammento di codice hello app MongoDB.

    ![Pannello di avvio rapido](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Ottenere hello MongoDB connessione stringa toocustomize
1. In un browser Internet, accedi toohello [portale di Azure](https://portal.azure.com).
2. In hello **Azure Cosmos DB** pannello selezionare hello API per conto di MongoDB. 
3. Nel riquadro di sinistra hello del Pannello di hello account, fare clic su **stringa di connessione**. 
4. Hello **stringa di connessione** apre blade. Dispone di tutti i hello informazioni tooconnect necessarie toohello account utilizzando un driver per MongoDB, tra cui una stringa di connessione partendo.

    ![Pannello Stringa di connessione](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Requisiti della stringa di connessione
> [!Important]
> Azure Cosmos DB presenta standard e requisiti di sicurezza restrittivi. Gli account Azure Cosmos DB richiedono l'autenticazione e la comunicazione sicura tramite *SSL*. 
>
>

DB Cosmos Azure supporta hello standard MongoDB formato stringa di connessione URI, con un paio di requisiti specifici: account di Azure Cosmos DB richiedono l'autenticazione e comunicazioni protette tramite SSL. In tal caso, è formato di stringa di connessione hello:

    mongodb://username:password@host:port/[database]?ssl=true

i valori Hello di questa stringa sono disponibili in hello **stringa di connessione** pannello illustrato in precedenza:

* Nome utente (obbligatorio): nome dell'account Azure Cosmos DB.
* Password (obbligatorio): password dell'account Azure Cosmos DB.
* Host (obbligatorio): nome di dominio completo di hello account Azure Cosmos DB.
* Porta (obbligatorio): 10255.
* Database (facoltativo): utilizza database hello hello connessione. Se viene specificato alcun database, database di hello predefinito è "test".
* ssl=true (obbligatorio)

Si consideri ad esempio account hello nella hello **stringa di connessione** blade. Una stringa di connessione valida è la seguente:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[utilizzare MongoChef](mongodb-mongochef.md) con un'API DB Cosmos di Azure per conto di MongoDB.
* Esplorare hello Azure Cosmos DB API per MongoDB visualizzando [esempi](mongodb-samples.md).
