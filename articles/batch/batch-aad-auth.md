---
title: Usare Azure Active Directory per autenticare le soluzioni del servizio Azure Batch | Microsoft Docs
description: Batch supporta Azure AD per l'autenticazione dal servizio Batch.
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
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="2cc24-103">Autenticare le soluzioni del servizio Batch con Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cc24-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="2cc24-104">Azure Batch supporta l'autenticazione con [Azure Active Directory][aad_about], ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="2cc24-105">Azure AD è il servizio Microsoft di gestione di identità e directory basato sul cloud e multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="2cc24-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="2cc24-106">Azure stesso usa Azure AD per l'autenticazione i propri clienti, gli amministratori del servizio e gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="2cc24-107">Quando si usa l'autenticazione di Azure AD con Azure Batch, è possibile eseguire l'autenticazione in uno dei due modi:</span><span class="sxs-lookup"><span data-stu-id="2cc24-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="2cc24-108">Usando **l'autenticazione integrata** per autenticare un utente che interagisce con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="2cc24-109">Un'applicazione che usa l'autenticazione integrata raccoglie le credenziali dell'utente e le usa per autenticare l'accesso alle risorse di Batch.</span><span class="sxs-lookup"><span data-stu-id="2cc24-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="2cc24-110">Usando un'**entità servizio** per autenticare un'applicazione automatica.</span><span class="sxs-lookup"><span data-stu-id="2cc24-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="2cc24-111">L'entità servizio definisce i criteri e le autorizzazioni per un'applicazione al fine di rappresentare l'applicazione al momento dell'accesso alle risorse in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="2cc24-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="2cc24-112">Per altre informazioni su Azure AD, vedere [Documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="2cc24-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="2cc24-113">Modalità di allocazione pool e autenticazione</span><span class="sxs-lookup"><span data-stu-id="2cc24-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="2cc24-114">Quando si crea un account Batch, è possibile specificare dove devono essere allocati i pool creati per tale account.</span><span class="sxs-lookup"><span data-stu-id="2cc24-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="2cc24-115">È possibile scegliere di allocare i pool nella sottoscrizione predefinita del servizio Batch o in una sottoscrizione utente.</span><span class="sxs-lookup"><span data-stu-id="2cc24-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="2cc24-116">La scelta influisce sulla modalità di autenticazione dell'accesso alle risorse nell'account.</span><span class="sxs-lookup"><span data-stu-id="2cc24-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="2cc24-117">**Sottoscrizione al servizio Batch**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-117">**Batch service subscription**.</span></span> <span data-ttu-id="2cc24-118">Per impostazione predefinita, i pool di Batch vengono allocati in una sottoscrizione del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="2cc24-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="2cc24-119">è Se si sceglie questa opzione, possibile eseguire l'autenticazione per l'accesso alle risorse in tale account con [chiave condivisa](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) o con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="2cc24-120">**Sottoscrizione utente.**</span><span class="sxs-lookup"><span data-stu-id="2cc24-120">**User subscription.**</span></span> <span data-ttu-id="2cc24-121">È possibile scegliere di allocare il pool Batch in una sottoscrizione utente specificata.</span><span class="sxs-lookup"><span data-stu-id="2cc24-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="2cc24-122">Se si sceglie questa opzione, è necessario eseguire l'autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="2cc24-123">Endpoint per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="2cc24-123">Endpoints for authentication</span></span>

<span data-ttu-id="2cc24-124">Per autenticare le applicazioni Batch con Azure AD, è necessario includere endpoint noti nel codice.</span><span class="sxs-lookup"><span data-stu-id="2cc24-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="2cc24-125">Endpoint di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cc24-125">Azure AD endpoint</span></span>

<span data-ttu-id="2cc24-126">L'endpoint dell'autorità di base di Azure AD è:</span><span class="sxs-lookup"><span data-stu-id="2cc24-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="2cc24-127">Per eseguire l'autenticazione con Azure AD, usare l'endpoint con l'ID tenant, ovvero l'ID directory.</span><span class="sxs-lookup"><span data-stu-id="2cc24-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="2cc24-128">L'ID tenant identifica il tenant di Azure AD da usare per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="2cc24-129">Per recuperare l'ID tenant, attenersi alla procedura descritta in [Ottenere l'ID tenant per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="2cc24-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="2cc24-130">L'endpoint specifico per il tenant è obbligatorio quando si esegue l'autenticazione tramite un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2cc24-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="2cc24-131">L'endpoint specifico del tenant è facoltativo quando si esegue l'autenticazione usando l'autenticazione integrata, ma è consigliabile usarlo.</span><span class="sxs-lookup"><span data-stu-id="2cc24-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="2cc24-132">Tuttavia, è anche possibile usare l'endpoint di Azure AD comune.</span><span class="sxs-lookup"><span data-stu-id="2cc24-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="2cc24-133">L'endpoint comune consente di usare un'interfaccia di raccolta di credenziali generiche quando non è disponibile un tenant specifico.</span><span class="sxs-lookup"><span data-stu-id="2cc24-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="2cc24-134">L'endpoint comune è `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="2cc24-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="2cc24-135">Per altre informazioni sugli endpoint di Azure AD, vedere [Scenari di autenticazione per Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="2cc24-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="2cc24-136">Endpoint di risorse Batch</span><span class="sxs-lookup"><span data-stu-id="2cc24-136">Batch resource endpoint</span></span>

<span data-ttu-id="2cc24-137">Usare l'**endpoint delle risorse di Azure Batch** per acquisire un token per autenticare le richieste al servizio Batch:</span><span class="sxs-lookup"><span data-stu-id="2cc24-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="2cc24-138">Registrare l'applicazione con un tenant</span><span class="sxs-lookup"><span data-stu-id="2cc24-138">Register your application with a tenant</span></span>

<span data-ttu-id="2cc24-139">Il primo passaggio nell'uso di Azure AD per eseguire l'autenticazione consiste nella registrazione dell'applicazione nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="2cc24-140">La registrazione dell'applicazione consente di chiamare l'[Active Directory Authentication Library][aad_adal], ovvero ADAL, di Azure dal codice.</span><span class="sxs-lookup"><span data-stu-id="2cc24-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="2cc24-141">ADAL offre un'API per eseguire l'autenticazione con Azure AD dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="2cc24-142">La registrazione dell'applicazione è necessaria se si prevede di usare l'autenticazione integrata o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2cc24-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="2cc24-143">Quando si registra l'applicazione, si danno informazioni sull'applicazione ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="2cc24-144">Azure AD fornisce quindi un ID applicazione che viene usato per associare l'applicazione ad Azure AD in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="2cc24-145">Per altre informazioni sull'ID applicazione, vedere [Oggetti applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="2cc24-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="2cc24-146">Per registrare l'applicazione Batch, seguire la procedura descritta nella sezione [Aggiunta di un'applicazione](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) dell'articolo [Integrazione di applicazioni con Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="2cc24-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="2cc24-147">Se si registra l'applicazione come applicazione nativa, è possibile specificare qualsiasi URI valido per l'**URI di reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="2cc24-148">Non è necessario che sia un endpoint reale.</span><span class="sxs-lookup"><span data-stu-id="2cc24-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="2cc24-149">Al termine della registrazione dell'applicazione, verrà visualizzata l'ID applicazione:</span><span class="sxs-lookup"><span data-stu-id="2cc24-149">After you've registered your application, you'll see the application ID:</span></span>

![Registrare l'applicazione Batch in Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="2cc24-151">Per altre informazioni sulla registrazione di un'applicazione con Azure AD, vedere [Scenari di autenticazione per Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="2cc24-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="2cc24-152">Ottenere l'ID tenant per Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cc24-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="2cc24-153">L'ID tenant identifica il tenant di Azure AD che offre servizi di autenticazione all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="2cc24-154">Per ottenere l'ID tenant, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2cc24-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="2cc24-155">Nel portale di Azure selezionare Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2cc24-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="2cc24-156">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-156">Click **Properties**.</span></span>
3. <span data-ttu-id="2cc24-157">Copiare il valore GUID indicato per l'ID directory.</span><span class="sxs-lookup"><span data-stu-id="2cc24-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="2cc24-158">Questo valore viene chiamato anche ID tenant.</span><span class="sxs-lookup"><span data-stu-id="2cc24-158">This value is also called the tenant ID.</span></span>

![Copiare l'ID directory](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="2cc24-160">Usare l'autenticazione integrata</span><span class="sxs-lookup"><span data-stu-id="2cc24-160">Use integrated authentication</span></span>

<span data-ttu-id="2cc24-161">Per eseguire l'autenticazione con l'autenticazione integrata, è necessario concedere le autorizzazioni per l'applicazione per connettersi all'API del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="2cc24-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="2cc24-162">Questo passaggio consente all'applicazione di autenticare le chiamate all'API del servizio Batch con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="2cc24-163">Dopo aver [registrato l'applicazione](#register-your-application-with-an-azure-ad-tenant), seguire questi passaggi nel portale di Azure per concedere l'accesso al servizio Batch:</span><span class="sxs-lookup"><span data-stu-id="2cc24-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="2cc24-164">Nel riquadro di spostamento a sinistra del portale di Azure scegliere **Altri servizi** e fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="2cc24-165">Cercare il nome dell'applicazione nell'elenco di registrazioni di app:</span><span class="sxs-lookup"><span data-stu-id="2cc24-165">Search for the name of your application in the list of app registrations:</span></span>

    ![Cercare il nome dell'applicazione](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="2cc24-167">Aprire il pannello **Impostazioni** per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="2cc24-168">Nella sezione **Accesso all'API** selezionare **Autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="2cc24-169">Nel pannello **Autorizzazioni necessarie** fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="2cc24-170">Nel passaggio 1 cercare l'API Batch.</span><span class="sxs-lookup"><span data-stu-id="2cc24-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="2cc24-171">Cercare ognuna di queste stringhe fino a trovare l'API:</span><span class="sxs-lookup"><span data-stu-id="2cc24-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="2cc24-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="2cc24-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="2cc24-174">I tenant di Azure AD più recenti potrebbero usare questo nome.</span><span class="sxs-lookup"><span data-stu-id="2cc24-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="2cc24-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** è l'ID dell'API Batch.</span><span class="sxs-lookup"><span data-stu-id="2cc24-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="2cc24-176">Dopo aver trovato l'API Batch, selezionarla e fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="2cc24-177">Nel passaggio 2 selezionare la casella di controllo accanto ad **Access Azure Batch Service** (Accedi al servizio Azure Batch) e fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="2cc24-178">Fare clic sul pulsante **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-178">Click the **Done** button.</span></span>

<span data-ttu-id="2cc24-179">Il pannello **Autorizzazioni necessarie** mostra ora che l'applicazione Azure AD concede l'accesso alle API sia di ADAL che del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="2cc24-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="2cc24-180">Le autorizzazioni vengono automaticamente concesse ad ADAL quando si registra per la prima volta l'app in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![Concedere le autorizzazioni delle API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="2cc24-182">Usare un’entità servizio</span><span class="sxs-lookup"><span data-stu-id="2cc24-182">Use a service principal</span></span> 

<span data-ttu-id="2cc24-183">Per autenticare un'applicazione in esecuzione automatica, usare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2cc24-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="2cc24-184">Dopo aver registrato l'applicazione, seguire questi passaggi nel portale di Azure per configurare un'entità servizio:</span><span class="sxs-lookup"><span data-stu-id="2cc24-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="2cc24-185">Richiedere una chiave privata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="2cc24-186">Assegnare un ruolo con controllo degli accessi in base al ruolo all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="2cc24-187">Richiedere una chiave privata per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="2cc24-187">Request a secret key for your application</span></span>

<span data-ttu-id="2cc24-188">Quando l'applicazione autentica con un'entità servizio, invia l'ID dell'applicazione e una chiave privata ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="2cc24-189">Sarà necessario creare e copiare la chiave privata da usare dal codice.</span><span class="sxs-lookup"><span data-stu-id="2cc24-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="2cc24-190">Seguire questa procedura nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="2cc24-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="2cc24-191">Nel riquadro di spostamento a sinistra del portale di Azure scegliere **Altri servizi** e fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="2cc24-192">Cercare il nome dell'applicazione nell'elenco di registrazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="2cc24-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="2cc24-193">Visualizzare il pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-193">Display the **Settings** blade.</span></span> <span data-ttu-id="2cc24-194">Nella sezione **Accesso all'API** selezionare **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="2cc24-195">Per creare una chiave, immettere una descrizione per la chiave.</span><span class="sxs-lookup"><span data-stu-id="2cc24-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="2cc24-196">Quindi selezionare la durata della chiave di uno o due anni.</span><span class="sxs-lookup"><span data-stu-id="2cc24-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="2cc24-197">Fare clic sul pulsante **Salva** per creare e visualizzare la chiave.</span><span class="sxs-lookup"><span data-stu-id="2cc24-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="2cc24-198">Copiare il valore della chiave in una posizione sicura, poiché non sarà possibile accedervi nuovamente dopo aver chiuso il pannello.</span><span class="sxs-lookup"><span data-stu-id="2cc24-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![Creare una chiave privata](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="2cc24-200">Assegnare un ruolo con controllo degli accessi in base al ruolo all'applicazione</span><span class="sxs-lookup"><span data-stu-id="2cc24-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="2cc24-201">Per eseguire l'autenticazione con un'entità servizio, è necessario assegnare il ruolo con controllo degli accessi in base al ruolo all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="2cc24-202">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2cc24-202">Follow these steps:</span></span>

1. <span data-ttu-id="2cc24-203">Nel portale di Azure passare all'account Batch usato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="2cc24-204">Nel pannello **Impostazioni** per l'account Batch selezionare **Controllo di accesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="2cc24-205">Fare clic su **Add** .</span><span class="sxs-lookup"><span data-stu-id="2cc24-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="2cc24-206">Dall'elenco a discesa **Ruolo** scegliere il ruolo _Collaboratore_ o _Lettore_ per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="2cc24-207">Per altre informazioni sui ruoli, vedere [Introduzione al controllo degli accessi in base al ruolo nel portale di Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2cc24-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="2cc24-208">Nel campo **Seleziona** immettere il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="2cc24-209">Selezionare l'applicazione dall'elenco e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="2cc24-210">L'applicazione dovrebbe ora essere visualizzata nelle impostazioni di controllo di accesso con un ruolo con controllo degli accessi in base al ruolo assegnato.</span><span class="sxs-lookup"><span data-stu-id="2cc24-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Assegnare un ruolo con controllo degli accessi in base al ruolo all'applicazione](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="2cc24-212">Ottenere l'ID tenant per Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cc24-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="2cc24-213">L'ID tenant identifica il tenant di Azure AD che offre servizi di autenticazione all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="2cc24-214">Per ottenere l'ID tenant, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2cc24-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="2cc24-215">Nel portale di Azure selezionare Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2cc24-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="2cc24-216">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-216">Click **Properties**.</span></span>
3. <span data-ttu-id="2cc24-217">Copiare il valore GUID indicato per l'ID directory.</span><span class="sxs-lookup"><span data-stu-id="2cc24-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="2cc24-218">Questo valore viene chiamato anche ID tenant.</span><span class="sxs-lookup"><span data-stu-id="2cc24-218">This value is also called the tenant ID.</span></span>

![Copiare l'ID directory](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="2cc24-220">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="2cc24-220">Code examples</span></span>

<span data-ttu-id="2cc24-221">Gli esempi di codice in questa sezione illustrano come eseguire l'autenticazione con Azure AD mediante l'autenticazione integrata e con un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="2cc24-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="2cc24-222">Questi esempi di codice usano .NET, ma i concetti sono simili per le altre lingue.</span><span class="sxs-lookup"><span data-stu-id="2cc24-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="2cc24-223">Un token di autenticazione di Azure AD scade dopo un'ora.</span><span class="sxs-lookup"><span data-stu-id="2cc24-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="2cc24-224">Quando si usa un oggetto **BatchClient** di lunga durata, è consigliabile recuperare un token da ADAL a ogni richiesta per assicurarsi di avere sempre un token valido.</span><span class="sxs-lookup"><span data-stu-id="2cc24-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="2cc24-225">A tale scopo, in .NET scrivere un metodo che recuperi il token da Azure AD e passi tale metodo a un oggetto **BatchTokenCredentials** come delegato.</span><span class="sxs-lookup"><span data-stu-id="2cc24-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="2cc24-226">Il metodo delegato verrà chiamato a ogni richiesta al servizio Batch per garantire che venga fornito un token valido.</span><span class="sxs-lookup"><span data-stu-id="2cc24-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="2cc24-227">Per impostazione predefinita, ADAL memorizza i token nella cache, quindi un nuovo token viene recuperato da Azure AD solo quando necessario.</span><span class="sxs-lookup"><span data-stu-id="2cc24-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="2cc24-228">Per altre informazioni sui token in Azure AD, vedere [Scenari di autenticazione per Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="2cc24-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="2cc24-229">Esempio di codice: uso dell'autenticazione integrata di Azure AD con .NET di Batch</span><span class="sxs-lookup"><span data-stu-id="2cc24-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="2cc24-230">Per eseguire l'autenticazione con l'autenticazione integrata di Batch .NET, fare riferimento al pacchetto [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) e al pacchetto [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="2cc24-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="2cc24-231">Includere le istruzioni `using` seguenti nel codice:</span><span class="sxs-lookup"><span data-stu-id="2cc24-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="2cc24-232">Fare riferimento all'endpoint di Azure AD nel codice, che include l'ID tenant.</span><span class="sxs-lookup"><span data-stu-id="2cc24-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="2cc24-233">Per recuperare l'ID tenant, attenersi alla procedura descritta in [Ottenere l'ID tenant per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="2cc24-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="2cc24-234">Riferimento all'endpoint delle risorse per il servizio Batch:</span><span class="sxs-lookup"><span data-stu-id="2cc24-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="2cc24-235">Riferimento all'account Batch:</span><span class="sxs-lookup"><span data-stu-id="2cc24-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="2cc24-236">Specificare l'ID dell'applicazione (ID client).</span><span class="sxs-lookup"><span data-stu-id="2cc24-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="2cc24-237">L'ID dell'applicazione è disponibile nella registrazione dell'app nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="2cc24-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="2cc24-238">Copiare anche l'URI di reindirizzamento specificato durante il processo di registrazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="2cc24-239">L'URI di reindirizzamento specificato nel codice deve corrispondere a quello specificato quando è stata registrata l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="2cc24-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="2cc24-240">Scrivere un metodo di callback per acquisire il token di autenticazione da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="2cc24-241">Il metodo di callback **GetAuthenticationTokenAsync** illustrato qui chiama ADAL per eseguire l'autenticazione a un utente che interagisce con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2cc24-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="2cc24-242">Il metodo **AcquireTokenAsync** indicato da ADAL richiede all'utente le credenziali e l'applicazione procede dopo che sono state specificate, a meno che queste credenziali non siano già state memorizzate nella cache:</span><span class="sxs-lookup"><span data-stu-id="2cc24-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="2cc24-243">Costruire un oggetto **BatchTokenCredentials** che accetta il delegato come parametro.</span><span class="sxs-lookup"><span data-stu-id="2cc24-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="2cc24-244">Usare tali credenziali per aprire un oggetto **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="2cc24-245">È possibile usare l'oggetto **BatchClient** per operazioni successive sul servizio Batch:</span><span class="sxs-lookup"><span data-stu-id="2cc24-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="2cc24-246">Esempio di codice: uso di un'entità servizio Azure AD con Batch .NET</span><span class="sxs-lookup"><span data-stu-id="2cc24-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="2cc24-247">Per eseguire l'autenticazione con un'entità servizio di Batch .NET, fare riferimento al pacchetto [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) e al pacchetto [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="2cc24-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="2cc24-248">Includere le istruzioni `using` seguenti nel codice:</span><span class="sxs-lookup"><span data-stu-id="2cc24-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="2cc24-249">Fare riferimento all'endpoint di Azure AD nel codice, che include l'ID tenant.</span><span class="sxs-lookup"><span data-stu-id="2cc24-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="2cc24-250">Quando si usa un'entità servizio, è necessario indicare un endpoint specifico del tenant.</span><span class="sxs-lookup"><span data-stu-id="2cc24-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="2cc24-251">Per recuperare l'ID tenant, attenersi alla procedura descritta in [Ottenere l'ID tenant per Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="2cc24-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="2cc24-252">Riferimento all'endpoint delle risorse per il servizio Batch:</span><span class="sxs-lookup"><span data-stu-id="2cc24-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="2cc24-253">Riferimento all'account Batch:</span><span class="sxs-lookup"><span data-stu-id="2cc24-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="2cc24-254">Specificare l'ID dell'applicazione (ID client).</span><span class="sxs-lookup"><span data-stu-id="2cc24-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="2cc24-255">L'ID dell'applicazione è disponibile nella registrazione dell'app nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="2cc24-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="2cc24-256">Specificare la chiave privata copiata dal portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="2cc24-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="2cc24-257">Scrivere un metodo di callback per acquisire il token di autenticazione da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc24-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="2cc24-258">Il metodo di callback **GetAuthenticationTokenAsync** illustrato di seguito chiama ADAL per l'autenticazione automatica:</span><span class="sxs-lookup"><span data-stu-id="2cc24-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="2cc24-259">Costruire un oggetto **BatchTokenCredentials** che accetta il delegato come parametro.</span><span class="sxs-lookup"><span data-stu-id="2cc24-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="2cc24-260">Usare tali credenziali per aprire un oggetto **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="2cc24-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="2cc24-261">È quindi possibile usare l'oggetto **BatchClient** per operazioni successive sul servizio Batch:</span><span class="sxs-lookup"><span data-stu-id="2cc24-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2cc24-262">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2cc24-262">Next steps</span></span>

<span data-ttu-id="2cc24-263">Per altre informazioni su Azure AD, vedere [Documentazione di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="2cc24-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="2cc24-264">Esempi dettagliati dell'uso di ADAL sono disponibili nella libreria degli [esempi di codice per Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="2cc24-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="2cc24-265">Per altre informazioni sull'entità servizio, vedere [Oggetti applicazione e oggetti entità servizio in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="2cc24-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="2cc24-266">Per creare un'entità servizio tramite il portale di Azure, vedere [Usare il portale per creare un'applicazione Azure Active Directory e un'entità servizio che possano accedere alle risorse](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2cc24-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="2cc24-267">È anche possibile creare un'entità servizio con PowerShell o con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc24-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="2cc24-268">Per eseguire l'autenticazione di applicazioni di gestione batch con Azure AD, vedere [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md) (Autenticare le soluzioni di gestione batch con Active Directoy).</span><span class="sxs-lookup"><span data-stu-id="2cc24-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="2cc24-269">[aad_about]: ../active-directory/active-directory-whatis.md "Informazioni su Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="2cc24-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="2cc24-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenari di autenticazione per Azure AD"</span><span class="sxs-lookup"><span data-stu-id="2cc24-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="2cc24-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrazione di applicazioni con Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="2cc24-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
