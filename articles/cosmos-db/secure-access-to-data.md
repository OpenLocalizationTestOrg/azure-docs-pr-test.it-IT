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
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="82782-103">Protezione dei dati di accesso tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="82782-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="82782-104">In questo articolo viene fornita una panoramica di sicurezza di accesso toodata archiviato in [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="82782-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="82782-105">Azure DB Cosmos utilizza due tipi di chiavi tooauthenticate utenti e fornire tooits accedere ai dati e risorse.</span><span class="sxs-lookup"><span data-stu-id="82782-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="82782-106">Tipo di chiave</span><span class="sxs-lookup"><span data-stu-id="82782-106">Key type</span></span>|<span data-ttu-id="82782-107">Risorse</span><span class="sxs-lookup"><span data-stu-id="82782-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="82782-108">Chiavi master</span><span class="sxs-lookup"><span data-stu-id="82782-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="82782-109">Usate per risorse amministrative, ovvero account di database, database, utenti e autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="82782-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="82782-110">Token delle risorse</span><span class="sxs-lookup"><span data-stu-id="82782-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="82782-111">Usati per le risorse dell'applicazione, ovvero raccolte, documenti, allegati, stored procedure, trigger e funzioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="82782-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="82782-112">Chiavi master</span><span class="sxs-lookup"><span data-stu-id="82782-112">Master keys</span></span> 

