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
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="2860c-103">Autenticare le soluzioni del servizio Batch con Active Directory</span><span class="sxs-lookup"><span data-stu-id="2860c-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="2860c-104">Azure Batch supporta l'autenticazione con [Azure Active Directory][aad_about], ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="2860c-105">Azure AD è il servizio Microsoft di gestione di identità e directory basato sul cloud e multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="2860c-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="2860c-106">Azure stesso utilizza Azure AD tooauthenticate relativi clienti, gli amministratori del servizio e gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="2860c-107">Quando si usa l'autenticazione di Azure AD con Azure Batch, è possibile eseguire l'autenticazione in uno dei due modi:</span><span class="sxs-lookup"><span data-stu-id="2860c-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="2860c-108">Utilizzando **l'autenticazione integrata di** tooauthenticate un utente che interagisce con un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2860c-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="2860c-109">Un'applicazione utilizzando l'autenticazione integrata raccoglie le credenziali dell'utente e utilizza tali credenziali tooauthenticate accedere tooBatch alle risorse.</span><span class="sxs-lookup"><span data-stu-id="2860c-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="2860c-110">Utilizzando un **dell'entità servizio** tooauthenticate un'applicazione automatica.</span><span class="sxs-lookup"><span data-stu-id="2860c-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="2860c-111">Un'entità servizio definisce criteri hello e le autorizzazioni per un'applicazione in un'applicazione hello toorepresent ordine quando accedono alle risorse in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2860c-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="2860c-112">toolearn ulteriori informazioni su Azure AD, vedere hello [documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="2860c-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="2860c-113">Modalità di allocazione pool e autenticazione</span><span class="sxs-lookup"><span data-stu-id="2860c-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="2860c-114">Quando si crea un account Batch, è possibile specificare dove devono essere allocati i pool creati per tale account.</span><span class="sxs-lookup"><span data-stu-id="2860c-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="2860c-115">È possibile scegliere pool tooallocate sottoscrizione al servizio Batch predefinito hello o in una sottoscrizione utente.</span><span class="sxs-lookup"><span data-stu-id="2860c-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="2860c-116">La scelta influisce sulla modalità di autenticazione accesso tooresources in tale account.</span><span class="sxs-lookup"><span data-stu-id="2860c-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="2860c-117">**Sottoscrizione al servizio Batch**.</span><span class="sxs-lookup"><span data-stu-id="2860c-117">**Batch service subscription**.</span></span> <span data-ttu-id="2860c-118">Per impostazione predefinita, i pool di Batch vengono allocati in una sottoscrizione del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="2860c-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="2860c-119">Se si sceglie questa opzione, è possibile autenticare accesso tooresources in quell'account con [chiave condivisa](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) o con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="2860c-120">**Sottoscrizione utente.**</span><span class="sxs-lookup"><span data-stu-id="2860c-120">**User subscription.**</span></span> <span data-ttu-id="2860c-121">È possibile scegliere tooallocate pool Batch in una sottoscrizione utente specificato.</span><span class="sxs-lookup"><span data-stu-id="2860c-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="2860c-122">Se si sceglie questa opzione, è necessario eseguire l'autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="2860c-123">Endpoint per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="2860c-123">Endpoints for authentication</span></span>

<span data-ttu-id="2860c-124">applicazioni di Batch tooauthenticate con Azure AD, è necessario tooinclude alcuni endpoint noto nel codice.</span><span class="sxs-lookup"><span data-stu-id="2860c-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="2860c-125">Endpoint di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2860c-125">Azure AD endpoint</span></span>

