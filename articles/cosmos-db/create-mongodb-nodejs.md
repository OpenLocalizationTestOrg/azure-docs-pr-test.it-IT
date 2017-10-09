---
title: aaaConnect un tooAzure di app di MongoDB DB Cosmos utilizzando Node.js | Documenti Microsoft
description: Informazioni su come tooconnect un tooAzure di app Node.js MongoDB Cosmos DB esistente
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
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a>Azure Cosmos DB: Eseguire la migrazione di un'app Web MongoDB Node.js esistente 

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa Guida introduttiva illustra come toouse esistente [MongoDB](mongodb-introduction.md) app scritte in Node.js e connetterla tooyour DB Cosmos Azure database, che supporta le connessioni client di MongoDB. In altre parole, l'applicazione di Node.js riconosce solo che viene stabilita la connessione database tooa utilizzando APIs MongoDB. È trasparente toohello applicazione hello dati viene archiviato nel database di Azure Cosmos.

Al termine, si avrà un'applicazione MEAN (MongoDB, Express, AngularJS e Node.js) in esecuzione in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). 

![App MEAN.js in esecuzione nel Servizio app di Azure](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prerequisites"></a>Prerequisiti 
Inoltre tooAzure CLI, è necessario [Node.js](https://nodejs.org/) e [Git](http://www.git-scm.com/downloads) installato localmente toorun `npm` e `git` comandi.

È necessario saper usare Node.js. Questa Guida rapida non è previsto toohelp si con lo sviluppo di applicazioni Node.js in generale.

## <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.  

Eseguire hello repository di esempio hello tooclone i comandi seguenti. Il repository di esempio contiene predefinito hello [MEAN.js](http://meanjs.org/) dell'applicazione. 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Installare i pacchetti hello necessarie e avviare un'applicazione hello.

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a>Accedi tooAzure

Se si utilizza un installato CLI di Azure, accedere tooyour sottoscrizione di Azure con hello [accesso az](/cli/azure/#login) comando e seguire hello le direzioni. È possibile ignorare questo passaggio se si usa hello Shell di Cloud di Azure.

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a>Aggiungere il modulo di Azure Cosmos DB hello

Se si utilizza un installato CLI di Azure, verificare toosee se hello `cosmosdb` componente è già installato eseguendo hello `az` comando. Se `cosmosdb` è hello elenco di comandi di base, procedere toohello del comando successivo. È possibile ignorare questo passaggio se si usa hello Shell di Cloud di Azure.

Se `cosmosdb` non è in elenco di comandi di base di hello, reinstallare [CLI di Azure 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con hello [gruppo az creare](/cli/azure/group#create). Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app Web, database e account di archiviazione. 

Hello seguente viene creato un gruppo di risorse nell'area Europa occidentale hello. Scegliere un nome univoco per il gruppo di risorse hello.

Se si utilizza una Shell di Cloud di Azure, fare clic su **Provalo**, seguire hello istruzioni visualizzate toologin, quindi copiare il comando di hello nel prompt dei comandi di hello.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a>Creare un account Azure Cosmos DB

Creare un account Azure Cosmos DB con hello [cosmosdb az creare](/cli/azure/cosmosdb#create) comando.

In hello seguente comando, sostituire il proprio nome di account Azure Cosmos DB univoco in cui si vedere hello `<cosmosdb-name>` segnaposto. Questo nome univoco da utilizzare come parte dell'endpoint Azure Cosmos DB (`https://<cosmosdb-name>.documents.azure.com/`), in modo che nome hello deve toobe univoco in tutti gli account di Azure Cosmos DB in Azure. 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

Hello `--kind MongoDB` parametro consente le connessioni client di MongoDB.

Quando viene creato l'account di Azure Cosmos DB hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente. 

> [!NOTE]
> In questo esempio utilizza JSON come formato di output di hello CLI di Azure, hello predefinito. toouse output di un altro formato, vedere [Output formati per i comandi CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/format-output-azure-cli).

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a>Connettere il database dell'applicazione toohello di Node.js

In questo passaggio è connettersi MEAN.js esempio database dell'applicazione tooan DB Cosmos Azure che appena creato, utilizzando una stringa di connessione di MongoDB. 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Configurare la stringa di connessione hello nell'applicazione Node.js

Nel repository di MEAN.js aprire `config/env/local-development.js`.

Sostituire il contenuto di hello del file con hello seguente codice. Assicurarsi di tooalso sostituire hello due `<cosmosdb-name>` segnaposto con il nome dell'account Azure Cosmos DB.

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a>Recuperare la chiave hello

Nel database di Azure Cosmos DB tooan tooconnect ordine, è necessario chiave hello del database. Hello utilizzare [az cosmosdb elenco chiavi](/cli/azure/cosmosdb#list-keys) chiave primaria di comando tooretrieve hello.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

Hello CLI di Azure genera informazioni toohello simile esempio seguente. 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

Copiare il valore di hello di `primaryMasterKey`. Incollare questo hello `<primary_master_key>` in `local-development.js`.

Salvare le modifiche.

### <a name="run-hello-application-again"></a>Eseguire nuovamente l'applicazione hello.

Eseguire di nuovo `npm start`. 

```bash
npm start
```

Un messaggio di console dovrebbero ora essere che tale ambiente di sviluppo hello sia in esecuzione. 

Passare troppo`http://localhost:3000` in un browser. Fare clic su **iscrizione** in toocreate menu e riprovare superiore hello due fittizio gli utenti. 

applicazione di esempio MEAN.js Hello archivia i dati utente nel database di hello. Se hanno esito positivo e MEAN.js accede automaticamente a hello creato utente, quindi la connessione di database di Azure Cosmos funziona. 

![MEAN.js si connette correttamente tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a>Visualizzare i dati in Esplora dati

Dati archiviati da un database di Azure Cosmos sono tooview disponibili, query e esecuzione della logica di business nel portale di Azure hello.

tooview, eseguire una query e utilizzare i dati utente hello creati nel passaggio precedente hello, account di accesso toohello [portale di Azure](https://portal.azure.com) nel web browser.

Nella casella di ricerca superiore hello, digitare Azure Cosmos DB. Quando il pannello dell'account Cosmos DB si apre, selezionare l'account Cosmos DB. Nel riquadro di spostamento sinistro di hello, fare clic su Esplora dati. Espandere la raccolta nel riquadro raccolte hello e quindi è possibile visualizzare documenti hello nella raccolta di hello, eseguire query sui dati, hello e anche creare ed eseguire le stored procedure, trigger e funzioni definite dall'utente. 

![Esplora dati in hello portale di Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a>Distribuire hello Node.js applicazione tooAzure

In questo passaggio, si distribuisce il tooAzure applicazione connessa MongoDB Node.js DB Cosmos.

Si è notato che file di configurazione hello che è stato modificato in precedenza è per l'ambiente di sviluppo hello (`/config/env/local-development.js`). Quando si distribuisce il tooApp di applicazione del servizio, verrà eseguito in ambiente di produzione hello per impostazione predefinita. A questo punto, è necessario toomake hello stesso modifica il file di configurazione corrispondente di toohello.

Nel repository di MEAN.js aprire `config/env/production.js`.

In hello `db` oggetto, sostituire il valore di hello di `uri` come illustrato nel seguente esempio hello. Impossibile verificare segnaposto tooreplace hello come prima.

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> Hello `ssl=true` opzione è importante perché [DB Cosmos Azure richiede SSL](connect-mongodb-account.md#connection-string-requirements). 
>
>

In hello terminal, eseguire il commit di tutte le modifiche in Git. È possibile copiare entrambi toorun comandi insieme.

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa Guida rapida, si è appreso come un database di Azure Cosmos toocreate account e creare un insieme di MongoDB mediante Esplora dati hello. È ora possibile eseguire la migrazione il tooAzure dati MongoDB DB Cosmos.  

> [!div class="nextstepaction"]
> [Importare i dati di MongoDB in Azure Cosmos DB](mongodb-migrate.md)
