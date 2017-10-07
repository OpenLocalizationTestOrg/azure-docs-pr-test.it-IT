---
title: soluzioni di gestione dei Batch aaaUse Azure Active Directory tooauthenticate | Documenti Microsoft
description: Le applicazioni compilate con Gestione risorse di Azure e provider di risorse Batch hello l'autenticazione con Azure AD.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Autenticare le soluzioni di gestione Batch con Active Directory

Eseguire l'autenticazione con le applicazioni che chiamano il servizio di gestione di Azure Batch hello [Azure Active Directory] [ aad_about] (Azure AD). Azure AD è il servizio Microsoft di gestione di identità e directory basato sul cloud e multi-tenant. Azure stesso utilizza Azure AD per l'autenticazione hello dei relativi clienti, gli amministratori del servizio e gli utenti dell'organizzazione.

libreria gestione .NET per Batch Hello espone i tipi per l'utilizzo di account Batch, le chiavi dell'account, applicazioni e pacchetti di applicazioni. libreria gestione .NET per Batch Hello è un client di provider di risorse di Azure e viene utilizzata in combinazione con [Azure Resource Manager] [ resman_overview] toomanage queste risorse a livello di codice. Azure AD è obbligatorio tooauthenticate richieste tramite qualsiasi client di provider di risorse di Azure, incluso libreria gestione .NET per Batch hello e [Azure Resource Manager][resman_overview].

In questo articolo, è esplorare usando Azure AD tooauthenticate da applicazioni che utilizzano una libreria di gestione .NET per Batch hello. Viene illustrato come tooauthenticate toouse Azure AD un amministratore della sottoscrizione o coamministratore usando l'autenticazione integrata. Utilizziamo hello [AccountManagment] [ acct_mgmt_sample] progetto di esempio, disponibile in GitHub, toowalk mediante Azure AD con libreria di gestione .NET per Batch hello.

vedere toolearn ulteriori informazioni sull'utilizzo della libreria di gestione .NET per Batch hello ed esempio AccountManagement hello [quote alla libreria client di gestione dei Batch hello per .NET e gestire Batch account](batch-management-dotnet.md).

## <a name="register-your-application-with-azure-ad"></a>Registrare l'applicazione in Azure AD

Hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) fornisce un tooAzure interfaccia programmatica Active Directory per l'utilizzo all'interno delle applicazioni. toocall ADAL dall'applicazione, è necessario registrare l'applicazione in un tenant di Azure AD. Quando si registra l'applicazione, si fornisce ad Azure AD con informazioni sull'applicazione, inclusi un nome per il tenant di Azure AD hello. Quindi AD Azure fornisce un ID applicazione di usare tooassociate l'applicazione con Azure AD in fase di esecuzione. vedere toolearn ulteriori informazioni su ID applicazione hello [applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

