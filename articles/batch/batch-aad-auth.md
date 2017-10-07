---
title: soluzioni di servizio Azure Batch tooauthenticate aaaUse Azure Active Directory | Documenti Microsoft
description: Batch supporta Azure AD per l'autenticazione dal servizio Batch hello.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Autenticare le soluzioni del servizio Batch con Active Directory

Azure Batch supporta l'autenticazione con [Azure Active Directory][aad_about], ovvero Azure AD. Azure AD è il servizio Microsoft di gestione di identità e directory basato sul cloud e multi-tenant. Azure stesso utilizza Azure AD tooauthenticate relativi clienti, gli amministratori del servizio e gli utenti dell'organizzazione.

Quando si usa l'autenticazione di Azure AD con Azure Batch, è possibile eseguire l'autenticazione in uno dei due modi:

- Utilizzando **l'autenticazione integrata di** tooauthenticate un utente che interagisce con un'applicazione hello. Un'applicazione utilizzando l'autenticazione integrata raccoglie le credenziali dell'utente e utilizza tali credenziali tooauthenticate accedere tooBatch alle risorse.
- Utilizzando un **dell'entità servizio** tooauthenticate un'applicazione automatica. Un'entità servizio definisce criteri hello e le autorizzazioni per un'applicazione in un'applicazione hello toorepresent ordine quando accedono alle risorse in fase di esecuzione.

