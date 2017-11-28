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
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="c97a6-103">Autenticare le soluzioni di gestione Batch con Active Directory</span><span class="sxs-lookup"><span data-stu-id="c97a6-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="c97a6-104">Eseguire l'autenticazione con le applicazioni che chiamano il servizio di gestione di Azure Batch hello [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c97a6-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="c97a6-105">Azure AD è il servizio Microsoft di gestione di identità e directory basato sul cloud e multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="c97a6-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="c97a6-106">Azure stesso utilizza Azure AD per l'autenticazione hello dei relativi clienti, gli amministratori del servizio e gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c97a6-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="c97a6-107">libreria gestione .NET per Batch Hello espone i tipi per l'utilizzo di account Batch, le chiavi dell'account, applicazioni e pacchetti di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c97a6-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="c97a6-108">libreria gestione .NET per Batch Hello è un client di provider di risorse di Azure e viene utilizzata in combinazione con [Azure Resource Manager] [ resman_overview] toomanage queste risorse a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="c97a6-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="c97a6-109">Azure AD è obbligatorio tooauthenticate richieste tramite qualsiasi client di provider di risorse di Azure, incluso libreria gestione .NET per Batch hello e [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="c97a6-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="c97a6-110">In questo articolo, è esplorare usando Azure AD tooauthenticate da applicazioni che utilizzano una libreria di gestione .NET per Batch hello.</span><span class="sxs-lookup"><span data-stu-id="c97a6-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="c97a6-111">Viene illustrato come tooauthenticate toouse Azure AD un amministratore della sottoscrizione o coamministratore usando l'autenticazione integrata.</span><span class="sxs-lookup"><span data-stu-id="c97a6-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="c97a6-112">Utilizziamo hello [AccountManagment] [ acct_mgmt_sample] progetto di esempio, disponibile in GitHub, toowalk mediante Azure AD con libreria di gestione .NET per Batch hello.</span><span class="sxs-lookup"><span data-stu-id="c97a6-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="c97a6-113">vedere toolearn ulteriori informazioni sull'utilizzo della libreria di gestione .NET per Batch hello ed esempio AccountManagement hello [quote alla libreria client di gestione dei Batch hello per .NET e gestire Batch account](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c97a6-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="c97a6-114">Registrare l'applicazione in Azure AD</span><span class="sxs-lookup"><span data-stu-id="c97a6-114">Register your application with Azure AD</span></span>