<span data-ttu-id="2860c-126">Hello base endpoint autorità di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="2860c-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="2860c-127">tooauthenticate con Azure AD, utilizzare l'endpoint con l'ID tenant hello (ID di directory).</span><span class="sxs-lookup"><span data-stu-id="2860c-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="2860c-128">l'ID tenant Hello identifica toouse tenant di Azure AD hello per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="2860c-129">tooretrieve hello ID tenant, seguire i passaggi di hello illustrati in [ottenere l'ID del tenant hello per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="2860c-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="2860c-130">endpoint specifico del tenant Hello è obbligatorio quando si autentica utilizzando un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2860c-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="2860c-131">endpoint specifico del tenant Hello è facoltativo quando si autentica utilizzando l'autenticazione integrata, ma consigliato.</span><span class="sxs-lookup"><span data-stu-id="2860c-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="2860c-132">Tuttavia, è possibile utilizzare anche l'endpoint comune hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="2860c-133">endpoint comune Hello fornisce le credenziali generica dell'interfaccia di raccolta quando non viene fornito un tenant specifico.</span><span class="sxs-lookup"><span data-stu-id="2860c-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="2860c-134">endpoint comuni Hello è `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="2860c-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="2860c-135">Per altre informazioni sugli endpoint di Azure AD, vedere [Scenari di autenticazione per Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="2860c-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="2860c-136">Endpoint di risorse Batch</span><span class="sxs-lookup"><span data-stu-id="2860c-136">Batch resource endpoint</span></span>

<span data-ttu-id="2860c-137">Hello utilizzare **endpoint di risorse di Azure Batch** tooacquire un token per l'autenticazione delle richieste di servizio Batch toohello:</span><span class="sxs-lookup"><span data-stu-id="2860c-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="2860c-138">Registrare l'applicazione con un tenant</span><span class="sxs-lookup"><span data-stu-id="2860c-138">Register your application with a tenant</span></span>

<span data-ttu-id="2860c-139">Hello innanzitutto usando Azure AD tooauthenticate sta registrando l'applicazione in un tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="2860c-140">Registrazione dell'applicazione consente toocall hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) dal codice.</span><span class="sxs-lookup"><span data-stu-id="2860c-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="2860c-141">Hello ADAL fornisce un'API per l'autenticazione con Azure AD dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="2860c-142">Registrazione dell'applicazione è necessario se si prevede l'autenticazione integrata di toouse o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2860c-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="2860c-143">Quando si registra l'applicazione, è fornire informazioni relative la tooAzure applicazione Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2860c-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="2860c-144">Quindi AD Azure fornisce un ID applicazione di usare tooassociate l'applicazione con Azure AD in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2860c-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="2860c-145">vedere toolearn ulteriori informazioni su ID applicazione hello [applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="2860c-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="2860c-146">tooregister l'applicazione di Batch, seguire la procedura seguente hello in hello [aggiunta di un'applicazione](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) sezione [integrazione di applicazioni con Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="2860c-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="2860c-147">Se si registra l'applicazione come applicazione nativa, è possibile specificare qualsiasi URI valido per hello **URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="2860c-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="2860c-148">Non è necessario un endpoint reale toobe.</span><span class="sxs-lookup"><span data-stu-id="2860c-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="2860c-149">Dopo aver registrato l'applicazione, verrà visualizzato l'ID dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-149">After you've registered your application, you'll see hello application ID:</span></span>

![Registrare l'applicazione Batch in Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="2860c-151">Per altre informazioni sulla registrazione di un'applicazione con Azure AD, vedere [Scenari di autenticazione per Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="2860c-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="2860c-152">Ottenere l'ID del tenant hello per Active Directory</span><span class="sxs-lookup"><span data-stu-id="2860c-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="2860c-153">l'ID tenant Hello identifica tenant di Azure AD hello che fornisce l'autenticazione servizi tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="2860c-154">tooget hello ID tenant, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2860c-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="2860c-155">Nel portale di Azure hello, selezionare Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2860c-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="2860c-156">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2860c-156">Click **Properties**.</span></span>
3. <span data-ttu-id="2860c-157">Copiare il valore GUID hello fornito per l'ID di directory hello.</span><span class="sxs-lookup"><span data-stu-id="2860c-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="2860c-158">Questo valore viene anche chiamato hello ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="2860c-158">This value is also called hello tenant ID.</span></span>

![Copiare l'ID di directory hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="2860c-160">Usare l'autenticazione integrata</span><span class="sxs-lookup"><span data-stu-id="2860c-160">Use integrated authentication</span></span>

<span data-ttu-id="2860c-161">tooauthenticate con l'autenticazione integrata, è necessario toogrant toohello di tooconnect le autorizzazioni applicazione API del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="2860c-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="2860c-162">Questo passaggio attiva le API del servizio Batch di applicazione tooauthenticate chiamate toohello con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="2860c-163">Dopo aver [registrazione dell'applicazione](#register-your-application-with-an-azure-ad-tenant), seguire questi passaggi nell'hello Azure toogrant portale, servizio Batch toohello di accesso:</span><span class="sxs-lookup"><span data-stu-id="2860c-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="2860c-164">Nel riquadro di navigazione a sinistra hello di hello portale di Azure, scegliere **più servizi**, fare clic su **registrazioni di App**.</span><span class="sxs-lookup"><span data-stu-id="2860c-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="2860c-165">Ricerca per nome hello dell'applicazione nell'elenco di hello di registrazioni di app:</span><span class="sxs-lookup"><span data-stu-id="2860c-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Cercare il nome dell'applicazione](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="2860c-167">Aprire hello **impostazioni** pannello per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="2860c-168">In hello **l'accesso all'API** selezionare **delle autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="2860c-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="2860c-169">In hello **delle autorizzazioni necessarie** pannello, fare clic su hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2860c-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="2860c-170">Nel passaggio 1, cercare hello API Batch.</span><span class="sxs-lookup"><span data-stu-id="2860c-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="2860c-171">Fino a individuare hello API di ricerca per ognuna di queste stringhe:</span><span class="sxs-lookup"><span data-stu-id="2860c-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="2860c-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="2860c-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="2860c-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="2860c-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="2860c-174">I tenant di Azure AD più recenti potrebbero usare questo nome.</span><span class="sxs-lookup"><span data-stu-id="2860c-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="2860c-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** ID hello per hello API Batch.</span><span class="sxs-lookup"><span data-stu-id="2860c-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="2860c-176">Dopo aver individuato hello API Batch, selezionarlo e fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2860c-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="2860c-177">Nel passaggio 2, selezionare hello casella di controllo accanto troppo**servizio di accesso Azure Batch** e fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2860c-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="2860c-178">Fare clic su hello **eseguita** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2860c-178">Click hello **Done** button.</span></span>

<span data-ttu-id="2860c-179">Hello **autorizzazioni obbligatorie** pannello indica che l'applicazione Azure AD dispone di accesso tooboth ADAL e hello API del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="2860c-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="2860c-180">Le autorizzazioni vengono concesse tooADAL automaticamente quando si innanzitutto registrare l'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![Concedere le autorizzazioni delle API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="2860c-182">Usare un’entità servizio</span><span class="sxs-lookup"><span data-stu-id="2860c-182">Use a service principal</span></span> 

<span data-ttu-id="2860c-183">tooauthenticate un'applicazione in esecuzione automatica, utilizzare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2860c-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="2860c-184">Dopo aver registrato l'applicazione, seguire questi passaggi in hello tooconfigure portale Azure un'entità servizio:</span><span class="sxs-lookup"><span data-stu-id="2860c-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="2860c-185">Richiedere una chiave privata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="2860c-186">Assegnare un'applicazione di tooyour RBAC ruolo.</span><span class="sxs-lookup"><span data-stu-id="2860c-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="2860c-187">Richiedere una chiave privata per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="2860c-187">Request a secret key for your application</span></span>

<span data-ttu-id="2860c-188">Quando l'applicazione esegue l'autenticazione con un'entità servizio, Invia ID applicazione hello sia un tooAzure chiave segreta Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2860c-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="2860c-189">Si sarà necessario toocreate e copiare toouse chiave segreta hello dal codice.</span><span class="sxs-lookup"><span data-stu-id="2860c-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="2860c-190">Seguire questi passaggi in hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="2860c-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="2860c-191">Nel riquadro di navigazione a sinistra hello di hello portale di Azure, scegliere **più servizi**, fare clic su **registrazioni di App**.</span><span class="sxs-lookup"><span data-stu-id="2860c-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="2860c-192">Ricerca per nome hello dell'applicazione nell'elenco di hello di registrazioni di app.</span><span class="sxs-lookup"><span data-stu-id="2860c-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="2860c-193">Hello visualizzazione **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="2860c-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="2860c-194">In hello **l'accesso all'API** selezionare **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="2860c-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="2860c-195">toocreate una chiave, immettere una descrizione per la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="2860c-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="2860c-196">Selezionare una durata per la chiave hello di uno o due anni.</span><span class="sxs-lookup"><span data-stu-id="2860c-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="2860c-197">Fare clic su hello **salvare** pulsante toocreate e visualizzare la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="2860c-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="2860c-198">Copiare il luogo sicuro tooa valore chiave hello, poiché non sarà in grado di tooaccess nuovamente dopo averlo lasciare pannello hello.</span><span class="sxs-lookup"><span data-stu-id="2860c-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![Creare una chiave privata](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="2860c-200">Assegnare un'applicazione di tooyour RBAC ruolo</span><span class="sxs-lookup"><span data-stu-id="2860c-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="2860c-201">tooauthenticate con un'entità servizio, è necessario tooassign un'applicazione di tooyour RBAC ruolo.</span><span class="sxs-lookup"><span data-stu-id="2860c-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="2860c-202">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2860c-202">Follow these steps:</span></span>

1. <span data-ttu-id="2860c-203">Nel portale di Azure hello, passare l'account Batch toohello utilizzati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="2860c-204">In hello **impostazioni** pannello per l'account Batch hello, selezionare **il controllo di accesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="2860c-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="2860c-205">Fare clic su hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2860c-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="2860c-206">Da hello **ruolo** elenco a discesa, selezionare entrambi hello _collaboratore_ o _lettore_ ruolo per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="2860c-207">Per ulteriori informazioni su questi ruoli, vedere [Introduzione a controllo di accesso basato sui ruoli nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2860c-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="2860c-208">In hello **selezionare** immettere nome hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="2860c-209">Selezionare l'applicazione hello elenco e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="2860c-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="2860c-210">L'applicazione dovrebbe ora essere visualizzata nelle impostazioni di controllo di accesso con un ruolo con controllo degli accessi in base al ruolo assegnato.</span><span class="sxs-lookup"><span data-stu-id="2860c-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Assegnare un'applicazione di tooyour RBAC ruolo](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="2860c-212">Ottenere l'ID del tenant hello per Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2860c-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="2860c-213">l'ID tenant Hello identifica tenant di Azure AD hello che fornisce l'autenticazione servizi tooyour applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="2860c-214">tooget hello ID tenant, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2860c-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="2860c-215">Nel portale di Azure hello, selezionare Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2860c-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="2860c-216">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2860c-216">Click **Properties**.</span></span>
3. <span data-ttu-id="2860c-217">Copiare il valore GUID hello fornito per l'ID di directory hello.</span><span class="sxs-lookup"><span data-stu-id="2860c-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="2860c-218">Questo valore viene anche chiamato hello ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="2860c-218">This value is also called hello tenant ID.</span></span>

![Copiare l'ID di directory hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="2860c-220">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="2860c-220">Code examples</span></span>

<span data-ttu-id="2860c-221">esempi di codice Hello in questa sezione illustrano come tooauthenticate con Azure AD mediante l'autenticazione integrata e con un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2860c-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="2860c-222">.NET di utilizzare questi esempi di codice, ma i concetti di hello sono simili ad altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="2860c-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="2860c-223">Un token di autenticazione di Azure AD scade dopo un'ora.</span><span class="sxs-lookup"><span data-stu-id="2860c-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="2860c-224">Quando si utilizza una lunga durata **BatchClient** dell'oggetto, si consiglia recuperare un token da ADAL su tooensure ogni richiesta è sempre necessario un token valido.</span><span class="sxs-lookup"><span data-stu-id="2860c-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="2860c-225">tooachieve in .NET, scrivere un metodo che recupera hello token da Azure AD e passa tale tooa metodo **BatchTokenCredentials** oggetto come un delegato.</span><span class="sxs-lookup"><span data-stu-id="2860c-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="2860c-226">metodo delegato Hello viene chiamato su ogni richiesta toohello Batch servizio tooensure viene fornito un token valido.</span><span class="sxs-lookup"><span data-stu-id="2860c-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="2860c-227">Per impostazione predefinita, ADAL memorizza i token nella cache, quindi un nuovo token viene recuperato da Azure AD solo quando necessario.</span><span class="sxs-lookup"><span data-stu-id="2860c-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="2860c-228">Per altre informazioni sui token in Azure AD, vedere [Scenari di autenticazione per Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="2860c-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="2860c-229">Esempio di codice: uso dell'autenticazione integrata di Azure AD con .NET di Batch</span><span class="sxs-lookup"><span data-stu-id="2860c-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="2860c-230">tooauthenticate con l'autenticazione integrata da .NET di Batch, hello riferimento [.NET di Azure Batch](https://www.nuget.org/packages/Azure.Batch/) pacchetto e hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2860c-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="2860c-231">Sono inclusi i seguenti hello `using` istruzioni nel codice:</span><span class="sxs-lookup"><span data-stu-id="2860c-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="2860c-232">Hello riferimento endpoint di Azure AD nel codice, tra cui hello tenant ID.</span><span class="sxs-lookup"><span data-stu-id="2860c-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="2860c-233">tooretrieve hello ID tenant, seguire i passaggi di hello illustrati in [ottenere l'ID del tenant hello per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="2860c-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="2860c-234">Fare riferimento a endpoint di risorse del servizio Batch hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="2860c-235">Riferimento all'account Batch:</span><span class="sxs-lookup"><span data-stu-id="2860c-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="2860c-236">Specificare l'ID dell'applicazione hello (ID client) per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="2860c-237">ID dell'applicazione Hello è disponibile tramite la registrazione dell'app nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="2860c-238">Copiare anche il reindirizzamento di hello URI specificato durante il processo di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="2860c-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="2860c-239">URI specificato nel codice di reindirizzamento Hello deve corrispondere reindirizzamento hello URI fornito dall'utente durante la registrazione di un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="2860c-240">Scrivere un token di autenticazione hello tooacquire metodo di callback da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="2860c-241">Hello **GetAuthenticationTokenAsync** metodo di callback illustrato di seguito chiama tooauthenticate ADAL un utente interagisce con un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2860c-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="2860c-242">Hello **AcquireTokenAsync** metodo fornite dalla libreria ADAL richiede hello le loro credenziali utente e un'applicazione hello continua una volta utente hello fornisce loro (a meno che non ha già memorizzato nella cache le credenziali):</span><span class="sxs-lookup"><span data-stu-id="2860c-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

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

<span data-ttu-id="2860c-243">Costruire un **BatchTokenCredentials** oggetto che accetta hello delegato come parametro.</span><span class="sxs-lookup"><span data-stu-id="2860c-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="2860c-244">Utilizzare tali tooopen credenziali un **BatchClient** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2860c-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="2860c-245">È possibile utilizzare tale **BatchClient** oggetto per le successive operazioni nel servizio Batch hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="2860c-246">Esempio di codice: uso di un'entità servizio Azure AD con Batch .NET</span><span class="sxs-lookup"><span data-stu-id="2860c-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="2860c-247">tooauthenticate con un'entità servizio da .NET di Batch, hello riferimento [.NET di Azure Batch](https://www.nuget.org/packages/Azure.Batch/) pacchetto e hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2860c-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="2860c-248">Sono inclusi i seguenti hello `using` istruzioni nel codice:</span><span class="sxs-lookup"><span data-stu-id="2860c-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="2860c-249">Hello riferimento endpoint di Azure AD nel codice, tra cui hello tenant ID.</span><span class="sxs-lookup"><span data-stu-id="2860c-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="2860c-250">Quando si usa un'entità servizio, è necessario indicare un endpoint specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="2860c-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="2860c-251">tooretrieve hello ID tenant, seguire i passaggi di hello illustrati in [ottenere l'ID del tenant hello per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="2860c-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="2860c-252">Fare riferimento a endpoint di risorse del servizio Batch hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="2860c-253">Riferimento all'account Batch:</span><span class="sxs-lookup"><span data-stu-id="2860c-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="2860c-254">Specificare l'ID dell'applicazione hello (ID client) per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2860c-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="2860c-255">ID dell'applicazione Hello è disponibile tramite la registrazione dell'app nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="2860c-256">Specificare una chiave segreta hello copiata dal portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="2860c-257">Scrivere un token di autenticazione hello tooacquire metodo di callback da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2860c-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="2860c-258">Hello **GetAuthenticationTokenAsync** il metodo di callback illustrato di seguito chiama ADAL per l'autenticazione automatica:</span><span class="sxs-lookup"><span data-stu-id="2860c-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="2860c-259">Costruire un **BatchTokenCredentials** oggetto che accetta hello delegato come parametro.</span><span class="sxs-lookup"><span data-stu-id="2860c-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="2860c-260">Utilizzare tali tooopen credenziali un **BatchClient** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2860c-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="2860c-261">È quindi possibile utilizzare che **BatchClient** oggetto per le successive operazioni nel servizio Batch hello:</span><span class="sxs-lookup"><span data-stu-id="2860c-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2860c-262">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2860c-262">Next steps</span></span>

<span data-ttu-id="2860c-263">toolearn ulteriori informazioni su Azure AD, vedere hello [documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="2860c-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="2860c-264">Esempi dettagliati che mostra come toouse ADAL sono disponibili in hello [esempi di codice di Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) libreria.</span><span class="sxs-lookup"><span data-stu-id="2860c-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="2860c-265">toolearn sulle entità servizio, vedere [applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="2860c-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="2860c-266">toocreate un servizio principale utilizzando hello Azure portale, vedere [utilizzare portale toocreate applicazione di Active Directory e dell'entità servizio che possono accedere alle risorse](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2860c-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="2860c-267">È anche possibile creare un'entità servizio con PowerShell o con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2860c-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="2860c-268">applicazioni di gestione dei Batch tooauthenticate mediante Azure AD, vedere [soluzioni di gestione dei Batch l'autenticazione con Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="2860c-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "Informazioni su Azure Active Directory"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenari di autenticazione per Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrazione di applicazioni con Azure Active Directory"
[azure_portal]: http://portal.azure.com