hello tooregister AccountManagement applicazione di esempio, seguire i passaggi hello hello [aggiunta di un'applicazione](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sezione [integrazione di applicazioni con Azure Active Directory] [ aad_integrate]. Specificare **applicazione Client nativa** per il tipo di hello dell'applicazione. Hello settore standard OAuth 2.0 URI hello **URI di reindirizzamento** è `urn:ietf:wg:oauth:2.0:oob`. Tuttavia, è possibile specificare qualsiasi URI valido (ad esempio `http://myaccountmanagementsample`) per hello **URI di reindirizzamento**, come se non è necessario un endpoint reale toobe:

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

Dopo aver completato il processo di registrazione hello, verranno vedere ID applicazione hello e ID di oggetto (entità servizio) elencati per l'applicazione hello.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Concedere a un'applicazione hello API di gestione risorse di Azure accesso tooyour

Successivamente, sarà necessario toodelegate accesso tooyour applicazione toohello API di gestione risorse di Azure. Identificatore Hello Azure AD per hello API di gestione risorse è **API di gestione del servizio di Windows Azure**.

Seguire questi passaggi in hello portale di Azure:

1. Nel riquadro di navigazione a sinistra hello di hello portale di Azure, scegliere **più servizi**, fare clic su **registrazioni di App**, fare clic su **Aggiungi**.
2. Ricerca per nome hello dell'applicazione nell'elenco di hello di registrazioni di app:

    ![Cercare il nome dell'applicazione](./media/batch-aad-auth-management/search-app-registration.png)

3. Hello visualizzazione **impostazioni** blade. In hello **l'accesso all'API** selezionare **delle autorizzazioni necessarie**.
4. Fare clic su **Aggiungi** tooadd una nuova autorizzazione richiesta. 
5. Nel passaggio 1, immettere **API di gestione del servizio di Windows Azure**, selezionare tale API hello elenco dei risultati e fare clic su hello **selezionare** pulsante.
6. Nel passaggio 2, selezionare hello casella di controllo accanto troppo**il modello di distribuzione classica accesso Azure come utenti dell'organizzazione**, fare clic su hello **selezionare** pulsante.
7. Fare clic su hello **eseguita** pulsante.

Hello **autorizzazioni obbligatorie** pannello ora mostra che l'applicazione tooyour le autorizzazioni vengono concesse tooboth hello ADAL e le API di gestione risorse. Le autorizzazioni vengono concesse tooADAL per impostazione predefinita quando si innanzitutto registrare l'applicazione con Azure AD.

![Delegare le autorizzazioni toohello API di gestione risorse di Azure](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Endpoint di Azure Active Directory

tooauthenticate le soluzioni di gestione dei Batch con Azure AD, è necessario due endpoint noto.

- Hello **endpoint comuni di Azure AD** fornisce le credenziali quando un tenant specifico non viene fornito, come nel caso di hello dell'autenticazione integrata di interfaccia di raccolta generiche:

    `https://login.microsoftonline.com/common`

- Hello **endpoint di Azure Resource Manager** è tooacquire usato un token per l'autenticazione del servizio di gestione di richieste toohello Batch:

    `https://management.core.windows.net/`

applicazione di esempio AccountManagement Hello definisce le costanti per questi endpoint. Lasciare invariate queste costanti:

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>Fare riferimento all'ID applicazione 

L'applicazione client utilizza tooaccess di ID (anche noto tooas hello client ID) dell'applicazione hello Azure AD in fase di esecuzione. Dopo aver registrato l'applicazione nel portale di Azure hello, aggiornare l'ID applicazione di codice toouse hello fornita da Azure AD per l'applicazione registrata. Nell'applicazione di esempio AccountManagement hello, copiare l'ID applicazione da appropriata costante di hello toohello portale di Azure:

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
Copiare anche il reindirizzamento di hello URI specificato durante il processo di registrazione hello. URI specificato nel codice di reindirizzamento Hello deve corrispondere il reindirizzamento di hello URI fornito dall'utente durante la registrazione di un'applicazione hello.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Acquisire un token di autenticazione di Azure AD

Dopo aver registrare esempio AccountManagement hello nel tenant di Azure AD hello e aggiornare codice sorgente dell'esempio hello con i valori, esempio hello è pronto tooauthenticate mediante Azure AD. Quando si esegue l'esempio hello, hello ADAL tenta tooacquire un token di autenticazione. A questo punto, richiede all'utente credenziali Microsoft: 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

Dopo aver fornito le credenziali, l'applicazione di esempio hello possibile procedere toohello richieste tooissue autenticato il servizio di gestione di Batch. 

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sull'esecuzione hello [l'applicazione di esempio AccountManagement][acct_mgmt_sample], vedere [account Batch di gestione e alle quote alla libreria client di gestione dei Batch hello per .NET](batch-management-dotnet.md).

toolearn ulteriori informazioni su Azure AD, vedere hello [documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/). Esempi dettagliati che mostra come toouse ADAL sono disponibili in hello [esempi di codice di Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) libreria.

applicazioni di servizio Batch tooauthenticate mediante Azure AD, vedere [soluzioni di servizio Batch con l'autenticazione con Active Directory](batch-aad-auth.md). 


[aad_about]: ../active-directory/active-directory-whatis.md "Informazioni su Azure Active Directory"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenari di autenticazione per Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrazione di applicazioni con Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