<span data-ttu-id="c97a6-115">Hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) fornisce un tooAzure interfaccia programmatica Active Directory per l'utilizzo all'interno delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c97a6-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="c97a6-116">toocall ADAL dall'applicazione, è necessario registrare l'applicazione in un tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c97a6-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="c97a6-117">Quando si registra l'applicazione, si fornisce ad Azure AD con informazioni sull'applicazione, inclusi un nome per il tenant di Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="c97a6-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="c97a6-118">Quindi AD Azure fornisce un ID applicazione di usare tooassociate l'applicazione con Azure AD in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c97a6-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="c97a6-119">vedere toolearn ulteriori informazioni su ID applicazione hello [applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="c97a6-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="c97a6-120">hello tooregister AccountManagement applicazione di esempio, seguire i passaggi hello hello [aggiunta di un'applicazione](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sezione [integrazione di applicazioni con Azure Active Directory] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="c97a6-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="c97a6-121">Specificare **applicazione Client nativa** per il tipo di hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c97a6-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="c97a6-122">Hello settore standard OAuth 2.0 URI hello **URI di reindirizzamento** è `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="c97a6-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="c97a6-123">Tuttavia, è possibile specificare qualsiasi URI valido (ad esempio `http://myaccountmanagementsample`) per hello **URI di reindirizzamento**, come se non è necessario un endpoint reale toobe:</span><span class="sxs-lookup"><span data-stu-id="c97a6-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="c97a6-124">Dopo aver completato il processo di registrazione hello, verranno vedere ID applicazione hello e ID di oggetto (entità servizio) elencati per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c97a6-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="c97a6-125">Concedere a un'applicazione hello API di gestione risorse di Azure accesso tooyour</span><span class="sxs-lookup"><span data-stu-id="c97a6-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="c97a6-126">Successivamente, sarà necessario toodelegate accesso tooyour applicazione toohello API di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c97a6-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="c97a6-127">Identificatore Hello Azure AD per hello API di gestione risorse è **API di gestione del servizio di Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="c97a6-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="c97a6-128">Seguire questi passaggi in hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="c97a6-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="c97a6-129">Nel riquadro di navigazione a sinistra hello di hello portale di Azure, scegliere **più servizi**, fare clic su **registrazioni di App**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c97a6-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="c97a6-130">Ricerca per nome hello dell'applicazione nell'elenco di hello di registrazioni di app:</span><span class="sxs-lookup"><span data-stu-id="c97a6-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Cercare il nome dell'applicazione](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="c97a6-132">Hello visualizzazione **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="c97a6-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="c97a6-133">In hello **l'accesso all'API** selezionare **delle autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="c97a6-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="c97a6-134">Fare clic su **Aggiungi** tooadd una nuova autorizzazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="c97a6-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="c97a6-135">Nel passaggio 1, immettere **API di gestione del servizio di Windows Azure**, selezionare tale API hello elenco dei risultati e fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c97a6-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="c97a6-136">Nel passaggio 2, selezionare hello casella di controllo accanto troppo**il modello di distribuzione classica accesso Azure come utenti dell'organizzazione**, fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c97a6-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="c97a6-137">Fare clic su hello **eseguita** pulsante.</span><span class="sxs-lookup"><span data-stu-id="c97a6-137">Click hello **Done** button.</span></span>

<span data-ttu-id="c97a6-138">Hello **autorizzazioni obbligatorie** pannello ora mostra che l'applicazione tooyour le autorizzazioni vengono concesse tooboth hello ADAL e le API di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c97a6-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="c97a6-139">Le autorizzazioni vengono concesse tooADAL per impostazione predefinita quando si innanzitutto registrare l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c97a6-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![Delegare le autorizzazioni toohello API di gestione risorse di Azure](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="c97a6-141">Endpoint di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c97a6-141">Azure AD endpoints</span></span>

<span data-ttu-id="c97a6-142">tooauthenticate le soluzioni di gestione dei Batch con Azure AD, è necessario due endpoint noto.</span><span class="sxs-lookup"><span data-stu-id="c97a6-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="c97a6-143">Hello **endpoint comuni di Azure AD** fornisce le credenziali quando un tenant specifico non viene fornito, come nel caso di hello dell'autenticazione integrata di interfaccia di raccolta generiche:</span><span class="sxs-lookup"><span data-stu-id="c97a6-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="c97a6-144">Hello **endpoint di Azure Resource Manager** è tooacquire usato un token per l'autenticazione del servizio di gestione di richieste toohello Batch:</span><span class="sxs-lookup"><span data-stu-id="c97a6-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="c97a6-145">applicazione di esempio AccountManagement Hello definisce le costanti per questi endpoint.</span><span class="sxs-lookup"><span data-stu-id="c97a6-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="c97a6-146">Lasciare invariate queste costanti:</span><span class="sxs-lookup"><span data-stu-id="c97a6-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="c97a6-147">Fare riferimento all'ID applicazione</span><span class="sxs-lookup"><span data-stu-id="c97a6-147">Reference your application ID</span></span> 

<span data-ttu-id="c97a6-148">L'applicazione client utilizza tooaccess di ID (anche noto tooas hello client ID) dell'applicazione hello Azure AD in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c97a6-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="c97a6-149">Dopo aver registrato l'applicazione nel portale di Azure hello, aggiornare l'ID applicazione di codice toouse hello fornita da Azure AD per l'applicazione registrata.</span><span class="sxs-lookup"><span data-stu-id="c97a6-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="c97a6-150">Nell'applicazione di esempio AccountManagement hello, copiare l'ID applicazione da appropriata costante di hello toohello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="c97a6-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="c97a6-151">Copiare anche il reindirizzamento di hello URI specificato durante il processo di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="c97a6-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="c97a6-152">URI specificato nel codice di reindirizzamento Hello deve corrispondere il reindirizzamento di hello URI fornito dall'utente durante la registrazione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c97a6-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="c97a6-153">Acquisire un token di autenticazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c97a6-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="c97a6-154">Dopo aver registrare esempio AccountManagement hello nel tenant di Azure AD hello e aggiornare codice sorgente dell'esempio hello con i valori, esempio hello è pronto tooauthenticate mediante Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c97a6-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="c97a6-155">Quando si esegue l'esempio hello, hello ADAL tenta tooacquire un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c97a6-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="c97a6-156">A questo punto, richiede all'utente credenziali Microsoft:</span><span class="sxs-lookup"><span data-stu-id="c97a6-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

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

<span data-ttu-id="c97a6-157">Dopo aver fornito le credenziali, l'applicazione di esempio hello possibile procedere toohello richieste tooissue autenticato il servizio di gestione di Batch.</span><span class="sxs-lookup"><span data-stu-id="c97a6-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c97a6-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c97a6-158">Next steps</span></span>

<span data-ttu-id="c97a6-159">Per ulteriori informazioni sull'esecuzione hello [l'applicazione di esempio AccountManagement][acct_mgmt_sample], vedere [account Batch di gestione e alle quote alla libreria client di gestione dei Batch hello per .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c97a6-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="c97a6-160">toolearn ulteriori informazioni su Azure AD, vedere hello [documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="c97a6-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="c97a6-161">Esempi dettagliati che mostra come toouse ADAL sono disponibili in hello [esempi di codice di Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) libreria.</span><span class="sxs-lookup"><span data-stu-id="c97a6-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="c97a6-162">applicazioni di servizio Batch tooauthenticate mediante Azure AD, vedere [soluzioni di servizio Batch con l'autenticazione con Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="c97a6-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "Informazioni su Azure Active Directory"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenari di autenticazione per Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrazione di applicazioni con Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
