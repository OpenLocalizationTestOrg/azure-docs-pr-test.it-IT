---
title: 'Azure Cosmos DB: Creare un''app Web con Xamarin e l''autenticazione di Facebook | Microsoft Docs'
description: "Visualizza un esempio di codice .NET è possibile utilizzare tooconnect tooand query Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB: Creare un'app Web con .NET, Xamarin e l'autenticazione di Facebook

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure. Verrà quindi compilare e distribuire un'app web di elenco todo basata su hello [API .NET di DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)e il motore di autorizzazione hello Azure Cosmos DB. app web di elenco attività Hello implementa un modello di dati per ogni utente che consente agli utenti toologin utilizzando Facebook Auth e gestire i propri elementi toodo.

## <a name="prerequisites"></a>Prerequisiti

Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creare un account di database

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Aggiungere una raccolta

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Ora si app clone un'API DocumentDB da github, impostare la stringa di connessione hello ed eseguirlo. Si noterà quanto sia facile toowork con i dati a livello di codice. 

1. Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.  

2. Eseguire hello seguenti repository di esempio di comando tooclone hello. 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. Aprire hello DocumentDBTodo.sln file dalla cartella samples/xamarin/UserItems/xamarin.forms hello in Visual Studio. 

## <a name="review-hello-code"></a>Esaminare il codice hello

codice Hello nella cartella Xamarin hello contiene:

* App Xamarin. applicazione Hello Archivia elementi di attività dell'utente hello in una raccolta partizionata denominata UserItems.
* API del gestore di token di risorsa. Una risorsa di Azure Cosmos DB toobroker API Web ASP.NET semplice token toohello gli utenti dell'applicazione hello connesso. I token di risorsa sono token di accesso di breve durata che forniscono app hello hello accesso toohello registrato nei dati dell'utente.

flusso di dati e l'autenticazione Hello è illustrato nel diagramma hello riportato di seguito.

* Hello UserItems raccolta viene creato con la chiave di partizione hello ' / userid'. Specifica che una chiave di partizione per una raccolta consente all'infinito tooscale Azure Cosmos DB come numero hello di utenti ed elementi aumenta.
* app Xamarin Hello consente toologin gli utenti con credenziali di Facebook.
* app Xamarin Hello utilizza l'API ResourceTokenBroker tooauthenticate token di accesso Facebook
* gestore di token Hello risorsa API autentica hello richiesta utilizzando la funzionalità di autenticazione del servizio App e richiede un token di risorsa di Azure Cosmos DB con i documenti tooall di accesso in lettura/scrittura condivisione chiave di partizione dell'utente autenticato hello.
* Gestore di token di risorsa restituisce hello risorsa toohello token client app.
* app Hello accede agli elementi di attività dell'utente hello utilizzando il token di risorsa hello.

![App elenco attività con dati di esempio](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.

1. In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**. Utilizzare i pulsanti di hello copia sul lato destro hello di hello toocopy di hello schermata URI e chiave primaria nel file Web. config hello nel passaggio successivo hello.

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-xamarin-dotnet/keys.png)

2. In Visual Studio 2017, aprire il file Web. config hello nella cartella di azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker hello. 

3. Copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderlo hello valore accountUrl hello in Web. config. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. Quindi copiare il valore di chiave primaria dal portale di hello e renderlo hello valore accountKey hello in Web.congif. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB. 

## <a name="build-and-deploy-hello-web-app"></a>Compilare e distribuire l'app web hello

1. Nel portale di Azure hello, creare una servizio App sito Web toohost hello risorse token broker API.
2. Nel portale di Azure hello, aprire il pannello Impostazioni applicazione hello del gestore di token hello risorsa sito Web API. Compilare hello seguendo le impostazioni dell'app:

    * accountUrl - URL di account Azure Cosmos DB hello dalla scheda di hello chiavi dell'account di Azure Cosmos DB.
    * accountKey - chiave master dell'account Azure Cosmos DB hello dalla scheda chiavi hello dell'account di Azure Cosmos DB.
    * Valori di databaseId e collectionId del database e della raccolta creati

3. Pubblicare hello ResourceTokenBroker soluzione tooyour creato sito Web.

4. Aprire il progetto di Xamarin hello e passare tooTodoItemManager.cs. Specificare i valori hello per accountURL, collectionId, databaseId, così come resourceTokenBrokerURL come hello url di base https per il sito Web di Service broker token risorsa hello.

5. Hello completo [come tooconfigure l'account di accesso Facebook di toouse applicazione di servizio App](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup esercitazione l'autenticazione di Facebook e configurare sito Web ResourceTokenBroker hello.

    Eseguire app Xamarin hello.

## <a name="review-slas-in-hello-azure-portal"></a>Esaminare i contratti di servizio nel portale di Azure hello

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente: 

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello appena creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa Guida rapida, si è appreso come toocreate un account Azure Cosmos DB, creare una raccolta utilizzando Esplora dati, hello e compilare e distribuire un'app Xamarin. È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi. 

> [!div class="nextstepaction"]
> [Importare dati in Azure Cosmos DB](import-data.md)
