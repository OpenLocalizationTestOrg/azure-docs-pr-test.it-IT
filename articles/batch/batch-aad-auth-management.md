---
title: Usare Azure Active Directory per autenticare le soluzioni di gestione Batch | Microsoft Docs
description: Le applicazioni compilate con Azure Resource Manager e il provider di risorse Batch vengono autenticate con Azure AD.
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
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="992b8-103">Autenticare le soluzioni di gestione Batch con Active Directory</span><span class="sxs-lookup"><span data-stu-id="992b8-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="992b8-104">Le applicazioni che chiamano il servizio di gestione di Azure Batch vengono autenticate con [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="992b8-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="992b8-105">Azure AD è il servizio Microsoft di gestione di identità e directory basato sul cloud e multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="992b8-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="992b8-106">Azure stesso usa Azure AD per l'autenticazione dei relativi clienti, amministratori del servizio e utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="992b8-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="992b8-107">La libreria .NET per la gestione di Batch espone tipi per l'uso di account Batch, chiavi dell'account, applicazioni e pacchetti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="992b8-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="992b8-108">La libreria .NET per la gestione di Batch è un client del provider di risorse di Azure e viene usata in combinazione con [Azure Resource Manager][resman_overview] per gestire tali risorse a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="992b8-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="992b8-109">Azure AD è necessario per autenticare le richieste effettuate tramite qualsiasi client del provider di risorse di Azure, inclusa la libreria .NET per la gestione di Batch, e tramite [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="992b8-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="992b8-110">Questo articolo illustra l'uso di Azure AD per eseguire l'autenticazione dalle applicazioni che usano la libreria .NET per la gestione di Batch.</span><span class="sxs-lookup"><span data-stu-id="992b8-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="992b8-111">Viene descritto come usare Azure AD per autenticare un amministratore o un co-amministratore della sottoscrizione tramite l'autenticazione integrata.</span><span class="sxs-lookup"><span data-stu-id="992b8-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="992b8-112">In questa sezione si usa il progetto di esempio [AccountManagement][acct_mgmt_sample], disponibile in GitHub, per illustrare l'uso di Azure AD con la libreria .NET per la gestione di Batch.</span><span class="sxs-lookup"><span data-stu-id="992b8-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="992b8-113">Per altre informazioni sull'uso della libreria .NET per la gestione di Batch e dell'esempio AccountManagement, vedere [Gestire le quote e gli account Batch con la libreria client di gestione Batch per .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="992b8-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="992b8-114">Registrare l'applicazione in Azure AD</span><span class="sxs-lookup"><span data-stu-id="992b8-114">Register your application with Azure AD</span></span>

<span data-ttu-id="992b8-115">[Azure Active Directory Authentication Library][aad_adal] (ADAL) offre un'interfaccia programmatica per Azure AD da usare nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="992b8-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="992b8-116">Per chiamare ADAL da un'applicazione, è necessario registrare l'applicazione in un tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="992b8-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="992b8-117">Quando si registra l'applicazione, si specificano in Azure AD le informazioni relative all'applicazione, incluso un nome per l'applicazione nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="992b8-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="992b8-118">Azure AD fornisce quindi un ID applicazione che viene usato per associare l'applicazione ad Azure AD in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="992b8-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="992b8-119">Per altre informazioni sull'ID applicazione, vedere [Oggetti applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="992b8-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="992b8-120">Per registrare l'applicazione di esempio AccountManagement, seguire la procedura descritta nella sezione [Aggiunta di un'applicazione](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) dell'articolo [Integrazione di applicazioni con Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="992b8-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="992b8-121">Specificare **Nativa** come tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="992b8-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="992b8-122">L'URI OAuth 2.0 standard per l'**URI di reindirizzamento** è `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="992b8-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="992b8-123">In **URI di reindirizzamento** è possibile specificare qualsiasi URI valido, ad esempio `http://myaccountmanagementsample`, perché non è necessario che sia un endpoint reale:</span><span class="sxs-lookup"><span data-stu-id="992b8-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="992b8-124">Al termine del processo di registrazione, verranno elencati l'ID applicazione e l'ID oggetto (entità servizio) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="992b8-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="992b8-125">Concedere all'API di Azure Resource Manager l'accesso all'applicazione</span><span class="sxs-lookup"><span data-stu-id="992b8-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="992b8-126">Successivamente, sarà necessario delegare l'accesso all'applicazione all'API di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="992b8-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="992b8-127">L'identificatore di Azure AD per l'API di Resource Manager è **API di gestione del servizio Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="992b8-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="992b8-128">Seguire questa procedura nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="992b8-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="992b8-129">Nel riquadro di spostamento sinistro del portale di Azure scegliere **Altri servizi** e fare clic su **Registrazioni per l'app** e quindi su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="992b8-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="992b8-130">Cercare il nome dell'applicazione nell'elenco di registrazioni di app:</span><span class="sxs-lookup"><span data-stu-id="992b8-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Cercare il nome dell'applicazione](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="992b8-132">Visualizzare il pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="992b8-132">Display the **Settings** blade.</span></span> <span data-ttu-id="992b8-133">Nella sezione **Accesso all'API** selezionare **Autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="992b8-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="992b8-134">Fare clic su **Aggiungi** per aggiungere una nuova autorizzazione necessaria.</span><span class="sxs-lookup"><span data-stu-id="992b8-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="992b8-135">Nel passaggio 1 immettere **API di gestione del servizio Microsoft Azure**, selezionare tale API nell'elenco dei risultati e fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="992b8-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="992b8-136">Nel passaggio 2 selezionare la casella di controllo accanto ad **Access Azure classic deployment model as organization users** (Accedi a modello di distribuzione classica di Azure come utente dell'organizzazione) e fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="992b8-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="992b8-137">Fare clic sul pulsante **Fine**.</span><span class="sxs-lookup"><span data-stu-id="992b8-137">Click the **Done** button.</span></span>

<span data-ttu-id="992b8-138">Il pannello **Autorizzazioni necessarie** mostra ora che le autorizzazioni per l'applicazione sono concesse sia ad ADAL che alle API di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="992b8-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="992b8-139">Le autorizzazioni vengono concesse ad ADAL per impostazione predefinita quando si registra per la prima volta l'app in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="992b8-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Delegare le autorizzazioni all'API di Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="992b8-141">Endpoint di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="992b8-141">Azure AD endpoints</span></span>

<span data-ttu-id="992b8-142">Per autenticare le soluzioni di gestione Batch con Azure AD, è necessario usare due endpoint noti.</span><span class="sxs-lookup"><span data-stu-id="992b8-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="992b8-143">L'**endpoint comune di Azure AD** consente di usare un'interfaccia di raccolta di credenziali generiche quando non è disponibile un tenant specifico, come nel caso l'autenticazione integrata:</span><span class="sxs-lookup"><span data-stu-id="992b8-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="992b8-144">L'**endpoint di Azure Resource Manager** consente di acquisire un token per autenticare le richieste al servizio di gestione Batch:</span><span class="sxs-lookup"><span data-stu-id="992b8-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="992b8-145">L'applicazione di esempio AccountManagement definisce le costanti per tali endpoint.</span><span class="sxs-lookup"><span data-stu-id="992b8-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="992b8-146">Lasciare invariate queste costanti:</span><span class="sxs-lookup"><span data-stu-id="992b8-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="992b8-147">Fare riferimento all'ID applicazione</span><span class="sxs-lookup"><span data-stu-id="992b8-147">Reference your application ID</span></span> 

<span data-ttu-id="992b8-148">L'ID applicazione (detto anche ID client) viene usato dall'applicazione client per accedere ad Azure AD in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="992b8-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="992b8-149">Dopo aver registrato l'applicazione nel portale di Azure, aggiornare il codice per usare l'ID applicazione fornito da Azure AD per l'applicazione registrata.</span><span class="sxs-lookup"><span data-stu-id="992b8-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="992b8-150">Nell'applicazione di esempio AccountManagement, copiare l'ID applicazione dal portale di Azure alla costante appropriata:</span><span class="sxs-lookup"><span data-stu-id="992b8-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="992b8-151">Copiare anche l'URI di reindirizzamento specificato durante il processo di registrazione.</span><span class="sxs-lookup"><span data-stu-id="992b8-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="992b8-152">L'URI specificato nel codice di reindirizzamento deve corrispondere a quello specificato quando è stata registrata l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="992b8-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="992b8-153">Acquisire un token di autenticazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="992b8-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="992b8-154">Dopo aver registrare l'esempio AccountManagement nel tenant di Azure AD e aggiornato il codice sorgente di esempio con i valori appropriati, l'esempio è pronto per eseguire l'autenticazione tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="992b8-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="992b8-155">Quando si esegue l'esempio, ADAL tenta di acquisire un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="992b8-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="992b8-156">A questo punto, richiede all'utente credenziali Microsoft:</span><span class="sxs-lookup"><span data-stu-id="992b8-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="992b8-157">Dopo che sono state specificate le credenziali, l'applicazione di esempio può procedere con l'invio di richieste autenticate al servizio di gestione di Batch.</span><span class="sxs-lookup"><span data-stu-id="992b8-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="992b8-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="992b8-158">Next steps</span></span>

<span data-ttu-id="992b8-159">Per altre informazioni sull'esecuzione dell'[applicazione di esempio AccountManagement][acct_mgmt_sample], vedere [Gestire le quote e gli account Batch con la libreria client di gestione Batch per .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="992b8-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="992b8-160">Per altre informazioni su Azure AD, vedere [Documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="992b8-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="992b8-161">Esempi dettagliati dell'uso di ADAL sono disponibili nella libreria degli [esempi di codice per Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="992b8-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="992b8-162">Per eseguire l'autenticazione di applicazioni del servizio Batch con Azure AD, vedere [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md) (Autenticare le soluzioni del servizio Batch con Active Directoy).</span><span class="sxs-lookup"><span data-stu-id="992b8-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="992b8-163">[aad_about]: ../active-directory/active-directory-whatis.md "Informazioni su Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="992b8-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="992b8-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenari di autenticazione per Azure AD"</span><span class="sxs-lookup"><span data-stu-id="992b8-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="992b8-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrazione di applicazioni con Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="992b8-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