toolearn ulteriori informazioni su Azure AD, vedere hello [documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Modalità di allocazione pool e autenticazione

Quando si crea un account Batch, è possibile specificare dove devono essere allocati i pool creati per tale account. È possibile scegliere pool tooallocate sottoscrizione al servizio Batch predefinito hello o in una sottoscrizione utente. La scelta influisce sulla modalità di autenticazione accesso tooresources in tale account.

- **Sottoscrizione al servizio Batch**. Per impostazione predefinita, i pool di Batch vengono allocati in una sottoscrizione del servizio Batch. Se si sceglie questa opzione, è possibile autenticare accesso tooresources in quell'account con [chiave condivisa](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) o con Azure AD.
- **Sottoscrizione utente.** È possibile scegliere tooallocate pool Batch in una sottoscrizione utente specificato. Se si sceglie questa opzione, è necessario eseguire l'autenticazione con Azure AD.

## <a name="endpoints-for-authentication"></a>Endpoint per l'autenticazione

applicazioni di Batch tooauthenticate con Azure AD, è necessario tooinclude alcuni endpoint noto nel codice.

### <a name="azure-ad-endpoint"></a>Endpoint di Azure AD

Hello base endpoint autorità di Azure AD:

`https://login.microsoftonline.com/`

tooauthenticate con Azure AD, utilizzare l'endpoint con l'ID tenant hello (ID di directory). l'ID tenant Hello identifica toouse tenant di Azure AD hello per l'autenticazione. tooretrieve hello ID tenant, seguire i passaggi di hello illustrati in [ottenere l'ID del tenant hello per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> endpoint specifico del tenant Hello è obbligatorio quando si autentica utilizzando un'entità servizio. 
> 
> endpoint specifico del tenant Hello è facoltativo quando si autentica utilizzando l'autenticazione integrata, ma consigliato. Tuttavia, è possibile utilizzare anche l'endpoint comune hello Azure AD. endpoint comune Hello fornisce le credenziali generica dell'interfaccia di raccolta quando non viene fornito un tenant specifico. endpoint comuni Hello è `https://login.microsoftonline.com/common`.
>
>

Per altre informazioni sugli endpoint di Azure AD, vedere [Scenari di autenticazione per Azure AD][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Endpoint di risorse Batch

Hello utilizzare **endpoint di risorse di Azure Batch** tooacquire un token per l'autenticazione delle richieste di servizio Batch toohello:

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Registrare l'applicazione con un tenant

Hello innanzitutto usando Azure AD tooauthenticate sta registrando l'applicazione in un tenant di Azure AD. Registrazione dell'applicazione consente toocall hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) dal codice. Hello ADAL fornisce un'API per l'autenticazione con Azure AD dall'applicazione. Registrazione dell'applicazione è necessario se si prevede l'autenticazione integrata di toouse o un'entità servizio.

Quando si registra l'applicazione, è fornire informazioni relative la tooAzure applicazione Active Directory. Quindi AD Azure fornisce un ID applicazione di usare tooassociate l'applicazione con Azure AD in fase di esecuzione. vedere toolearn ulteriori informazioni su ID applicazione hello [applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister l'applicazione di Batch, seguire la procedura seguente hello in hello [aggiunta di un'applicazione](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sezione [integrazione di applicazioni con Azure Active Directory][aad_integrate]. Se si registra l'applicazione come applicazione nativa, è possibile specificare qualsiasi URI valido per hello **URI di reindirizzamento**. Non è necessario un endpoint reale toobe.

Dopo aver registrato l'applicazione, verrà visualizzato l'ID dell'applicazione hello:

![Registrare l'applicazione Batch in Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

Per altre informazioni sulla registrazione di un'applicazione con Azure AD, vedere [Scenari di autenticazione per Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Ottenere l'ID del tenant hello per Active Directory

l'ID tenant Hello identifica tenant di Azure AD hello che fornisce l'autenticazione servizi tooyour applicazione. tooget hello ID tenant, seguire questi passaggi:

1. Nel portale di Azure hello, selezionare Active Directory.
2. Fare clic su **Proprietà**.
3. Copiare il valore GUID hello fornito per l'ID di directory hello. Questo valore viene anche chiamato hello ID del tenant.

![Copiare l'ID di directory hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Usare l'autenticazione integrata

tooauthenticate con l'autenticazione integrata, è necessario toogrant toohello di tooconnect le autorizzazioni applicazione API del servizio Batch. Questo passaggio attiva le API del servizio Batch di applicazione tooauthenticate chiamate toohello con Azure AD.

Dopo aver [registrazione dell'applicazione](#register-your-application-with-an-azure-ad-tenant), seguire questi passaggi nell'hello Azure toogrant portale, servizio Batch toohello di accesso:

1. Nel riquadro di navigazione a sinistra hello di hello portale di Azure, scegliere **più servizi**, fare clic su **registrazioni di App**.
2. Ricerca per nome hello dell'applicazione nell'elenco di hello di registrazioni di app:

    ![Cercare il nome dell'applicazione](./media/batch-aad-auth/search-app-registration.png)

3. Aprire hello **impostazioni** pannello per l'applicazione. In hello **l'accesso all'API** selezionare **delle autorizzazioni necessarie**.
4. In hello **delle autorizzazioni necessarie** pannello, fare clic su hello **Aggiungi** pulsante.
5. Nel passaggio 1, cercare hello API Batch. Fino a individuare hello API di ricerca per ognuna di queste stringhe:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. I tenant di Azure AD più recenti potrebbero usare questo nome.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** ID hello per hello API Batch. 
6. Dopo aver individuato hello API Batch, selezionarlo e fare clic su hello **selezionare** pulsante.
6. Nel passaggio 2, selezionare hello casella di controllo accanto troppo**servizio di accesso Azure Batch** e fare clic su hello **selezionare** pulsante.
7. Fare clic su hello **eseguita** pulsante.

Hello **autorizzazioni obbligatorie** pannello indica che l'applicazione Azure AD dispone di accesso tooboth ADAL e hello API del servizio Batch. Le autorizzazioni vengono concesse tooADAL automaticamente quando si innanzitutto registrare l'applicazione con Azure AD.

![Concedere le autorizzazioni delle API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Usare un’entità servizio 

tooauthenticate un'applicazione in esecuzione automatica, utilizzare un'entità servizio. Dopo aver registrato l'applicazione, seguire questi passaggi in hello tooconfigure portale Azure un'entità servizio:

1. Richiedere una chiave privata per l'applicazione.
2. Assegnare un'applicazione di tooyour RBAC ruolo.

### <a name="request-a-secret-key-for-your-application"></a>Richiedere una chiave privata per l'applicazione

Quando l'applicazione esegue l'autenticazione con un'entità servizio, Invia ID applicazione hello sia un tooAzure chiave segreta Active Directory. Si sarà necessario toocreate e copiare toouse chiave segreta hello dal codice.

Seguire questi passaggi in hello portale di Azure:

1. Nel riquadro di navigazione a sinistra hello di hello portale di Azure, scegliere **più servizi**, fare clic su **registrazioni di App**.
2. Ricerca per nome hello dell'applicazione nell'elenco di hello di registrazioni di app.
3. Hello visualizzazione **impostazioni** blade. In hello **l'accesso all'API** selezionare **chiavi**.
4. toocreate una chiave, immettere una descrizione per la chiave di hello. Selezionare una durata per la chiave hello di uno o due anni. 
5. Fare clic su hello **salvare** pulsante toocreate e visualizzare la chiave di hello. Copiare il luogo sicuro tooa valore chiave hello, poiché non sarà in grado di tooaccess nuovamente dopo averlo lasciare pannello hello. 

    ![Creare una chiave privata](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>Assegnare un'applicazione di tooyour RBAC ruolo

tooauthenticate con un'entità servizio, è necessario tooassign un'applicazione di tooyour RBAC ruolo. A tale scopo, seguire questa procedura:

1. Nel portale di Azure hello, passare l'account Batch toohello utilizzati dall'applicazione.
2. In hello **impostazioni** pannello per l'account Batch hello, selezionare **il controllo di accesso (IAM)**.
3. Fare clic su hello **Aggiungi** pulsante. 
4. Da hello **ruolo** elenco a discesa, selezionare entrambi hello _collaboratore_ o _lettore_ ruolo per l'applicazione. Per ulteriori informazioni su questi ruoli, vedere [Introduzione a controllo di accesso basato sui ruoli nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md).  
5. In hello **selezionare** immettere nome hello dell'applicazione. Selezionare l'applicazione hello elenco e fare clic su **salvare**.

L'applicazione dovrebbe ora essere visualizzata nelle impostazioni di controllo di accesso con un ruolo con controllo degli accessi in base al ruolo assegnato. 

![Assegnare un'applicazione di tooyour RBAC ruolo](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Ottenere l'ID del tenant hello per Azure Active Directory

l'ID tenant Hello identifica tenant di Azure AD hello che fornisce l'autenticazione servizi tooyour applicazione. tooget hello ID tenant, seguire questi passaggi:

1. Nel portale di Azure hello, selezionare Active Directory.
2. Fare clic su **Proprietà**.
3. Copiare il valore GUID hello fornito per l'ID di directory hello. Questo valore viene anche chiamato hello ID del tenant.

![Copiare l'ID di directory hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Esempi di codice

esempi di codice Hello in questa sezione illustrano come tooauthenticate con Azure AD mediante l'autenticazione integrata e con un'entità servizio. .NET di utilizzare questi esempi di codice, ma i concetti di hello sono simili ad altri linguaggi.

> [!NOTE]
> Un token di autenticazione di Azure AD scade dopo un'ora. Quando si utilizza una lunga durata **BatchClient** dell'oggetto, si consiglia recuperare un token da ADAL su tooensure ogni richiesta è sempre necessario un token valido. 
>
>
> tooachieve in .NET, scrivere un metodo che recupera hello token da Azure AD e passa tale tooa metodo **BatchTokenCredentials** oggetto come un delegato. metodo delegato Hello viene chiamato su ogni richiesta toohello Batch servizio tooensure viene fornito un token valido. Per impostazione predefinita, ADAL memorizza i token nella cache, quindi un nuovo token viene recuperato da Azure AD solo quando necessario. Per altre informazioni sui token in Azure AD, vedere [Scenari di autenticazione per Azure AD][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Esempio di codice: uso dell'autenticazione integrata di Azure AD con .NET di Batch

tooauthenticate con l'autenticazione integrata da .NET di Batch, hello riferimento [.NET di Azure Batch](https://www.nuget.org/packages/Azure.Batch/) pacchetto e hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pacchetto.

Sono inclusi i seguenti hello `using` istruzioni nel codice:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Hello riferimento endpoint di Azure AD nel codice, tra cui hello tenant ID. tooretrieve hello ID tenant, seguire i passaggi di hello illustrati in [ottenere l'ID del tenant hello per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Fare riferimento a endpoint di risorse del servizio Batch hello:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Riferimento all'account Batch:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Specificare l'ID dell'applicazione hello (ID client) per l'applicazione. ID dell'applicazione Hello è disponibile tramite la registrazione dell'app nel portale di Azure hello:

```csharp
private const string ClientId = "<application-id>";
```

Copiare anche il reindirizzamento di hello URI specificato durante il processo di registrazione hello. URI specificato nel codice di reindirizzamento Hello deve corrispondere reindirizzamento hello URI fornito dall'utente durante la registrazione di un'applicazione hello:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Scrivere un token di autenticazione hello tooacquire metodo di callback da Azure AD. Hello **GetAuthenticationTokenAsync** metodo di callback illustrato di seguito chiama tooauthenticate ADAL un utente interagisce con un'applicazione hello. Hello **AcquireTokenAsync** metodo fornite dalla libreria ADAL richiede hello le loro credenziali utente e un'applicazione hello continua una volta utente hello fornisce loro (a meno che non ha già memorizzato nella cache le credenziali):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Costruire un **BatchTokenCredentials** oggetto che accetta hello delegato come parametro. Utilizzare tali tooopen credenziali un **BatchClient** oggetto. È possibile utilizzare tale **BatchClient** oggetto per le successive operazioni nel servizio Batch hello:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>Esempio di codice: uso di un'entità servizio Azure AD con Batch .NET

tooauthenticate con un'entità servizio da .NET di Batch, hello riferimento [.NET di Azure Batch](https://www.nuget.org/packages/Azure.Batch/) pacchetto e hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pacchetto.

Sono inclusi i seguenti hello `using` istruzioni nel codice:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Hello riferimento endpoint di Azure AD nel codice, tra cui hello tenant ID. Quando si usa un'entità servizio, è necessario indicare un endpoint specifico del tenant. tooretrieve hello ID tenant, seguire i passaggi di hello illustrati in [ottenere l'ID del tenant hello per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Fare riferimento a endpoint di risorse del servizio Batch hello:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Riferimento all'account Batch:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Specificare l'ID dell'applicazione hello (ID client) per l'applicazione. ID dell'applicazione Hello è disponibile tramite la registrazione dell'app nel portale di Azure hello:

```csharp
private const string ClientId = "<application-id>";
```

Specificare una chiave segreta hello copiata dal portale di Azure hello:

```csharp
private const string ClientKey = "<secret-key>";
```

Scrivere un token di autenticazione hello tooacquire metodo di callback da Azure AD. Hello **GetAuthenticationTokenAsync** il metodo di callback illustrato di seguito chiama ADAL per l'autenticazione automatica:

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Costruire un **BatchTokenCredentials** oggetto che accetta hello delegato come parametro. Utilizzare tali tooopen credenziali un **BatchClient** oggetto. È quindi possibile utilizzare che **BatchClient** oggetto per le successive operazioni nel servizio Batch hello:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su Azure AD, vedere hello [documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/). Esempi dettagliati che mostra come toouse ADAL sono disponibili in hello [esempi di codice di Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) libreria.

toolearn sulle entità servizio, vedere [applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md). toocreate un servizio principale utilizzando hello Azure portale, vedere [utilizzare portale toocreate applicazione di Active Directory e dell'entità servizio che possono accedere alle risorse](../resource-group-create-service-principal-portal.md). È anche possibile creare un'entità servizio con PowerShell o con l'interfaccia della riga di comando di Azure. 

applicazioni di gestione dei Batch tooauthenticate mediante Azure AD, vedere [soluzioni di gestione dei Batch l'autenticazione con Active Directory](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "Informazioni su Azure Active Directory"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenari di autenticazione per Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrazione di applicazioni con Azure Active Directory"
[azure_portal]: http://portal.azure.com
