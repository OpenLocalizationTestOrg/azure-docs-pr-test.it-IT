---
title: "aaaLearn modalità di accesso nel database di Azure Cosmos toodata toosecure | Documenti Microsoft"
description: Informazioni sui concetti di controllo di accesso in Azure Cosmos DB, tra cui chiavi master, chiavi di sola lettura, utenti e autorizzazioni.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a>Protezione dei dati di accesso tooAzure Cosmos DB
In questo articolo viene fornita una panoramica di sicurezza di accesso toodata archiviato in [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).

Azure DB Cosmos utilizza due tipi di chiavi tooauthenticate utenti e fornire tooits accedere ai dati e risorse. 

|Tipo di chiave|Risorse|
|---|---|
|[Chiavi master](#master-keys) |Usate per risorse amministrative, ovvero account di database, database, utenti e autorizzazioni|
|[Token delle risorse](#resource-tokens)|Usati per le risorse dell'applicazione, ovvero raccolte, documenti, allegati, stored procedure, trigger e funzioni definite dall'utente|

<a id="master-keys"></a>

## <a name="master-keys"></a>Chiavi master 

Le chiavi master forniscono accesso toohello tutte le risorse di amministrazione hello per account di database hello. Chiavi master:  
- Fornire accesso tooaccounts, database, gli utenti e autorizzazioni. 
- Non può essere utilizzato tooprovide accesso granulare toocollections e documenti.
- Vengono creati durante la creazione di un account hello.
- Possono essere rigenerate in qualsiasi momento.

Ogni account è costituito da due chiavi master: una chiave primaria e una chiave secondaria. scopo di Hello di due chiavi è in modo che è possibile rigenerare o distribuire chiavi, che forniscono dati e account di accesso continuo tooyour. 

In aggiunta toohello due master chiavi per conto di DB Cosmos hello, sono disponibili due chiavi di sola lettura. Queste chiavi di sola lettura consentono solo operazioni di lettura sul conto hello. Le chiavi di sola lettura non consentono di accedere alle risorse di autorizzazioni tooread.

Primario, secondario di sola lettura e le chiavi master di lettura / scrittura possono essere recuperate e rigenerate usando hello portale di Azure. Per istruzioni, vedere [Visualizzare, copiare e rigenerare le chiavi di accesso](manage-account.md#keys).

![Controllo di accesso (IAM) nel portale di Azure - dimostrazione di sicurezza del database NoSQL hello](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

il processo di Hello di rotazione la chiave master è semplice. Passare a toohello tooretrieve portale Azure la chiave secondaria, quindi sostituire la chiave primaria con la chiave secondaria dell'applicazione, quindi ruotare una chiave primaria hello hello portale di Azure.

![Rotazione della chiave master nel portale di Azure - dimostrazione di sicurezza del database NoSQL hello](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>Codice di esempio toouse una chiave master

Hello nell'esempio di codice seguente viene illustrato come un database Cosmos toouse account tooinstantiate endpoint e la chiave master di un DocumentClient e creare un database. 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a>Token delle risorse

I token di risorsa forniscono l'accesso toohello risorse dell'applicazione all'interno di un database. Token delle risorse:
- Fornire accesso toospecific raccolte, le chiavi di partizione, documenti, allegati, stored procedure, trigger e funzioni definite dall'utente.
- Vengono creati quando un [utente](#users) viene concessa [autorizzazioni](#permissions) tooa di risorse.
- Vengono ricreati quando si interviene su una risorsa di autorizzazione tramite chiamata POST, GET o PUT.
- Utilizzare un token di risorsa hash costruito specificamente per l'autorizzazione, risorse e utente hello.
- Hanno un limite di tempo con un periodo di validità personalizzabile. Hello timespan valido di valore predefinito è 1 ora. Durata del token, tuttavia, può essere specificata in modo esplicito, backup tooa massimo di cinque ore.
- Fornire una provvisoria toogiving alternativo out hello master key. 
- Consentire ai client tooread, scrittura e risorse delete nell'account Cosmos DB hello in base che ha concesso le autorizzazioni di toohello.

È possibile utilizzare un token di risorsa (creando Cosmos DB utenti e autorizzazioni) quando si desidera tooprovide tooresources di accesso nel database del Cosmos account tooa client che non può essere attendibile con la chiave master di hello.  

I token di risorsa COSMOS DB forniscono un metodo alternativo che consente al client tooread, scrittura ed eliminazione risorse nell'account Cosmos DB in base sono state concesse le autorizzazioni di toohello e senza necessità di entrambi un master o leggere la chiave solo.

Di seguito è riportato un tipico modello di progettazione in base al quale i token di risorsa potrebbero essere richiesto, generati e recapitati tooclients:

1. Un servizio di livello intermedio è tooserve una foto dell'utente tooshare applicazioni per dispositivi mobili. 
2. il servizio di livello intermedio Hello abbia chiave master di hello di hello Cosmos DB account.
3. app di foto di Hello viene installato nei dispositivi mobili dell'utente finale. 
4. Account di accesso, app di foto di hello stabilisce l'identità di hello dell'utente hello con il servizio di livello intermedio hello. Questo meccanismo di stabilimento di identità è puramente backup toohello applicazione.
5. Dopo aver stabilito l'identità di hello, il servizio di livello intermedio hello richiede autorizzazioni in base all'identità hello.
6. il servizio di livello intermedio Hello invia un'app phone token toohello indietro di risorse.
7. app telefono Hello è possibile continuare toouse hello token toodirectly access DB Cosmos di risorse con le autorizzazioni di hello definite dal token della risorsa hello e per l'intervallo di hello consentita dal token della risorsa hello. 
8. Alla scadenza del token della risorsa hello, le richieste successive visualizzato un'eccezione 401 non autorizzato.  A questo punto, app telefono hello ristabilisce identità hello e richiede un nuovo token di risorsa.

    ![Flusso di lavoro dei token delle risorse di Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

Gestione e generazione dei token risorsa vengono gestite dal hello Cosmos DB librerie native client; Tuttavia, se si usa REST è necessario creare le intestazioni di richiesta/autenticazione hello. Per ulteriori informazioni sulla creazione di intestazioni di autenticazione per REST, vedere [controllo di accesso sulle risorse DB Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) o hello [codice sorgente per il SDK di](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).

Per un esempio di un servizio di livello intermedio toogenerate o del gestore di token di risorsa, vedere hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).

<a id="users"></a>

## <a name="users"></a>Utenti
Gli utenti di Cosmos DB sono associati a un database Cosmos DB.  Ogni database può contenere zero o più utenti di Cosmos DB.  Hello seguente esempio di codice viene illustrato come una risorsa utente DB Cosmos toocreate.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> Ogni utente DB Cosmos dispone di una proprietà PermissionsLink che può essere utilizzati tooretrieve hello elenco [autorizzazioni](#permissions) associato hello utente.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>Autorizzazioni
Una risorsa autorizzazione di Cosmos DB è associata a un utente di Cosmos DB.  Ogni utente può contenere zero o più autorizzazioni di Cosmos DB.  Una risorsa di autorizzazione fornisce token di sicurezza di tooa accesso hello esigenze degli utenti durante il tentativo di tooaccess una risorsa di applicazione specifico.
Sono disponibili due livelli di accesso che possono essere forniti da una risorsa di autorizzazione:

* All: hello utente dispone di autorizzazioni complete sulla risorsa hello.
* Leggere: utente hello può solo leggere il contenuto di hello della risorsa hello ma non è possibile eseguire le operazioni delete sulle risorse hello, update o scrittura.

> [!NOTE]
> In ordine toorun DB Cosmos stored procedure hello utente devono essere hello tutte le autorizzazioni per la raccolta di hello in cui hello stored procedure verrà eseguita.
> 
> 

### <a name="code-sample-toocreate-permission"></a>Autorizzazione toocreate esempio di codice

Hello nell'esempio di codice seguente viene illustrato come hello token della risorsa della risorsa di autorizzazione hello toocreate una risorsa di autorizzazione, leggere e associare le autorizzazioni di hello hello [utente](#users) creato in precedenza.

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

Se è stata specificata che una chiave di partizione per la raccolta, quindi autorizzazione hello per le risorse di raccolta, documenti e degli allegati è necessario includere anche hello ResourcePartitionKey in aggiunta toohello ResourceLink.

### <a name="code-sample-tooread-permissions-for-user"></a>Autorizzazioni tooread di esempio di codice per utente

tooeasily ottenere tutte le risorse di autorizzazione associate a un utente specifico, DB Cosmos rende disponibile un'autorizzazione feed per ogni oggetto utente.  Hello frammento di codice seguente viene illustrato come costruire un elenco di autorizzazioni autorizzazione hello tooretrieve associato hello utente creato in precedenza e creare un'istanza di un nuovo DocumentClient per conto di utente hello.

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni su sicurezza database Cosmos DB, vedere [DB Cosmos: protezione dei Database](database-security.md).
* toolearn sulla gestione delle chiavi master e di sola lettura, vedere [come un account Azure Cosmos DB toomanage](manage-account.md#keys).
* token di autorizzazione di Azure Cosmos DB tooconstruct, vedere toolearn [controllo di accesso sulle risorse di Azure Cosmos DB](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).