<span data-ttu-id="82782-113">Le chiavi master forniscono accesso toohello tutte le risorse di amministrazione hello per account di database hello.</span><span class="sxs-lookup"><span data-stu-id="82782-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="82782-114">Chiavi master:</span><span class="sxs-lookup"><span data-stu-id="82782-114">Master keys:</span></span>  
- <span data-ttu-id="82782-115">Fornire accesso tooaccounts, database, gli utenti e autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="82782-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="82782-116">Non può essere utilizzato tooprovide accesso granulare toocollections e documenti.</span><span class="sxs-lookup"><span data-stu-id="82782-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="82782-117">Vengono creati durante la creazione di un account hello.</span><span class="sxs-lookup"><span data-stu-id="82782-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="82782-118">Possono essere rigenerate in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="82782-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="82782-119">Ogni account è costituito da due chiavi master: una chiave primaria e una chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="82782-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="82782-120">scopo di Hello di due chiavi è in modo che è possibile rigenerare o distribuire chiavi, che forniscono dati e account di accesso continuo tooyour.</span><span class="sxs-lookup"><span data-stu-id="82782-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="82782-121">In aggiunta toohello due master chiavi per conto di DB Cosmos hello, sono disponibili due chiavi di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="82782-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="82782-122">Queste chiavi di sola lettura consentono solo operazioni di lettura sul conto hello.</span><span class="sxs-lookup"><span data-stu-id="82782-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="82782-123">Le chiavi di sola lettura non consentono di accedere alle risorse di autorizzazioni tooread.</span><span class="sxs-lookup"><span data-stu-id="82782-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="82782-124">Primario, secondario di sola lettura e le chiavi master di lettura / scrittura possono essere recuperate e rigenerate usando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="82782-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="82782-125">Per istruzioni, vedere [Visualizzare, copiare e rigenerare le chiavi di accesso](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="82782-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Controllo di accesso (IAM) nel portale di Azure - dimostrazione di sicurezza del database NoSQL hello](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="82782-127">il processo di Hello di rotazione la chiave master è semplice.</span><span class="sxs-lookup"><span data-stu-id="82782-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="82782-128">Passare a toohello tooretrieve portale Azure la chiave secondaria, quindi sostituire la chiave primaria con la chiave secondaria dell'applicazione, quindi ruotare una chiave primaria hello hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="82782-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![Rotazione della chiave master nel portale di Azure - dimostrazione di sicurezza del database NoSQL hello](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="82782-130">Codice di esempio toouse una chiave master</span><span class="sxs-lookup"><span data-stu-id="82782-130">Code sample toouse a master key</span></span>

<span data-ttu-id="82782-131">Hello nell'esempio di codice seguente viene illustrato come un database Cosmos toouse account tooinstantiate endpoint e la chiave master di un DocumentClient e creare un database.</span><span class="sxs-lookup"><span data-stu-id="82782-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

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

## <a name="resource-tokens"></a><span data-ttu-id="82782-132">Token delle risorse</span><span class="sxs-lookup"><span data-stu-id="82782-132">Resource tokens</span></span>

<span data-ttu-id="82782-133">I token di risorsa forniscono l'accesso toohello risorse dell'applicazione all'interno di un database.</span><span class="sxs-lookup"><span data-stu-id="82782-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="82782-134">Token delle risorse:</span><span class="sxs-lookup"><span data-stu-id="82782-134">Resource tokens:</span></span>
- <span data-ttu-id="82782-135">Fornire accesso toospecific raccolte, le chiavi di partizione, documenti, allegati, stored procedure, trigger e funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="82782-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="82782-136">Vengono creati quando un [utente](#users) viene concessa [autorizzazioni](#permissions) tooa di risorse.</span><span class="sxs-lookup"><span data-stu-id="82782-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="82782-137">Vengono ricreati quando si interviene su una risorsa di autorizzazione tramite chiamata POST, GET o PUT.</span><span class="sxs-lookup"><span data-stu-id="82782-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="82782-138">Utilizzare un token di risorsa hash costruito specificamente per l'autorizzazione, risorse e utente hello.</span><span class="sxs-lookup"><span data-stu-id="82782-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="82782-139">Hanno un limite di tempo con un periodo di validità personalizzabile.</span><span class="sxs-lookup"><span data-stu-id="82782-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="82782-140">Hello timespan valido di valore predefinito è 1 ora.</span><span class="sxs-lookup"><span data-stu-id="82782-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="82782-141">Durata del token, tuttavia, può essere specificata in modo esplicito, backup tooa massimo di cinque ore.</span><span class="sxs-lookup"><span data-stu-id="82782-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="82782-142">Fornire una provvisoria toogiving alternativo out hello master key.</span><span class="sxs-lookup"><span data-stu-id="82782-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="82782-143">Consentire ai client tooread, scrittura e risorse delete nell'account Cosmos DB hello in base che ha concesso le autorizzazioni di toohello.</span><span class="sxs-lookup"><span data-stu-id="82782-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="82782-144">È possibile utilizzare un token di risorsa (creando Cosmos DB utenti e autorizzazioni) quando si desidera tooprovide tooresources di accesso nel database del Cosmos account tooa client che non può essere attendibile con la chiave master di hello.</span><span class="sxs-lookup"><span data-stu-id="82782-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="82782-145">I token di risorsa COSMOS DB forniscono un metodo alternativo che consente al client tooread, scrittura ed eliminazione risorse nell'account Cosmos DB in base sono state concesse le autorizzazioni di toohello e senza necessità di entrambi un master o leggere la chiave solo.</span><span class="sxs-lookup"><span data-stu-id="82782-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="82782-146">Di seguito è riportato un tipico modello di progettazione in base al quale i token di risorsa potrebbero essere richiesto, generati e recapitati tooclients:</span><span class="sxs-lookup"><span data-stu-id="82782-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="82782-147">Un servizio di livello intermedio è tooserve una foto dell'utente tooshare applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="82782-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="82782-148">il servizio di livello intermedio Hello abbia chiave master di hello di hello Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="82782-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="82782-149">app di foto di Hello viene installato nei dispositivi mobili dell'utente finale.</span><span class="sxs-lookup"><span data-stu-id="82782-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="82782-150">Account di accesso, app di foto di hello stabilisce l'identità di hello dell'utente hello con il servizio di livello intermedio hello.</span><span class="sxs-lookup"><span data-stu-id="82782-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="82782-151">Questo meccanismo di stabilimento di identità è puramente backup toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="82782-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="82782-152">Dopo aver stabilito l'identità di hello, il servizio di livello intermedio hello richiede autorizzazioni in base all'identità hello.</span><span class="sxs-lookup"><span data-stu-id="82782-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="82782-153">il servizio di livello intermedio Hello invia un'app phone token toohello indietro di risorse.</span><span class="sxs-lookup"><span data-stu-id="82782-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="82782-154">app telefono Hello è possibile continuare toouse hello token toodirectly access DB Cosmos di risorse con le autorizzazioni di hello definite dal token della risorsa hello e per l'intervallo di hello consentita dal token della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="82782-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="82782-155">Alla scadenza del token della risorsa hello, le richieste successive visualizzato un'eccezione 401 non autorizzato.</span><span class="sxs-lookup"><span data-stu-id="82782-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="82782-156">A questo punto, app telefono hello ristabilisce identità hello e richiede un nuovo token di risorsa.</span><span class="sxs-lookup"><span data-stu-id="82782-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![Flusso di lavoro dei token delle risorse di Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="82782-158">Gestione e generazione dei token risorsa vengono gestite dal hello Cosmos DB librerie native client; Tuttavia, se si usa REST è necessario creare le intestazioni di richiesta/autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="82782-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="82782-159">Per ulteriori informazioni sulla creazione di intestazioni di autenticazione per REST, vedere [controllo di accesso sulle risorse DB Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) o hello [codice sorgente per il SDK di](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="82782-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="82782-160">Per un esempio di un servizio di livello intermedio toogenerate o del gestore di token di risorsa, vedere hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="82782-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="82782-161">Utenti</span><span class="sxs-lookup"><span data-stu-id="82782-161">Users</span></span>
<span data-ttu-id="82782-162">Gli utenti di Cosmos DB sono associati a un database Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="82782-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="82782-163">Ogni database può contenere zero o più utenti di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="82782-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="82782-164">Hello seguente esempio di codice viene illustrato come una risorsa utente DB Cosmos toocreate.</span><span class="sxs-lookup"><span data-stu-id="82782-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="82782-165">Ogni utente DB Cosmos dispone di una proprietà PermissionsLink che può essere utilizzati tooretrieve hello elenco [autorizzazioni](#permissions) associato hello utente.</span><span class="sxs-lookup"><span data-stu-id="82782-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="82782-166">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="82782-166">Permissions</span></span>
<span data-ttu-id="82782-167">Una risorsa autorizzazione di Cosmos DB è associata a un utente di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="82782-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="82782-168">Ogni utente può contenere zero o più autorizzazioni di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="82782-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="82782-169">Una risorsa di autorizzazione fornisce token di sicurezza di tooa accesso hello esigenze degli utenti durante il tentativo di tooaccess una risorsa di applicazione specifico.</span><span class="sxs-lookup"><span data-stu-id="82782-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="82782-170">Sono disponibili due livelli di accesso che possono essere forniti da una risorsa di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="82782-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="82782-171">All: hello utente dispone di autorizzazioni complete sulla risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="82782-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="82782-172">Leggere: utente hello può solo leggere il contenuto di hello della risorsa hello ma non è possibile eseguire le operazioni delete sulle risorse hello, update o scrittura.</span><span class="sxs-lookup"><span data-stu-id="82782-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="82782-173">In ordine toorun DB Cosmos stored procedure hello utente devono essere hello tutte le autorizzazioni per la raccolta di hello in cui hello stored procedure verrà eseguita.</span><span class="sxs-lookup"><span data-stu-id="82782-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="82782-174">Autorizzazione toocreate esempio di codice</span><span class="sxs-lookup"><span data-stu-id="82782-174">Code sample toocreate permission</span></span>

<span data-ttu-id="82782-175">Hello nell'esempio di codice seguente viene illustrato come hello token della risorsa della risorsa di autorizzazione hello toocreate una risorsa di autorizzazione, leggere e associare le autorizzazioni di hello hello [utente](#users) creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="82782-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

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

<span data-ttu-id="82782-176">Se è stata specificata che una chiave di partizione per la raccolta, quindi autorizzazione hello per le risorse di raccolta, documenti e degli allegati è necessario includere anche hello ResourcePartitionKey in aggiunta toohello ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="82782-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="82782-177">Autorizzazioni tooread di esempio di codice per utente</span><span class="sxs-lookup"><span data-stu-id="82782-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="82782-178">tooeasily ottenere tutte le risorse di autorizzazione associate a un utente specifico, DB Cosmos rende disponibile un'autorizzazione feed per ogni oggetto utente.</span><span class="sxs-lookup"><span data-stu-id="82782-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="82782-179">Hello frammento di codice seguente viene illustrato come costruire un elenco di autorizzazioni autorizzazione hello tooretrieve associato hello utente creato in precedenza e creare un'istanza di un nuovo DocumentClient per conto di utente hello.</span><span class="sxs-lookup"><span data-stu-id="82782-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="82782-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82782-180">Next steps</span></span>
* <span data-ttu-id="82782-181">toolearn ulteriori informazioni su sicurezza database Cosmos DB, vedere [DB Cosmos: protezione dei Database](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="82782-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="82782-182">toolearn sulla gestione delle chiavi master e di sola lettura, vedere [come un account Azure Cosmos DB toomanage](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="82782-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="82782-183">token di autorizzazione di Azure Cosmos DB tooconstruct, vedere toolearn [controllo di accesso sulle risorse di Azure Cosmos DB](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="82782-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
